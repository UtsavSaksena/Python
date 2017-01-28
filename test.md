<H2> Descriptive Statistics of main variable </H2>



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

