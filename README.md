# Image Captioning

## Task
The primary task was to perform image captioning on the Flickr Dataset, consisting of Images annotated with 5 captions per Image:

## Datasets
The dataset was initially divided into a training set and a hold-out test set. For inference the Batch Size was kept as 1 while for training it was set as 32.

## Model
The Model Consisted of a 3 stage pipeline:
![Image_Captioning_Model_Pic](https://github.com/jishu123456789/ImageCaptioning/assets/131681225/72d18109-995f-40cc-937c-cec24f8503a0)

### Pre-Trained ResNet Backbone:
- Transformed Images were passed through a pre-trained ResNet-101 whose last 2 layers were removed.
- Reshaping was done on the output and 1D positional embeddings were applied to the reshaped resnet outputs.
- 2D positional embeddings and other Swin-Transformer based backbones also tried but ResNet-101 with 1D positional embeddings gave best results

### Transformer Encoder:
- The ResNet-101 outputs were then passed through a Transformer Encoder Block containing 3 Encoder Layers.

### Transformer Decoder:
- The Encoder outputs were then fed through a Transformer Decoder Block containing 4 Decoder Layers.
- The outputs were then flattened and Cross Entropy Loss was used as the loss function

## Configurations
### Hyperparameters:
- Training Batch size : 32
- Testing Batch size : 1
- Learning Rate : 3e-4
- Epochs : 15
- Numb Encoder Layers : 3
- Num Decoder Layers : 4
- Num Attention Heads : 8
- Dropout Prob : 0.1
### Results : 
- The model seems to understand the images well even when trained on small epochs. I plan to see why Positonal Embeddings in 2D for images did not work as expected
- Also other kinds of relative embeddings could be tried like Rotary Positional Encodings(RoPE).


![Dog_Pic](https://github.com/jishu123456789/ImageCaptioning/assets/131681225/52206c33-31fb-4743-8e85-15de704d1123)
![Couple_Pic](https://github.com/jishu123456789/ImageCaptioning/assets/131681225/dfb3a6b5-6800-401d-a2c5-0cea3f728f00)
![Hiking_Pic](https://github.com/jishu123456789/ImageCaptioning/assets/131681225/4a29c87b-d3d6-40b8-a7e8-af4798560c7c)
![Girl_Pic](https://github.com/jishu123456789/ImageCaptioning/assets/131681225/415573ea-e3fe-4c63-83dd-f06bdc67ed5f)

Overall, this project was very fun to develop from scratch and a was a great learning experience.


## DatasetLink 

###
- [https://drive.google.com/drive/folders/1vhu3LJ9eYDDQfmUZB62jFRf6PuqMbqr](https://www.kaggle.com/datasets/adityajn105/flickr8k)-
- This link contains the Flickr Dataset which contains the testing and training data
  
## Mentions

### Much of the codebase was inspired by
- Alaadin Pearson
- Image Captioning using CNN and Transformers
