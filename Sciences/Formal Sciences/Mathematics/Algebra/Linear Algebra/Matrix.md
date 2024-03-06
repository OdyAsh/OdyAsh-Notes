
Main sources:
* Source 1: [Interactive Linear Algebra](https://textbooks.math.gatech.edu/ila/index.html) Textbook by Georgia Institute of Technology 
	* Note 1: Check the UBC version [here](https://personal.math.ubc.ca/~tbjw/ila/index.html), which is a [fork](https://github.com/tbjw/ILAUBC) of [Georgia's GitHub repository](https://github.com/QBobWatson/ila), in case the latter website is down. Note that the order of some content is changed in this version, as mentioned [here](https://personal.math.ubc.ca/~tbjw/ila/preface-2.html). Moreover, when I mention "s1" in my math notes, I will sometimes refer to the UBC edition.
	* Note 2: Alternatively, you can use the [way back machine](https://web.archive.org/web/20240117012305/https://textbooks.math.gatech.edu/ila/ila.pdf) in case the book isn't available online anymore.

covectors and transpose: [Mathemaniac YT video](https://www.youtube.com/watch?v=g4ecBFmvAYU)

Visualizing Gram-Schmidt Orthogonalization: [Dan Gries' YT video](https://www.youtube.com/watch?v=KOkuTXrv5Gg)

Useful GitHub resource for understanding some parts of the [Mathematics for Machine Learning: Linear Algebra](https://www.coursera.org/learn/linear-algebra-machine-learning) course: [here](https://github.com/Renatochaz/Mathematics_for_Machine_Learning/tree/master)


# Augmented Matrix

You can see the relationship between augmented matrix and row operations and vector equations [here](Algebraic%20Equations.md#Solving%20SLE%20Using%20Augmented%20Matrices).

Row operations for augmented matrices ([s1](https://personal.math.ubc.ca/~tbjw/ila/row-reduction.html#p-143)):

![](Media-Temp/Pasted%20image%2020240303191846.png)

Definition of <mark style="background: #FFF3A3A6;">row equivalent matrices</mark>: Two matrices are called row equivalent ***if one can be obtained from the other*** by doing some row operations ([s1](https://personal.math.ubc.ca/~tbjw/ila/row-reduction.html#row-reduction-elimination:~:text=Two%20matrices%20are%20called%20row%20equivalent%20if%20one%20can%20be%20obtained%20from%20the%20other%20by%20doing%20some%20number%20of%20row%20operations.)).

Therefore, row equivalent matrices have the same [solution set](Sciences/Formal%20Sciences/Mathematics/Algebra/Linear%20Algebra/Algebraic%20Equations.md#System%20of%20Linear%20Equations%20SLE).

# Echelon Form

## Row Echelon Form (REF)

definitions of row [echelon](#Echelon%20-%20Reason%20Behind%20Naming) form and [pivot](#Pivot%20-%20Reason%20Behind%20Naming) ([s1](https://personal.math.ubc.ca/~tbjw/ila/row-reduction.html#row-reduction-echelon-forms)):

![](Media-Temp/Pasted%20image%2020240303203610.png)

Side note 1: "all zero rows are at the bottom" ... that's assuming there are zero rows in the matrix to begin with. If there aren't, but the rest of the conditions apply, then it's still REF.

Side note 2: if you think about it, condition "2." will always be true if condition "3." is true, so I believe we can write conditions "1." and "3." only. 

Side note 3: Check this section to see why it's called a "pivot".

Why convert a matrix to REF? Because it's generally easy to solve using back-substitution. For example:

![](Media-Temp/Pasted%20image%2020240303202159.png)

We can easily get $z, y, x$ by back-substitution.

## Reduced Row Echelon Form (RREF)

Definition: A matrix is in _reduced row echelon form (RREF)_ if it is in [Row Echelon Form (REF)](#Row%20Echelon%20Form%20(REF)), and in addition:

![](Media-Temp/Pasted%20image%2020240303203015.png)

To summarize ([source](https://math.stackexchange.com/questions/1714783/is-it-okay-to-determine-pivot-positions-in-a-matrix-in-echelon-form-not-in-redu)): a matrix is RREF if 
* Its leading entries are 1's
* There are 0's below and above each leading 1
* All *zero rows* are at the bottom

Note 1: the presence or absence of augmented columns (i.e., the vertical line at the right of a matrix) isn't a factor for deciding if a matrix is RREF/REF or not.

Note 2: When you think about it, a RREF matrix is completely solved. For example:

![](Media-Temp/Pasted%20image%2020240303203103.png)

## REF and RREF Examples

For each of the following matrices, specify which are REF, RREF, none:

![](Media-Temp/Pasted%20image%2020240303204229.png)

Answers:

1-4 are RREF, 5-8 are REF, 9-12 are neither RREF nor REF

Explanation of some of these answers:

For matrix (1), we deduce that it's RREF by seeing that:
* There is nothing but zeros above and below both pivots (which are `1` in r1c1 and `1` in r2c2), and this is a condition for RREF.
* `2` and `-1` are not pivots. Remember. A pivot is the first non-zero element in a row. And in both r1 and r2, that pivot was `1`, which is a condition for RREF.

For matrix (7), we deduce that it's REF not RREF because there's `17` above the second pivot (i.e., `1` in r2c2).

For matrix (9), it's not RREF because it's not REF, and it's not REF because there's a `1` (not a `0`) under the second pivot (which is `2` at r2c3). Same logic for matrix (10) and (11).

For matrix (12), it's not RREF because it's not REF, and it's not REF because there's a ***zero row*** above the first pivot (which is `1`). However, a REF matrix must have all zero rows at the bottom of the matrix.

## Echelon - Reason Behind Naming

The term _echelon_ comes from the French word _"échelon"_, which means "level" or step of a ladder (which is a rung) ([source: Wikipedia](https://en.wikipedia.org/wiki/Row_echelon_form#:~:text=Every%20matrix%20can%20be%20put,look%20like%20an%20inverted%20staircase.)). 

It refers to the fact that the nonzero entries of a matrix in row echelon form look like an inverted staircase.

Fun fact: An **echelon formation** also means a (usually [military](https://en.wikipedia.org/wiki/Tactical_formation "Tactical formation")) formation in which its units are arranged diagonally. Each unit can be stationed behind and to the right (a "right echelon"):

![](Media-Temp/Pasted%20image%2020240305173339.png)

![](Media-Temp/Pasted%20image%2020240305173348.png)

## Pivot - Reason Behind Naming

In [Row Echelon Form (REF)](#Row%20Echelon%20Form%20(REF)), we introduced what a "pivot" means in a matrix, but why the word "pivot" ([s1](https://personal.math.ubc.ca/~tbjw/ila/row-reduction.html#remark-7))?

Consider the following [System of Linear Equations (SLE)](Algebraic%20Equations.md#System%20of%20Linear%20Equations%20(SLE)):

![](Media-Temp/Pasted%20image%2020240304201956.png)

We can visualize this system as a pair of lines in $\mathbb{R}^2$ that intersect at the point $(1,1)$:

![](Media-Temp/Pasted%20image%2020240304202522.png)

Now, rewriting this SLE to REF:

![](Media-Temp/Pasted%20image%2020240304202827.png)

And visualizing these to REF rows:

![](Media-Temp/Pasted%20image%2020240304202856.png)

We see, geometrically, the original blue line has been replaced with the new light green line $y=1$. We can think of that new line as ***rotating, or pivoting, around the solution*** $(1,1)$. We used the pivot position in the matrix in order to make the original blue line pivot like this. This is one possible explanation for the terminology “pivot”.

