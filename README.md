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

# Dataset
All models were trained using the [SeasFire dataset](https://zenodo.org/records/7108392). 

The SeasFire Cube is a scientific datacube designed for global seasonal fire forecasting, funded by the European Space Agency (ESA). This advanced tool integrates spatial and temporal data to provide detailed insights into wildfire patterns and drivers. The SeasFire Cube incorporates both spatial and temporal components:

- **Spatial Component:** Provides detailed information about the geographical locations of wildfires, enabling precise mapping and analysis of fire-affected areas.
- **Temporal Component:** Captures the timing and duration of wildfire events, allowing for the study of fire seasonality and trends over time.

**Data Characteristics and Resolution**

The SeasFire Cube contains 21 years of data, spanning from 2001 to 2021. The data is organized with an 8-day time resolution and a 0.25-degree grid resolution, providing a granular and high-resolution dataset for analysis.

## Input Features



# Usage


# Results



