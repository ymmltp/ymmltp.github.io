---
title: Yolo
date: 2024-09-25 13:25:14
tags: 学无止境
---
## Yolo

### YoloV5

#### 模型导出成openvino格式

需要使用 `./openvino/tool/mo` 文件夹里对应的脚本来完成格式转换

```sh
python "C:\Users\1382919\AppData\Local\Programs\Python\Python310\yolo_env\Lib\site-packages\openvino\tools\mo\mo_onnx.py" --input_model ./export/best.onnx
```

#### train model

```python 
python train.py --data coco128.yaml --weights yolov5n.pt --img 640
```

#### export model

```python
python export.py --data coco128.yaml --weights yolov5n.pt --img 640
```

#### detect

- 1 使用yolo自带的detect脚本
  
```python
python detect.py --weights ./export/best_half.onnx --source ./imgData
```

- 2 使用openvion平台

  - 下载该库 [yolo-openvion github](https://github.com/SamSamhuns/yolov5_export_cpu)
  - 导入utils中的文件 ,general.py 加入 DataStreamer

```python
python detect_openvino.py -i ./imgData --model_xml ./export/best.xml --model_bin ./export/best.bin -d CPU
```

#### 调优
