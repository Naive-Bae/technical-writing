# Boolean masking in pandas

Now that you know how to select data in pandas by referring to rows and columns, the next step is to learn how to use Boolean masks. Data professionals use Boolean masks to select data in pandas based on conditions. In this reading, you will discover Boolean masking and how to use pandas’ logical operators to form multi-conditional selection statements. Understanding the fundamentals of pandas will help make your work as a data professional easier and more efficient.

## Boolean masks

You know that "Boolean" is used to describe any binary variable whose possible values are `True` or `False`. With pandas, **Boolean masking** (also called **Boolean indexing**) is used to overlay a Boolean grid onto a dataframe in order to select only the values in the dataframe that align with the `True` values of the grid. 

Return to the example from the video. Suppose you have a dataframe of planets, their radii, and their number of moons:

| **planet**  | **radius_km** | **moons** |
| ------- | --------- | ----- |
| Mercury | 2,440     | 0     |
| Venus   | 6,052     | 0     |
| Earth   | 6,371     | 1     |
| Mars    | 3,390     | 2     |
| Jupiter | 69,911    | 80    |
| Saturn  | 58,232    | 83    |
| Uranus  | 25,362    | 27    |
| Neptune | 24,622    | 14    |

Now suppose that you want to keep the rows of any planets that have fewer than 20 moons and filter out the rest. A Boolean mask is a pandas `Series` object indicating whether a condition is true or false for each value in the moons column:

|   | **Moons < 20?** |
| - | ----------- |
| 0 | True        |
| 1 | True        |
| 2 | True        |
| 3 | True        |
| 4 | False       |
| 5 | False       |
| 6 | False       |
| 7 | True        |

The dtype contained in this series is `bool`. Boolean masking effectively overlays this Boolean series onto the dataframe’s index. The result is that any rows in the dataframe that are indicated as `False` in the Boolean mask get filtered out, and any rows that are indicated as `True` remain in the dataframe:

| **planet**  | **radius_km** | **moons** |
| ------- | --------- | ----- |
| Mercury | 2,440     | 0     |
| Venus   | 6,052     | 0     |
| Earth   | 6,371     | 1     |
| Mars    | 3,390     | 2     |
| Neptune | 24,622    | 14    |

### Coding Boolean masks in pandas

Here is how to perform this operation in pandas.

Begin with a DataFrame object.

```Python
data = {
        'planet': ['Mercury', 'Venus', 'Earth', 'Mars', 'Jupiter', 'Saturn', 'Uranus', 'Neptune'],
        'radius_km': [2440, 6052, 6371, 3390, 69911, 58232, 25362, 24622],
       	'moons': [0, 0, 1, 2, 80, 83, 27, 14]
        }
df = pd.DataFrame(data)
df
```

<img width="248" alt="Moons dataframe" src="https://github.com/Naive-Bae/technical-writing/assets/33466507/031dd656-7548-4e96-8cba-d74c2ed00880">

Then, write a logical statement. Remember, the objective is to keep planets that have fewer than 20 moons and filter out the rest.

```python
df['moons'] < 20
```
<img width="248" alt="Boolean series where number of moons < 20" src="https://github.com/Naive-Bae/technical-writing/assets/33466507/6e1cee9c-b9d0-44ee-b8e4-3d9c85364e92">

This results in a Series object of dtype `bool` that consists of the row indices where each index contains a `True` or `False` value depending on whether that row satisfies the given condition. This is the Boolean mask. To apply this mask to the dataframe, simply insert this statement into selector brackets and apply it:

```python
df[df['moons'] < 20]
```
<img width="248" alt="Filtered dataframe containing only rows where moons < 20" src="https://github.com/Naive-Bae/technical-writing/assets/33466507/7bc2fd87-6cf7-4ceb-a482-eb3a41394887">

You can also assign the Boolean mask to a named variable and then apply that to your dataframe:

