
# Evaluating Regression Lines Lab

### Introduction

In the previous lesson, we learned to evaluate how well a regression line estimated our actual data.  In this lab, we will turn these formulas into code.  In doing so, we'll build lots of useful functions for both calculating and displaying our errors for a given regression line and dataset.   We'll have access to our [graph](https://github.com/learn-co-curriculum/evaluating-regression-lines-lab/blob/master/graph.py) library and our [linear equations](https://github.com/learn-co-curriculum/evaluating-regression-lines-lab/blob/master/linear_equations.py) library as we work through these tasks.

### Determining Quality

In the file, `movie_data.py` you will find movie data written as a python list of dictionaries, with each dictionary representing a movie.  The movies are derived from the first 30 entries from the 538 dataset [provided here](https://raw.githubusercontent.com/fivethirtyeight/data/master/bechdel/movies.csv).


```python
from movie_data import movies 
len(movies)
```




    30




```python
movies[0]
```




    {'budget': 13000000, 'domgross': 25682380.0, 'title': '21 &amp; Over'}



Note that like in previous lessons, we are still referencing a budget as our `x_values` or explanatory value and our revenue as our ouput.  Here revenue is represented as the key `domgross`.  First, convert the explanatory budget values to `x_values`, and convert the domgross values to `y_values`.


```python
def build_x_values(movies):
    pass
```


```python
x_values = build_x_values(movies) or ['implement']
```


```python
x_values[0] #  13000000
```




    'implement'




```python
def build_y_values(movies):
    pass
```


```python
y_values = build_y_values(movies) or ['implement']
```


```python
y_values[0] # 25682380.0
```




    'implement'



Assign a variable called `titles` equal to the titles of the movies.


```python
def build_titles(movies):
    pass
```


```python
titles = build_titles(movies) or ['implement']
```


```python
titles[0] # '21 &amp; Over'
```




    'implement'



For the dataset, let's use the following regression formula: $\overline{y} = \overline{m} x + \overline{b}$, with $\overline{m} = 1.7$, and $\overline{y} = 100,000$.  Write a function called `regression_formula` that calculates our $\overline{y}$ for any provided value of $x$. 


```python
def regression_formula(x):
    pass
```


```python
regression_formula(100000) # 270000.0
regression_formula(250000) # 525000.0
```




    525000.0



Let's plot the data as well as the regression line to get a sense of what we are looking at.  We can make use of the [graph.py](https://github.com/learn-co-curriculum/evaluating-regression-lines-lab/blob/master/graph.py) library, that we wrote earlier.


```python
from plotly.offline import iplot, init_notebook_mode
init_notebook_mode(connected=True)
from graph import trace_values, m_b_trace, plot


# movies_trace = trace_values(x_values, y_values, text=titles, name='movie data')
# regression_trace = m_b_trace(1.7, 100000, x_values, name='estimated revenue')
# plot([movies_trace, regression_trace])
```


<script>requirejs.config({paths: { 'plotly': ['https://cdn.plot.ly/plotly-latest.min']},});if(!window.Plotly) {{require(['plotly'],function(plotly) {window.Plotly=plotly;});}}</script>


### Calculating errors of a regression Line

Now that we have our regression formula, we can move towards calculating the error.  Let's start by writing a function named `y_actual`, that given a value, $x$, a list of `x_values` and a list of `y_values` to represent our dataset, returns the value of $y$ at $x$.


```python
def y_actual(x, x_values, y_values):
    pass
```


```python
y_actual(13000000, x_values, y_values) # 25682380.0
```




    25682380.0



Now write a function called `error`, that given a list of `x_values`, and a list of `y_values`, the values `m` and `b` of a regression line, and a value of `x`, returns the error at that x value.  Remember ${\varepsilon_i} =  y_i - \overline{y}_i$.  


```python
def error(x_values, y_values, m, b, x):
    pass
```


```python
# error(x_values, y_values, 1.7, 100000, 13000000) # 3482380.0
```

Now that we have a formula to calculate our errors, write a function that returns a trace of an error at a given point.  The function is called `error_line` and it takes our dataset of `x_values` as the first argument, and `y_values` as the second argument.  It also takes in values of $m$ and $b$ as the next two arguments, to represent the regression line it is calculating errors from.  Finally, it's last argument is the value $x$ it is drawing an error for.

The return value is a dictionary that represents a trace.  The x values of the trace are two x values, and the y values of the trace are the actual value and the expected value.  The mode of the trace should equal `line`.


```python
def error_line_trace(x_values, y_values, m, b, x):
    pass
```


```python
error_at_120m = error_line_trace(x_values, y_values, 1.7, 10000, 120000000)

# {'marker': {'color': 'red'},
#  'mode': 'line',
#  'name': 'error at 120000000',
#  'x': [120000000, 120000000],
#  'y': [93050117.0, 204010000.0]}
error_at_120m
```




    {'marker': {'color': 'red'},
     'mode': 'line',
     'name': 'error at 120000000',
     'x': [120000000, 120000000],
     'y': [93050117.0, 204010000.0]}



We just ran the our function to draw a trace of the error for the movie Elysium.  Let's see how it looks.


```python
movies[19]
```




    {'budget': 120000000, 'domgross': 93050117.0, 'title': 'Elysium'}



We can use a function from our [linear_equations](https://github.com/learn-co-curriculum/evaluating-regression-lines-lab/blob/master/linear_equations.py) library that we previously wrote.


```python
from linear_equations import expected_value_for_line

# y_actual(13000000, x_values, y_values) # 25682380.0
# expected_value_for_line(1.7, 10000, 13000000) # 22110000.0
```


```python
from plotly.offline import iplot, init_notebook_mode
init_notebook_mode(connected=True)

from graph import trace_values, m_b_trace, plot

# movies_trace = trace_values(x_values, y_values, text=titles, name='movie data')
# regression_trace = m_b_trace(1.7, 100000, x_values, name='estimated revenue')
# plot([movies_trace, regression_trace, error_at_120m])
```


<script>requirejs.config({paths: { 'plotly': ['https://cdn.plot.ly/plotly-latest.min']},});if(!window.Plotly) {{require(['plotly'],function(plotly) {window.Plotly=plotly;});}}</script>



<script>requirejs.config({paths: { 'plotly': ['https://cdn.plot.ly/plotly-latest.min']},});if(!window.Plotly) {{require(['plotly'],function(plotly) {window.Plotly=plotly;});}}</script>


From there, we can write a function called `error_lines`, that takes in a list of `x_values` as an argument, `y_values` as an argument, and returns a list of traces for every x_value provided.


```python
def error_line_traces(x_values, y_values, m, b):
    pass
```


```python
# errors_for_regression = error_line_traces(x_values[0:5], y_values[0:5], 1.7, 100000)
```


```python
# len(errors_for_regression) # 5
# errors_for_regression[-1]

# {'marker': {'color': 'red'},
#  'mode': 'line',
#  'name': 'error at 40000000',
#  'x': [40000000, 40000000],
#  'y': [95020213.0, 68100000.0]}
```


```python
from plotly.offline import iplot, init_notebook_mode
init_notebook_mode(connected=True)

from graph import trace_values, m_b_trace, plot
# movies_trace = trace_values(x_values, y_values, text=titles, name='movie data')
# regression_trace = m_b_trace(1.7, 100000, x_values, name='estimated revenue')
# plot([movies_trace, regression_trace, *errors_for_regression])
```


<script>requirejs.config({paths: { 'plotly': ['https://cdn.plot.ly/plotly-latest.min']},});if(!window.Plotly) {{require(['plotly'],function(plotly) {window.Plotly=plotly;});}}</script>



<div id="8bb30f40-edd1-40d7-96db-6935fd4c9b06" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("8bb30f40-edd1-40d7-96db-6935fd4c9b06", [{"x": [13000000, 45658735, 20000000, 61000000, 40000000, 225000000, 92000000, 12000000, 13000000, 130000000, 40000000, 25000000, 50000000, 18000000, 55000000, 30000000, 78000000, 76000000, 5500000, 120000000, 110000000, 100000000, 40000000, 70000000, 17000000, 160000000, 150000000, 140000000, 60000000, 30000000], "y": [25682380.0, 13414714.0, 53107035.0, 75612460.0, 95020213.0, 38362475.0, 67349198.0, 15323921.0, 18007317.0, 60522097.0, 148430908.0, 37304874.0, 19452138.0, 33345833.0, 107136417.0, 35266619.0, 119640264.0, 368065385.0, 24477704.0, 93050117.0, 61737191.0, 107518682.0, 57012977.0, 25213103.0, 54239856.0, 238679850.0, 393050114.0, 122523060.0, 46000903.0, 4167493.0], "mode": "markers", "name": "movie data", "text": ["21 &amp; Over", "Dredd 3D", "12 Years a Slave", "2 Guns", "42", "47 Ronin", "A Good Day to Die Hard", "About Time", "Admission", "After Earth", "American Hustle", "August: Osage County", "Beautiful Creatures", "Blue Jasmine", "Captain Phillips", "Carrie", "Cloudy with a Chance of Meatballs 2", "Despicable Me 2", "Don Jon", "Elysium", "Ender&#39;s Game", "Epic", "Escape from Planet Earth", "Escape Plan", "Evil Dead", "Fast and Furious 6", "Frozen", "G.I. Joe: Retaliation", "Gangster Squad", "Gloria"]}, {"x": [13000000, 45658735, 20000000, 61000000, 40000000, 225000000, 92000000, 12000000, 13000000, 130000000, 40000000, 25000000, 50000000, 18000000, 55000000, 30000000, 78000000, 76000000, 5500000, 120000000, 110000000, 100000000, 40000000, 70000000, 17000000, 160000000, 150000000, 140000000, 60000000, 30000000], "y": [22200000.0, 77719849.5, 34100000.0, 103800000.0, 68100000.0, 382600000.0, 156500000.0, 20500000.0, 22200000.0, 221100000.0, 68100000.0, 42600000.0, 85100000.0, 30700000.0, 93600000.0, 51100000.0, 132700000.0, 129300000.0, 9450000.0, 204100000.0, 187100000.0, 170100000.0, 68100000.0, 119100000.0, 29000000.0, 272100000.0, 255100000.0, 238100000.0, 102100000.0, 51100000.0], "mode": "line", "name": "estimated revenue"}, {"x": [13000000, 13000000], "y": [25682380.0, 22200000.0], "mode": "line", "marker": {"color": "red"}, "name": "error at 13000000"}, {"x": [45658735, 45658735], "y": [13414714.0, 77719849.5], "mode": "line", "marker": {"color": "red"}, "name": "error at 45658735"}, {"x": [20000000, 20000000], "y": [53107035.0, 34100000.0], "mode": "line", "marker": {"color": "red"}, "name": "error at 20000000"}, {"x": [61000000, 61000000], "y": [75612460.0, 103800000.0], "mode": "line", "marker": {"color": "red"}, "name": "error at 61000000"}, {"x": [40000000, 40000000], "y": [95020213.0, 68100000.0], "mode": "line", "marker": {"color": "red"}, "name": "error at 40000000"}], {}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


### Calculating RSS

Now write a function called `squared_error`, that given a value of x, returns the squared error at that x value.

${\varepsilon_i}^2 =  (y_i - \overline{y}_i)^2$


```python
def squared_error(x_values, y_values, m, b, x):
    pass
```


```python
# squared_error(x_values, y_values, 1.7, 100000, x_values[0]) # 12126970464400.0
```




    12126970464400.0



Next, write a function called `residual_sum_squares` that provided a list of points returns the total squared error for the movies in our dataset.


```python
def squared_errors(x_values, y_values, m, b):
    pass
```


```python
# squared_errors(x_values, y_values, 1.7, 100000)
```


```python
def residual_sum_squares(x_values, y_values, m, b):
    pass

residual_sum_squares(x_values, y_values, 1.7, 100000)
```

Now we'll provide a couple functions for you. a function called `trace_rss`, that build a bar chart displaying the value of the RSS.  The return value is a dictionary with keys of `x` and `y`, both which point to lists.  The $x$ key should point to a list with one element, the string 'RSS'.  The $y$ list should be a list which points to the value of the RSS for the line.


```python
import plotly.graph_objs as go

def trace_rss(x_values, y_values, m, b):
    pass

trace_rss(x_values, y_values, 1.7, 100000)
# {'type': 'bar', 'x': ['RSS'], 'y': [3.0025171100327725e+17]}
```

Once this is built, we can turn build a subplot showing the regression line, as well as the related RSS for the regression line.


```python
import plotly
from plotly import tools
import plotly.graph_objs as go

def plot_regression_and_rss(scatter_trace, regression_trace, rss_calc_trace):
    fig = tools.make_subplots(rows=1, cols=2)
    fig.append_trace(scatter_trace, 1, 1)
    fig.append_trace(regression_trace, 1, 1)
    fig.append_trace(rss_calc_trace, 1, 2)
    plotly.offline.iplot(fig)
```


```python
# m = 1.7
# b = 100000


# scatter_trace = trace_values(x_values, y_values, text=titles, name='movie data')
# regression_trace = m_b_trace(m, b, x_values, name='estimated revenue')
# rss_calc_trace = trace_rss(x_values, y_values, m, b)

# plot_regression_and_rss(scatter_trace, regression_trace, rss_calc_trace)
```


```python

```
