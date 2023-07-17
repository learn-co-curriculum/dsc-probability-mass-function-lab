# The Probability Mass Function - Lab

In this lab you'll apply what you previously learned about probability mass functions (PMFs) to explore the *class size paradox*. The class size paradox describes apparent contradictory findings where a total allocation of resources is fixed. 

The idea behind this paradox is that there is a difference in how events are actually distributed and how events are perceived to be distributed. These types of divergence can have important consequences for data analysis. Probability mass functions can help resolve some of these situations, as you'll learn below.

## Objectives

You will be able to:

* Explain the class size paradox
* Create visualizations to visually compare actual and biased observations 
* Calculate the mean from PMFs to identify the expected value


## The Problem 

At a university, the expected student-to-teacher ratio is 32.5 : 1. But randomly interviewed students often feel that their average class size is bigger than 32.5. There are two main reasons for this:

1. Students typically take 4 - 5 classes at any given time, but teachers usually only teach 1 or 2 classes.
2. The number of students in a small class is small, and the number of students in a large class is large.

Due to the second fact, while randomly taking feedback from students (and sampling randomly), it is expected we will come across _more_ students from larger classes simply because there are more of them.

Let's work through a set of data to recreate and analyze this paradox. 

Suppose that a college offers 74 classes in a term. We can start with the following distribution of sizes and counts:

| Class size |  Class count |
|--------|------|
|15-19|	10|
|20-24|	10|
|25-29|	18|
|30-34|	6|
|35-39|	8|
|40-44|	10|
|45-49|	5|
|50-54|	3|
|55-59| 4|

If the campus manager were asked about the average class size, he would perform the following tasks:

1. Construct a PMF from given data
2. Compute the mean using the PMF

Let's follow the management approach first and see what expected value we get from our PMF. Here is a `size_and_count` dictionary to get you started. Calculate the PMF from this data as we have done before.

To make it slightly more straightforward, we have averaged the class sizes for each class, i.e. for size "15 - 19", we use the average value, 17. This allows us to treat each row of the table above as a single discrete category, represented by the average value of the category.


```python
size_and_count = {17: 10, 22: 10, 27: 18, 32: 6, 37: 8, 42: 10, 47: 5, 52: 3, 57: 4}
```


```python
# __SOLUTION__ 
size_and_count = {17: 10, 22: 10, 27: 18, 32: 6, 37: 8, 42: 10, 47: 5, 52: 3, 57: 4}
```

Following the approach seen in the previous lesson, calculate a list of PMF values by normalizing each size.

(Treat the `size_and_count` dictionary as the equivalent of the `counter` variable from the previous lesson — you do not need to count the raw data values because it has already been done for you, but the logic to find the total number of classes will be a bit more elaborate because you don't have access to the raw data.)

We will also use this an an opportunity to practice using pandas, which has convenient built-in methods and broadcasting.


```python
import pandas as pd

# Determine total number of classes (integer value)
sum_class = None

# Create a pandas Series of all possible outcomes (class sizes)
sizes = None

# Divide each class size value by the total number of classes
# to create a pandas Series of PMF values
actual_pmf = None

# Display probabilities in a dataframe
pmf_df = pd.concat([sizes, actual_pmf], axis=1)
pmf_df.columns = ["Class Size", "Overall Probability"]
pmf_df.style.hide(axis='index')
```


```python
# __SOLUTION__ 
import pandas as pd

# Determine total number of classes (integer value)
sum_class = sum(size_and_count.values())

# Create a pandas Series of all possible outcomes (class sizes)
sizes = pd.Series(size_and_count.keys())

# Divide each class size value by the total number of classes
# to create a pandas Series of PMF values
actual_pmf = pd.Series([value/sum_class for value in size_and_count.values()])

# Display probabilities in a dataframe
pmf_df = pd.concat([sizes, actual_pmf], axis=1)
pmf_df.columns = ["Class Size", "Overall Probability"]
pmf_df.style.hide(axis='index')
```




<style  type="text/css" >
</style><table id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bc" ><thead>    <tr>        <th class="col_heading level0 col0" >Class Size</th>        <th class="col_heading level0 col1" >Overall Probability</th>    </tr></thead><tbody>
                <tr>
                                <td id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bcrow0_col0" class="data row0 col0" >17</td>
                        <td id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bcrow0_col1" class="data row0 col1" >0.135135</td>
            </tr>
            <tr>
                                <td id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bcrow1_col0" class="data row1 col0" >22</td>
                        <td id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bcrow1_col1" class="data row1 col1" >0.135135</td>
            </tr>
            <tr>
                                <td id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bcrow2_col0" class="data row2 col0" >27</td>
                        <td id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bcrow2_col1" class="data row2 col1" >0.243243</td>
            </tr>
            <tr>
                                <td id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bcrow3_col0" class="data row3 col0" >32</td>
                        <td id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bcrow3_col1" class="data row3 col1" >0.081081</td>
            </tr>
            <tr>
                                <td id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bcrow4_col0" class="data row4 col0" >37</td>
                        <td id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bcrow4_col1" class="data row4 col1" >0.108108</td>
            </tr>
            <tr>
                                <td id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bcrow5_col0" class="data row5 col0" >42</td>
                        <td id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bcrow5_col1" class="data row5 col1" >0.135135</td>
            </tr>
            <tr>
                                <td id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bcrow6_col0" class="data row6 col0" >47</td>
                        <td id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bcrow6_col1" class="data row6 col1" >0.067568</td>
            </tr>
            <tr>
                                <td id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bcrow7_col0" class="data row7 col0" >52</td>
                        <td id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bcrow7_col1" class="data row7 col1" >0.040541</td>
            </tr>
            <tr>
                                <td id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bcrow8_col0" class="data row8 col0" >57</td>
                        <td id="T_7d79bd00_af81_11eb_a1b6_94f6d61123bcrow8_col1" class="data row8 col1" >0.054054</td>
            </tr>
    </tbody></table>



As an additional check, these probability values must sum to 1. Let's check for that. Run the following cell: 


```python
# The output should be 1
actual_pmf.sum()
```


```python
# __SOLUTION__ 
# The output should be 1
actual_pmf.sum()
```




    1.0



Because this is a dataframe, we can use the built-in `.plot.bar` method to view the class sizes as a bar graph:


```python
import matplotlib.pyplot as plt
%matplotlib inline
plt.style.use('ggplot')
pmf_df.plot.bar(x="Class Size", y="Overall Probability");
```


```python
# __SOLUTION__
import matplotlib.pyplot as plt
%matplotlib inline
plt.style.use('ggplot')
pmf_df.plot.bar(x="Class Size", y="Overall Probability");
```


    
![png](index_files/index_11_0.png)
    


Let's also write the PMF as a Python function `p_actual`. Meaning, it takes in a given $x_i$ value (a class size) and returns the probability of that outcome from the management perspective.

You can use the global variables `size_and_count` and `sum_class`.


```python
def p_actual(x_i):
    # Your code here
    pass

p_actual(17) # 0.13513513513513514
```


```python
# __SOLUTION__
def p_actual(x_i):
    return size_and_count[x_i] / sum_class

p_actual(17)
```




    0.13513513513513514



## Calculate the Mean or Expected Value $E(X)$

We can now calculate the mean or **Expected Value** for this distribution.

>The mean $\mu$ or expected value **E(X)** of a random variable $X$ is the sum of the possible values for $X$ weighted by their respective probabilities.

$$ E(X) = \mu = \sum_i p(x_i)x_i$$

In simple terms, you have to multiply each element in the sizes list by their probability of occurrence then sum the resulting values.

We can do this in one line of code using pandas broadcasting. (E.g. `sizes.apply(p_actual)` will result in a series containing all $p(x_i)$ values.)


```python
# Calculate the expected value (mu) using formula above
mu = None
mu 

# 32.472972972972975
```


```python
# __SOLUTION__ 
mu = (sizes.apply(p_actual) * sizes).sum()
mu
```




    32.472972972972975



Recall, we expected the average class size to be 32.5. Indeed, the calculation above confirms this.

## Random Student Survey

Next, we conduct a survey on a random group of students about their class sizes and then compute the mean. Paradoxically, we observed that the average class is bigger than 32.5. How did this happen? Let's see this in action below:

First, let's compute a distribution as a likely observation **by students**, where the probability associated with each class size is "biased" by the **number of students** in the class. If this sounds confusing, think of it this way: instead of calculating a PMF using the counts of class sizes, calculate it using the counts of students.

Perform the following tasks to introduce this bias. 

* For each class size $x$, multiply the class probability by $x$, the number of students who observe that particular class size
* Get the sum of biased class sizes

The result is a new PMF that represents the biased distribution.


```python
biased = sizes.apply(p_actual) * sizes
biased
```


```python
# __SOLUTION__ 
biased = sizes.apply(p_actual) * sizes
biased
```




    0    2.297297
    1    2.972973
    2    6.567568
    3    2.594595
    4    4.000000
    5    5.675676
    6    3.175676
    7    2.108108
    8    3.081081
    dtype: float64



You can now normalize the new biased list with the sum of its values, just like you did before. 
- Normalize the biased list and calculate the new PMF


```python
biased_pmf = pd.Series([value/mu for value in biased])
biased_pmf
```


```python
# __SOLUTION__
biased_pmf = pd.Series([value/mu for value in biased])
biased_pmf
```




    0    0.070745
    1    0.091552
    2    0.202247
    3    0.079900
    4    0.123179
    5    0.174782
    6    0.097794
    7    0.064919
    8    0.094881
    dtype: float64



You can see that probability values in this PMF are different than our original pmf. Note the differences in the table below:


```python
pmf_df["Perceived Probability"] = biased_pmf
pmf_df
```


```python
# __SOLUTION__
pmf_df["Perceived Probability"] = biased_pmf
pmf_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Class Size</th>
      <th>Overall Probability</th>
      <th>Perceived Probability</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>17</td>
      <td>0.135135</td>
      <td>0.070745</td>
    </tr>
    <tr>
      <th>1</th>
      <td>22</td>
      <td>0.135135</td>
      <td>0.091552</td>
    </tr>
    <tr>
      <th>2</th>
      <td>27</td>
      <td>0.243243</td>
      <td>0.202247</td>
    </tr>
    <tr>
      <th>3</th>
      <td>32</td>
      <td>0.081081</td>
      <td>0.079900</td>
    </tr>
    <tr>
      <th>4</th>
      <td>37</td>
      <td>0.108108</td>
      <td>0.123179</td>
    </tr>
    <tr>
      <th>5</th>
      <td>42</td>
      <td>0.135135</td>
      <td>0.174782</td>
    </tr>
    <tr>
      <th>6</th>
      <td>47</td>
      <td>0.067568</td>
      <td>0.097794</td>
    </tr>
    <tr>
      <th>7</th>
      <td>52</td>
      <td>0.040541</td>
      <td>0.064919</td>
    </tr>
    <tr>
      <th>8</th>
      <td>57</td>
      <td>0.054054</td>
      <td>0.094881</td>
    </tr>
  </tbody>
</table>
</div>



Again, we can represent this as a function, this time called `p_perceived`.


```python
def p_perceived(x_i):
    return p_actual(x_i)*x_i / mu

p_perceived(17)
```


```python
# __SOLUTION__
def p_perceived(x_i):
    return p_actual(x_i)*x_i / mu

p_perceived(17)
```




    0.07074490220557636



Just like before, you can calculate the expected value $\mu$. This time, use `p_perceived` instead of `p_actual` in your calculation.


```python
mu_biased = None
mu_biased

# 36.51310861423221
```


```python
# __SOLUTION__ 
mu_biased = (sizes.apply(p_perceived) * sizes).sum()
mu_biased
```




    36.51310861423221



## Here Is the Paradox 

Here we see it, the average or expected value of biased results comes out higher than the actual values. In some situations, a paradox like this can be mind-boggling. As an extra measure, inspect both PMFs side by side visually to see the differences. 

You can use `.plot.bar` again on `pmf_df`, this time changing the `y` parameter so that both probability distributions will be plotted side-by-side. Your plot should look like this:

![bar graph with two PMFs side by side](side_by_side_graph.png)


```python
# Your code here
```


```python
# __SOLUTION__
ax = pmf_df.plot.bar(x="Class Size", y=["Overall Probability", "Perceived Probability"]);
# Alternatively (there are only 3 columns, so it will plot all remaining cols as y):
# pmf_df.plot.bar(x="Class Size");
```


    
![png](index_files/index_36_0.png)
    


Your results tell you that in the biased distribution there are fewer small classes and more large classes. 

The mean of the biased distribution is ~36.5, which is quite a bit higher than the actual mean of ~32.5.

For an alternative comparison where it is easier to see which value is higher, plot these PMFs on top of each other with semi-transparent bar fill.

Your plot should look like this:

![bar graph with overlapping PMFs](overlapping_semitransparent_graph.png)

Hints:

* You will need call `.plot.bar` twice, and pass in `ax`, so that both plots use the same axes
* Change the parameter `alpha` to adjust the transparency
* If you don't specify a color, both will plot with the default red color and you won't be able to tell which is which. In the above version, "Overall Probability" has a `color` of `"tab:red"` and "Perceived Probability" has a `color` of `"tab:blue"`, but you're free to customize it differently!


```python
# Setting up shared axes
fig, ax = plt.subplots()

# Your code here
```


```python
# __SOLUTION__

# Setting up shared axes
fig, ax = plt.subplots()

# Plot overall probability in semitransparent red
pmf_df.plot.bar(
    x="Class Size", y="Overall Probability",
    ax=ax,
    alpha=0.5, color="tab:red"
)
# Plot perceived probability in semitransparent blue
pmf_df.plot.bar(
    x="Class Size", y="Perceived Probability",
    ax=ax,
    color="tab:blue", alpha=0.5
);
```


    
![png](index_files/index_39_0.png)
    


Here is the key: for smaller class sizes, the probability of coming across a students is lower than the actual probability. For larger classes, the probability of coming across a student is much higher than actual probability. This explains why the paradox takes place!

## Summary 
In this lesson, we looked at a common paradox called the "class size paradox", which deals with differences in observation by different people based on their circumstances. 

Note that this phenomenon is not just limited to class sizes. It applies to many scenarios where people are grouped together, such as in the context of social networks. This paradox can become really complicated due to the large number of individuals involved and the resulting variations in the probabilities of their observations which arise due to their settings. 
