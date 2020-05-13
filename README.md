# Spread-of-COVID-19

Predict the spread of infection in India using various mathematical models used of epidemics.
The intent of this blog is to help understand the transmission dynamics of COVID-19 and recommend operation suggestions
to slow down the epidemic. It is suggested that quickly detecting cases, enough quarantine implementation and public self-protection behaviors are critical to slow down the epidemic.

With growing number of cases have occurred in more than 150 countries and regions, modeling the COVID-19’s transmission dynamics and estimating its development are crucial to provide decision supports for public health departments and healthcare policy makers. Mathematical models are widely used in evaluating epidemic transmissions, forecasting the trend of disease spread, and providing optimal intervention strategies and control measures. Considerable recent studies have contended to estimate COVID-19’s scale and severity, several mathematical models and predicting approaches have attempted to estimate the transmission of COVID-194-8. Majority
of the researches estimated the basic reproductive number R0, a key parameter to evaluate the potential of COVID-19 transmission. However, different models often yield different conclusions in terms of differences in model structure and input parameters. It is imperative and critical to improve early predictive and warning capability for the pandemic.

Data source:
https://api.covid19india.org/data.json

Note: Content from this page is strictly only for educational and research purposes and may contain errors. Also, analysis results and predictions changes day to day based on latest data points.

1. Exponential Model¶

Epidemics in intial stages have exponetial growth.Exponential Growth is characterized by the following formula:
x(t)=x0*b^t
x(t) is the number of cases at any given time t 
x0 is the number of cases at the beginning, also called initial value 
b is the number of people infected by each sick person, the growth factor

Linear Regression for finding the Growth Factor: log x(t)=log(x0)+log(b)*t
we use the log of the number of infections instead of the number of infections we use the log of growth factor instead of growth factor.

Attached graph shows covid infection in India till 26th April follow exponential path. The growth factor is channged from 1.18 to 0.99
![Image description](https://github.com/kadhak/Spread-of-COVID-19/blob/master/Covid%20Exponential%20model_1.PNG)

2. Logistic model:
The logistic model’s essence is that curve fitting and its prediction results highly depend on the historical data. It has been often used in epidemics dynamics prediction in previous studies. Mathematically, the logistic model describes dynamic evolution of infected individuals being controlled by the growth rate and population capacity. Below equation

Logistic model on the other hand predicts the eventual decay.
I(t) = c/1 + exp(-(x-b)/a)

a: infection speed
b: the day with maxium infections occured
c: total number of recorded infected people at infection's end
x: time

We used the least squares method to fit the logistic growth function, and then to predict the number of future confirmed cases. Since the case numbers reported at very early stage are usually inaccuracy or missing, the initiate date of the model was set as the day since the 100th confirmed case was reached. That is 14th March 2020 with 102 total confirmed cases and 2 deaths

Attached graph shows predicts the end of covid infection in India using data till 13th May.
![Image description](https://github.com/kadhak/Spread-of-COVID-19/blob/master/Covid%20Logistics%20Model_1.PNG)

Model Results: as of 13th may 2020
Infection speed(a):  11.532127642948556  and the day with maxium infections occured from 2020-03-14 =  62.37142227396574  and Maximum infected cases =  172532.3778604776  on: 12 October 2020
Death speed(a):  11.004341994256052  and the day with maxium death occured from 2020-03-14 =  59.92882630078968  and Maximum death cases =  5063.83544275687 on: 16 August 2020

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

One can derive β and γ parameters by fitting real epidemic data to the curve using optimize.curve_fit() function.
Attached graph shows fitting data to non linear curve. SIR model for India covid data.
![Image description](https://github.com/kadhak/Spread-of-COVID-19/blob/master/Fitting%20SIR%20curve%2029%20march.PNG)

1. When initiatal date of the model was set as the day since the 1000th confirmed case was reached. That is 28th March 2020 with 1019 total confirmed cases and 14 deaths. We get below predictions.
![Image description](https://github.com/kadhak/Spread-of-COVID-19/blob/master/SIR%20model%2028%20march.PNG)
Maximum number of infected people: 79785.7199031136 on: 17 May 2020

2. When initiatal date of the model was set as 29th march 2020 with 1139 total confirmed cases and 15 deaths. We get below predictions.
![Image description](https://github.com/kadhak/Spread-of-COVID-19/blob/master/SIR%20model%2029%20march.PNG)
Maximum number of infected people: 104968.91224885875 on: 22 May 2020

3. When initiatal date of the model was set as 8th April 2020 with 5915 total confirmed cases and 25 deaths. We get below predictions.
![Image description](https://github.com/kadhak/Spread-of-COVID-19/blob/master/SIR%20model%208%20april.PNG)
Maximum number of infected people: 96791.96090693276 on: 24 May 2020

We can see that with reproduction rate as (1.026,1.0) (R0>1) there can be approx. 29246 infected cases in India.Since there is no cure developed yet for COVID-19,non-pharmaceutical measure are required. Avoiding close contact with infected individuals and keeping personal hygienic are some of the suggested steps.

Government of India have been taking strict actions since early march. Starting with internation travel ban, 1 day voluntary lockdown(Janta curfew)on 23rd March, 21 days lockdown from 25th march till 15th April followed by today's annoucement to extend lockdown till 3rd May. These actions are to reduce person-to-person contact to reduce the spread of infection. 

MODEL WITH GOVERNMENT INTERVENTION IS BASED ON OLDER DATA.IT'S BIT TRICKY AS R_0 NEEDS TO VARIED WITH TIME.NEED TO BE UPDATED

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

I have used optimize.curve_fit() function to derive β,σ and γ parameter from the real data.I have used data since 2nd march till 26th April as since then the number of infected cases started to rise.

R_0 = 1.026.Using these parameters and solving above equation we can do prediction.

![Image description](https://github.com/kadhak/Spread-of-COVID-19/blob/master/Fitting%20SEIR%20curve.PNG)

References:
1. https://www.idmod.org/docs/hiv/model-seir.html#seir-without-vital-dynamics.
2. https://www.kaggle.com/super13579/covid-19-global-forecast-seir-visualize.
3. https://www.medrxiv.org/content/10.1101/2020.03.26.20044289v1.full.pdf




