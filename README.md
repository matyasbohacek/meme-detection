# Meme detection

Machine learning model trained to classify memes from images. The model has been trained on a dataset of several thousand annotated images and can label an image as either `meme` or `photo`.

It is also very lightweight and can be used for multiple use-cases.

## Metrics

| Version | Training accuracy | Validation accuracy | Testing accuracy |
|---------|-------------------|---------------------|------------------|
| 1.0     | 100%              | 91%                 | To be done.      |

## Implementation

### Usage in Python

To use the model in your Python project, make sure to install **coremltools** and **Pillow** packages first. Then, you can simply use the following snippet to envoke the model:

```python
import coremltools
from PIL import Image

model = coremltools.models.MLModel('meme-detection.mlmodel')
image = Image.open("source_file.png")

result = model.predict({"image": image})
result_label = result["classLabel"]
```

### Usage in Swift

If you want to use the model in your Swift app, simply drag the model file into your project in **Xcode**. A wrapping class will be generated automatically, on top of which you will be able to use the model. Supposing you have your `CVPixelBuffer` ready, it is as simple as:

```Swift
import CoreML

let model = try VNCoreMLModel(for: meme_detection().model)
guard let scene = try? model.prediction(image: pixelBuffer) else {
  fatalError("Unable to predict from the model")
}
        
let result = scene.classLabel
```

Alternatively, you can follow Apple's [Classifying Images with Vision and Core ML Tutorial](https://developer.apple.com/documentation/vision/classifying_images_with_vision_and_core_ml).
