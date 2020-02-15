<p align="center"><img width=45% src="https://raw.githubusercontent.com/sukkritsharmaofficial/NEURALFUSE/master/media/large_neuralfuse.png"></p>


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
![Python](https://img.shields.io/badge/python-v3.6+-blue.svg)
[![Build Status](https://travis-ci.org/anfederico/Clairvoyant.svg?branch=master)](https://travis-ci.org/anfederico/Clairvoyant)
![Dependencies](https://img.shields.io/badge/dependencies-up%20to%20date-brightgreen.svg)]
![Contributions welcome](https://img.shields.io/badge/contributions-welcome-orange.svg)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://opensource.org/licenses/MIT)

## Basic Overview

Given a content photo and a style photo,the code can transfer the style of the style photo to the content photo.

<p align="center"><img width=80% src="https://raw.githubusercontent.com/sukkritsharmaofficial/NEURALFUSE/master/media/Output.png"></p>

<br>

<!-- ## Visualize the Learning Process
<img src="https://github.com/anfederico/Clairvoyant/blob/master/media/Learning.gif" width=40%>
-->
<br> 

## Last Dependencies
```python
pip install numpy
pip install Pillow
pip install keras
pip install scipy
```

## Latest Development Changes
```bash
git clone https://github.com/sukkritsharmaofficial/NEURALFUSE
```

## Code

Importing Dependencies

```python
# Imports
import numpy as np
from PIL import Image
import requests
from io import BytesIO

from keras import backend
from keras.models import Model
from keras.applications.vgg16 import VGG16

from scipy.optimize import fmin_l_bfgs_b
```

## Changable Hyperparameters and setting paths
```python
# Hyperparams
ITERATIONS = 30
CHANNELS = 3
IMAGE_SIZE = 500
IMAGE_WIDTH = IMAGE_SIZE
IMAGE_HEIGHT = IMAGE_SIZE
IMAGENET_MEAN_RGB_VALUES = [123.68, 116.779, 103.939]
CONTENT_WEIGHT = 0.02
STYLE_WEIGHT = 4.5
TOTAL_VARIATION_WEIGHT = 0.995
TOTAL_VARIATION_LOSS_FACTOR = 1.25

# Paths
input_image_path = "input.png"
style_image_path = "style.png"
output_image_path = "output.png"
combined_image_path = "combined.png"
```

## Adding links to Content and Style photo

```python

content_image_path = "YOUR LINK GOES HERE"
style_image_path = "YOUR LINK GOES HERE"

```

#### Output

<p align="center"><img width=50% src="https://raw.githubusercontent.com/sukkritsharmaofficial/NEURALFUSE/master/media/Content.png"></p>

<p align="center"><img width=50% src="https://raw.githubusercontent.com/sukkritsharmaofficial/NEURALFUSE/master/media/Style.png"></p>

## Running Model 
```python
x = np.random.uniform(0, 255, (1, IMAGE_HEIGHT, IMAGE_WIDTH, 3)) - 128.

for i in range(ITERATIONS):
    x, loss, info = fmin_l_bfgs_b(evaluator.loss, x.flatten(), fprime=evaluator.gradients, maxfun=20)
    print("Iteration %d completed with loss %d" % (i, loss))
    
x = x.reshape((IMAGE_HEIGHT, IMAGE_WIDTH, CHANNELS))
x = x[:, :, ::-1]
x[:, :, 0] += IMAGENET_MEAN_RGB_VALUES[2]
x[:, :, 1] += IMAGENET_MEAN_RGB_VALUES[1]
x[:, :, 2] += IMAGENET_MEAN_RGB_VALUES[0]
x = np.clip(x, 0, 255).astype("uint8")
output_image = Image.fromarray(x)
output_image.save(output_image_path)
```
#### Output

```text
Iteration 0 completed with loss 62434377728
Iteration 1 completed with loss 33507442688
Iteration 2 completed with loss 21433647104
Iteration 3 completed with loss 16948576256
Iteration 4 completed with loss 14893883392
Iteration 5 completed with loss 13701744640
.
.
.
.
Iteration 25 completed with loss 11944347648
Iteration 26 completed with loss 11941498880
Iteration 27 completed with loss 11939000320
Iteration 28 completed with loss 11936762880
Iteration 29 completed with loss 11934586880
```

## Visualizing Combined results

```python
combined = Image.new("RGB", (IMAGE_WIDTH*3, IMAGE_HEIGHT))
x_offset = 0
for image in map(Image.open, [input_image_path, style_image_path, output_image_path]):
    combined.paste(image, (x_offset, 0))
    x_offset += IMAGE_WIDTH
combined.save(combined_image_path)
```

#### Output

<p align="center"><img width=80% src="https://raw.githubusercontent.com/sukkritsharmaofficial/NEURALFUSE/master/media/Output.png"></p>

<!-- ## Other Projects
#### Intensive Backtesting
The primary purpose of this project is to rapidly test datasets on machine learning algorithms (specifically Support Vector Machines). While the Simulation class allows for basic strategy testing, there are other projects more suited for that task. Once you've tested patterns within your data and simulated a basic strategy, I'd recommend taking your model to the next level with:
```text
https://github.com/anfederico/Gemini
```

#### Social Sentiment Scores
The examples shown use data derived from a project where we are data mining social media and performing stock sentiment analysis. To get an idea of how we do that, please take a look at:
```text
https://github.com/anfederico/Stocktalk
```

## Notes
#### Multivariate Functionality
Remember, more is not always better!
```python
variables = ["SSO"]                            # 1 feature
variables = ["SSO", "SSC"]                     # 2 features
variables = ["SSO", "SSC", "RSI"]              # 3 features
variables = ["SSO", "SSC", "RSI", ... , "Xn"]  # n features
```

## Contributing
Please take a look at our [contributing](https://github.com/anfederico/Clairvoyant/blob/master/CONTRIBUTING.md) guidelines if you're interested in helping!
#### Pending Features
- Export model
- Support for multiple sklearn SVM models
- Visualization for models with more than 2 features  -->
