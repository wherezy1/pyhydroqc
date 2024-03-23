# 水生传感器数据异常检测与校正
该存储库包含用于识别和纠正原位水生传感器收集的时间序列数据中的异常值的软件。该代码是为应用于洛根河天文台收集的数据而开发的，这些数据来自<http://lrodata.usu.edu/tsa/>或 [HydroShare]（https://www.hydroshare.org/search/?q=logan%20river%20observatory）。软件包中包含的所有函数都 [在此处记录]（https://ambersjones.github.io/pyhydroqc/）。可以从 [Python 包索引]（https://pypi.org/project/pyhydroqc/） 安装该包。

封装开发、测试和性能在 Jones， A.S.， Jones， T.L.， Horsburgh， J.S. （2022） 中报告。实现水生传感器数据的自动后处理，环境建模和软件，<https://doi.org/10.1016/j.envsoft.2022.105364>

目前实施的方法包括 ARIMA（自回归综合移动平均）和 LSTM（长短期记忆）。这些是时间序列回归方法，通过将模型估计值与传感器观测值进行比较，并在点超过阈值时将点标记为异常来检测异常。

有多种可能的方法可用于应用 LSTM 进行异常检测/纠正。
- Vanilla LSTM：使用单个变量的过去值来估计该变量的下一个值。
- 多变量 Vanilla LSTM：使用多个变量的过去值来估计所有变量的下一个值。
- 双向 LSTM：使用单个变量的过去和未来值来估计该变量在感兴趣时间步长的值。
- 多变量双向 LSTM：使用多个变量的过去和未来值来估计所有变量在感兴趣时间步长的值。

校正方法取决于方法。对于 ARIMA，每组连续异常点都被视为一个要校正的单位。针对异常组前后的有效点开发了单独的ARIMA模型。模型估计值混合在一起以实现校正。对于 LSTM，校正可能基于单变量或多变量方法。校正是逐点进行的，其中每个点都被视为要校正的单独单元。开发的模型用于估计对组中第一个异常点的校正，然后将其用作估计下一个异常点的输入，依此类推。

文件按异常检测和数据更正的方法进行组织。实用程序文件包含由其他脚本调用的函数、包装器和参数定义。典型的工作流程包括：
1. 检索数据
2. 应用基于规则的检测来筛选数据并应用初始校正
3. 开发模型（即 ARIMA 或 LSTM）
4. 应用模型进行时间序列预测
5. 通过将传感器观测值与建模结果进行比较来确定阈值并检测异常
6. 扩大识别异常的窗口
7. 将异常检测与技术人员标记的数据（如果可用）进行比较并确定指标
8. 应用开发的模型对异常事件进行校正

## 文件说明

### detect.script.py
此脚本包含将异常检测方法应用于来自洛根河天文台六个站点的四个传感器（水温、比电导、pH 值、溶解氧）的数据的代码。该脚本调用函数来检索数据、执行基于规则的异常检测和校正、开发和获取来自五个模型（ARIMA、LSTM univaraite、LSTM 单变量双向、LSTM multivaraiate 和 LSTM 多变量双向）的估计值、确定动态阈值和检测异常、扩大检测窗口并与原始数据进行比较，以及确定指标。此应用程序脚本引用存储在参数文件中的参数。

### parameters.py
此文件包含异常情况检测工作流所有步骤的参数分配。特定于检测脚本中引用的每个站点和传感器定义的参数。LSTM 参数在站点和变量之间是一致的。ARIMA 超参数特定于每个站点/传感器组合，其他参数用于基于规则的异常检测、确定动态阈值以及扩大异常事件。 

### anomaly_utilities.py
包含用于执行异常检测和纠正的函数：
- get_data：检索数据并设置其格式。将LRO中的数据从数据库提取到csv文件中，并根据文件组织根据站点，传感器和年份进行检索。要完成后续步骤，所需的格式是一个数据框，其中包含与日期时间（作为索引）、原始数据、更正数据和数据标签（技术人员识别的异常）相对应的列。
- anomaly_events：扩大异常范围，并为事件或异常数据组编制索引。
- assign_cm：一个辅助函数，用于将异常事件调整为原始大小，以确定指标。
- compare_events：将算法检测到的异常事件与技术人员标记的事件进行比较。
- metrics：确定检测相对于标记数据的性能指标。
- event_metrics：根据事件数而不是数据点数确定性能指标。
- print_metrics：将指标打印到控制台。
- group_bools：对连续的异常和有效数据组进行索引，以便于更正。
- xfade：使用交叉淡入淡出将预测数据和反向预测数据混合到异常事件上，以生成数据校正。
- set_dynamic_threshold：创建一个阈值，该阈值根据模型残差动态变化。
- set_cons_threshold：创建常量值的阈值。
- detect_anomalies：使用模型残差和阈值对异常数据进行分类。
- aggregate_results：将来自多个模型的检测组合在一起，以提供异常检测的单个输出。
- plt_threshold：绘制阈值和模型残差。
- plt_results：绘制原始数据、模型预测、检测和标记异常。

### modeling_utilities.py
包含用于生成和训练模型的函数：
- pdq：自动确定 ARIMA 建模时间序列的 （p， d， q） 超参数。
- build_arima_model、lstm_univar、lstm_multivar、lstm_univar_bidir、lstm_multivar_bidir：调用文件中其他函数以缩放和重塑数据（仅适用于 LSTM 模型）、创建和训练模型以及输出模型预测和残差的包装器。
- create_scaler：创建用于缩放和取消缩放数据的缩放器对象。
- create_training_dataset和create_bidir_training_dataset：根据从数据集中随机选择的点创建训练数据集。调整数据以包括输入到 LSTM 模型所需的time_steps - 要检查的过去数据点数或过去和未来点（双向）的数量。确保不使用已识别为异常的数据（即，通过基于规则的检测）。
- create_sequenced_dataset和create_bidir_sequenced_dataset：将所有输入重塑为序列，其中包含用于输入 LSTM 模型的time_steps - 仅使用过去的数据点或过去和未来的数据点（双向）。用于测试或将模型应用于完整数据集。
- create_vanilla_model、create_bidir_model：用于创建单层 LSTM 模型的辅助函数。
- train_model：使模型适合训练数据。使用验证子集来监视改进，以确保训练不会太长。

### rules_detect.py
包含用于基于规则的异常检测和预处理的函数。取决于anomaly_utilities.py功能包括：
- range_check：扫描超出用户定义限制的数据，并将点标记为异常。
- 持久性：扫描数据中的重复值，如果持续时间超过用户定义的长度，则将点标记为异常。
- group_size：确定上述步骤中识别的异常组的最大长度。
- 插值：使用线性插值校正数据，这是短期异常事件的典型方法。
- add_labels：允许添加异常标签（指专家先前识别的异常），以防更正后的数据可能遗漏了标签，这些标签是 NaN 或无数据值（例如，-9999）。

### calibration.py
包含用于识别和校正校准事件的函数。功能包括：
- calib_edge_detect：使用边沿滤波识别可能的校准候选事件。
- calib_persist_detect：根据用户定义长度的持久性识别可能的校准候选事件。
- calib_overlap：通过从calib_persist_detect功能中查找多个传感器的并发事件来识别可能的校准候选事件。
- find_gap：根据日期时间前后的时间窗口内的最大数据差异确定校准事件的间隙值。
- lin_drift_cor：执行线性漂移校正，以解决给定校准日期和间隙值的传感器漂移问题。

### model_workflow.py
包含用于构建和训练 ARIMA 和 LSTM 模型、应用模型进行预测、设置阈值、检测异常、扩大异常事件以及确定指标的功能。取决于anomaly_utilities.py、modeling_utilities.py和rules_detect.py。
包装函数名称为：arima_detect、lstm_detect_univar 和 lstm_detect_multivar。LSTM 模型工作流包括普通或双向选项。在每个包装器函数中，都遵循完整的检测工作流程。选项允许输出绘图、摘要和指标。

### ARIMA_correct.py
包含使用 ARIMA 模型执行校正和绘图结果的功能。取决于anomaly_utilities.py。
- arima_group：确保围绕异常点和点组的有效数据足以进行预测/回溯。
- arima_forecast：对发生异常情况的数据进行预测。
- generate_corrections：确定校正的主要功能。传递具有异常的数据，并使用分段 ARIMA 模型确定校正。修正是通过对预测和回溯预测进行平均（交叉淡入淡出）来确定的。

## 依赖
此软件依赖于以下 Python 包：
- numpy
- pandas
- matplotlib
- os
- scipy
- warnings
- random
- tensorflow
- statsmodels
- sklearn
- pmdarima
- copy

## 赞助商和信用
[![美国国家科学基金会-1931297]（https://img.shields.io/badge/NSF-1931297-blue.svg）]（https://nsf.gov/awardsearch/showAward?AWD_ID=1931297）

该存储库中的材料基于美国国家科学基金会资助 [1931297]（http://www.nsf.gov/awardsearch/showAward?AWD_ID=1931297） 支持的工作。所表达的任何意见、发现、结论或建议均为作者的观点，并不一定反映美国国家科学基金会的观点。