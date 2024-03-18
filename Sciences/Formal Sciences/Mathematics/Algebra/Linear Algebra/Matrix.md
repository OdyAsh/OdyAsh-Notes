
Main sources:
* Source 1: [Interactive Linear Algebra](https://textbooks.math.gatech.edu/ila/index.html) Textbook by Georgia Institute of Technology 
	* Note 1: Check the UBC version [here](https://personal.math.ubc.ca/~tbjw/ila/index.html), which is a [fork](https://github.com/tbjw/ILAUBC) of [Georgia's GitHub repository](https://github.com/QBobWatson/ila), I personally like how they ordered/re-explained certain concepts more than Georgia's version. 
	* Note that the order of some content is changed in this version, as mentioned [here](https://personal.math.ubc.ca/~tbjw/ila/preface-2.html). Moreover, when I mention "s1" in my math notes, I will sometimes refer to the UBC edition.
	* Note 2: Alternatively, you can use the [way back machine](https://web.archive.org/web/20240117012305/https://textbooks.math.gatech.edu/ila/ila.pdf) in case the book isn't available online anymore (but it's a little slower).

covectors and transpose: [Mathemaniac YT video](https://www.youtube.com/watch?v=g4ecBFmvAYU)

Visualizing Gram-Schmidt Orthogonalization: [Dan Gries' YT video](https://www.youtube.com/watch?v=KOkuTXrv5Gg)

Useful GitHub resource for understanding some parts of the [Mathematics for Machine Learning: Linear Algebra](https://www.coursera.org/learn/linear-algebra-machine-learning) course: [here](https://github.com/Renatochaz/Mathematics_for_Machine_Learning/tree/master)

# Defining Augmented Matrices by Relating Them to Linear Systems and Vector Equations

The relationship between linear systems and augmented matrices ([s1](https://personal.math.ubc.ca/~tbjw/ila/row-reduction.html#p-139)):

Solving equations by elimination requires writing the variables $x,y,z$ and the equals sign $=$ over and over again, merely as placeholders. 

Since the coefficient _numbers_ are the only thing that change, we can make our life easier by extracting only the numbers, and putting them in a box (called augmented matrix):

$$\left\{\begin{array}{cccc|c}x+2y+3z=&6\\2x-3y+2z=&14\\3x+y-z=&-2\end{array}\right.\;\;\xrightarrow{\mathrm{becomes}}\left(\begin{array}{rrr|r}1&2&3&6\\2&-3&2&14\\3&1&-1&-2\end{array}\right)$$

<mark style="background: #FFF3A3A6;">The word “augmented” refers to the vertical line</mark>, which we draw to remind ourselves where the equals sign belongs.

<mark style="background: #FFF3A3A6;">A matrix is a grid of numbers without the vertical line</mark>.

The relationship between vector equations and augmented matrices:

![](Media-Temp/Pasted%20image%2020240303191450.png)

Now, you can read more about augmented matrices [here](Matrix.md#Possible%20Row%20Operations).

# Possible Row Operations

Row operations for augmented matrices ([s1](https://personal.math.ubc.ca/~tbjw/ila/row-reduction.html#p-143)):

![](Media-Temp/Pasted%20image%2020240303191846.png)

# Row Equivalent Matrices

Definition of <mark style="background: #FFF3A3A6;">row equivalent matrices</mark>: Two matrices are called row equivalent ***if one can be obtained from the other*** by doing some row operations ([s1](https://personal.math.ubc.ca/~tbjw/ila/row-reduction.html#row-reduction-elimination:~:text=Two%20matrices%20are%20called%20row%20equivalent%20if%20one%20can%20be%20obtained%20from%20the%20other%20by%20doing%20some%20number%20of%20row%20operations.)).

Therefore, row equivalent matrices have the same [solution set](Sciences/Formal%20Sciences/Mathematics/Algebra/Linear%20Algebra/Algebraic%20Equations.md#System%20of%20Linear%20Equations%20SLE).

# Echelon Form

## Row Echelon Form (REF)


definitions of <mark style="background: #FFF3A3A6;">row echelon form</mark> and <mark style="background: #FFF3A3A6;">pivot</mark> ([s1](https://personal.math.ubc.ca/~tbjw/ila/row-reduction.html#row-reduction-echelon-forms)):

![](Media-Temp/Pasted%20image%2020240303203610.png)

Side note 1: "all <mark style="background: #FFF3A3A6;">zero rows</mark> are at the bottom" ... that's assuming there are zero rows in the matrix to begin with. If there aren't, but the rest of the conditions apply, then it's still REF.

Side note 2: if you think about it, condition "2." will always be true if condition "3." is true, so I believe we can write conditions "1." and "3." only. 

Side note 3: Check [this](#Echelon%20-%20Reason%20Behind%20Naming) and [this](#Pivot%20-%20Reason%20Behind%20Naming) section to see why it's called a "echelon" and "pivot".

<mark style="background: #FF5582A6;">Important note 1</mark>: Why convert a matrix to REF? Because it's generally easy to solve using back-substitution. For example:

![](Media-Temp/Pasted%20image%2020240303202159.png)

We can easily get $z, y, x$ by back-substitution.

<mark style="background: #FF5582A6;">Important note 2</mark>: check out how to transform an augmented matrix into its REF form by checking the [row reduction algorithm](Algebraic%20Equations.md#SLE%20as%20an%20Augmented%20Matrix).

## Reduced Row Echelon Form (RREF)

Definition: A matrix is in <mark style="background: #FFF3A3A6;">reduced row echelon form (RREF)</mark> if it is in [Row Echelon Form (REF)](#Row%20Echelon%20Form%20(REF)), and in addition:

![](Media-Temp/Pasted%20image%2020240303203015.png)

To summarize ([source](https://math.stackexchange.com/questions/1714783/is-it-okay-to-determine-pivot-positions-in-a-matrix-in-echelon-form-not-in-redu)): a matrix is RREF if 
* Its leading entries are 1's
* There are 0's below and above each leading 1
* All *zero rows* are at the bottom

Note 1: the presence or absence of augmented columns (i.e., the vertical line at the right of a matrix) isn't a factor for deciding if a matrix is RREF/REF or not.

Note 2: When you think about it, a RREF matrix is completely solved. For example:

![](Media-Temp/Pasted%20image%2020240303203103.png)

<mark style="background: #FF5582A6;">Important note</mark>: check out how to transform an augmented matrix into its RREF form by checking the [row reduction algorithm](Algebraic%20Equations.md#SLE%20as%20an%20Augmented%20Matrix).

## Distinguishing Between REF and RREF Matrices

For each of the following matrices, specify which are REF, RREF, none:

![](Media-Temp/Pasted%20image%2020240303204229.png)

Answers:

1-4 are RREF, 5-8 are REF, 9-12 are neither RREF nor REF

Explanation of some of these answers:

For matrix (1), we deduce that it's RREF by seeing that:
* There is nothing but zeros above and below both pivots (which are `1` in r1c1 and `1` in r2c2), and this is a condition for RREF.
* `2` and `-1` are not pivots. Remember. A pivot is the first non-zero element in a row. And in both r1 and r2, that pivot was `1`, which is a condition for RREF.

For matrix (7), we deduce that it's REF not RREF because there's `17` above the second pivot (i.e., `1` in r2c2).

For matrix (9), it's not RREF because it's not REF, and it's not REF because there's a `1` (not a `0`) **below** the second pivot (which is `2` at r2c3). Same logic for matrix (10) and (11).

For matrix (12), it's not RREF because it's not REF, and it's not REF because there's a ***zero row*** **above** the first pivot (which is `1`). 
* Recall that a REF matrix must have all zero rows at the bottom of the matrix.

## Pivot Position and Pivot Column

Later, it will be very important to know the positions that will later become a pivot (i.e., after the matrix is a REF); this is the reason for the following definitions ([s1](https://personal.math.ubc.ca/~tbjw/ila/row-reduction.html#p-174)):

A <mark style="background: #FFF3A3A6;">pivot position</mark> of a matrix is an entry that is a pivot of a [REF](#Row%20Echelon%20Form%20(REF)) of that matrix.

A <mark style="background: #FFF3A3A6;">pivot column</mark> of a matrix is a column that contains a pivot position.

Example ([s1](https://personal.math.ubc.ca/~tbjw/ila/row-reduction.html#p-174)):

![](Media-Temp/Pasted%20image%2020240314113208.png)

## Inconsistent REF

An augmented matrix corresponds to an inconsistent system of equations if and only if the last column (i.e., the augmented column) is a [pivot column](#Pivot%20Position%20and%20Pivot%20Column) ([s1](https://personal.math.ubc.ca/~tbjw/ila/row-reduction.html#p-182)).

Example ([s1](https://personal.math.ubc.ca/~tbjw/ila/row-reduction.html#p-182)):

![](Media-Temp/Pasted%20image%2020240314113717.png)

Note: recall the [SLE as an Augmented Matrix](Algebraic%20Equations.md#SLE%20as%20an%20Augmented%20Matrix) if you don't understand the solution above.

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

