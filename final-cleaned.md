

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```


```python
import os
os.getcwd()
```




    'C:\\Users\\Utsav Saksena\\Documents'




```python
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




```python
plt.clf () # starts a new graph
plt.plot(df.avexpr, df.logpgp95, '.', color='red', linewidth=2) # add more feutures
plt.title("GDP per capita 1995 vs Expropriation risk", fontsize=15)
plt.ylabel("$log PPP GDP per capita, 1995, World Bank$", fontsize=10)
plt.xlabel("$average protection against expropriation risk$", fontsize=10)
plt.ylim(6, 10)
plt.xlim(0, 10)
    # add lfit and distinguish the dotted line by the characteristic of colonization
plt.savefig('Graph_10.png')
```

<a href="https://github.com/UtsavSaksena/Python/blob/master/Graph10.png"> Click here to view </a>

```python
plt.clf () # starts a new graph
plt.plot(df.logem4, df.avexpr, '.', color='blue', linewidth=2) # add more feutures
plt.title("Expropriation risk vs Log settler mortalilty", fontsize=15)
plt.ylabel("$average protection against expropriation risk$", fontsize=10)
plt.xlabel("$log settler mortalility$", fontsize=10)
plt.ylim(0, 10)
plt.xlim(0, 8)
    # add lfit and distinguish the dotted line by the characteristic of colonization
plt.savefig('Graph_20.png')
```
<a href="https://github.com/UtsavSaksena/Python/blob/master/Graph20.png"> Click here to view </a>



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


```python
# Run regression: logpgp95 avexpr
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




```python

```


```python
# Run regression: logpgp95 avexpr
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




```python


```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


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
    


```python

```
