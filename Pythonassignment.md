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
In the paper, the authors exploit differences in European mortality rates to estimate the effect of institutions on current economic performance. The ‘chain of causality’ is defined as follows - 
</P>
<I> High mortality rates of settlers -> extractive institutions -> Prevalence of institutions -> current state of economic performance </I> 

</P>


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





```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from scipy import arange, optimize

```


```python
import os
os.getcwd()

```




    'C:\\Users\\Utsav Saksena\\Documents'




```python
df=pd.read_stata('data_python.dta')
df
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
    <tr>
      <th>5</th>
      <td>0.268333</td>
      <td>10.000000</td>
      <td>1.0</td>
      <td>7.500000</td>
      <td>9.285448</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>85.000000</td>
      <td>4.442651</td>
      <td>145.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.188889</td>
      <td>30.000002</td>
      <td>1.0</td>
      <td>5.636364</td>
      <td>7.926602</td>
      <td>3.0</td>
      <td>170.0</td>
      <td>4.0</td>
      <td>3.0</td>
      <td>71.000000</td>
      <td>4.262680</td>
      <td>150.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.111111</td>
      <td>40.000000</td>
      <td>1.0</td>
      <td>7.909091</td>
      <td>8.727454</td>
      <td>1.0</td>
      <td>171.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>71.000000</td>
      <td>4.262680</td>
      <td>151.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.666667</td>
      <td>99.000000</td>
      <td>1.0</td>
      <td>9.727273</td>
      <td>9.986449</td>
      <td>7.0</td>
      <td>128.0</td>
      <td>9.0</td>
      <td>7.0</td>
      <td>16.100000</td>
      <td>2.778819</td>
      <td>159.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.333333</td>
      <td>50.000000</td>
      <td>1.0</td>
      <td>7.818182</td>
      <td>9.336092</td>
      <td>1.0</td>
      <td>177.0</td>
      <td>5.0</td>
      <td>7.0</td>
      <td>68.900002</td>
      <td>4.232656</td>
      <td>162.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.388889</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>7.772727</td>
      <td>7.886081</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>118.000000</td>
      <td>4.770685</td>
      <td>163.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>0.088889</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>7.000000</td>
      <td>7.444249</td>
      <td>1.0</td>
      <td>35.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>668.000000</td>
      <td>6.504288</td>
      <td>164.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>0.066667</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>6.454545</td>
      <td>7.501082</td>
      <td>3.0</td>
      <td>35.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>280.000000</td>
      <td>5.634789</td>
      <td>165.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0.011111</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>4.681818</td>
      <td>7.420579</td>
      <td>4.0</td>
      <td>35.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>240.000000</td>
      <td>5.480639</td>
      <td>166.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>0.044444</td>
      <td>20.000000</td>
      <td>1.0</td>
      <td>7.318182</td>
      <td>8.809863</td>
      <td>3.0</td>
      <td>163.0</td>
      <td>3.0</td>
      <td>5.0</td>
      <td>71.000000</td>
      <td>4.262680</td>
      <td>167.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0.111111</td>
      <td>20.000000</td>
      <td>1.0</td>
      <td>7.045455</td>
      <td>8.794825</td>
      <td>3.0</td>
      <td>157.0</td>
      <td>10.0</td>
      <td>7.0</td>
      <td>78.099998</td>
      <td>4.357990</td>
      <td>170.0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>0.211111</td>
      <td>25.000000</td>
      <td>1.0</td>
      <td>6.181818</td>
      <td>8.364042</td>
      <td>3.0</td>
      <td>151.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>130.000000</td>
      <td>4.867535</td>
      <td>183.0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>0.311111</td>
      <td>13.000000</td>
      <td>1.0</td>
      <td>6.500000</td>
      <td>8.389359</td>
      <td>2.0</td>
      <td>33.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>78.199997</td>
      <td>4.359270</td>
      <td>184.0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>0.022222</td>
      <td>30.000002</td>
      <td>1.0</td>
      <td>6.545455</td>
      <td>8.470101</td>
      <td>3.0</td>
      <td>165.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>71.000000</td>
      <td>4.262680</td>
      <td>185.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>0.300000</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>6.772727</td>
      <td>7.951560</td>
      <td>1.0</td>
      <td>184.0</td>
      <td>7.0</td>
      <td>7.0</td>
      <td>67.800003</td>
      <td>4.216562</td>
      <td>186.0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>0.088889</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>5.727273</td>
      <td>6.109248</td>
      <td>1.0</td>
      <td>49.0</td>
      <td>5.0</td>
      <td>7.0</td>
      <td>26.000000</td>
      <td>3.258096</td>
      <td>190.0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>0.511111</td>
      <td>100.000000</td>
      <td>0.0</td>
      <td>9.727273</td>
      <td>9.963641</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.880000</td>
      <td>1.057790</td>
      <td>194.0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>0.011111</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>7.818182</td>
      <td>8.907883</td>
      <td>2.0</td>
      <td>35.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>280.000000</td>
      <td>5.634789</td>
      <td>198.0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>0.600000</td>
      <td>100.000000</td>
      <td>0.0</td>
      <td>9.772727</td>
      <td>9.878170</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.550000</td>
      <td>0.936093</td>
      <td>199.0</td>
    </tr>
    <tr>
      <th>24</th>
      <td>0.088889</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>6.272727</td>
      <td>7.365180</td>
      <td>1.0</td>
      <td>35.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>668.000000</td>
      <td>6.504288</td>
      <td>201.0</td>
    </tr>
    <tr>
      <th>25</th>
      <td>0.122222</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>6.545455</td>
      <td>7.489971</td>
      <td>1.0</td>
      <td>37.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>483.000000</td>
      <td>6.180017</td>
      <td>202.0</td>
    </tr>
    <tr>
      <th>26</th>
      <td>0.147556</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>8.272727</td>
      <td>7.272398</td>
      <td>7.0</td>
      <td>30.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1470.000000</td>
      <td>7.293018</td>
      <td>204.0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>0.170000</td>
      <td>20.000000</td>
      <td>1.0</td>
      <td>5.136364</td>
      <td>8.294049</td>
      <td>1.0</td>
      <td>156.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>71.000000</td>
      <td>4.262680</td>
      <td>210.0</td>
    </tr>
    <tr>
      <th>28</th>
      <td>0.055556</td>
      <td>2.000000</td>
      <td>1.0</td>
      <td>5.886364</td>
      <td>7.904704</td>
      <td>7.0</td>
      <td>29.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>32.180000</td>
      <td>3.471345</td>
      <td>213.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>0.246111</td>
      <td>4.000000</td>
      <td>1.0</td>
      <td>8.136364</td>
      <td>10.049750</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>14.900000</td>
      <td>2.701361</td>
      <td>214.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>40</th>
      <td>0.255556</td>
      <td>15.000001</td>
      <td>1.0</td>
      <td>7.500000</td>
      <td>8.943768</td>
      <td>3.0</td>
      <td>173.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>71.000000</td>
      <td>4.262680</td>
      <td>265.0</td>
    </tr>
    <tr>
      <th>41</th>
      <td>0.188889</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>4.000000</td>
      <td>6.565265</td>
      <td>3.0</td>
      <td>35.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>2940.000000</td>
      <td>7.986165</td>
      <td>269.0</td>
    </tr>
    <tr>
      <th>42</th>
      <td>0.394444</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>7.227273</td>
      <td>9.427063</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>16.299999</td>
      <td>2.791165</td>
      <td>270.0</td>
    </tr>
    <tr>
      <th>43</th>
      <td>0.025556</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>7.954545</td>
      <td>8.894258</td>
      <td>7.0</td>
      <td>38.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>17.700001</td>
      <td>2.873565</td>
      <td>281.0</td>
    </tr>
    <tr>
      <th>44</th>
      <td>0.177778</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>5.000000</td>
      <td>6.733402</td>
      <td>3.0</td>
      <td>37.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>400.000000</td>
      <td>5.991465</td>
      <td>286.0</td>
    </tr>
    <tr>
      <th>45</th>
      <td>0.111111</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>5.545455</td>
      <td>6.813445</td>
      <td>7.0</td>
      <td>35.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>2004.000000</td>
      <td>7.602901</td>
      <td>287.0</td>
    </tr>
    <tr>
      <th>46</th>
      <td>0.144444</td>
      <td>20.000000</td>
      <td>1.0</td>
      <td>5.227273</td>
      <td>7.544332</td>
      <td>1.0</td>
      <td>157.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>163.300003</td>
      <td>5.095589</td>
      <td>289.0</td>
    </tr>
    <tr>
      <th>47</th>
      <td>0.455556</td>
      <td>93.000000</td>
      <td>1.0</td>
      <td>9.727273</td>
      <td>9.756147</td>
      <td>7.0</td>
      <td>138.0</td>
      <td>10.0</td>
      <td>7.0</td>
      <td>8.550000</td>
      <td>2.145931</td>
      <td>295.0</td>
    </tr>
    <tr>
      <th>48</th>
      <td>0.333333</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>6.045455</td>
      <td>7.352441</td>
      <td>1.0</td>
      <td>48.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>36.990002</td>
      <td>3.610648</td>
      <td>300.0</td>
    </tr>
    <tr>
      <th>49</th>
      <td>0.100000</td>
      <td>20.000000</td>
      <td>1.0</td>
      <td>5.909091</td>
      <td>8.836374</td>
      <td>3.0</td>
      <td>92.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>163.300003</td>
      <td>5.095589</td>
      <td>301.0</td>
    </tr>
    <tr>
      <th>50</th>
      <td>0.111111</td>
      <td>30.000002</td>
      <td>1.0</td>
      <td>5.772727</td>
      <td>8.396154</td>
      <td>1.0</td>
      <td>174.0</td>
      <td>4.0</td>
      <td>3.0</td>
      <td>71.000000</td>
      <td>4.262680</td>
      <td>302.0</td>
    </tr>
    <tr>
      <th>51</th>
      <td>0.255556</td>
      <td>25.000000</td>
      <td>1.0</td>
      <td>6.954545</td>
      <td>8.207947</td>
      <td>1.0</td>
      <td>184.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>78.099998</td>
      <td>4.357990</td>
      <td>311.0</td>
    </tr>
    <tr>
      <th>52</th>
      <td>0.166667</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>4.000000</td>
      <td>7.306531</td>
      <td>7.0</td>
      <td>41.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>88.199997</td>
      <td>4.479607</td>
      <td>321.0</td>
    </tr>
    <tr>
      <th>53</th>
      <td>0.155556</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>6.000000</td>
      <td>7.402452</td>
      <td>3.0</td>
      <td>35.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>164.660004</td>
      <td>5.103883</td>
      <td>322.0</td>
    </tr>
    <tr>
      <th>54</th>
      <td>0.013556</td>
      <td>4.000000</td>
      <td>1.0</td>
      <td>9.318182</td>
      <td>10.146434</td>
      <td>7.0</td>
      <td>36.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>17.700001</td>
      <td>2.873565</td>
      <td>323.0</td>
    </tr>
    <tr>
      <th>55</th>
      <td>0.092222</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>5.818182</td>
      <td>6.253829</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>483.000000</td>
      <td>6.180017</td>
      <td>325.0</td>
    </tr>
    <tr>
      <th>56</th>
      <td>0.150000</td>
      <td>20.000000</td>
      <td>1.0</td>
      <td>5.000000</td>
      <td>7.948032</td>
      <td>3.0</td>
      <td>157.0</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>78.099998</td>
      <td>4.357990</td>
      <td>326.0</td>
    </tr>
    <tr>
      <th>57</th>
      <td>0.044444</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>4.681818</td>
      <td>8.010000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>32.180000</td>
      <td>3.471345</td>
      <td>329.0</td>
    </tr>
    <tr>
      <th>58</th>
      <td>0.088889</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>6.909091</td>
      <td>7.222566</td>
      <td>3.0</td>
      <td>35.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>668.000000</td>
      <td>6.504288</td>
      <td>337.0</td>
    </tr>
    <tr>
      <th>59</th>
      <td>0.166667</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>7.636364</td>
      <td>8.774931</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>140.000000</td>
      <td>4.941642</td>
      <td>338.0</td>
    </tr>
    <tr>
      <th>60</th>
      <td>0.122222</td>
      <td>40.000000</td>
      <td>1.0</td>
      <td>7.454545</td>
      <td>8.768730</td>
      <td>7.0</td>
      <td>33.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>85.000000</td>
      <td>4.442651</td>
      <td>344.0</td>
    </tr>
    <tr>
      <th>61</th>
      <td>0.377778</td>
      <td>3.000000</td>
      <td>1.0</td>
      <td>6.454545</td>
      <td>8.482602</td>
      <td>1.0</td>
      <td>36.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>63.000000</td>
      <td>4.143135</td>
      <td>345.0</td>
    </tr>
    <tr>
      <th>62</th>
      <td>0.066667</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>6.636364</td>
      <td>6.253829</td>
      <td>3.0</td>
      <td>33.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>145.000000</td>
      <td>5.634789</td>
      <td>349.0</td>
    </tr>
    <tr>
      <th>63</th>
      <td>0.011111</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>4.454545</td>
      <td>6.966024</td>
      <td>7.0</td>
      <td>33.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>280.000000</td>
      <td>5.634789</td>
      <td>350.0</td>
    </tr>
    <tr>
      <th>64</th>
      <td>0.366667</td>
      <td>60.000004</td>
      <td>1.0</td>
      <td>7.000000</td>
      <td>9.031214</td>
      <td>1.0</td>
      <td>165.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>71.000000</td>
      <td>4.262680</td>
      <td>352.0</td>
    </tr>
    <tr>
      <th>65</th>
      <td>0.422222</td>
      <td>87.500000</td>
      <td>1.0</td>
      <td>10.000000</td>
      <td>10.215740</td>
      <td>7.0</td>
      <td>195.0</td>
      <td>10.0</td>
      <td>7.0</td>
      <td>15.000000</td>
      <td>2.708050</td>
      <td>353.0</td>
    </tr>
    <tr>
      <th>66</th>
      <td>0.088889</td>
      <td>20.000000</td>
      <td>1.0</td>
      <td>7.136364</td>
      <td>9.071078</td>
      <td>1.0</td>
      <td>165.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>78.099998</td>
      <td>4.357990</td>
      <td>357.0</td>
    </tr>
    <tr>
      <th>67</th>
      <td>0.177778</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>6.409091</td>
      <td>7.279319</td>
      <td>1.0</td>
      <td>41.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>140.000000</td>
      <td>4.941642</td>
      <td>359.0</td>
    </tr>
    <tr>
      <th>68</th>
      <td>0.322222</td>
      <td>22.000000</td>
      <td>1.0</td>
      <td>6.863636</td>
      <td>8.885994</td>
      <td>3.0</td>
      <td>139.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>15.500000</td>
      <td>2.740840</td>
      <td>369.0</td>
    </tr>
    <tr>
      <th>69</th>
      <td>0.000000</td>
      <td>8.000000</td>
      <td>1.0</td>
      <td>3.500000</td>
      <td>6.866933</td>
      <td>1.0</td>
      <td>35.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>240.000000</td>
      <td>5.480639</td>
      <td>370.0</td>
    </tr>
  </tbody>
</table>
<p>70 rows × 12 columns</p>
</div>




```python
plt.clf () # starts a new graph
plt.plot(df.avexpr, df.logpgp95, '.', color='red', linewidth=2) # add more feutures
plt.title("Graph 1", fontsize=15)
plt.ylabel("$log PPP GDP per capita, 1995, World Bank$", fontsize=10)
plt.xlabel("$average protection against expropriation risk$", fontsize=10)
plt.ylim(6, 10)
plt.xlim(0, 10)
    # add lfit and distinguish the dotted line by the characteristic of colonization
plt.savefig('Graph_1.png')

```


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
plt.clf () # starts a new graph
plt.plot(df.logem4, df.avexpr, '.', color='blue', linewidth=2) # add more feutures
plt.title("Graph 2", fontsize=15)
plt.ylabel("$average protection against expropriation risk$", fontsize=10)
plt.xlabel("$log settler mortalility$", fontsize=10)
plt.ylim(0, 10)
plt.xlim(0, 8)
    # add lfit and distinguish the dotted line by the characteristic of colonization
plt.savefig('Graph_2.png')
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
# Run 2 Stage OLS  Y=logpgp95  Treatment=avexpr    Instrument=logem4
df=pd.read_stata('data_python.dta')
import numpy as np
import pysal
import pysal.spreg.diagnostics as diagnostics
from pysal.spreg.ols import OLS
from pysal.spreg.twosls import TSLS

df=pd.read_stata('data_python.dta')

y = np.array(df.by_col("logpgp95")) #dependent variable

X = np.array(df["lat_abst"])
yd = np.array(df["avexpr"])
q = np.array(df["logem4"])

spreg.twosls = TSLS(y, X, yd, q)
reg



```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-122-57fdac9348c0> in <module>()
          9 df=pd.read_stata('data_python.dta')
         10 
    ---> 11 y = np.array(df.by_col("logpgp95")) #dependent variable
         12 
         13 X = np.array(df["lat_abst"])
    

    C:\Users\Utsav Saksena\Anaconda2\lib\site-packages\pandas\core\generic.py in __getattr__(self, name)
       2670             if name in self._info_axis:
       2671                 return self[name]
    -> 2672             return object.__getattribute__(self, name)
       2673 
       2674     def __setattr__(self, name, value):
    

    AttributeError: 'DataFrame' object has no attribute 'by_col'



```python


```


```python

```
