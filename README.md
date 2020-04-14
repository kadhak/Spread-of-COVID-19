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
![Image description](https://github.com/kadhak/Spread-of-COVID-19/blob/master/Covid%20Exponential%20model.PNG)

2. Logistic model

Logistic model on the other hand predicts the eventual decay.
I(t) = c/1 + exp(-(x-b)/a)

a: infection speed
b: the day with maxium infections occured
c: total number of recorded infected people at infection's end
x: time

Attached graph shows predicts the end of covid infection in India using data till 13th April.
![Image description](https://github.com/kadhak/Spread-of-COVID-19/blob/master/Covid%20Logistics%20Model.PNG)

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

One can derive β and γ parameters by fitting real epidemic data to the curve using optimize.curve_fit() function. I have used data since 2nd march till 14th April as since then the number of infected cases started to rise.
R_0=1.026 .Using these parameters and solving above equation we can do prediction.

Attached graph shows fitting data to non linear curve. SIR model for India covid data.
![Image description](https://github.com/kadhak/Spread-of-COVID-19/blob/master/Fitting%20SIR%20curve.PNG)
![Image description](https://github.com/kadhak/Spread-of-COVID-19/blob/master/SIR%20modlel%20without%20Intervention.PNG)

We can see that with reproduction rate as 1.026 (R0>1) there can be approx. 465831 infected cases in India.Since there is no cure developed yet for COVID-19,non-pharmaceutical measure are required. Avoiding close contact with infected individuals and keeping personal hygienic are some of the suggested steps.

Government of India have been taking strict actions since early march. Starting with internation travel ban, 1 day voluntary lockdown(Janta curfew)on 23rd March, 21 days lockdown from 25th march till 15th April followed by today's annoucement to extend lockdown till 3rd May. These actions are to reduce person-to-person contact to reduce the spread of infection. 

Lets implement these in our model. Keeping the recovery rate (γ) as same we change the contact or infection rate(β).
![Image description](https://github.com/kadhak/Spread-of-COVID-19/blob/master/SIR%20model%20with%20government%20%20Intervention.PNG)

Change in beta value is derived by trial and error to fit the actual infected numbers till date. Understanding and approach may vary.
Using this we see peak is with approx 17600 on mid April.

Simple SIR model does not account for latency period.Individuals who are exposed (E) have had contact with an infected person, but are not themselves infectious. In case of COVID-19 we have observed that exposed individual may not show symptoms immediately but after certain days of exposure. Thus lets also consider SEIR model.

4. SEIR Model (Susceptible - Exposed - Infectious - Recovered)
The flow of this model may be considered as follows:
S-->E-->I-->R


dS/dt=-βSI/N

dE/dt=βSI/N-σE

dI/dt=σE-γI

dR/dt=γI

where N = S + E + I + R is the total population.

β:the contact or infection rate of the disease.

σ:the Incubation Rate(1/σ the mean period of incubation).

γ:the mean recovery/death rate(1/γ the mean infective period).

I have used optimize.curve_fit() function to derive β,σ and γ parameter from the real data.I have used data since 2nd march till 14th April as since then the number of infected cases started to rise.

R_0=1.026 .Using these parameters and solving above equation we can do prediction.

![Image description]()

References:
1. https://www.idmod.org/docs/hiv/model-seir.html#seir-without-vital-dynamics




