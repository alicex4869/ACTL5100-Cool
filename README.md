# 2022 SOA Challenge: Construction of a Competitive national football team for Rarita

**The University of New South Wales**

**Team Cool**

**Team Member: YIXUAN WANG, WENYAN REN, BIHAN SHEN, YIFAN XIAO, YIFAN LI**

<p align="center">
<img src="football.gif"  width="700" height="500"/>
</p>


---

## Overview

This page is used to showcase our project briefly. This showcase page will include brief discussion on the main objective of the project, assumptions, team selection, expense and revenue analysis, implementation, economic impact, risks and risk mitigation, and data and data limitation.

> To access the full report, please click [Full Report](Team Cool_Report of Construction of the Competitive national football team for Rarita.docx).
> To find more details on 2022 SOA Challenge, please click [2022 SOA Challenge] (https://www.soa.org/research/opportunities/2022-student-research-case-study-challenge/).

---

## Objectives

Football has been a heavily watched sport worldwide and the success of the national soccer team can bring positive effects on a country’s economy. The international Football and Sporting Association (FSA) gets increasingly more attention in the world the winning countries’ global visibility enhances; it attracts many new investments, develops the national tourism and political influence hence accelerating the economic growth. Therefore we plan to construct a “competitive” national soccer team for Rarita which aims to become top 10 members of the FSA in the next five years with relatively high probability of being an FSA champion. In addition, some potential impacts of the construction of such a national team on Rarita’s economy over next 10 years are also discussed.

## Assumptions

* Metrics in players’ data is regarded as standardized values with a “special” method. We regarded some “negative” metrics as indicators of  “extremely” bad performance;
* Assume that players employed by other countries which attend tournament are all  local players hence their football-soccer expense does not include foreign players’ salaries.
* Purchasing Power Parity theory. Assume that Rarita’s currencies should have the same purchasing power with other currencies after adjusting for exchange rate- i.e. prices of the same goods/services should be equal when they are expressed in Doubloons.
* Assume that the outflow of expenses and the inflow of revenues are at end of each year;
* Discount rate – 4.45% 

The average rate for nominal spot rates of risk-free bonds mature in 2032 which is higher than that of earlier maturity hence being more conservative.

<p align="center">
<img src=" discount_rate_estimate.png "  width="200" height="300"/>
</p>


* Annual percentage rate for 6-year loan - 2.8%

The average of nominal risk-free rate for the maturity of 6 years during the year 2010-2020

## Team Selection

### <u>Structure</u>

Rarita needs 25 footballers to build a formative national team, including 11 starters and 14 substitutes.

### <u>Data Preparation</u>

**1.Missing value**

To build the model to help us select team we mainly use the tournament information (which has the results) provided. We found that defensing and passing data only include the information of 2021 tournament. Although there are some 2020 data of shooting performance however there exists high proportion of missing for some metrics (e.g. Standard Dist has 100% of missing) therefore we only use data for 2021 tournament to build model in this project.

> Missing data for shooting and goalkeeping:
>
> <p align="center">
> <img src="missing_data_shooting.png"  width="650" height="400"/>
> </p>
>
> <p align="center">
> <img src="missing_data_goalkeep.png"  width="650" height="400"/>
> </p>

**2.variable selection**

We first checked the correlations and analyzed the meaning of metrics to reduce the dimensions. Through analysis of correlations and meanings we remove some metrics which have similar representatives with another metric(s).

> Correlation matrix plots:
>
> <p align="center">
> <img src="passing.png"  width="400" height="400"/>
> </p>
>
> <p align="center">
> <img src="goalkeeping.png"  width="400" height="400"/>
> </p>




### <u>Entropy weighted method</u>

First we standardized both league and tournament data. Then we separate 4 original metrics into 7 independent metrics based on positions:

* Forward: shooting
* Forward: passing
* Midfielder: defense
* Midfielder: passing
* Defender: defender
* Defender: passing
* Goalkeeper: goalkeeping

Furthermore, there are numerous minor measurement features in each main metric which could significantly increase the model complexity. Also, our team are lack of experiences in soccer which the subjective weighted methods are not suitable in this case. Thus, we applied Entropy Weight Method (EWM) to determines the objective index weight for each minor measurements according to the dispersion degree and calculate an overall score for each major metric. Moreover, since the success of soccer team is based on the performance of every player, therefore, we take the average score for each team by position for further analysis instead of solely considering the personal performance. 

After the data manipulation procedures, the dimension of measurement for each nation are reduced to 7 variables that explain the tournament rank:
![](/Users/yifanxiao/Desktop/tournament_rank.png)

> Example of entropy weighted method applied to forward shooting:
> Standardized data:
> ![](/Users/yifanxiao/Desktop/Standardized_ShootingFW.png)
> Index’s Entropy:
> ![](/Users/yifanxiao/Desktop/Index_Entropy_ShootingFW.png)
> Entropy weight:
> ![](/Users/yifanxiao/Desktop/Entropy_weight_ShootingFW.png)

### <u>Modelling and team selection</u>

Rather than directly choosing players from league data based on scores, we did regression analysis in advance to discover the relative significance of scores for each position on the overall rank. We replace the rank by 1 and 0 with 1 indicates successfully achieving top 10 in FSA and implement logistic regression to derive success rate. The relative significance of variables is based on AIC stepwise selection. In addition, we checked the feature importance by random forest method which also provide a similar result on variable significance. The variables chosen for modelling are ShootingFW, PassingFW, PassingDF, DefenseMF, and GoalkeepingGK.

<p align="center">
<img src=" feature_importance.png "  width="300" height="300"/>
</p>

The selection of Rarita team is generally based on scores of ShootingFW, PassingDF, DefenseMF, and GoalkeepingGK for corresponding positions. We choose the players with top 5% scores in league from Rarita and then hire top players from other nations if there are insufficient players in the team. 

| Player         | Nation                  | Pos  |
| -------------- | ----------------------- | ---- |
| K. Adong       | Dosqaly                 | FWMF |
| F. Akongo      | Nganion                 | MFFW |
| A. Perez       | Rarita                  | FW   |
| V. Zhao        | Rarita                  | MF   |
| H. Jew         | Landsfupua              | GK   |
| L. De Wit      | Greri Landmoslands      | FW   |
| L. Ndyanabo    | Imaar Vircoand          | FWMF |
| D. Tukamuhebwa | People's Land of Maneau | FW   |
| H. Makumbi     | Rarita                  | FW   |
| F. Acayo       | Rarita                  | DF   |
| H. Azizi       | Rarita                  | DF   |
| K. Musah       | Rarita                  | DF   |
| P. Murmu       | Rarita                  | DF   |
| R. Mensah      | Rarita                  | DF   |
| W. Mbaziira    | Rarita                  | DF   |
| X. Takagi      | Rarita                  | DF   |
| Z. Kakai       | Rarita                  | MFDF |
| N. Bondarenko  | People's Land of Maneau | FWMF |
| U. Angella     | People's Land of Maneau | MF   |
| M. Ludwig      | Rarita                  | DFMF |
| O. Tshuma      | Rarita                  | DFMF |
| V. Sultan      | Rarita                  | DFMF |
| B. Ayuba       | Rarita                  | MF   |
| F. Akumu       | Rarita                  | GK   |
| W. Nasiru      | Rarita                  | GK   |



> Players selected:

<p align="center">
<img src=" team_selected.png " />
</p>



## Expense and Revenue

### <u>Expense</u>

a. Calculated the average expenses (total, staff cost and commercial) of top 10 countries in tournament as the expected total football expense for a country which assembles a competitive national team.(in 2020 total expense: ∂279.92, staff cost: ∂189.07,other expense:∂90.85)

b. Subtracting corresponding Rarita’s original expense (without national team) as the direct expenses of the team.( ∂131.23 in 2020)

c. Adjusting with adjusting factors (1.1 for first 3 years and 1 afterwards)

d. Adding expenses on foreign players to get the total (per Capita) team expense

e. From 2021, each term used in calculation should be derived by multiplying the corresponding term of the last year inflation factor. 
![](/Users/yifanxiao/Desktop/expense_prediction.png)

> Predicted inflation rates, populations for Rarita, expenses for foreign players:

<p align="center">
<img src=" inflation.png " />
</p>


![](/Users/yifanxiao/Desktop/population.png)
![population estimate](/Users/yifanxiao/Desktop/populaion_estimate.png) ![foreign players](/Users/yifanxiao/Desktop/expense_foreignplayers.png)

### <u>Revenue</u>

Revenues are predicted with the similar process with expenses projection. The only difference is that there is no revenue from foreign players.
![](/Users/yifanxiao/Desktop/revenue_prediction.png)

### <u>Net income</u>

After predicting expenses and revenues the net income over the next 10 year are also generated:
![](/Users/yifanxiao/Desktop/profit.png)

Initial losses existed for first three years after construction of the national team. In addition to ∂ 995000000 of Rarita’s one-time fund the team still needs the fund of ∂305836631.64 to cover these excess expenses. A six-year loan can be made in 2022 to raise the capital needed. 

We are provided with nominal risk-free spot rate yield curves for different issuance years and maturities which can be used to estimate discount rate. To be conservative, we used 4.45% (highest) as discount rate to calculate NPV.

<p align="center">
<img src="discount_rate_estimate.png " />
</p>


Consequently, the net present value of net incomes generated by the national team from 2022 to 2031 is about ∂ 495443295.16.
![](/Users/yifanxiao/Desktop/NPV.png)

> To access more details about projection and calculation of NPV, please see [revenue and expense](Revenue_expense.xlsx).

## Economic Effects

### <u>Impact on other industries</u>

If the national soccer team we constructed is a competitive team, which means it reaches the top 10 in FSA, the impact that comes from being competitive will certainly boost other related industries, such as local tourism, manufacturing of sportswear and equipment, online broadcasting, and media industry.

### <u>International impact and net exports</u>

It seems no exaggeration to say that excellent national sports results can enhance international influence of a country to some extent, which is also a reflection of comprehensive national strength. A country with stable economic development and high international influence is relatively less at risk of capital flight than a country with political instability. Furthermore, countries with the high international influence will also increase the awareness of their products and the trust of more foreign investors and customers.

## Implementation plan

* 2022: do the preparatory work
* 2023-2027: participate and get the qualification
* 2028: repay the loan 
* 2029-2032: Keep monitoring (revenue and growth on GDP) and lend the substitutes to other countries, if possible, to achieve extra revenue     

Key metrics to monitor:

1.	The win percentage and the ranking, which directly represents the strength (twice a year) 
2.	The players’ statistics which can help the coach team to adjust. (twice a year) 
3.	Occupancy rate and audience rating (once a year) 
4.	The actual revenue/expense and compare with the expected one (once a year) 
5.	The growth in GDP (once a year） 

## Risk and Risk mitigation

### <u>biased data</u>

There has been a concern about data sets for foreign players, where the information of best players could be hidden or changed by their countries rather than exposed to the public. The issue can cause an overestimation of the competitiveness of our team.

**Mitigation: Obtain player information from multiple channels and keep track of the competition.**

### <u>misjudged expense</u>

Detailed dimensions for historical expense data are not provided, so whether there is an extra budget for training before competition is unknown. The first attempt at this challenge may cost more than expected.

**Mitigation: Add 6% loading to extreme scenario.**

### <u>sensitivity test of annual percentage rate and discount rate</u>

* For discount rate, the NPV of net income would be within 10% of the projection if it is within (1.47%, 7.63%)

* For risk-free rate, the NPV of net income would be within 10% of the projection if it is within (0%,5.65%)

* The choices of risk-free rate and discount rate can influence the projected NPV for the national team over 2022-2031. There is about a range of ∂118M in the NPV by varying the discount rate between 1.5% and 7.5%. There is about a range of ∂121M in the NPV by varying the annual percentage rate between 1% and 6%.
    ![](/Users/yifanxiao/Desktop/sensitivity.png)

## Data and Data Limitation

### <u>Data used</u>

Data used are provided by SOA: [2022 SOA Challenge]( https://www.soa.org/research/opportunities/2022-student-research-case-study-challenge/).

### <u>Data limitation</u>

* Lack of data for players and revenue/expenses
* Unusual data in players’data

---

Overall, the team we selected has the expected probability of success of about 70% which is not bad. Although assembling the national team seemly will not earn so much money the potential economic growth that the construction of such a competitive team will bring is a more significant consideration.

---

> Feel free to see [report outline](group outline_group cool.docx), [full report](Team Cool_Report of Construction of the Competitive national football team for Rarita.docx), [team selected and corresponding costs](team-selected.csv), and [R codes for project](Team Cool_codes_RMarkdown.Rmd).
> ![](/Users/yifanxiao/Desktop/thanks.gif)

