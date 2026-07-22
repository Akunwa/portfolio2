Helper functions


```python
"""
This function is used to create a permutation of the vertices of an n-sided polygon induced by rotations and reflections. 
Inputs:
    n (int) is the number of polygon vertices
    start (int) is the starting value of the dictionary
    ref (bool) is True if the permutation is induced by a reflection. False otherwise
    
Output: 
    R is the dictionary representing a permutation of n vertices begining with start
"""
def Rn(n,start,ref):
    R = {}
    key = 1
    val = start
    for i in range(n):
        R[key] = val     
        key += 1     
        if ref:   
            val -= 1
        else: 
            val += 1
        val = val%n
        if val == 0:  # n mod n is 0, val = 0. But we want val = n
            val = n
    return R
```


```python
"""
This function composes two permutation elements of a given n-sided polygon
Input: 
    Rs, Rt (dictonary) are the two permutation elements to be composed
    dictofElem (dictionary) contains all permutation elements of an n-sided polygon
Output:
    k (dictionary) is the resulting composition of Rs with Rt. It is a single permutation element in dictofElem
"""

def composition(Rs, Rt, dictofElem):
    dict = {} 
    for k, v in Rt.items():
        dict[k] = Rs[v]      #set the value of dict with key K equal to the the value in Rs with key V
        
    for k, v in dictofElem.items():
        if dict == dictofElem[k]:   #find which element of in dictofElem corresponds with the newly created dict
            return k                #note: k is a string
    return 
```


```python
"""
This function creates the composition table for all the permutation elements of an n-sided polygon
Input:
    a dictionary of all the permutation elements of a given n-sided polygon
Outupt: 
    two data frames, one with string elements and the other with integer elements
"""
import pandas as pd

def compTable(dictofElem):
    df = {} #<---- dataframe of all the compositions of Rs*Rt
    df_int = {} #<---- dataframe of compositions, but converted to integers to create heatmap
    i = 0 
    for V in dictofElem.values():           #compose every element in dictofElem with every element in dictofElem
        for v in dictofElem.values():
            x = composition(v,V,dictofElem)
            if i in df:                                     
                df[i] += [x]                
                df_int[i] += [int(x[1:])]

            else:
                df[i] = [x]
                df_int[i] = [int(x[1:])]        
        i += 1

    df = pd.DataFrame(df)
    df_int = pd.DataFrame(df_int)
    return df, df_int
```

## The hexagon


```python
R0 = Rn(6,1,False) #identity element 
R1 = Rn(6,2,False); R2 = Rn(6,3,False); R3 = Rn(6,4,False); R4 = Rn(6,5,False); R5 = Rn(6,6,False) #rotations
R6 = Rn(6,6,True); R7 = Rn(6,1,True); R8 = Rn(6,2,True); R9 = Rn(6,3,True); R10 = Rn(6,4,True); R11 = Rn(6,5,True) #reflections
dictofHex = {'R0': R0, 'R1': R1, 'R2': R2, 'R3': R3, 'R4': R4, 'R5': R5, 'R6': R6, 'R7': R7, 'R8': R8, 'R9': R9, 'R10': R10, 'R11': R11}
```


```python
compTable(dictofHex)[0]
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>R0</td>
      <td>R1</td>
      <td>R2</td>
      <td>R3</td>
      <td>R4</td>
      <td>R5</td>
      <td>R6</td>
      <td>R7</td>
      <td>R8</td>
      <td>R9</td>
      <td>R10</td>
      <td>R11</td>
    </tr>
    <tr>
      <th>1</th>
      <td>R1</td>
      <td>R2</td>
      <td>R3</td>
      <td>R4</td>
      <td>R5</td>
      <td>R0</td>
      <td>R7</td>
      <td>R8</td>
      <td>R9</td>
      <td>R10</td>
      <td>R11</td>
      <td>R6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>R2</td>
      <td>R3</td>
      <td>R4</td>
      <td>R5</td>
      <td>R0</td>
      <td>R1</td>
      <td>R8</td>
      <td>R9</td>
      <td>R10</td>
      <td>R11</td>
      <td>R6</td>
      <td>R7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>R3</td>
      <td>R4</td>
      <td>R5</td>
      <td>R0</td>
      <td>R1</td>
      <td>R2</td>
      <td>R9</td>
      <td>R10</td>
      <td>R11</td>
      <td>R6</td>
      <td>R7</td>
      <td>R8</td>
    </tr>
    <tr>
      <th>4</th>
      <td>R4</td>
      <td>R5</td>
      <td>R0</td>
      <td>R1</td>
      <td>R2</td>
      <td>R3</td>
      <td>R10</td>
      <td>R11</td>
      <td>R6</td>
      <td>R7</td>
      <td>R8</td>
      <td>R9</td>
    </tr>
    <tr>
      <th>5</th>
      <td>R5</td>
      <td>R0</td>
      <td>R1</td>
      <td>R2</td>
      <td>R3</td>
      <td>R4</td>
      <td>R11</td>
      <td>R6</td>
      <td>R7</td>
      <td>R8</td>
      <td>R9</td>
      <td>R10</td>
    </tr>
    <tr>
      <th>6</th>
      <td>R6</td>
      <td>R11</td>
      <td>R10</td>
      <td>R9</td>
      <td>R8</td>
      <td>R7</td>
      <td>R0</td>
      <td>R5</td>
      <td>R4</td>
      <td>R3</td>
      <td>R2</td>
      <td>R1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>R7</td>
      <td>R6</td>
      <td>R11</td>
      <td>R10</td>
      <td>R9</td>
      <td>R8</td>
      <td>R1</td>
      <td>R0</td>
      <td>R5</td>
      <td>R4</td>
      <td>R3</td>
      <td>R2</td>
    </tr>
    <tr>
      <th>8</th>
      <td>R8</td>
      <td>R7</td>
      <td>R6</td>
      <td>R11</td>
      <td>R10</td>
      <td>R9</td>
      <td>R2</td>
      <td>R1</td>
      <td>R0</td>
      <td>R5</td>
      <td>R4</td>
      <td>R3</td>
    </tr>
    <tr>
      <th>9</th>
      <td>R9</td>
      <td>R8</td>
      <td>R7</td>
      <td>R6</td>
      <td>R11</td>
      <td>R10</td>
      <td>R3</td>
      <td>R2</td>
      <td>R1</td>
      <td>R0</td>
      <td>R5</td>
      <td>R4</td>
    </tr>
    <tr>
      <th>10</th>
      <td>R10</td>
      <td>R9</td>
      <td>R8</td>
      <td>R7</td>
      <td>R6</td>
      <td>R11</td>
      <td>R4</td>
      <td>R3</td>
      <td>R2</td>
      <td>R1</td>
      <td>R0</td>
      <td>R5</td>
    </tr>
    <tr>
      <th>11</th>
      <td>R11</td>
      <td>R10</td>
      <td>R9</td>
      <td>R8</td>
      <td>R7</td>
      <td>R6</td>
      <td>R5</td>
      <td>R4</td>
      <td>R3</td>
      <td>R2</td>
      <td>R1</td>
      <td>R0</td>
    </tr>
  </tbody>
</table>
</div>




```python
import seaborn as sns; sns.set_theme()
x = compTable(dictofHex)[1]
ax = sns.heatmap(x)
```


    
![png](output_7_0.png)
    


## The Square 


```python
R0 = Rn(4,1,False) #identity element 
R1 = Rn(4,2,False); R2 = Rn(4,3,False); R3 = Rn(4,4,False) #rotations
R4 = Rn(4,2,True); R5 = Rn(4,3,True); R6 = Rn(4,4,True); R7 = Rn(4,1,True) #reflections
dictofSquare = {'R0': R0, 'R1': R1, 'R2': R2, 'R3': R3, 'R4': R4, 'R5': R5, 'R6': R6, 'R7': R7}
```


```python
compTable(dictofSquare)[0]
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>R0</td>
      <td>R1</td>
      <td>R2</td>
      <td>R3</td>
      <td>R4</td>
      <td>R5</td>
      <td>R6</td>
      <td>R7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>R1</td>
      <td>R2</td>
      <td>R3</td>
      <td>R0</td>
      <td>R5</td>
      <td>R6</td>
      <td>R7</td>
      <td>R4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>R2</td>
      <td>R3</td>
      <td>R0</td>
      <td>R1</td>
      <td>R6</td>
      <td>R7</td>
      <td>R4</td>
      <td>R5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>R3</td>
      <td>R0</td>
      <td>R1</td>
      <td>R2</td>
      <td>R7</td>
      <td>R4</td>
      <td>R5</td>
      <td>R6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>R4</td>
      <td>R7</td>
      <td>R6</td>
      <td>R5</td>
      <td>R0</td>
      <td>R3</td>
      <td>R2</td>
      <td>R1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>R5</td>
      <td>R4</td>
      <td>R7</td>
      <td>R6</td>
      <td>R1</td>
      <td>R0</td>
      <td>R3</td>
      <td>R2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>R6</td>
      <td>R5</td>
      <td>R4</td>
      <td>R7</td>
      <td>R2</td>
      <td>R1</td>
      <td>R0</td>
      <td>R3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>R7</td>
      <td>R6</td>
      <td>R5</td>
      <td>R4</td>
      <td>R3</td>
      <td>R2</td>
      <td>R1</td>
      <td>R0</td>
    </tr>
  </tbody>
</table>
</div>




```python
import seaborn as sns; sns.set_theme()
x = compTable(dictofSquare)[1]
ax = sns.heatmap(x)
```


    
![png](output_11_0.png)
    


## The Rectangular Hex


```python
R0 = Rn(6,1,False) #identity element 
R1 = Rn(6,4,False) #rotation
R2 = Rn(6,3,True); R3 = Rn(6,6,True) #reflections
dictofRHex = {'R0': R0, 'R1': R1, 'R2': R2, 'R3': R3}
```


```python
compTable(dictofRHex)[0] #group table under composition of permutations
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>R0</td>
      <td>R1</td>
      <td>R2</td>
      <td>R3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>R1</td>
      <td>R0</td>
      <td>R3</td>
      <td>R2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>R2</td>
      <td>R3</td>
      <td>R0</td>
      <td>R1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>R3</td>
      <td>R2</td>
      <td>R1</td>
      <td>R0</td>
    </tr>
  </tbody>
</table>
</div>




```python
import seaborn as sns; sns.set_theme()
x = compTable(dictofRHex)[1]
ax = sns.heatmap(x)
```


    
![png](output_15_0.png)
    


## The Rectangle 


```python
R0 = Rn(4,1,False) #identity element 
R1 = Rn(4,1,True); R2 = Rn(4,3,True) #reflections
R3 = Rn(4,3,False) #rotation
dictofRect = {'R0': R0, 'R1': R1, 'R2': R2, 'R3': R3}
```


```python
compTable(dictofRect)[0]
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>R0</td>
      <td>R1</td>
      <td>R2</td>
      <td>R3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>R1</td>
      <td>R0</td>
      <td>R3</td>
      <td>R2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>R2</td>
      <td>R3</td>
      <td>R0</td>
      <td>R1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>R3</td>
      <td>R2</td>
      <td>R1</td>
      <td>R0</td>
    </tr>
  </tbody>
</table>
</div>




```python
import seaborn as sns; sns.set_theme()
x = compTable(dictofRect)[1]
ax = sns.heatmap(x)
```


    
![png](output_19_0.png)
    

