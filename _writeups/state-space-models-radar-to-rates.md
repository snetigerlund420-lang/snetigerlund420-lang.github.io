---
title: "One Model, Two Worlds: State-Space Estimation from Radar to Interest Rates"
date: 2026-08-25
summary: "Why the same mean-reverting state-space model shows up in a radar tracking project and in interest-rate modelling — and what that says about learning math for finance."
related_project: /projects/radar-target-tracking/
---

<!--
  EDIT ME: this is a skeleton built around the analogy you drew between
  the radar project's OU/Kalman work and Vasicek-style rate models. Replace
  the bracketed notes with your own derivation/plot/example, or cut a
  section if it doesn't earn its place. Keep this short — one page,
  one idea, done well, beats a long survey.
-->

Two problems that look unrelated turn out to be the same problem wearing different clothes. In a radar tracking project, I needed a model for a target's angular velocity that could speed up, slow down, and reverse — not spin at one constant rate forever. In self-studying mathematical finance, I kept running into the same equation used to model a mean-reverting interest rate. It's the same process.

## The model

An Ornstein-Uhlenbeck (OU) process describes a quantity that drifts back toward a long-run mean, with the pull toward that mean proportional to how far away it currently is:

```
dX_t = θ(μ − X_t) dt + σ dW_t
```

[ADD: one or two sentences in your own words on what θ, μ, σ each control, and why this shape — as opposed to, say, a plain random walk — is the right one for a mean-reverting quantity.]

- In the **radar project**, X_t is the target's angular velocity, mean-reverting instead of constant, which lets the tracked target behave like something real rather than an object stuck in a perfect circle.
- In **interest-rate modelling** (the Vasicek model), X_t is the short rate, mean-reverting toward a long-run level instead of drifting off unboundedly.
- The same structure also shows up in **pairs trading**, where the spread between two cointegrated assets is modelled as mean-reverting, and the trading signal is essentially "how far has X wandered from μ, and how fast should I expect it back."

## Why this mattered practically

Getting the OU process right in the radar project wasn't just theoretical — [ADD a sentence tying this to the actual bug you found: the variance/std-dev mismatch in the discrete update, and/or the timescale-matching issue, and what checking against the analytical stationary variance taught you about validating a stochastic simulation rather than trusting that it "looks reasonable."]

## Where the estimation side connects

Once you have a state that evolves like this but that you can't observe directly — only noisy measurements of it — you need an estimator. That's what a Kalman filter is for: it combines a model's prediction of the state with a new noisy observation, weighted by how much you trust each. [ADD: a sentence connecting this to how a Kalman filter is used to infer an unobserved short rate or unobserved volatility from noisy market data, if you want to make the finance-side estimation connection explicit rather than leaving it as an exercise for the reader.]

## Takeaway

[ADD: one closing sentence — what this exercise showed you about self-studying math for finance: that the same handful of stochastic building blocks (mean reversion, filtering, estimation under noise) reappear everywhere once you know to look for them, which is why building something concrete with them (the radar project) was worth more than reading about them in isolation.]
