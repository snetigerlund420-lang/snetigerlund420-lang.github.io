---
title: "Simulation-Based Radar Target Tracking"
period: "2026"
summary: "An FMCW radar simulation paired with a Kalman/EKF tracking layer, built with a friend as a semester side project under a lightweight V-model process."
tags: ["state-space models", "Kalman filtering", "stochastic processes", "Python"]
repo: "https://github.com/yourusername/radar-tracking"   # <- point this at the real repo
featured: true
order: 1
---

<!--
  EDIT ME: this is a drafted skeleton based on what you've described,
  not a finished write-up. Replace the bracketed notes, add a plot or
  two if you have them (drop images in assets/img/ and reference them
  with ![](/assets/img/your-plot.png)), and cut anything that doesn't
  hold up.
-->

## What it is

A two-person project simulating radar-based target tracking end to end: an FMCW signal chain generating noisy range/velocity measurements, feeding into a state-space tracking layer that estimates the target's true trajectory. My friend, an electrical engineering student, owns the radar signal chain; I own the tracking layer.

## My contribution

I designed the target motion model and the estimator that tracks it. The tracking layer is a Kalman filter / extended Kalman filter over a state-space model of the target's motion, taking the radar's raw measurements as noisy observations of an underlying state we don't see directly.

## The interesting decision

The first version modelled motion in Cartesian coordinates with constant angular speed. It technically worked, but it forced the target into unrealistic single-direction orbiting — the model had no way to express a target that speeds up, slows down, or reverses direction, which is exactly the behavior you'd want to track in a real setting.

I replaced it with an Ornstein-Uhlenbeck (OU) process on range and angular velocity in polar coordinates. Mean-reverting dynamics let the target's angular velocity wander and revert around a baseline instead of being pinned to one constant value, which is a much more honest model of how a real target moves — and it's the same mathematical object used to model mean-reverting interest rates (Vasicek) or mean-reverting spreads in pairs trading. [OPTIONAL: say a sentence here about why that connection mattered to you, or cut this if it feels like it's overreaching for a project readme.]

## A bug worth mentioning

While tuning the OU process, I found a mismatch between the model's discrete-time update and its intended stationary variance — I was carrying a standard deviation through an update that expected a variance, which is a one-character-looking bug that quietly changes the entire noise scale of the process. Catching it meant checking the simulated process's stationary variance against the analytical formula rather than trusting that "it runs and produces plausible-looking noise."

There's also a timescale-matching issue worth naming: mean-reversion in an OU process is only visible in a simulation if the sampling interval is short relative to the reversion timescale — sample too coarsely and a mean-reverting process just looks like a random walk.

## Process

We ran this as a lightweight V-model: requirements and interface definitions before implementation, version control via Git, and documentation in LaTeX. [ADD: a sentence on why the V-model was a deliberate choice, if it was, or what it bought you over just building ad hoc.]

## What I'd point a reader to

- [ADD a link or two: the repo file with the OU implementation, the Kalman/EKF update step, a plot of true vs. estimated trajectory]
