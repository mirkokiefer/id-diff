#id-diff
Diff arrays of identifyable objects.

The output can be used to do 3-way merges with [id-merge](https://github.com/mirkok/id-merge).

``` js
var origin = [
  {id: 1, value: 1},
  {id: 2, value: 2},
  {id: 3, value: 3},
  {id: 4, value: 4}
]
var modified = [
  {id: 5, value: 6},
  {id: 3, value: 8},
  {id: 2, value: 2},
  {id: 4, value: 4},
  {id: 1, value: 5}
]
var result = diff(origin, modified)
// returns:
{
  values: {
    1: ['m', 1, 5],
    2: ['=', 2],
    3: ['m', 3, 8],
    4: ['=', 4],
    5: ['+', 6]
  },
  ids: [["x",1],["x",2],["+",5],["=",3],["p",2],["=",4],["p",1]]
}
```
_result.ids_ uses [array-diff's format](https://github.com/mirkok/array-diff).  
_result.values_ returns all values both of the original and the changed version including change markers 'm' (modified), '=', '+' and '-'.

An example including deletes:
``` js
var origin = [
  {id: 1, value: 1},
  {id: 2, value: 2},
  {id: 3, value: 3},
  {id: 4, value: 4}
]
var modified = [
  {id: 2, value: 2},
  {id: 1, value: 9},
  {id: 4, value: 5}
]
var result = diff(origin, modified)
// returns:
{
  values: {
    1: ['m', 1, 9],
    2: ['=', 2],
    3: ['-', 3],
    4: ['m', 4, 5]
  },
  ids: [["x",1],["=",2],["-",3],["p",1],["=",4]]
}
```

