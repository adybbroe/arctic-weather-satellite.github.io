---
layout: page
title: News and Results
---

## Status (end of September 2024):

The project has setup:

 - an AWS direct data broadcast ground segment to receive the data in
   near real-time, and
 - a special version of the operational regional HARMONIE-AROME Numerical
   Weather Prediction (NWP) system to assimilate AWS radiances

We are currently waiting for updated L0/L1 processors from ESA, updated sample
data (raw and level-1b) and access to live orbital parameters (Two-Line element
files - TLEs). Once we have that we can finish the setup of the Nordic ground
segment (see <a href="data_access.html">here</a>) and do any possible final
adjustments to the NWP modelling system. Then when satellite commissioning has
been completed we will start the real-time data acquisition and processing and
start the actual evaluation of data.

## Data evaluation procedure

The project aims at performing an early evaluation of the quality of AWS data
and its potential benefit in operational regional NWP at high latitudes. We will
investigate how AWS brightness temperatures fit and benefit to the NWP
model background using different metrics such as time series of the mean
and standard deviation of first-guess departures statistics, analysis
increments, forecast scores. AWS radiances will also be compared to other
microwave instruments with similar weighting functions by computing "double
differences" using large samples of data.