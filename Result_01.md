
Rules based detection complete.


Processing ARIMA detections.

temp ARIMA model complete.
Threshold determination complete.
ratio of detections: 0.002856 %

Processing ARIMA detections.
cond ARIMA model complete.
Threshold determination complete.
ratio of detections: 0.174191 %

Processing ARIMA detections.
D:\毕业论文\code\pyhydroqc-lasted\pyhydroqc\modeling_utilities.py:74: FutureWarning: ChainedAssignmentError: behaviour will change in pandas 3.0!
You are setting values through chained assignment. Currently this works in certain cases, but when using Copy-on-Write (which will become the default behaviour in pandas 3.0) this will never work to update the original DataFrame or Series, because the intermediate object on which we are setting values will behave as a copy.
A typical example is when you are setting values in a column of a DataFrame, like:



ph ARIMA model complete.
Threshold determination complete.
ratio of detections: 0.025700 %

Processing ARIMA detections.
D:\毕业论文\code\pyhydroqc-lasted\pyhydroqc\modeling_utilities.py:74: FutureWarning: ChainedAssignmentError: behaviour will change in pandas 3.0!
You are setting values through chained assignment. Currently this works in certain cases, but when using Copy-on-Write (which will become the default behaviour in pandas 3.0) this will never work to update the original DataFrame or Series, because the intermediate object on which we are setting values will behave as a copy.
A typical example is when you are setting values in a column of a DataFrame, like:


do ARIMA model complete.
Threshold determination complete.
ratio of detections: 0.008567 %
ARIMA detection complete.


Processing LSTM univariate ModelType.VANILLA detections.
WARNING:tensorflow:From D:\Python\python-3.11.8\Lib\site-packages\keras\src\backend.py:873: The name tf.get_default_graph is deprecated. Please use tf.compat.v1.get_default_graph instead.

2024-03-22 16:17:20.976445: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: SSE SSE2 SSE3 SSE4.1 SSE4.2 AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
WARNING:tensorflow:From D:\Python\python-3.11.8\Lib\site-packages\keras\src\optimizers\__init__.py:309: The name tf.train.Optimizer is deprecated. Please use tf.compat.v1.train.Optimizer instead.

WARNING:tensorflow:From D:\Python\python-3.11.8\Lib\site-packages\keras\src\utils\tf_utils.py:492: The name tf.ragged.RaggedTensorValue is deprecated. Please use tf.compat.v1.ragged.RaggedTensorValue instead.

625/625 [==============================] - 4s 4ms/step
1095/1095 [==============================] - 6s 5ms/step
1095/1095 [==============================] - 6s 5ms/step - loss: 0.0264
temp ModelType.VANILLA LSTM model complete.
Threshold determination complete.
ratio of detections: 0.028560 %

Processing LSTM univariate ModelType.VANILLA detections.
625/625 [==============================] - 1s 2ms/step
1095/1095 [==============================] - 2s 2ms/step
1095/1095 [==============================] - 2s 2ms/step - loss: 0.1002
cond ModelType.VANILLA LSTM model complete.
Threshold determination complete.
ratio of detections: 0.137088 %

Processing LSTM univariate ModelType.VANILLA detections.
625/625 [==============================] - 1s 2ms/step
1095/1095 [==============================] - 2s 2ms/step
1095/1095 [==============================] - 2s 2ms/step - loss: 0.1658
ph ModelType.VANILLA LSTM model complete.
Threshold determination complete.
ratio of detections: 0.008568 %

Processing LSTM univariate ModelType.VANILLA detections.
625/625 [==============================] - 4s 4ms/step
1095/1095 [==============================] - 7s 5ms/step
1095/1095 [==============================] - 6s 5ms/step - loss: 0.1732
do ModelType.VANILLA LSTM model complete.
Threshold determination complete.
ratio of detections: 0.000000 %

Processing LSTM univariate ModelType.BIDIRECTIONAL detections.
625/625 [==============================] - 5s 6ms/step
1095/1095 [==============================] - 8s 5ms/step
1095/1095 [==============================] - 3s 2ms/step - loss: 0.0364
temp ModelType.BIDIRECTIONAL LSTM model complete.
Threshold determination complete.
ratio of detections: 0.028564 %

Processing LSTM univariate ModelType.BIDIRECTIONAL detections.
625/625 [==============================] - 5s 6ms/step
1095/1095 [==============================] - 8s 5ms/step
1095/1095 [==============================] - 6s 6ms/step - loss: 0.0746
cond ModelType.BIDIRECTIONAL LSTM model complete.
Threshold determination complete.
ratio of detections: 0.151390 %

Processing LSTM univariate ModelType.BIDIRECTIONAL detections.
625/625 [==============================] - 5s 6ms/step
1095/1095 [==============================] - 8s 6ms/step
1095/1095 [==============================] - 6s 6ms/step - loss: 0.1517
ph ModelType.BIDIRECTIONAL LSTM model complete.
Threshold determination complete.
ratio of detections: 0.005713 %

Processing LSTM univariate ModelType.BIDIRECTIONAL detections.
625/625 [==============================] - 3s 3ms/step
1095/1095 [==============================] - 4s 3ms/step
1095/1095 [==============================] - 3s 3ms/step - loss: 0.1417
do ModelType.BIDIRECTIONAL LSTM model complete.
Threshold determination complete.
ratio of detections: 0.005713 %

Processing LSTM multivariate ModelType.VANILLA detections.
Raw data shape: (35019, 4)
Observed data shape: (35019, 4)
Initial anomalies data shape: (35019, 4)
625/625 [==============================] - 4s 5ms/step
1095/1095 [==============================] - 6s 4ms/step
1095/1095 [==============================] - 5s 4ms/step - loss: 0.1699
multivariate ModelType.VANILLA LSTM model complete.

ratio of detections: 0.028560 %
ratio of detections: 0.157080 %
ratio of detections: 0.011424 %
ratio of detections: 0.000000 %
Threshold determination complete.

Processing LSTM multivariate ModelType.BIDIRECTIONAL detections.
Raw data shape: (35019, 4)
Observed data shape: (35019, 4)
Initial anomalies data shape: (35019, 4)
625/625 [==============================] - 2s 3ms/step
1095/1095 [==============================] - 4s 3ms/step
1095/1095 [==============================] - 3s 3ms/step - loss: 0.1427
multivariate ModelType.BIDIRECTIONAL LSTM model complete.

ratio of detections: 0.028564 %
ratio of detections: 0.145677 %
ratio of detections: 0.005713 %
ratio of detections: 0.005713 %
Threshold determination complete.








D:\毕业论文\code\pyhydroqc-lasted\pyhydroqc\arima_correct.py:34: FutureWarning: Series.__getitem__ treating keys as positions is deprecated. In a future version, integer keys will always be treated as labels (consistent with DataFrame behavior). To access a value by position, use `ser.iloc[pos]`
  if ((df.loc[df[group] == i][anomalies][0] == 0) and (group_len < min_group_len)):
D:\毕业论文\code\pyhydroqc-lasted\pyhydroqc\arima_correct.py:34: FutureWarning: Series.__getitem__ treating keys as positions is deprecated. In a future version, integer keys will always be treated as labels (consistent with DataFrame behavior). To access a value by position, use `ser.iloc[pos]`
  if ((df.loc[df[group] == i][anomalies][0] == 0) and (group_len < min_group_len)):
D:\毕业论文\code\pyhydroqc-lasted\pyhydroqc\arima_correct.py:156: FutureWarning: Setting an item of incompatible dtype is deprecated and will raise an error in a future version of pandas. Value '0' has dtype incompatible with bool, please explicitly cast to a compatible dtype first.
  df.loc[df['arima_group'] == i, 'ARIMA_event'] = 0
D:\Python\python-3.11.8\Lib\site-packages\pmdarima\arima\auto.py:444: UserWarning: Input time-series is completely constant; returning a (0, 0, 0) ARMA.
  warnings.warn('Input time-series is completely constant; '
Traceback (most recent call last):
  File "D:\Python\PyCharm 2023.3.2\plugins\python\helpers\pydev\pydevd.py", line 1534, in _exec
    pydev_imports.execfile(file, globals, locals)  # execute the script
    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "D:\Python\PyCharm 2023.3.2\plugins\python\helpers\pydev\_pydev_imps\_pydev_execfile.py", line 18, in execfile
    exec(compile(contents+"\n", file, 'exec'), glob, loc)
  File "D:\毕业论文\code\pyhydroqc-lasted\Examples\SingleSite_Detect.py", line 280, in <module>
    corrections[snsr] = arima_correct.generate_corrections(df=results_all[snsr],
                        ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "D:\毕业论文\code\pyhydroqc-lasted\pyhydroqc\arima_correct.py", line 186, in generate_corrections
    df = df.drop('group', 1)
         ^^^^^^^^^^^^^^^^^^^
TypeError: DataFrame.drop() takes from 1 to 2 positional arguments but 3 were given
python-BaseException

Process finished with exit code 1
