# Time Series Normalization
Recently, many sophisticated methods have been proposed for time series forecasting, however, the bulk of improvements have been achieved by preprocessing methods, namely normalization[1](https://github.com/ts-kim/RevIN)-[2](https://arxiv.org/pdf/2401.16777) and patching [3](https://github.com/yuqinie98/PatchTST/tree/main). Moreover, [4](https://arxiv.org/pdf/2205.13504)-[5](https://arxiv.org/abs/2406.16964) have shown that simpler methods often achieve state of the art performance. So, I think that one of the more promising approaches to improve time series forecasting is through improving the normalization. Current normalization methods discard the raw time series values and base their prediction on shape of the time series. While this approach increases the generalizability of the time series, I argue that the discarded information contains meaning ful information that can improve the accuracy of the forecast. Moreover, using the same normalization throughout the forecasting horizon can cause issues since the time series is not stationary.
## Approach
The approach uses [PatchTST](https://github.com/yuqinie98/PatchTST/tree/main) as the baseline. First, the network is trained using the standard procedure in PatchTST, then the network is frozen a residual network using the same architecture as the first network but with non-normalized input is trained to learn the difference between the outputs of the first network and the ground truth.
## Usage
Use the Normalize_PatchTST.ipynb. It first clones the PatchTST repository and overrides some functions (e.g. dataloading, experiment, and model) with the functions implemented in the notebook. The args.start controls when the first network is frozen and the second network kicks in.

Download data. You can download all the datasets from [Autoformer](https://drive.google.com/drive/folders/1ZOYpTUa82_jCcxIdTmyr0LXQfvaM9vIy). Create a seperate folder ./dataset and put all the csv files in the directory.

## Results
The implemented method does not improve the prediction accuracy. The MSE for prediction horizon of 144 steps on ETTm2 dataset is 0.2990145 for the baseline and 0.3108904 for the implemented method.

Notably, the training loss is lower than the baseline. It can be due to extra parameters in the model. Reducing the number of parameters in the residual network might help the accuracy.
