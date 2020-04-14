# Spread-of-COVID-19

Predict the spread of infection in India using various mathematical models used of epidemics.
These model project how infectious diseases progress to show the likely outcome of an epidemic and help inform public health interventions.

Data source:
https://api.covid19india.org/data.json

1. Exponential Model¶

Epidemics in intial stages have exponetial growth.Exponential Growth is characterized by the following formula:
x(t)=x0*b^t
x(t) is the number of cases at any given time t 
x0 is the number of cases at the beginning, also called initial value 
b is the number of people infected by each sick person, the growth factor

Linear Regression for finding the Growth Factor: log x(t)=log(x0)+log(b)*t
we use the log of the number of infections instead of the number of infections we use the log of growth factor instead of growth factor.

Attached graph shows covid infection in India till 13th April follow exponential path.
![Image description](C:\Users\KaminiK\Desktop)

2. Logistic model

Logistic model on the other hand predicts the eventual decay.
I(t) = c/1 + exp(-(x-b)/a)

a: infection speed
b: the day with maxium infections occured
c: total number of recorded infected people at infection's end
x: time

Attached graph shows predicts the end of covid infection in India using data till 13th April.

3. SIR model

The flow of this model may be considered as follows:
S--> I-->R
S(t) is used to represent the number of individuals not yet infected with the disease at time t, or those susceptible to the disease.

I(t) denotes the number of individuals who have been infected with the disease and are capable of spreading the disease to those in the susceptible category.

R(t) is the compartment used for those individuals who have been infected and then removed from the disease, either due to immunization or due to death. Those in this category are not able to be infected again or to transmit the infection to others.

The transition rates from one class to another are mathematically expressed as derivatives, hence the model is formulated using differential equations. While building such models, it must be assumed that the population size in a compartment is differentiable with respect to time and that the epidemic process is deterministic.

dS/dt=-βSI/N

dI/dt=βSI/N-γI

dR/dt=γI

β:the contact or infection rate of the disease.

γ:the mean recovery/death rate(1/γ the mean infective period).

One can derive β and γ parameters by fitting real epidemic data to the curve using optimize.curve_fit() function. Using these parameters and solving above equation we can do prediction.

Attached graph shows fitting data to non linear curve. SIR model for India covid data.


