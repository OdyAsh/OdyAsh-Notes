
Main sources:
* Source 1: [Interactive Linear Algebra](https://textbooks.math.gatech.edu/ila/index.html) Textbook by Georgia Institute of Technology 
	* Note 1: Check the UBC version [here](https://personal.math.ubc.ca/~tbjw/ila/index.html), which is a [fork](https://github.com/tbjw/ILAUBC) of [Georgia's GitHub repository](https://github.com/QBobWatson/ila), in case the latter website is down. Note that the order of some content is changed in this version, as mentioned [here](https://personal.math.ubc.ca/~tbjw/ila/preface-2.html). Moreover, when I mention "s1" in my math notes, I will sometimes refer to the UBC edition.
	* Note 2: Alternatively, you can use the [way back machine](https://web.archive.org/web/20240117012305/https://textbooks.math.gatech.edu/ila/ila.pdf) in case the book isn't available online anymore.

covectors and transpose: [Mathemaniac YT video](https://www.youtube.com/watch?v=g4ecBFmvAYU)

Visualizing Gram-Schmidt Orthogonalization: [Dan Gries' YT video](https://www.youtube.com/watch?v=KOkuTXrv5Gg)

Useful GitHub resource for understanding some parts of the [Mathematics for Machine Learning: Linear Algebra](https://www.coursera.org/learn/linear-algebra-machine-learning) course: [here](https://github.com/Renatochaz/Mathematics_for_Machine_Learning/tree/master)


# Linear Equation (LE)

Linear equation definition ([s1](https://textbooks.math.gatech.edu/ila/systems-of-eqns.html#p-32)): 

![](Media-Temp/Pasted%20image%2020240226163632.png)

## System of Linear Equations (SLE)

System of linear equations (SLE) definition ([s1](https://textbooks.math.gatech.edu/ila/systems-of-eqns.html#p-35)):

![](Media-Temp/Pasted%20image%2020240229084120.png)

The ***solution*** of an SLE is defined as the list of numbers $x,y,z,\cdots$ that make ***all the equations true simultaneously***.

The ***solution set*** of an SLE is the collection of all solutions.

***Solving*** an SLE means finding all solutions with formulas involving some number of parameters.

An SLE is called ***inconsistent*** if it has no solutions. It is called ***consistent*** if it has at least one solution.

## SLE vs Vector Equations

It turns out that vector equations are simply systems of linear equations in different notation ([s1](https://personal.math.ubc.ca/~tbjw/ila/systems-of-linear-equations.html#p-109)). For example, the vector equation:

$$ x\begin{pmatrix}1\cr2\cr6\end{pmatrix}+y\begin{pmatrix}-1\cr-2\cr-1\end{pmatrix}=\begin{pmatrix}8\cr16\cr3\end{pmatrix}$$

is actually an SLE:

$$\begin{array}{r}x-y=8\cr2x-2y=16\cr6x-y=3\end{array}$$


## Visualizing Solution Set of LE

Consider the linear equation $x+y=1$. We can rewrite this as $y=1−x$, which defines a [Line](../../Geometry/Geometry.md#Line) in the [Plane](../../Geometry/Geometry.md#Plane) as follows:

![](Media-Temp/Pasted%20image%2020240229093605.png)

Here, the solution set of this single equation is all the points on the line.

Side note: the line above represents a 1-plane in 2-space, since the equation has 2 variables.

Now, consider the linear equation $x+y+z=1$. This is the [Implicit Equation](#Implicit%20Equation) for a plane in space:

![](Media-Temp/Pasted%20image%2020240229184350.png)

Here, the solution set of this single equation is all the points on the plane.

Side note 1: the plane above represents a 2-plane in 3-space, since the equation has 3 variables.

Side note 2: more generally, a single linear equation in $n$ variables defines an $(n-1)$-plane in $n$-space ([s1](https://personal.math.ubc.ca/~tbjw/ila/systems-of-linear-equations.html#definition-11)).

Now, consider this SLE of 2 linear equations (LEs):

$$\begin{aligned}x-3y&=-3\\2x+y&=-8.\end{aligned}$$

You can see that the solution set of this SLE consists of 1 point, which is $(3,2)$, as shown here:

![](Media-Temp/Pasted%20image%2020240229185709.png)

Moreover, we can have an inconsistent solution set, like this:

![](Media-Temp/Pasted%20image%2020240229185932.png)

Or an infinite solution set, like this:

![](Media-Temp/Pasted%20image%2020240229185906.png)


Another example of an infinite solution set is all the points on the red line shown here:

![](Media-Temp/Pasted%20image%2020240229190147.png)

Side note 1: The 2 equations above are called the [Implicit Equations](#Implicit%20Equation) of that red line, as the red line is defined implicitly as the simultaneous solutions to those 2 equations. Another example of this is shown [here](https://personal.math.ubc.ca/~tbjw/ila/parametric-form.html#note-7).

Side note 2: Check [this](https://personal.math.ubc.ca/~tbjw/ila/systems-of-linear-equations.html#subsection-8) section to see how we can visualize the solution set in the [Parametric Form](Algebraic%20Equations.md#Parametric%20Equation) instead of implicit equations.

## Solving SLE Using Gaussian Elimination (i.e., Row Reduction) Method

In mathematics, **Gaussian elimination**, also known as **row reduction**, is an [algorithm](https://en.wikipedia.org/wiki/Algorithm "Algorithm") for solving [systems of linear equations](https://en.wikipedia.org/wiki/System_of_linear_equations "System of linear equations"). The method is named after [Carl Friedrich Gauss](https://en.wikipedia.org/wiki/Carl_Friedrich_Gauss "Carl Friedrich Gauss") (1777–1855) ([source: wikipedia](https://en.wikipedia.org/wiki/Gaussian_elimination)).

We will solve systems of linear equations algebraically using the *elimination* method. In other words, we will combine the equations in various ways to try to eliminate as many variables as possible from each equation ([s1](https://personal.math.ubc.ca/~tbjw/ila/row-reduction.html#row-reduction-elimination)).

Note: You can see the relationship between augmented matrix and linear systems and vector equations [here](Matrix.md#Defining%20Augmented%20Matrices%20by%20Relating%20Them%20to%20Linear%20Systems%20and%20Vector%20Equations).

### SLE as a Linear System

There are three valid operations we can perform on an SLE ([s1](https://personal.math.ubc.ca/~tbjw/ila/row-reduction.html#row-reduction-elimination)):

![](Media-Temp/Pasted%20image%2020240229192020.png)

### SLE as an Augmented Matrix

Side note: you can read more about augmented matrices [here](Matrix.md#Defining%20Augmented%20Matrices%20by%20Relating%20Them%20to%20Linear%20Systems%20and%20Vector%20Equations).

Here is the row reduction algorithm, summarized in pictures ([s1](https://personal.math.ubc.ca/~tbjw/ila/row-reduction.html#p-173)):

![](Media-Temp/Pasted%20image%2020240314093206.png)

Side note: observe that the step "Get 1 here" can either be done using step **a** or **b** (or both) in the pseudocode below.

Assuming you're familiar with the [possible row operations](Matrix.md#Possible%20Row%20Operations), here is the row reduction algorithm as pseudocode ([s1](https://personal.math.ubc.ca/~tbjw/ila/row-reduction.html#algo-row-reduction)):

1. **Step 1a:** Swap the first row with a lower one so a leftmost nonzero entry is in the first row (if necessary).
2. **Step 1b:** Scale the first row so that its first nonzero entry is equal to 1.
3. **Step 1c:** Use row replacement so all entries below this 1 are 0.
---
1. **Step 2a:** Swap the second row with a lower one so that the leftmost nonzero entry is in the second row.
2. **Step 2b:** Scale the second row so that its first nonzero entry is equal to 1.
3. **Step 2c:** Use row replacement so all entries below this one are zero.
---
1. **Step 3a:** Swap the third row with a lower one so that the leftmost nonzero entry is in the third row.
2. ...Repeat the process until all rows have been processed...
---
1. **Last Step:** Use row replacement to clear all entries above the pivots, starting with the last pivot.

#### Examples

An example is provided [here](https://personal.math.ubc.ca/~tbjw/ila/row-reduction.html#p-173) (click on the word "Example").

Another example: convert the following augmented matrix to RREF:


$$
\left(\begin{array}{rrr|r}2&-1&3&3\cr4&2&-2&2\cr6&-3&1&9\end{array}\right)
$$

Answer:

![](Media-Temp/Pasted%20image%2020240314103208.png)

Note: If you don't understand how this matrix is a REF, check [this](Sciences/Formal%20Sciences/Mathematics/Algebra/Linear%20Algebra/Matrix.md#Row%20Echelon%20Form%20REF).

Continuing:

![](Media-Temp/Pasted%20image%2020240314103847.png)

Therefore:

$$\begin{alignat*}{3}
1x&+0y&+0z&=1 \cr 
0x&+1y&+0z&=-1 \cr 
0x&+0y&+1z&=0
\end{alignat*}$$

In other words, the final answer is:

$$
x=1,\space y=-1,\space z=0
$$

Note 1: If you don't understand how this matrix is a RREF, check [this](Matrix.md#Reduced%20Row%20Echelon%20Form%20(RREF)).

Note 2: you can visualize the answer [here](https://personal.math.ubc.ca/~tbjw/ila/demos/rrinter.html?mat=2,-1,3,3:4,2,-2,2:6,-3,1,9&ops=m0:1.2,r0:-4:1,r0:-6:2,m1:1.4,m2:-1.8,r2:2:1,r2:-3.2:0,r1:1.2:0&cur=0) (click the right blue arrow to see different row operations).

# Implicit Equation

An _implicit equation_ is an equation which relates the variables involved ([source](https://undergroundmathematics.org/glossary/implicit-equation): underground mathematics). For example, the equation:

$$ x^2+y^2=4$$

gives a relationship between $x$ and $y$, even though it does not specify $y$ explicitly in the form $y=f(x)$.

As this example shows, it may not be possible to convert an implicit equation into an equation of the form $y=f(x)$ for some function $f(x)$, as the $x$ values in the range $-2<x<2$ each correspond to two values for $y$.




# Parametric Equation

[source](https://textbooks.math.gatech.edu/ila/systems-of-eqns.html#specialcase-13)

Consider the linear equation $x+y=1$; we call this an _implicit equation_ of the line. We can write the same line in _parametric form_ as follows:

$$ (x,y)=(t,1-t)\quad\text{for any}\quad t\in\mathbb{R}.$$

This means that every point on the line has the form $(t,1−t)$ for some real number $t$. In this case, we call $t$ a _parameter_, as it _parameterizes_ the points on the line. Visualization of equation above when substituting for multiple $t$ values:

![](Attachments%20-%20Algebraic%20Equations/Pasted%20image%2020231116045520.png)

Notice that this is the same line you'll get if you decide to use [the traditional method for drawing lines](https://www.radfordmathematics.com/algebra/line-equations/line-equations-drawing-line-from-equation.html).

I highly suggest checking out [this example](https://textbooks.math.gatech.edu/ila/systems-of-eqns.html#specialcase-13:~:text=1-,Now%20consider%20the%20system%20of%20two%20linear%20equations,-B) as well.


