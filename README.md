Problem Description

Ema has a grid consisting of Good (G) and Bad (B) cells.

A plus is formed by:

One center cell.
Equal-length arms extending up, down, left, and right.
All cells used by the plus must be G.

Examples:

Length 0 Plus:

G

Area = 1
Length 1 Plus:

  G
GGGGG
  G

Area = 5
Length 2 Plus:

    G
    G
GGGGGGGGG
    G
    G

Area = 9

The area of a plus is:

Area=1+4×arm_length

The task is to find two non-overlapping valid pluses whose area product is maximized.

Approach
Step 1: Generate All Possible Pluses

For every G cell:

Treat it as the center.
Expand equally in all four directions.
Continue expanding while:
All arm cells remain inside the grid.
All arm cells are G.

For each valid expansion:

Compute its area.
Store every occupied cell.

Example:

GGG
GGG
GGG

Possible pluses:

Center only:
Area = 1
Length 1:
  G
GGG
  G

Area = 5
Step 2: Store Occupied Cells

For overlap checking, store all cells occupied by a plus.

Example:

{
 (1,1),
 (0,1),
 (2,1),
 (1,0),
 (1,2)
}

Using sets allows fast intersection checks.

Step 3: Compare Every Pair

For every pair of pluses:

plus1
plus2

Check:

cells1.isdisjoint(cells2)

If true:

The pluses do not overlap.
Calculate:
product = area1 × area2

Update the maximum answer.

Example

Input:

5 6
GGGGGG
GBBBGB
GGGGGG
GGBBGB
GGGGGG

Possible selection:

Plus 1 area = 5
Plus 2 area = 1

Product:

5 × 1 = 5

Output:

5
Algorithm
Generate Pluses
For each cell:
    If cell is G:
        length = 0

        While expansion possible:
            Create plus
            Store area
            Store occupied cells
            length += 1
Find Maximum Product
maxProduct = 0

For each plus A:
    For each plus B:
        If A and B do not overlap:
            maxProduct =
                max(maxProduct,
                    areaA × areaB)
Correctness

A plus is generated only when:

Every arm cell exists.
Every arm cell is G.

Therefore all generated pluses are valid.

Every pair of generated pluses is examined.

Using set intersection guarantees overlap detection.

Thus the algorithm checks every valid non-overlapping pair and returns the maximum area product.

Complexity Analysis

Let:

R = number of rows
C = number of columns
P = total number of valid pluses

Generating pluses:

O(R × C × min(R,C))

Comparing pairs:

O(P²)

Overall:

Time Complexity: O(P²)

Space Complexity: O(P)
Key Formula

Area of a plus:

Area=1+4×arm_length

Examples:

Arm Length	Area
0	1
1	5
2	9
3	13
