## rowfind
Find points that make an equally spaced row on a 2D plane.

Fast and simple, works by walking in 4 directions `1,0  0,1  1,1  1,-1` to n steps from a point and checking if the next point exists, until the required row size is reached.

```python
import rowfind

coords = [
    (0, 0), (1, 1), (2, 2), (3, 3), (3, 4),
    (3, 5), (12, 3), (12, 4), (11, 3), (11, 2),
    (11, 1), (10, 3), (5, 3), (6, 2), (7, 1),
    (7, 0), (8, 1), (8, 5), (9, 5)
]
row_size = 3
steps = 1
rows = rowfind.find_rows(coords, row_size, steps)

# Where `coords` is a tuple/list of (x, y) coordinates, `row_size` is the
# length of rows to find and `steps` is the number of steps to walk before
# checking a point.
#
# The `steps` parameter can be a single integer, a tuple/list of integers
# or None.
#
# For example, if it's set to 1, only immediate neighbors will be matched.
#
#                      . x x x .
#                      o . . x .
#                      . . x . x
#                      . x . . o
#
# If it's set to 2, only gaps of 1 will be matched.
#
#                      x . x . x
#                      . . . . o
#                      . . x . o
#                      . o . . .
#                      x . x . .
#
# Passing a tuple will match rows that satisfy any of the steps.
#
# If it's set as None, all possible steps that fit into the plane's bounds
# will be tried. This can be slow if the min and max are far apart.
#
# The return value is a tuple of tuples, where each tuple is a group of
# points that form a row.

# Visualize the results
print("\n".join(str(row) for row in rows))
graph = rowfind.draw_graph(coords, rows)
print(graph)

"""
((5, 3), (6, 2), (7, 1))
((11, 1), (11, 2), (11, 3))
((3, 3), (3, 4), (3, 5))
((0, 0), (1, 1), (2, 2))
((1, 1), (2, 2), (3, 3))
((10, 3), (11, 3), (12, 3))
. . . X . . . . O O . . .
. . . X . . . . . . . . O
. . . X . X . . . . X X X
. . X . . . X . . . . X .
. X . . . . . X O . . X .
X . . . . . . O . . . . .
"""
```
