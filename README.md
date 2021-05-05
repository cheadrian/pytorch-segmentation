# pytorch-segmentation    
Fork from original Pytorch segmentation for Jetson Nano and other Jetson platform devices which needs TensorRT acceleration.    

Tested with PyTorch 1.8.1 and TorchVision 0.9.1   

Improve training performance up to 15x by caching dataset using [TORCHDATA](https://szymonmaszke.github.io/torchdata "TORCHDATA")      
**Caching** is applied only to COCO Dataset loader. 
You can apply it to any format by modify files inside **datasets** folders. 
Example in **coco_utils.py **:
```python
import torchdata as td
def _coco_remove_images_without_annotations(dataset, cat_list=None):
	assert isinstance(dataset, torchvision.datasets.CocoDetection)
	dataset = td.datasets.WrapDataset(dataset).cache() #apply cache using torchdata
```

To use the package with TorchVision 0.9.1, **patch TorchVision** with this: https://gist.github.com/cheadrian/f8ea250d78c2bb9bc913aa89f18f8e21
I will add fixes for conversion to ONNX, TensorRT, fcn_resnet18, fcn_resnet34.

Recommend to use num_workers=0 when training over Google Colab.
