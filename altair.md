# Overview

## Bar Chart

```python 
trend_bar = alt.Chart(trends).mark_bar().encode( 
x="search_term", 
y="value", 
color="search_term" 
) 
```
## Line Chart
```python
trend_line= alt.Chart(trends).mark_line().encode(
    x="yearmonth(date):T",
    y="mean(value)",
    color="search_term"
)
```

## Scatter plot
```python
alt.Chart(lifecountries).mark_circle().encode( 
    x='Country GDP', 
    y='Life Expectancy',
    color= 'Continent',
    tooltip='country',
    size='size'
).interactive() 
```

## Map
```python
# remote geojson data object 
url = "https://raw.githubusercontent.com/datasets/geo-countries/master/data/countries.geojson" 
data_geojson_remote = alt.Data(url=url, format=alt.DataFormat(property='features',type='json')) 

# chart object 
alt.Chart(data_geojson_remote).mark_geoshape( 
).encode( 
color="properties.name:N" 
).properties( 
projection={'type': 'identity', 'reflectY': True} 
) 
```


## Histograma
```python
alt.Chart(brain).mark_bar().encode(
    x=alt.X("Body Weight", bin= True),
    y= "count()"
) 
```


## Lineal Composition
```python
trend_line|trend_bar
```

## Vertical Composition
```python
trend_line & trend_bar
```

## Layer
```python
(background+points)
```

## Single Selection
```python
select_type = alt.selection(type="single",encodings=["x"]) 

scatter=alt.Chart(snake).mark_circle().encode( 
    x='evidence', 
    y='popularity', 
    color= 'type' 
).transform_filter( 
select_term 
) 

bar= alt.Chart(snake).mark_bar().encode( 
    x='type', 
    y='count()', 
    color= 'type' 
).properties( 
selection=select_term 
) 

chart|bar
```

## Multiple Selection
```python
select_date = alt.selection(type="interval",encodings=["x"]) 

trend_line = alt.Chart(trends).mark_line().encode( 
x="yearmonth(date):T", 
y="mean(value)", 
color="search_term" 
).properties( 
selection=select_date 
) 

trend_bar = alt.Chart(trends).mark_bar().encode( 
x="search_term", 
y="value", 
color="search_term", 
tooltip="search_term" 
).transform_filter( 
select_date 
) 

trend_bar|trend_line
```
