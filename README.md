# European Options Pricing: Black-Scholes vs. Monte Carlo Convergence

## Objective
To implement the closed-form Black-Scholes-Merton (BSM) analytical pricing model and empirically validate it against a vectorized Monte Carlo numerical simulation. The project demonstrates the Law of Large Numbers and explores the computational cost of variance.

## Mathematical Framework

### 1. Analytical Solution (Black-Scholes)
The exact price of a European Call Option is calculated using the BSM formula:

$$C = S_0 N(d_1) - K e^{-rT} N(d_2)$$

Where $d_1$ and $d_2$ incorporate the underlying price, strike, risk-free rate, time to maturity, and implied volatility.

### 2. Numerical Solution (Monte Carlo)
The numerical pricer simulates the terminal stock price $S_T$ using the exact solution to Geometric Brownian Motion:

$$S_T = S_0 \exp\left( \left( r - \frac{\sigma^2}{2} \right)T + \sigma \sqrt{T} Z \right)$$

The expected payoff is calculated as $\max(S_T - K, 0)$ and discounted to present value using $e^{-rT}$.

## Implementation Details
* **Vectorization:** The Monte Carlo engine bypasses standard loops, utilizing `numpy` arrays to instantly compute the payoffs for $1,000,000+$ simulated paths.
* **Defensive Programming:** The analytical pricer incorporates boundary checks for strict positivity constraints on strike, volatility, and time to expiry.

## Results: Law of Large Numbers

*(Insert your `convergence_plot.png` here using `![Convergence Proof](images/convergence_plot.png)`)*

The numerical simulation demonstrates high initial variance at low sample sizes ($M < 1,000$). As the number of paths increases ($M \to \infty$), the standard error collapses, and the Monte Carlo price converges perfectly onto the Black-Scholes analytical ground truth.

## Sensitivity Analysis: The Cost of Volatility

Extended testing was conducted across different volatility ($\sigma$) regimes. Observations:
* **Low Volatility Regime:** The Monte Carlo simulation converges rapidly with fewer required paths.
* **High Volatility Regime:** The terminal price distribution widens significantly. Due to the relationship between standard error and variance ($SE = \frac{s}{\sqrt{M}}$), high-volatility environments require exponentially larger sample sizes to achieve the same precision as the analytical model. 

This confirms that while Monte Carlo is a powerful tool for complex, path-dependent derivatives, its computational cost scales aggressively with the asset's variance.
