---
title: "Pandas DataFrames"
teaching: 15
exercises: 15
questions:
- "How can I do statistical analysis of tabular data?"
objectives:
- "Select individual values from a Pandas dataframe."
- "Select entire rows or entire columns from a dataframe."
- "Select a subset of both rows and columns from a dataframe in a single operation."
- "Select a subset of a dataframe by a single Boolean criterion."
keypoints:
- "Use `DataFrame.iloc[..., ...]` to select values by integer location."
- "Use `:` on its own to mean all columns or all rows."
- "Select multiple columns or rows using `DataFrame.loc` and a named slice."
- "Result of slicing can be used in further operations."
- "Use comparisons to select data based on value."
- "Select values or NaN using a Boolean mask."
---
## Use `DataFrame.iloc[..., ...]` to select values by numerical index.

*   Can specify location by numerical index analogously to 2D version of character selection in strings.

~~~
data = pandas.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
print(data.iloc[0, 0])
~~~
{: .language-python}
~~~
1601.056136
~~~
{: .output}

## Use `DataFrame.loc[..., ...]` to select values by names.

*   Can specify location by row name analogously to 2D version of dictionary keys.

~~~
data = pandas.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
print(data.loc["Albania", "gdpPercap_1952"])
~~~
{: .language-python}
~~~
1601.056136
~~~
{: .output}
## Use `:` on its own to mean all columns or all rows.

*   Just like Python's usual slicing notation.

~~~
print(data.loc["Albania", :])
~~~
{: .language-python}
~~~
gdpPercap_1952    1601.056136
gdpPercap_1957    1942.284244
gdpPercap_1962    2312.888958
gdpPercap_1967    2760.196931
gdpPercap_1972    3313.422188
gdpPercap_1977    3533.003910
gdpPercap_1982    3630.880722
gdpPercap_1987    3738.932735
gdpPercap_1992    2497.437901
gdpPercap_1997    3193.054604
gdpPercap_2002    4604.211737
gdpPercap_2007    5937.029526
Name: Albania, dtype: float64
~~~
{: .output}

*   Would get the same result printing `data.loc["Albania"]` (without a second index).

~~~
print(data.loc[:, "gdpPercap_1952"])
~~~
{: .language-python}
~~~
country
Albania                    1601.056136
Austria                    6137.076492
Belgium                    8343.105127
⋮ ⋮ ⋮
Switzerland               14734.232750
Turkey                     1969.100980
United Kingdom             9979.508487
Name: gdpPercap_1952, dtype: float64
~~~
{: .output}

*   Would get the same result printing `data["gdpPercap_1952"]`
*   Also get the same result printing `data.gdpPercap_1952` (since it's a column name)

## Select multiple columns or rows using `DataFrame.loc` and a named slice.

~~~
print(data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'])
~~~
{: .language-python}
~~~
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy           8243.582340    10022.401310    12269.273780
Montenegro      4649.593785     5907.850937     7778.414017
Netherlands    12790.849560    15363.251360    18794.745670
Norway         13450.401510    16361.876470    18965.055510
Poland          5338.752143     6557.152776     8006.506993
~~~
{: .output}

In the above code, we discover that **slicing using `loc` is inclusive at both
ends**, which differs from **slicing using `iloc`**, where slicing indicates
everything up to but not including the final index. 


## Result of slicing can be used in further operations.

*   Usually don't just print a slice.
*   All the statistical operators that work on entire dataframes
    work the same way on slices.
*   E.g., calculate max of a slice.

~~~
print(data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'].max())
~~~
{: .language-python}
~~~
gdpPercap_1962    13450.40151
gdpPercap_1967    16361.87647
gdpPercap_1972    18965.05551
dtype: float64
~~~
{: .output}

~~~
print(data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'].min())
~~~
{: .language-python}
~~~
gdpPercap_1962    4649.593785
gdpPercap_1967    5907.850937
gdpPercap_1972    7778.414017
dtype: float64
~~~
{: .output}

## Use comparisons to select data based on value.

*   Comparison is applied element by element.
*   Returns a similarly-shaped dataframe of `True` and `False`.

~~~
# Use a subset of data to keep output readable.
subset = data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972']
print('Subset of data:\n', subset)

# Which values were greater than 10000 ?
print('\nWhere are values large?\n', subset > 10000)
~~~
{: .language-python}
~~~
Subset of data:
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy           8243.582340    10022.401310    12269.273780
Montenegro      4649.593785     5907.850937     7778.414017
Netherlands    12790.849560    15363.251360    18794.745670
Norway         13450.401510    16361.876470    18965.055510
Poland          5338.752143     6557.152776     8006.506993

Where are values large?
            gdpPercap_1962 gdpPercap_1967 gdpPercap_1972
country
Italy                False           True           True
Montenegro           False          False          False
Netherlands           True           True           True
Norway                True           True           True
Poland               False          False          False
~~~
{: .output}

## Select values or NaN using a Boolean mask.

*   A frame full of Booleans is sometimes called a *mask* because of how it can be used.

~~~
mask = subset > 10000
print(subset[mask])
~~~
{: .language-python}
~~~
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy                   NaN     10022.40131     12269.27378
Montenegro              NaN             NaN             NaN
Netherlands     12790.84956     15363.25136     18794.74567
Norway          13450.40151     16361.87647     18965.05551
Poland                  NaN             NaN             NaN
~~~
{: .output}

*   Get the value where the mask is true, and NaN (Not a Number) where it is false.
*   Useful because NaNs are ignored by operations like max, min, average, etc.

~~~
print(subset[subset > 10000].describe())
~~~
{: .language-python}
~~~
       gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
count        2.000000        3.000000        3.000000
mean     13120.625535    13915.843047    16676.358320
std        466.373656     3408.589070     3817.597015
min      12790.849560    10022.401310    12269.273780
25%      12955.737547    12692.826335    15532.009725
50%      13120.625535    15363.251360    18794.745670
75%      13285.513523    15862.563915    18879.900590
max      13450.401510    16361.876470    18965.055510
~~~
{: .output}

> ## Selection of Individual Values
>
> Assume Pandas has been imported and the Gapminder GDP
> data for Europe has been loaded:
>
> ~~~
> import pandas
>
> df = pandas.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
> ~~~
> {: .language-python}
>
> Write an expression to find the Per Capita GDP of Serbia in 2007.
> > ## Solution
> > This could be done with `df.loc`:
> > ~~~
> > print(df.loc['Serbia', 'gdpPercap_2007'])
> > ~~~
> >{: .language-python}
> {: .solution}
{: .challenge}

> ## Extent of Slicing
>
> 1.  Do the two statements below produce the same output?
> 2.  Based on this,
>     what rule governs what is included (or not) in numerical slices and named slices in Pandas?
>
> ~~~
> print(data.iloc[0:2, 0:2])
> print(data.loc['Albania':'Belgium', 'gdpPercap_1952':'gdpPercap_1962'])
> ~~~
> {: .language-python}
> > ## Solution
> > No, They do not produce the same output
> >
> > ~~~
> > print(data.iloc[0:2, 0:2])
> > ~~~
> >{: .language-python}
> > ~~~
> >          gdpPercap_1952  gdpPercap_1957
> > country                                
> > Albania     1601.056136     1942.284244
> > Austria     6137.076492     8842.598030
> > ~~~
> >{: .output}
> > ~~~
> > print(data.loc['Albania':'Belgium', 'gdpPercap_1952':'gdpPercap_1962'])
> > ~~~
> >{: .language-python}
> > ~~~
> >          gdpPercap_1952  gdpPercap_1957  gdpPercap_1962
> > country                                                
> > Albania     1601.056136     1942.284244     2312.888958
> > Austria     6137.076492     8842.598030    10750.721110
> > Belgium     8343.105127     9714.960623    10991.206760
> > ~~~
> >{: .output}
> >
> >
> > Numerical slices present the first numbered index up to, but not including, the second index provided, just like slices of strings.  Named slices present the first up to and including the second index provided.
> {: .solution}
{: .challenge}

> ## Reconstructing Data
>
> Explain what each line in the following short program does:
> what is in `first`, `second`, etc.?
>
> ~~~
> first = pandas.read_csv('data/gapminder_all.csv', index_col='country')
> second = first[first['continent'] == 'Americas']
> third = second.drop('Puerto Rico')
> fourth = third.drop('continent', axis = 1)
> fourth.to_csv('result.csv')
> ~~~
> {: .language-python}
> > ## Solution
> > ~~~
> > first = pandas.read_csv('data/gapminder_all.csv', index_col='country')
> > ~~~
> >{: .language-python}
> > This creates a new DataFrame named `first` and reads the contents of the file `data/gapminder_all.csv` into it, using the `country` column to index the values.
> > ~~~
> > second = first[first['continent'] == 'Americas']
> > ~~~
> >{: .language-python}
> > This line makes a selection: only those rows of the DataFrame, `first`, for which the `‘continent’` column matches `‘Americas’` are extracted. Notice how the Boolean expression inside the brackets, `first['continent'] == 'Americas'`, is used to select only those rows where the expression is true. Try printing this expression! Can you print also its individual True/False elements? (hint: first assign the expression to a variable)
> > ~~~
> > third = second.drop('Puerto Rico')
> > ~~~
> >{: .language-python}
> > This creates a new DataFrame named `third` which is a copy of `second`, but with the row indexed by the country `Puerto Rico` excluded or "dropped".  When using `DataFrame.drop`, there is an optional argument, `axis` that indicates whether you are dropping a row or a column.  If you do not provide it, the function presumes you want to drop a row.
> > ~~~
> > fourth = third.drop('continent', axis = 1)
> > ~~~
> >{: .language-python}
> > This creates a new DataFrame names `fourth` which is a copy of `third`, but with the column indexed by the name `continent` excluded or "dropped".  Unlike the previous example, where the row was dropped, the `axis = 1` is required to indicate that a column should be dropped.
> > ~~~
> > fourth.to_csv('result.csv')
> > ~~~
> >{: .language-python}
> > This writes the contents of the DataFrame `fourth` oout to a file named `result.csv`.  As no path was given, it will write the file to the current working directory.
> {: .solution}
{: .challenge}

> ## Selecting Indices
>
> Explain in simple terms what `idxmin` and `idxmax` do in the short program below.
> When would you use these methods?
>
> ~~~
> data = pandas.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
> print(data.idxmin())
> print(data.idxmax())
> ~~~
> {: .language-python}
> > ## Solution
> > `data.idxmin` returns the index of the each of the rows that has the lowest value in each of the colums of the DataFrame `data`.  `data.idxmax` returns the index of the each of the rows that has the highest value in each of the colums of the DataFrame `data`.  
> >   
> > Much like the `data.drop` that we used earlier, unless explicitly stated, these methods presume you want the index of the row with the lowest or highest value.  Similarly, you could get the index of the column with the lowest or highest values for each of the columns by using `print(data.idxmin(axis = 1))` or `print(data.idxman(axis = 1))`, respectively.
> {: .solution}
{: .challenge}

> ## Practice with Selection
>
> Assume Pandas has been imported and the Gapminder GDP data for Europe has been loaded.
> Write an expression to select each of the following:
>
> 1.  GDP per capita for all countries in 1982.
> 2.  GDP per capita for Denmark for all years.
> 3.  GDP per capita for all countries for years *after* 1985.
> 4.  GDP per capita for each country in 2007 as a multiple of 
>     GDP per capita for that country in 1952.  
>
> > ## Solution
> > GDP per capita for all countries in 1982.
> > ~~~
> > data.loc[:, 'gdpPercap_1982']
> > ~~~
> >{: .language-python}
> ><br>
> > GDP per capita for Denmark for all years.
> > ~~~
> > data.loc['Denmark', :]
> > ~~~
> >{: .language-python}
> ><br>
> > GDP per capita for all countries for years *after* 1985.
> > ~~~
> > data.loc[:, 'gdpPercap_1985':]
> > ~~~
> >{: .language-python}
> > Pandas is smart enough to recognize the number at the end of the column label and does not give you an error, although no column named `gdpPercap_1985` actually exists. This is useful if new columns are added to the CSV file later.
> ><br>
> > GDP per capita for each country in 2007 as a multiple of  
> > GDP per capita for that country in 1952.  
> > ~~~
> > data.loc[:, 'gdpPercap_2007'] / data[:, 'gdpPercap_1952']
> > ~~~
> >{: .language-python}
> {: .solution}
{: .challenge}


> ## Interpretation
>
> Poland's borders have been stable since 1945,
> but changed several times in the years before then.
> How would you handle this if you were creating a table of GDP per capita for Poland
> for the entire Twentieth Century?
{: .challenge}
