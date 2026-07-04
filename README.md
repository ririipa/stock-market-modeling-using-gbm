# stock-market-modeling-using-gbm
Simulates synthetic stock price paths using Geometric Brownian Motion, built with NumPy, Pandas, and Matplotlib.

# Stock Market Modeling with Geometric Brownian Motion

A project exploring how to synthetically generate stock market data that approximates real-world stock behavior, built while following along with a YouTube tutorial.

## Tools Used

- **NumPy** — for numerical operations and random number generation
- **Pandas** — for handling and structuring stock market data
- **Matplotlib** — for visualizing simulated vs. real stock price paths

## What This Project Does

This project stochastically models stock market behavior by generating close approximations of actual stock market returns. Rather than being truly random, the numbers generated are *reasonably* random — meaning they're constructed to give a percentage change in a stock or stock market index over a given time step that approximately matches real stock market returns.

In other words: it mimics a reasonable path that an actual stock might take, without being an exact prediction.

## Core Concept: Random Walks

At its core, this kind of stock simulation is a **random walk** — a path built from a series of random steps, where each step represents the percentage change in a stock/index over a small amount of time.

The building block used here is **Geometric Brownian Motion (GBM)**.

## Geometric Brownian Motion (GBM)

### Continuous Time

Let `S_t` = the price of a stock (or stock market index) at time `t`.

The change in the stock's dollar value over time is described by:

```
dS_t = μ S_t dt + σ S_t dW_t
```

Where:
- `dS_t` — the change in dollar value of the stock/index at time `t`
- `dt` — a tiny amount of time (an infinitesimal time step)
- `μ` — the **drift** (average/expected rate of return)
- `σ` — the **volatility** of the stock
- `dW_t` — a random component (Brownian motion / Wiener process)

Since real data is discrete (not continuous), we need to convert this into discrete time steps to actually simulate it.

### Discrete Time

To simulate this on a computer, time is broken into discrete steps rather than continuous flow. The percentage change of the stock over one time step `dt` is given by:

```
(S_(t+dt) - S_t) / S_t = μ·dt + σ·√dt·X_t
```

Where:
- `S_(t+dt)` — the stock price at the next time step
- `S_t` — the stock price at the current time step
- `μ·dt` — the drift component scaled by the time step
- `σ·√dt·X_t` — the volatility component, scaled by the square root of the time step and multiplied by a random variable `X_t` (drawn from a standard normal distribution)

This equation tells us how much time moves the stock price by `S_t`, giving the percentage change needed to step forward to `S_(t+dt)`.

Rearranged to solve for the next price:

```
S_(t+dt) = S_t + S_t·(μ·dt + σ·√dt·X_t)
```

## Key Parameters

| Symbol | Meaning |
|--------|---------|
| `μ` (mu) | Drift — the average expected return |
| `σ` (sigma) | Volatility — how much the stock price fluctuates |
| `dt` | Discrete time step |
| `X_t` | Random variable (standard normal distribution) at time `t` |

## Data

The model can be built using either:
- **Real historical stock data**, or
- **Randomly generated data**

to gather the parameters (drift and volatility) used to drive the simulation.

## Notes

This README is based on handwritten notes taken while following along with a YouTube tutorial on stock market modeling using GBM. It's meant as a reference for the core math and concepts behind the simulation, alongside the code in this repo.
