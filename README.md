# KWS Demo

## 文件结构说明

### zynq
- kws_dataset_client.py: 运行测试集，将结果返回上位机
- input_data_zynq.py: 加载测试集时的预处理文件
- layers.py: 使用numpy实现的神经网络算子
- realtime_kws_client.py: 不在zynq上运行的代码，在一台linux上模拟有麦克分的板子，实时检测麦克风的输入识别后将结果返回上位机
- kws_ps_pl.py: 使用pl侧识别，将结果返回至ps，ps再将结果发送至上位机
- pl_simulate.py: 模拟pl侧的操作，实现请求数据，读取，推理，返回结果的流程
- tkinter_kws.py: 使用tkinter通过vnc显示结果
- tmp.py: tkinter测试代码，实现了通过Queue让mainloop和工作进程的数据共享，因此该代码暂时留下
- test_tflite_numpy.py: 在zynq上测试数据集的准确率(未提前处理好MFCC)
- test_sdcard_numpy.py: 使用mfcc预处理好的数据进行前向推理。**使用该脚本发现精度差异均来自mfcc预处理**

### get_kernel_feature_area
该目录下的代码用于存储一次推理中各种中间结果，具体可看[README.md](../get_kernel_feature_area/README.md)

### test_log
该目录下存储了模型权重、MFCC处理后的数据(input_data)
- mobilenetv3_quant_mfcc_gen/layers_output_view.py: 查看保存的各层输出数据

----------------------------

## 环境要求
- python3
- Numpy
- python_speech_features==0.6 (test_tflite_numpy.py使用)

## 运行说明
使用MFCC处理后的数据进行神经网络推理(若不需要考虑MFCC预处理过程，推荐使用此脚本)
```
python3 zynq/test_sdcard_numpy.py
```

使用正常数据集，进行MFCC处理后再进行神经网络推理
```
bash zynq/test_tflite_numpy.sh
```

想要查看或保存单次推理的中间数据，请参考[README.md](../get_kernel_feature_area/README.md)