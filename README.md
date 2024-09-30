# Introduction
This project expands upon the findings of Michail et al. [^1] and Prapas et al. [^2] by implementing and evaluating a diverse set of models to predict wildfire occurrences. Our objective is to compare the effectiveness of multiple algorithms, aiming to identify the most reliable predictors of wildfires. The models we have utilized include:

1. **Logistic Regression (L1, L2):**
   - **L1 Regularization:** Also known as Lasso regression, this technique helps in feature selection by forcing some coefficients to be exactly zero, thereby removing less important features.
   - **L2 Regularization:** Also known as Ridge regression, this technique penalizes the magnitude of coefficients to prevent overfitting by distributing error across all terms.

2. **Long Short-Term Memory (LSTM):**
   - LSTM networks are a type of recurrent neural network (RNN) that are particularly well-suited for time series data. They are designed to remember long-term dependencies, making them ideal for capturing temporal patterns in wildfire data.

3. **Random Forest:**
   - This ensemble learning method combines multiple decision trees to improve predictive performance. Random forests are robust to overfitting and can handle a large number of input variables, making them suitable for complex datasets.

4. **Feed Forward Neural Network:**
   - A basic type of neural network where connections between the nodes do not form a cycle. This model is used for various prediction tasks and can be adjusted in complexity by varying the number of layers and nodes.
  
[^1]: Michail, D., Panagiotou, L.-I., Davalas, C., Prapas, I., Kondylatos, S., Bountos, N. I., & Papoutsis, I. (n.d.). Seasonal Fire Prediction using Spatio-Temporal Deep Neural Networks.

[^2]: Prapas, I., Ahuja, A., Kondylatos, S., Karasante, I., Panagiotou, E., Alonso, L., Davalas, C., Michail, D., Carvalhais, N., & Papoutsis, I. (n.d.). Deep Learning for Global Wildfire Forecasting.

# Executive Summary

Four machine learning models were used to predict the occurrence and spread of wildfires across Europe, Africa, Asia and Australia. Both linear and non-linear models were compared, they were L1 Logistic Regression, L2 Logistic Regression, Random Forest and LSTM. 

Overall, the Random Forest model performed best when predicting the spread of wildfires 8 days into the future. achieving a precision of 86% and recall of 77%. This model placed high importance on the normalized difference vegetation index (ndvi),  soil water level (swvl1), solar irradiance (ssrd) and vapor pressure deficit (vpd).

Neural networks performed the worst however, this may be attributed to the lack of hyperparameter tuning and low epoch iterations during training. 

Logistic regression worked well but failed to accurately capture the wildfire spread in Asia and Australia. This is likely due to the linear behaviour of regression models failing to capture the nonlinearities in the wildfire spread. 


# Getting Started

- Download the [SeasFire dataset](https://zenodo.org/records/7108392) and place in a directory of your choice

- Install Python ```3.11``` or later and install all dependancies from ```requirements.txt```

``` 
$ conda create --name <env> --file requirements.txtrequirements.txt
```

- Open ```/Code/Note Book.ipynb``` and replace ```data_path``` with your data directory

```python
data_path = '../Data/dataset.zarr'  # Update with your data path

try:
    ds = xr.open_zarr(data_path)
except ValueError as e:
    print(f"Error loading dataset: {e}")
    raise
```

- Run ```/Code/Note Book.ipynb```

# Dataset
All models were trained using the [SeasFire dataset](https://zenodo.org/records/7108392). 

The SeasFire Cube is a scientific datacube designed for global seasonal fire forecasting, funded by the European Space Agency (ESA). This advanced tool integrates spatial and temporal data to provide detailed insights into wildfire patterns and drivers. The SeasFire Cube incorporates both spatial and temporal components:

- **Spatial Component:** Provides detailed information about the geographical locations of wildfires, enabling precise mapping and analysis of fire-affected areas.
- **Temporal Component:** Captures the timing and duration of wildfire events, allowing for the study of fire seasonality and trends over time.

**Data Characteristics and Resolution**

The SeasFire Cube contains 21 years of data, spanning from 2001 to 2021. The data is organized with an 8-day time resolution and a 0.25-degree grid resolution, providing a granular and high-resolution dataset for analysis.

## Input Features and Target Variable

This project uses 10 different variables selected based on their relevance and usage in burned area prediction tasks from existing literature. These variables were standardized before use, except for the cube coordinates.

|  **Input Features**       | **Variable Name**| 
| ------------- |:-------------:| 
| Mean Sea level pressure      | mslp | 
| Total precipitation      | tp   |  
| Vapor Pressure Deficit | vpd  | 
| Sea surface temperature |  sst | 
| Temperaeture at 2 meters - Mean |  t2m_mean | 
| Surface solar radiation downwards | ssrd  | 
| Volumetric soil water level 1| swvl1   | 
| Land surface temperature at day| lst_day   | 
| Normalized Difference Vegetation Index| ndvi   | 
|  Population Density |  pop_dens |
| **Target** | **Variable Name**  | 
| Burned Areas (as binary)| gwis_ba  |  

## Input Feature Distribution

![Histograms on input features](/Images/input_feature_dist.png)

## Target Variable

Visualization of burned areas around the globe from 2001-2020.
![Target Variable Visualization](/Images/BAs_GWIS_gif_fps09.gif)


# Results

## Random Forest:

- Accuracy:    96%
- Precision:   86%
- Recall:      77%
- F1-score:    81%

Inference: This model provides a good balance between high recall and precision, making it highly reliable for detecting wildfires without generating too many false alarms.

## LSTM (ReLU):

- Accuracy:    12%
- Precision:   12%
- Recall:      100%
- F1-score:    22%

Inference: While the recall is very high, indicating that it detects most wildfires, the precision is very low. This means it generates a lot of false positives, which might not be practical for resource management.

## FeedForward NN:

- Accuracy:    69%
- Precision:   73%
- Recall:      61%
- F1-score:    67%

Inference: This model has moderate precision but low recall, meaning it misses a significant number of wildfires, which is not ideal for this application.

## Logistic Regression (L2):

- Accuracy:    91%
- Recall:      41%
- Precision:   67%
- F1-score:    51%

## Logistic Regression (L1):

- Accuracy:    91%
- Precision:   68%
- Recall:      43%
- F1-score:    53%

Inference: Similar to FeedForward NN, it has low recall and moderate precision, making it less effective for wildfire prediction.

## Predictions

![Predictions](/Images/predictions.png)


# Conclusion

Best Model: Random Forest is the best choice because it offers a strong balance between high recall and high precision, reflected in its high F1-score. This balance ensures that most wildfires are detected while keeping the number of false positives manageable.

## Recommendations

 Due to the high correlation of wildfire spread to vegetation, soil water solar irradiance and humidity, it is recommended that policies be developed to control the growth of plant life in heavily populated areas which may be exposed to excessive solar radiation and little rainfall. 
 
 Fire retardants or barriers can be strategically placed around homes or buildings in these areas especially during extended periods of hot and dry weather. Governments can also build more fire stations to decrease the response times and spread of wildfires. 
