# Option Pricing Practicing Project


# Introduction
In 2022, I undertook a project focusing on the pricing of European Basket options under Black-Scholes assumptions using a neural network (NN) approach. This project involves building and training a NN model with generated data, aiming to compare its efficacy against the traditional Monte-Carlo (MC) simulation method. Additionally, I evaluate the performance of both the NN model and MC simulation against the classic Black-Scholes (B-S) model in single-asset scenarios.

# Data Generation
The data for training and testing the NN model is synthetically generated based on the following criteria:
  -	The basket option contains two assets.
  -	These two assets are equally weighted.
  -	The range of initial spot price is from $30 to $70.
  -	The strike price is from $10 to $90.
  -	The risk-free rate is from 1% to 3%.
  -	The volatility of each asset is from 0.15 to 0.6.
  -	The correlation between the two assets is from 0.05 to 0.7
  -	Time to maturity is 3-, 6-, 9-, and 12-month.

The data is uniformly distributed across these parameters. Due to the non-log-normal distribution of the sum of log-normal variables, a modified Black-Scholes formula with moment matching adjustment is used for price generation. The formulas used are:

$$ C(0) = \delta({F\Phi(d_{+}) - K\Phi(d_{-})}) $$

$$ d_{+} = {{\ln {F \over K} + {1 \over 2}\tilde{\sigma}^2(T-t)} \over {\tilde{\sigma}\sqrt{T-t}}} $$

$$ d_{-} = d_{+} - \tilde{\sigma}\sqrt{T-t} $$

# Methodology
## Neural Network Model
The NN model consists of four layers: an input layer with seven nodes, two hidden layers with ten nodes each, and an output layer with a single node for the option price. The model employs the rectified linear unit (ReLU) function as the activation function. The loss function is the mean-squared error (MSE), and the optimizer is the Adam algorithm. The dataset size is 186,624, with a 90% training and 10% test split. Additionally, 20% of the training data is used for validation.

### Graph of Validation Loss

<img width="413" alt="Validation Loss" src="https://user-images.githubusercontent.com/72664069/174505184-4c5db935-00d4-4e07-94a7-03b07d4240c4.png">

### Graph of Actual Price vs. Predicted Price

<img width="411" alt="Actual vs Predicted" src="https://user-images.githubusercontent.com/72664069/174505207-e4684d72-bac2-4f1d-897b-a2971753f48a.png">

## Monte-Carlo Simulation
The MC simulation, a common method for pricing basket options, is based on modeling asset price movements under the B-S assumption as geometric Brownian motions. The simulation involves constructing random final asset prices, calculating basket option payoffs, and discounting them to present value. The number of iterations for the MC simulation is $ 3 \times 10^7 $.

# Results
## Two-Asset Basket Option
In this part, I compare the predicted prices of the NN model and the MC simulation under a random dataset. The random dataset contains 100 data and the settings of the two-asset basket option are:
-	Two assets are equally weighted.
-	Spot prices of two assets are randomly from $40 to $60.
-	The strike price of the basket option is randomly from $30 to $70.
-	Sigma of Asset 1 is randomly from 0.1 to 0.2 (Low-risk).
-	Sigma of Asset 2 is randomly from 0.4 to 0.5 (High-risk).
-	The correlation between the two assets is randomly from 0.1 to 0.6.
-	Risk-free rates are randomly from 1% to 3%.
-	Time to maturity is randomly chosen among 3-, 6-, 9-, and 12 months.

The average predicted option price using the NN model is $7.34, and the average predicted option price using the MC simulation is $8.26. The difference between these two methods is $0.92, and the Mean-Square-Error (MSE) is 1.2758.

| Avg_Price (NN) | Avg_Price (MC) | Diff. | MSE |
| --- | --- | --- | --- |
| $7.34 | $8.26 | $0.92 | 1.2758 |

## One-Asset Option
I also compare the predicted prices of the NN model, MC simulation, and the B-S model under the one-asset situation. The setup of this random dataset is the same as the two-asset dataset, except it only contains one asset and its sigma is randomly from 0.15 to 0.5. The average predicted option prices using the B-S model, NN model, and MC simulation are $8.38, $8.58, and $8.59, respectively. Although the difference is smaller between B-S predicted price and NN predicted price ($0.19), the volatility is higher with MSE equals 0.2017. The difference between B-S predicted prices and MC predicted prices is $0.21 and the MSE is 0.0951.

| Avg_Price (B-S) | Avg_Price (NN) | Diff. | MSE |
| --- | --- | --- | --- |
| $8.38 | $8.58 | $0.19 | 0.2017 |
|||||
| **Avg_Price (B-S)** | **Avg_Price (MC)** | **Diff.** | **MSE** |
| $8.38 | $8.59 | $0.21 | 0.0951 |

# Conclusion
This project effectively showcases the viability of using a neural network (NN) model for the complex task of predicting prices for European Basket options. A detailed comparison was conducted against the traditional Monte-Carlo (MC) simulation and the Black-Scholes (B-S) model, focusing on both two-asset and single-asset scenarios. Key findings reveal that the NN model generally forecasts slightly lower option prices for two-asset baskets compared to the MC simulation. However, it's important to note that these results offer valuable insights into the potential and adaptability of neural networks in financial modeling.

The model's current performance, while promising, suggests considerable room for enhancement. Future improvements could include further hyperparameter tuning, which is expected to refine the model's predictive accuracy. Additionally, integrating real-world market data into the training process could significantly bolster the model's robustness and reliability, ensuring a more realistic and practical application in real-world financial scenarios. This project underscores the evolving landscape of financial modeling, highlighting the integration of advanced machine learning techniques as a pivotal development in the field.
