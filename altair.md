# Import

```python
import altair as alt
# for notebooks
alt.renderers.enable("notebook")
```

# Charts
### Hitogram
```python
alt.Chart(df).mark_bar().encode(x=alt.X('col1',bin=alt.Bin(maxbins=30),title="Titulo eje"),
y="count()").properties(width=200,height=200,title="Titulo grafico")
```

### Bar chart
```python
alt.Chart(df).mark_bar().encode(x='col1',y='sum(value)',color='search_term')
```

### Scatter plot
```python
scatter=alt.Chart(df).mark_circle().encode(x="col1", y="col2").properties(width=300)
```

### Line plot
```python
alt.Chart(df).mark_line().encode(x='date:T',y='sum(value)',color='search_term')
```

### Saving charts
```python
(graph1 & graph2).save('file.html')
```

# Maping charts
### Horizontal concatenation
```python
graph1 | graph2
```

### Vertical concatenation
```python
graph1 & graph2
```

# Interactivity
### Single selection
```python
select_search_term=alt.selection_single(encodings=['x'])
trends_line=alt.Chart(trends).mark_line().encode(x='date:T',
                                                 y='sum(value)',color='search_term').transform_filter(select_search_term)

trends_bar=alt.Chart(trends).mark_bar().encode(x='search_term',
y='sum(value)',color='search_term').properties(selection=select_search_term)

trends_bar|trends_line
```
### Interval selection
```python
selection=alt.selection_interval(encodings=['x'])

trends_line=alt.Chart(trends).mark_line().encode(x='date:T',y='sum(value)',
                                                 color='search_term').transform_filter(selection)
                                                 
trends_line_samll=alt.Chart(trends).mark_line().encode(x='date:T',y='sum(value)',
                                                       color='search_term').properties(
                                                           height=100,selection=selection )
trends_line_samll & trends_line
```

