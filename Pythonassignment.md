<H1> Applied Economic Analysis - Python Assignment </H1>
<H2> Topic: Historical Origins of Economic Development </H2>

By - <Br>
<a href="https://github.com/Lkhagvaa-1995"> Lkhagvaa Erdurensen (u810977) </a> <BR>
<a href="https://github.com/UtsavSaksena"> Utsav Saksena (u629797) </a> 

<H3>Abstract and Introduction: </H3>
<P> 
Historical processes have played a huge role in determining the state of the world today: both politically and economically. From the late 18th century onwards, imperialism in the form of conquering/setting up of colonies is a good example of such a process. In the literature, the works of <a href="https://econ-papers.upf.edu/papers/202.pdf">Bertocchi and Canova (1996)</a> and <a href="http://faculty-staff.ou.edu/G/Robin.M.Grier-1/colonialism.pdf">Grier (1999)</a> have palced some emphasis on the post-colonial experiences of erstwhile European Colonies, but a breakthrough was obtained with the paper <a href="http://economics.mit.edu/files/4123">‘The Colonial Origins of Comparative Development: An Emperical Investigation’</a> by Acemoglu, Johnson, and Robinson that was published in 2001. 

A truly fascinating read for academics and policy makers alike, it played a crucial role in joining the links of development that were theorized in earlier research, but were not well validated empirically.  It outlines a methodology that explains fundamental causes of large differences in income per capita across countries through the lens of historical data. 
</P>

<H3> Theory: </H3>
<P>
Briefly, the economic theory that underlies this model is as follows -  ‘good’ political, financial and legal institutions  are causally associated to more secure property rights & less scope of excessive government intervention. This implies a lower level and likelihood of distortionary policies being implemented. In the form of higher investment in physical and human capital and their efficient use in production leads to higher levels of income (<a href="http://www.eh.net/?s=The%20rise%20of%20the%20western%20world">North and Thomas, 1973</a>; <a href="http://www.cambridge.org/nl/academic/subjects/history/global-history/european-miracle-environments-economies-and-geopolitics-history-europe-and-asia-3rd-edition?format=PB&isbn=9780521527835">Jones, 1981</a>). 

<P>
In the paper, the authors exploit differences in European mortality rates to estimate the effect of institutions on current economic performance. The ‘chain of causality’ can be visualised <a href="https://github.com/UtsavSaksena/Python/blob/master/graphic%201.svg"> here</a> - 
</P>


```python
import graphviz as gv
g1 = add_edges(
    add_nodes(digraph(), [
        ('A', {'label': 'Settler Mortality'}),
        ('B', {'label': 'Good Institutions'}),
        ('C', {'label': 'GDP/capita'})
    ]),
    [
        (('A', 'B'), {'label': 'First Stage'}),
        (('A', 'C'), {'label': 'Exclusion Restriction'}),
        (('B', 'C'), {'label': 'Second Stage'})
    ]
)
    
def add_nodes(graph, nodes):
    for n in nodes:
        if isinstance(n, tuple):
            graph.node(n[0], **n[1])
        else:
            graph.node(n)
    return graph

def add_edges(graph, edges):
    for e in edges:
        if isinstance(e[0], tuple):
            graph.edge(*e[0], **e[1])
        else:
            graph.edge(*e)
    return graph

import functools
graph = functools.partial(gv.Graph, format='svg')
digraph = functools.partial(gv.Digraph, format='svg')

g1 = add_edges(
    add_nodes(digraph(), [
        ('A', {'label': 'Settler Mortality'}),
        ('B', {'label': 'Good Institutions'}),
        ('C', {'label': 'GDP/capita'})
    ]),
    [
        (('A', 'B'), {'label': 'First Stage'}),
        (('A', 'C'), {'label': 'Exclusion Restriction'}),
        (('B', 'C'), {'label': 'Second Stage'})
    ]
)

styles = {
    'graph': {
        'fontsize': '16',
        'rankdir': 'BT',
    },
    'nodes': {
        'fontname': 'Helvetica',
        'shape': 'square',
        'fillcolor': '#006699',
    },
    'edges': {
        'style': 'dashed',
        'arrowhead': 'open',
        'fontname': 'Courier',
        'fontsize': '12',
    }
}

def apply_styles(graph, styles):
    graph.graph_attr.update(
        ('graph' in styles and styles['graph']) or {}
    )
    graph.node_attr.update(
        ('nodes' in styles and styles['nodes']) or {}
    )
    graph.edge_attr.update(
        ('edges' in styles and styles['edges']) or {}
    )
    return graph

g1 = apply_styles(g1, styles)
g1.render('graphic 1')
```

<H3>Methodology: </H3> 
<P>
To test this hypothesis empirically, they use the instrumental variable approach wherein the mortality rate of colonial settlers (soldiers, priests, bureaucrats, etc.) is used as an instrument for current economic performance. The purpose of using this is to utilize the exogenous variation in mortalities and then use it to explain variation in observed economic performance today. 
In our representation, we seek to test the validity of the use of this variable as an instrument. We do so by way of several ‘naive’ tests and representations. 
</P>

<H3>Assumptions: </H3> 
<P>
The authors make use of the following assumptions in their estimations - 
    <OL>
        <LI> Stark difference in policies used by the colonizers – 
             <OL type="a">
                     <LI> Setting up of extractive states which not did provide protection for private property or checks against                                 government expropriation and set up for transfer resources from the colony to the ‘home’ state </LI>
                     <LI> Settler of ‘Neo-Europes’ (<a href="https://books.google.nl/books/about/Ecological_Imperialism.html?                                     id=Phtqa_3tNykC&redir_esc=y">Alfred Crosby, 1986</a>) placed a strong emphasis on private property and checks                           against excessive government power </LI>
             </OL>
        <LI> Colonialization policies were determined by feasibility of settlements </LI>
        <LI> Colonial states and institutions persisted after independence of countries </LI>
        <LI> Exclusion restriction: Current economic performance does not in any way affected by mortality rates of colonists other     
           than by way of setting up (and prevalence) of economic institutions </LI>
    </OL>       
</P>

<H3> Estimation Equation </H3>

<img src="http://mathurl.com/hra3yxt.png"> 

<P>
In this analysis we are going to estimate the Two-Stage Lease Square as shown in the above equations. <BR>
The <B> instrument </B> is the log value of mortality rate of the colonial settlers when the country <I> i </I> was colonised <BR>
The <B> treatment </B> variable is the index of protection against expropriation - having a value between 0 and 10 for each country and year, with 0 corresponding to the lowest protection level. The average value for each country between 1985 and 1995is used. This is a proxy for the current level of institutional development for each country. <BR>   
The <B> outcome variable </B> is GDP per capita of each country in year 1995. <BR>
As additional covariates we use 'Absolute value of lattitude from equator' (to control for geographical distribution of countries) and 'European Settler Mortality rate' (to control for health levels of populations).
</P>

<H3> Data Analysis </H3>

<P>
In this section, we show some graphs and descriptive statistics. The data has observations from 64 countries. 
</P>

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import os
os.getcwd()
df=pd.read_stata('data_python.dta')
df.head()
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>lat_abst</th>
      <th>euro1900</th>
      <th>excolony</th>
      <th>avexpr</th>
      <th>logpgp95</th>
      <th>cons1</th>
      <th>indtime</th>
      <th>democ00a</th>
      <th>cons00a</th>
      <th>extmort4</th>
      <th>logem4</th>
      <th>country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.136667</td>
      <td>8.000000</td>
      <td>1.0</td>
      <td>5.363636</td>
      <td>7.770645</td>
      <td>3.0</td>
      <td>20.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>280.000000</td>
      <td>5.634789</td>
      <td>125.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.377778</td>
      <td>60.000004</td>
      <td>1.0</td>
      <td>6.386364</td>
      <td>9.133459</td>
      <td>1.0</td>
      <td>170.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>68.900002</td>
      <td>4.232656</td>
      <td>131.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.300000</td>
      <td>98.000000</td>
      <td>1.0</td>
      <td>9.318182</td>
      <td>9.897972</td>
      <td>7.0</td>
      <td>94.0</td>
      <td>10.0</td>
      <td>7.0</td>
      <td>8.550000</td>
      <td>2.145931</td>
      <td>135.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.144444</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>4.454545</td>
      <td>6.845880</td>
      <td>3.0</td>
      <td>35.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>280.000000</td>
      <td>5.634789</td>
      <td>141.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.266667</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>5.136364</td>
      <td>6.877296</td>
      <td>7.0</td>
      <td>23.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>71.410004</td>
      <td>4.268438</td>
      <td>142.0</td>
    </tr>
  </tbody>
</table>
</div>

<P>  
These variables can be explained as follows - 

<Table border="1" type="dataframe">
     <tbody>
          <tr>
               <td> <b> No. </b> </td>
               <td> <b> Code </b> </td>
               <td> <b> Description </b> </td>
           </tr> 
           <tr>
               <td> 1 </td>
               <td> logpgp95 </td>
               <td> GDP per capita in 1995 </td>
           </tr> 
           <tr>
               <td> 2 </td>
               <td> avexpr </td>
               <td> Average risk of expropriation
           </tr>
           <tr> 
               <td> 3 </td> 
               <td> lat_abst </td>
               <td> Absolute value of latitude from equator </td>
           </tr>   
           <tr>
               <td> 4 </td>
               <td> logem4 </td>
               <td> Mortality rate of settlers when colonised </td>
           </tr>
           <tr>
               <td> 5 </td>
               <td> extmort4 </td>    
               <td> Log European settler mortality </td>
           </tr>
    </tbody>
</Table>

<H2> Descriptive Statistics of main variable </H2>
<P> aaaa <P> 

```python
import pandas
df=pd.read_stata('data_graph.dta')
df.describe() 
```

<P> The Output can be seen <A href="https://github.com/UtsavSaksena/Python/blob/master/Desc%20stats.png">here</A>. </P>
 

```python
plt.clf () 
plt.plot(df.avexpr, df.logpgp95, '.', color='red', linewidth=2)
plt.title("GDP per capita 1995 vs Expropriation risk", fontsize=15)
plt.ylabel("$log PPP GDP per capita, 1995, World Bank$", fontsize=10)
plt.xlabel("$average protection against expropriation risk$", fontsize=10)
plt.ylim(6, 10)
plt.xlim(0, 10)
plt.savefig('Graph_10.png')
```

<P> <a href="https://github.com/UtsavSaksena/Python/blob/master/Graph10.png"> Click here to view </a> </P>

```python
plt.clf () 
plt.plot(df.logem4, df.avexpr, '.', color='blue', linewidth=2) 
plt.title("Expropriation risk vs Log settler mortalilty", fontsize=15)
plt.ylabel("$average protection against expropriation risk$", fontsize=10)
plt.xlabel("$log settler mortalility$", fontsize=10)
plt.ylim(0, 10)
plt.xlim(0, 8)
plt.savefig('Graph_20.png')
```
<P><a href="https://github.com/UtsavSaksena/Python/blob/master/Graph20.png"> Click here to view </a> </P>

```python
from plotly.offline import plot
import plotly.graph_objs as go
import plotly.plotly as py
from plotly.graph_objs import Scatter, Layout
df_graph=pd.read_stata('data_graph.dta')

plotly.offline.init_notebook_mode()

plotly.offline.iplot({
"data": [Scatter(
   x=df_graph['loggdp95'],
   y=df_graph['avexpr'],
   text=country_names,
   mode='markers'
)],
"layout": Layout(
    title='Average protection against expropriation risk vs GDP per capita 1995',
    xaxis=XAxis( type='log', title='GPD per capita, 1995' ),
    yaxis=YAxis( title='Average protection against expropriation risk' ),
)
})
```

<a href="https://plot.ly/~Lhagva_1995/5/"> Click here to view an interactive scatter plot </a>

<H4> Econometrics Analysis </H4> 
<P>
We hypothesize that settler mortality affected settlements; settlements affected early institutions; and early institutions persisted and formed the basis of current institutions.First regression table reports ordinary least-squares (OLS) regressions of log per capita income on the protection against expropriation variable.
</P>
```python
from pandas.stats.api import ols
reg1=ols(y=df['logpgp95'], x=df['avexpr'])
reg1
```
    
    -------------------------Summary of Regression Analysis-------------------------
    
    Formula: Y ~ <x> + <intercept>
    
    Number of Observations:         70
    Number of Degrees of Freedom:   2
    
    R-squared:         0.5715
    Adj R-squared:     0.5652
    
    Rmse:              0.6985
    
    F-stat (1, 68):    90.6945, p-value:     0.0000
    
    Degrees of Freedom: model 1, resid 68
    
    -----------------------Summary of Estimated Coefficients------------------------
          Variable       Coef    Std Err     t-stat    p-value    CI 2.5%   CI 97.5%
    --------------------------------------------------------------------------------
                 x     0.5158     0.0542       9.52     0.0000     0.4097     0.6220
         intercept     4.7135     0.3695      12.76     0.0000     3.9892     5.4377
    ---------------------------------End of Summary---------------------------------

<P>
As we can perceive from the regression table, the coefficient for the variable avexpr is positive. For this model the interpretation of this result is as follow. For a unitary increase on average protection against expropriation risk we see that the GDP per capita increases by approximately 67%. Even though we see that the average protection against expropriation risk is statistically highly significant - to support this we have the high t-statistic result and the p-value is zero - we can also say that the results we have obtained in this regression are somewhat overestimated. This overestimation is due to the fact that there are omitted variables that are relevant for our analysis.
</P>
<P>
Second regression table reports ordinary least-squares (OLS) regressions of protection against expropriation on the log value of mortalilty rate of settlers. This regression shows how strongly the instrument variable affects to the treatment variable. 
</P>

```python
# Run regression: avexpr logem4
df=pd.read_stata('data_python.dta')
reg2=ols(y=df['avexpr'], x=df['logem4'])
reg2
```

    
    -------------------------Summary of Regression Analysis-------------------------
    
    Formula: Y ~ <x> + <intercept>
    
    Number of Observations:         70
    Number of Degrees of Freedom:   2
    
    R-squared:         0.3047
    Adj R-squared:     0.2945
    
    Rmse:              1.3041
    
    F-stat (1, 68):    29.7983, p-value:     0.0000
    
    Degrees of Freedom: model 1, resid 68
    
    -----------------------Summary of Estimated Coefficients------------------------
          Variable       Coef    Std Err     t-stat    p-value    CI 2.5%   CI 97.5%
    --------------------------------------------------------------------------------
                 x    -0.6314     0.1157      -5.46     0.0000    -0.8581    -0.4047
         intercept     9.5146     0.5481      17.36     0.0000     8.4403    10.5889
    ---------------------------------End of Summary---------------------------------

<P>
From the regression above we see that the coefficient is negative. What this means is that, for a 1% increase in European Settler mortality rate the average protections against expropriation risk fall by approximately 0,63 units. In this situation we should also look at the value given by the  R-Square: that 30% of the variation on the average protection against expropriation risk is explained by the variable logem4 (European Settler's mortality rate). All in all we have that this instrument is sufficiently strong.
</P>

<P>
Now we estimate the 2SLS in which we take the fitted values of the variable <I> avexpr </I> and run a regression according to equation (2).
</P>
```python
# Keeping predicted value
averpx_hat=9.5146-0.6314*df['logem4']
# Run regression averpx_hat on logpgp95
reg3=ols(y=df['logpgp95'], x=averpx_hat)
reg3
```
    -------------------------Summary of Regression Analysis-------------------------
    
    Formula: Y ~ <x> + <intercept>
    
    Number of Observations:         70
    Number of Degrees of Freedom:   2
    
    R-squared:         0.4935
    Adj R-squared:     0.4861
    
    Rmse:              0.7594
    
    F-stat (1, 68):    66.2673, p-value:     0.0000
    
    Degrees of Freedom: model 1, resid 68
    
    -----------------------Summary of Estimated Coefficients------------------------
          Variable       Coef    Std Err     t-stat    p-value    CI 2.5%   CI 97.5%
    --------------------------------------------------------------------------------
                 x     0.8684     0.1067       8.14     0.0000     0.6593     1.0775
         intercept     2.3698     0.7148       3.32     0.0015     0.9687     3.7708
    ---------------------------------End of Summary---------------------------------

<P>
According to the estimation, for one unit increase on average protection against expropriation risk, the GDP per capita increases approximately 137%. Not only the p-value we obtained is rather small but also the R-Squared is high, with a value of 49% - avexpr_hat explains almost 50% of the variations on the GDP per capita. Having performed the first stage we saw that our instrumental variable (logem4) explains our treatment variable (avexpr) well.
</P>

<H4> Robustness check: Addtional control variables </H4>
<P> The validity of our 2SLS estimation in previos regressions depends on the assumption that settler mortality in the past has no direct effect on current economic performance. Although this presumption appears reasonable (at least to us), here we substantiate it further by directly controlling for many of the variables that could plausibly be correlated with both settler mortality and economic outcomes, and checking whether the addition of these variables affects our estimates.
</P>
<P>
In this analysis, we add (1) absolute value of latitude from equator and (2) log value of mortality rate of European settlers. 
</P>
```python
import numpy as np
import pandas as pd
import statsmodels.formula.api as smf
df=pd.read_stata('data_python.dta')
lm=smf.ols(formula='avexpr ~ logem4 + lat_abst + extmort4', data=df).fit()
print(lm.summary())

```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                 avexpr   R-squared:                       0.378
    Model:                            OLS   Adj. R-squared:                  0.349
    Method:                 Least Squares   F-statistic:                     13.36
    Date:                Fri, 27 Jan 2017   Prob (F-statistic):           6.55e-07
    Time:                        16:02:58   Log-Likelihood:                -113.01
    No. Observations:                  70   AIC:                             234.0
    Df Residuals:                      66   BIC:                             243.0
    Df Model:                           3                                         
    Covariance Type:            nonrobust                                         
    ==============================================================================
                     coef    std err          t      P>|t|      [95.0% Conf. Int.]
    ------------------------------------------------------------------------------
    Intercept      8.6550      0.942      9.191      0.000         6.775    10.535
    logem4        -0.5856      0.185     -3.164      0.002        -0.955    -0.216
    lat_abst       2.7581      1.258      2.192      0.032         0.246     5.270
    extmort4       0.0005      0.000      1.005      0.319        -0.000     0.001
    ==============================================================================
    Omnibus:                        1.486   Durbin-Watson:                   1.908
    Prob(Omnibus):                  0.476   Jarque-Bera (JB):                1.177
    Skew:                          -0.081   Prob(JB):                        0.555
    Kurtosis:                       2.386   Cond. No.                     5.01e+03
    ==============================================================================
    
    Warnings:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The condition number is large, 5.01e+03. This might indicate that there are
    strong multicollinearity or other numerical problems.
    
```python
df=pd.read_stata('data_python.dta')
avexpr_hat=8.6550-0.5856*df.logem4+2.7581*df.lat_abst+0.0005*df.extmort4
lm=smf.ols(formula='logpgp95 ~ avexpr_hat + lat_abst + extmort4', data=df).fit()
print(lm.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:               logpgp95   R-squared:                       0.524
    Model:                            OLS   Adj. R-squared:                  0.502
    Method:                 Least Squares   F-statistic:                     24.22
    Date:                Fri, 27 Jan 2017   Prob (F-statistic):           1.10e-10
    Time:                        16:07:24   Log-Likelihood:                -76.873
    No. Observations:                  70   AIC:                             161.7
    Df Residuals:                      66   BIC:                             170.7
    Df Model:                           3                                         
    Covariance Type:            nonrobust                                         
    ==============================================================================
                     coef    std err          t      P>|t|      [95.0% Conf. Int.]
    ------------------------------------------------------------------------------
    Intercept      2.6682      1.107      2.410      0.019         0.458     4.879
    avexpr_hat     0.8643      0.189      4.583      0.000         0.488     1.241
    lat_abst      -1.0611      1.128     -0.941      0.350        -3.313     1.190
    extmort4      -0.0003      0.000     -1.266      0.210        -0.001     0.000
    ==============================================================================
    Omnibus:                        5.328   Durbin-Watson:                   2.183
    Prob(Omnibus):                  0.070   Jarque-Bera (JB):                4.636
    Skew:                          -0.470   Prob(JB):                       0.0985
    Kurtosis:                       3.841   Cond. No.                     8.48e+03
    ==============================================================================
    
    Warnings:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The condition number is large, 8.48e+03. This might indicate that there are
    strong multicollinearity or other numerical problems.
  <P>
 As we can see from our regression table, after adding more covariates does not change the estimated parameter of the variable avexpr_hat remarkably. Hence, we can conclude that estimated parameter of the variable avexpr_hat is robust and unbiased. 
  </P>
