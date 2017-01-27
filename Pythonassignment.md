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












