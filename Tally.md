
## Tally, Depth, Match: `≢≡`[](https://xpqz.github.io/learnapl/manip.html#tally-depth-match "Permalink to this headline")

[_Tally_](http://help.dyalog.com/18.0/index.htm#Language/Primitive%20Functions/Tally.htm), monadic `≢`, gives the number of major cells in an array, kind of like Python’s [len()](https://docs.python.org/3/library/functions.html#len):

≢7 5 1 2 9
≢'Hello world'
≢mat
5
11
3

# Tally
R←≢Y
Y may be any array.  R is a simple numeric scalar.
Tally returns the number of major cells of Y. See [Cells and Sub-arrays](https://help.dyalog.com/latest/Content/Language/Introduction/Variables/Cells%20and%20Subarrays.htm#CellsSubarrays).

This can also be expressed as the length of the leading axis or 1 if Y is a scalar. Tally is equivalent to the function {⍬⍴(⍴⍵),1}.
#### Examples
      ≢2 3 4⍴⍳10  
2  
      ≢2  
1  
      ≢⍬  
0
Note that ≢V is useful for returning the length of vector V as a scalar. (In contrast, ⍴V is a one-element vector.)

![[Screen Shot 2022-10-24 at 10.05.53 AM.png]]

## Depth, tally `≡≢`[](https://xpqz.github.io/cultivations/Functions3.html#depth-tally "Permalink to this headline")

Monadic `≡B` gives the [depth](http://help.dyalog.com/latest/index.htm#Language/Primitive%20Functions/Depth.htm) of `B`, which is the amount of nesting. A simple scalar is 0, a vector is 1, a vector of vectors is 2, etc. If the amount of nesting is uneven throughout the array, the result will be negative, and indicate the maximum depth.

`≢B` is the [tally](http://help.dyalog.com/latest/index.htm#Language/Primitive%20Functions/Tally.htm) of `B`, i.e. how many major cells `B` has. For a scalar, that’s 1. For a vector, it is the number of elements, for a matrix it is the number of rows, for a 3D array it is the number of layers, and so on.

≡(1 2 (3 4 5 (6 7 8)))  ⍝ unevenly nested vector
≢1                      ⍝ scalars tally to 1
≢3 2⍴⍳6                 ⍝ matrix tally is the number of rows

¯3
1
3

-   Equal underbar  
    
    The Equal underbar (`≡`) serves two purposes. In its monadic form, it shows the depth of a specific structure.
    
    ≡2 2⍴1 (2 3) (4 5 6 7) (8 (9 10) 11)
    
    In its dyadic form, it attempts to match both parameters to see if they are equal in shape, order and values:
    
    't' 'e' 's' 't'≡'test'
    
-   Equal underbar slash  
    
    The Equal underbar slash (`≢`) does the exact opposite of `≡`. In its monadic form, it shows the tally (shallowest depth) of a specific structure:
    
    ≢2 2⍴1 (2 3) (4 5 6 7) (8 (9 10) 11)
    
    In its dyadic form, it checks if both parameters **do not match**:
    
    ('t' 'e') ('s' 't')≢'test'

#### dyadic `≡` (Match)

Match does a comparison to see if 2 objects are equal. It is similar to `=`, but it works on entire objects rather than elementwise. In other words it is equal with a wider scope.

In [ ]:

1 ≡ 1

Out[ ]:
1
In [ ]:
1 ≡ 0
Out[ ] 
0
`≡` works on whole objects and **not** elementwise with broadcasting.

In [ ]:
1 ≡ 1 1
Out[ ]:
0
### `≢` (Equal Underbar Slash)

#### monadic `≢` (Tally)

Tally counts the major cells in an array. This means it gives the length of the leading axis. For a vector, or rank 1 array, this is the same as it's shape but as a scalar.

In [ ]:

≢ 1 2 3

Out[ ]:
 
3

In [ ]:

⍴ 1 2 3
Out[ ]:

┌→┐
│3│
└~┘

If there are multiple dimensions, Tally returns the number of major cells, which is the size of the first dimension

In [ ]:
≢ 2 3 ⍴ ⍳6
Out[ ]:
2
In [ ]:
≢ 3 2 ⍴ ⍳6
Out[ ]:

3
#### dyadic `≢` (Not match)

Not match does a comparison to see if 2 objects are not equal. It is similar to `≠`, but it works on entire objects rather than elementwise. In other words, it is equal with a wider scope.

In [ ]:

1 ≢ 1

Out[ ]:

0

In [ ]:

1 ≢ 0

Out[ ]:
1
 
`≢` works on whole objects and **not** elementwise with broadcasting.

In [ ]:

1 ≢ 1 1

Out[ ]:

 
1