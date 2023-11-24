#math #linear-algebra 

Main sources:
[khan academy: Unit 1: Vectors and spaces](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces)

# Vector Definition

<mark style="background: #FF5582A6;">It is something that has a magnitude and a direction</mark>.

Technically, we should say "a mathematical object" instead of "something".

Intuitive example ([source](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/vector-introduction-linear-algebra)):

![](Attachments%20-%20Vectors/Pasted%20image%2020231104130417.png)

# Vector vs Scalar

Source: comment section of [this](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/vector-introduction-linear-algebra) KA video.

* A vector is a quantity or phenomenon that has two independent properties: **magnitude and direction**. 
	* The term also denotes the mathematical or geometrical representation of such a quantity.  
	* Examples of vectors in nature are velocity, momentum, force, electromagnetic fields, and weight. (Weight is the force produced by the acceleration of gravity acting on a mass.) 
* A scalar is a quantity or phenomenon that exhibits **magnitude only**, with no specific direction. 
	* Examples of scalars include speed, mass, electrical resistance, and hard-drive storage capacity.

# Vector Notation

It has notation like the following: 

$$\vec{v}=\left(5,0\right)=\left[\begin{array}{l}{5}\cr{0}\end{array}\right]=5i+0j$$

Such that:
* $5$ and $0$ are called ***components*** of a vector, while $(5,0)$ is called a ***2-tuple*** in a 2-D real coordinate space $\left(\mathbb{R}^2\right)$ ([source](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/real-coordinate-spaces)).
	* Side note 1: $\mathbb{R}^2$ is also called a ***set***, such that $\vec{v}\in\mathbb{R}^2$ is called " vector $\vec{v}$  belongs in the set $\mathbb{R}^2$ "
* It can also be represented using unit vectors $i$ and $j$ , as explained in the [Unit vector](#Unit%20Vector) section.
* It can be [added](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/adding-vectors) and [multiplied (by scalers)](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/multiplying-vector-by-scalar)

Side notes:
* It is a common convention to see vectors represented with a small, italic letter with an arrow like this: $\vec{v}$. However, sometimes, we'll see images from the internet neglecting this convention, for example, vector $A$, so try not to get confused when this happens, and just read the preceding paragraphs to understand what $A$ represents.
* Normally, we tend think of vectors as starting from the origin point of a coordinate plane. Example:
  
  ![](Attachments%20-%20Vectors/Pasted%20image%2020231104160540.png)
  
  Consequently, when we do operations on these vectors, like [adding vectors](#Vector%20Addition), we get a vector like this:
  
  ![](Attachments%20-%20Vectors/Pasted%20image%2020231104160832.png)
  
  However, we may move these vectors' starting points (i.e., tails) to easily conceptualize these operations, for example:
  
  ![](Attachments%20-%20Vectors/Pasted%20image%2020231104161011.png)
  
  Now the question is the following: "why is it allowed for us to move these vectors' starting points to anywhere we want in the coordinate plane?" 
  
  Answer: Because if we recall the [definition of a vector](#Vector%20Definition), we see that we only care about encoding two pieces of information: **magnitude** and **direction**. Therefore, the actual location of the vector in the plane does not matter.

# Vector Addition

## Triangle Law of Vector Addition

Addition visualization ([interactive source](https://sciencepickleapps.com/VisuallyAddingVectorsV1-0-0/), from [this](https://sciencepickle.com/earth-systems/vectors-and-forces/adding-vectors/)):
![vector-addition](Attachments%20-%20Vectors/vector-addition.mp4)

Example: 

$$\vec{v}=\vec{red}+\vec{green}+\vec{blue}=\left[\begin{array}{c}{-9}\cr{3}\end{array}\right]+\left[\begin{array}{c}{2}\cr{3}\end{array}\right]+\left[\begin{array}{c}{2}\cr{0.2}\end{array}\right]=\left[\begin{array}{c}{-5}\cr{6.2}\end{array}\right]$$

Note: If the example above adds 2 vectors only, then the method of addition above is called [the triangle law of vector addition](https://byjus.com/physics/triangle-law-of-vector-addition/#:~:text=Triangle%20law%20of%20vector%20addition%20states%20that%20when%20two%20vectors,direction%20of%20the%20resultant%20vector.).

## Parallelogram Law of Vector Addition

[source](https://www.khanacademy.org/math/precalculus/x9e81a4f98389efdf:vectors/x9e81a4f98389efdf:vector-add-sub/v/parallelogram-rule-for-vector-addition#:~:text=The%20parallelogram%20rule%20says%20that,same%20point%20as%20the%20vectors.)

The parallelogram rule says that if we place two vectors so they have the same initial point, and then complete the vectors into a parallelogram, then ***the sum of the vectors is the directed diagonal*** that starts at the same point as the vectors.

Example:

step 1:

![](Attachments%20-%20Vectors/Pasted%20image%2020231110175351.png)

step 2:

![](Attachments%20-%20Vectors/Pasted%20image%2020231110175424.png)

step 3: start from step 1, then move a to b instead:

![](Attachments%20-%20Vectors/Pasted%20image%2020231110175522.png)

step 4: merge steps 2 and 3:

![](Attachments%20-%20Vectors/Pasted%20image%2020231110175612.png)

Step 5: draw the diagonal (which is the result of a + b):

![](Attachments%20-%20Vectors/Pasted%20image%2020231110180525.png)

# Vector Subtraction

Suppose you have these two vectors:

![](Attachments%20-%20Vectors/Pasted%20image%2020231104155811.png)
(Adapted from [here](https://www.google.com/search?q=vector+subtraction&sca_esv=579447376&tbm=isch&sxsrf=AM9HkKnGtLJ6VqlC3AJLr_SJv37CNWgI9w:1699105968608&source=lnms&sa=X&ved=2ahUKEwix5sb9vqqCAxW_UKQEHatZBbEQ_AUoAXoECAQQAw&biw=1920&bih=911&dpr=1#vhid=V5qJxTe7D4HnZM&vssid=3981:1DaQEkvNT6JBSM))

Now, what if we want to subtract B from A? (i.e., A - B)?

Mathematical example:

$$A-B=\left[\begin{array}{c}{3}\cr{5}\end{array}\right]-\left[\begin{array}{c}{4}\cr{2}\end{array}\right]=\left[\begin{array}{c}{-1}\cr{3}\end{array}\right]$$

Now, this vector can be represented like this:

![](Attachments%20-%20Vectors/Pasted%20image%2020231104162015.png)

Now, to intuitively grasp how subtraction works geometrically, there are two methods of moving the vector $A-B$:

* Method 1 ([source](https://www.onlinemathlearning.com/vector-subtraction.html)):
  
  ![](Attachments%20-%20Vectors/Pasted%20image%2020231104162158.png)
  
  Applying this on the previous example:
  
  ![](Attachments%20-%20Vectors/Pasted%20image%2020231104162448.png)
  
  So it's as if we're [adding](#Vector%20Addition) $A$ to $-B$ to get the emerged vector $A-B$:  
  
  ![](Attachments%20-%20Vectors/Pasted%20image%2020231104162559.png)
  
  Final image which contains all of the previous images' steps:
  
  ![](Attachments%20-%20Vectors/Pasted%20image%2020231104162712.png)
  
	* Side note: this method (i.e., a + (-b)) is used as a first step in subtracting vectors using the [Parallelogram Rule of Adding Vectors](#Parallelogram%20Law%20of%20Vector%20Addition) ([detailed video](https://www.khanacademy.org/math/precalculus/x9e81a4f98389efdf:vectors/x9e81a4f98389efdf:vector-add-sub/v/subtracting-vectors-with-parallelogram-rule))
	  
* Method 2: 
  
  Starting from this image:
  
  ![](Attachments%20-%20Vectors/Pasted%20image%2020231104162015.png)
  
  Simply move the vector $A-B$ to be between $A$ and $B$:
  
  ![](Attachments%20-%20Vectors/Pasted%20image%2020231104163010.png)
  
  Why is this logical? First, recall how we visualize [vector addition](#Vector%20Addition), then, recognize that what we're doing above is simply: $A=B+(A-B)$, so it's as if the vector $A$ emerged like the image above due to adding $B$ to $A-B$.
	* Side note: this method gives the same visual result as the one in the [Triangle Law of Vector Addition](#Triangle%20Law%20of%20Vector%20Addition).

## Vector Subtraction Visual summary

![](Attachments%20-%20Vectors/Pasted%20image%2020231104163904.png)

# Vector Scalar Multiplication

Multiplication visualization ([source](https://makeagif.com/gif/vector-multiplication-by-scalar-G4qCVh)):
![vector-scalar-multiplication](Attachments%20-%20Vectors/vector-scalar-multiplication.gif)

Formula of a scalar-multiplied vector: $c \cdot \vec v$

Formula of a scalar-multiplied vector's magnitude: $||c\cdot \vec v||=|c|\cdot ||\vec v||$ 


To get the reverse direction of a vector, add 180 to its direction.

Example ([source](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/e/scaling_vectors)):

![](Attachments%20-%20Vectors/Pasted%20image%2020231104110053.png)

Answer:

![](Attachments%20-%20Vectors/Pasted%20image%2020231104112518.png)

![](Attachments%20-%20Vectors/Pasted%20image%2020231104112617.png)


# Vector Forms

[KA source](https://www.khanacademy.org/math/algebra-home/alg-vectors/alg-magnitude-direction/a/vector-forms-review)

Different vector forms:

![](Attachments%20-%20Vectors/Pasted%20image%2020231110203104.png)

![](Attachments%20-%20Vectors/Pasted%20image%2020231110203317.png)


## Vector Component Form vs 

# Vector Types

[Useful source](https://byjus.com/maths/types-of-vectors/)

## Unit Vector (UV)

[source](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/intro-unit-vector-notation)

### Special UVs

Definition: 
* <mark style="background: #FF5582A6;">A vector that has a magnitude of 1 is a unit vector.</mark>
* It is also known as Direction Vector.

Specifically, in cartesian coordinates, <mark style="background: #FF5582A6;">special unit vectors along the axis are denoted by i and j respectively</mark>. Their formulae (in $\mathbb{R}^2$):

$$\begin{aligned}
\hat{i}&=
\left[\begin{matrix}{1}\cr{0}\cr\end{matrix}\right] \cr\cr
\hat{j}&=
\left[\begin{matrix}{0}\cr{1}\cr\end{matrix}\right]
\end{aligned}$$

Visualization:

![](Attachments%20-%20Vectors/Pasted%20image%2020231106155417.png)
([source](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/intro-unit-vector-notation))

These *special vectors* can be generalized to more dimensions. For example, in $\mathbb{R}^3$, we have the following *special* unit vectors:


$$\begin{aligned}
\hat{i}&=
\left[\begin{matrix}{1}\cr{0}\cr{0}\cr\end{matrix}\right] \cr\cr
\hat{j}&=
\left[\begin{matrix}{0}\cr{1}\cr{0}\cr\end{matrix}\right] \cr\cr
\hat{k}&=
\left[\begin{matrix}{0}\cr{0}\cr{1}\cr\end{matrix}\right] \cr\cr
\end{aligned}$$


### General UVs

Moreover, if a vector $\vec{v}$ is not *special*, then its unit vector is denoted by $\left|\left|\vec{v}\right|\right|$. 

Visualization:
![](Attachments%20-%20Vectors/Pasted%20image%2020231107092101.png)


and its equation:

$$\hat{u}=\frac{\vec{v}}{\left|\left|\vec{v}\right|\right|}$$

where 
$\hat{u}$ = normalized vector (i.e., unit vector)
$\vec{v}$ = non-zero vector
$\left|\left|\vec{v}\right|\right|$ = norm (or length) of $\vec{v}$

### Exercise Explanation of The UV Formula

[source](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/e/unit-vector)

![](Attachments%20-%20Vectors/Pasted%20image%2020231110171537.png)

![](Attachments%20-%20Vectors/Pasted%20image%2020231110171639.png)

Making sure that this unit vector has a magnitude of 1:

![](Attachments%20-%20Vectors/Pasted%20image%2020231110174904.png)

Visualizing the answer:

![](Attachments%20-%20Vectors/Pasted%20image%2020231110174941.png)

### Intuitive Explanation of The UV Formula

From [Vector Multiplication](#Vector%20Scalar%20Multiplication) rule, we have $c \cdot \hat u = \vec v$ 

dividing both sides by $c$:

$$\hat{u}=\frac{\vec{v}}{c}=\frac{\vec{v}}{\left|\left|\vec{v}\right|\right|}$$

However, this formulation is considered to be the unit vector formula only if $\hat u$ has a magnitude (i.e., $||\hat u||$) equal to 1.

Essentially, we're saying that:
* vector multiplication formula: multiply a scalar by a small vector to get a big vector
* unit vector formula: divide a big vector by a scalar to get a small vector
	* the "small vector" here has to have a magnitude of  1 (i.e., unit vector)


## Collinear Vectors

Definition ([source](https://unacademy.com/content/jee/study-material/mathematics/all-about-collinear-vectors/#:~:text=Whenever%20any%20two%20provided%20vectors,or%20parallel%20to%20one%20another.)):
* Two (or more) vectors are said to be collinear if they are parallel to each other.
* Examples:
  
  ![](Attachments%20-%20Vectors/Pasted%20image%2020231110194740.png)

## Position Vector

[source 1](https://www.physicsread.com/displacement-vector/#:~:text=And%20when%20the%20position%20of%20a%20point%20is%20represented%20in%20vector%20form%2C%20it%20is%20called%20a%20position%20vector.), [source 2](https://www.nagwa.com/en/explainers/505138303596/), [source 3](https://byjus.com/physics/position-and-displacement-vectors/#what-is-a-position-vector), [KA video explanation](https://www.khanacademy.org/math/ap-calculus-bc/bc-advanced-functions-new/bc-9-4/v/position-vector-valued-functions)

Definition: It is the position of a point when it is represented in a vector form:
  
![](Attachments%20-%20Vectors/Pasted%20image%2020231110205330.png)

([source](https://www.google.com/search?q=position+vector+vs+non+position+vector&tbm=isch&ved=2ahUKEwifteSbjLqCAxXpmCcCHeaVBH0Q2-cCegQIABAA&oq=position+vector+vs+non+position+vector&gs_lcp=CgNpbWcQAzoECCMQJ1DKCFi8H2D8H2gCcAB4AIABzAGIAfUWkgEGMC4xOS4ymAEAoAEBqgELZ3dzLXdpei1pbWfAAQE&sclient=img&ei=8XpOZd_4JOmxnsEP5quS6Ac&bih=923&biw=1920&hl=en#vhid=MR7wlvEObohfDM&vssid=3981:11csnMkTDlQ9jM))

noting that $\vec O$ always signifies that the start of the vector is the origin point $(0,0)$.


## Displacement Vector

[source](https://www.physicsread.com/displacement-vector/)

For example, you traveled from point **A** to point **B**. And if you look at your journey path, you will see that your total displacement is **AB**:

![](Attachments%20-%20Vectors/Pasted%20image%2020231110204352.png)

And if you express this displacement in vector form, it is called displacement vector:

$$ \vec{s}=\overrightarrow{AB}$$

this displacement vector is not dependent on that curvy path; It just depends on your initial and final position.

The displacement vector can also be defined as the [change in](../Math%20Jargon.md#"Change%20in...") position vectors:

![](Attachments%20-%20Vectors/Pasted%20image%2020231110210612.png)
([source](https://www.google.com/search?q=displacement+vector&tbm=isch&ved=2ahUKEwisjoWej7qCAxV8sicCHeFiBCsQ2-cCegQIABAA&oq=disp&gs_lcp=CgNpbWcQARgAMgQIIxAnMgQIIxAnMgcIABCKBRBDMgcIABCKBRBDMgsIABCABBCxAxCDATIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEOgYIABAIEB46CAgAELEDEIMBOggIABCABBCxAzoKCAAQigUQsQMQQ1DsBFiwCGCSDmgAcAB4AIABnAGIAeMFkgEDMC41mAEAoAEBqgELZ3dzLXdpei1pbWfAAQE&sclient=img&ei=G35OZeyUJ_zknsEP4cWR2AI&bih=923&biw=1920#imgrc=Sm0W1jTIiJDh4M))

Formula:

$$\overrightarrow{AB} = \overrightarrow{OB} - \overrightarrow{OA}$$

or:

$$\nabla \vec{r} = \vec{{r}_{2}} - \vec{{r}_{1}}$$

# Vector Equation of a Line

[source 1](https://www.nagwa.com/en/explainers/350134612051/#:~:text=This%20form%20of%20the,vector%20of%20the%20line.), [source 2](https://youtu.be/hWhs2cIj7Cw?t=1191)

instead of writing the [displacement vector](#Displacement%20Vector) in the "change in position vectors" formula, we can rewrite it in the following equation form:

![](Media-Temp/Pasted%20image%2020231123161524.png)

So again, the math equation will be:

$$ \vec{r}=\vec{r}_0+t\vec{d}$$

Since ⃑𝑟 is dependent on the value of the scalar 𝑡 , we often write this equation as:

$$\vec{r}(t)=\vec{r}_0+t\vec{d}$$

Note that if we have two distinct points 𝐴(𝑥,𝑦) and 𝐵(𝑥,𝑦) on the line, we can find the direction vector ⃑𝑑 by calculating the vector 𝐴𝐵:

# Vector Space (Linear Combination of Vectors)

a vector space is a set whose elements, often called vectors, may be added together and multiplied by numbers called scalars. ([source](https://en.wikipedia.org/wiki/Vector_space))

A **linear combination of vectors** has the same definition of a **vector space**.

Mathematically, it can be defined like this ([source 1](https://textbooks.math.gatech.edu/ila/vectors.html#definition-15), [source 2](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/linear-combinations/v/linear-combinations-and-span)):

Let $c_{1},c_{2},\ldots,c_{k}$ be scalars, and let $v_{1},v_{2},\ldots,v_{k}$ be vectors in $\mathbf{R}^{n}$. The vector in $\mathbf{R}^{n}$ :

$$ c_1\nu_1+c_2\nu_2+\cdots+c_k\nu_k$$

is called a _linear combination_ of the vectors $v_{1},v_{2},\ldots,v_{k}$, with _weights_ or _coefficients_ $c_{1},c_{2},\ldots,c_{k}$.

kindly follow the interactive example at [source 1](https://textbooks.math.gatech.edu/ila/vectors.html#definition-15) to see how **any vector on the plane in $\mathbf{R}^{2}$ can be obtained as a linear combination of $v1,v2$** ***with suitable coefficients***:

![](Media-Temp/Pasted%20image%2020231118134707.png)



# Vector Subspace

[source 1](https://textbooks.math.gatech.edu/ila/subspaces.html#subspaces-defn-of), [source 2](https://brilliant.org/wiki/vector-space/%20%22vector%20space%22), source 3

* A **subspace** is a [vector space](#Vector%20Space%20(Linear%20Combination%20of%20Vectors)) that is entirely contained within another [vector space](https://brilliant.org/wiki/vector-space/ "vector space"). ([source](https://brilliant.org/wiki/subspace/#:~:text=A%20subspace%20is%20a%20vector,4%2C%20C2%2C%20etc.))
* As a subspace is defined _relative_ to its containing space, both are necessary to fully define one; for example, $\mathbf{R}^{2}$ is a subspace of $\mathbf{R}^{3}$, but also of $\mathbf{R}^{4}$, etc.
* In general, A _subspace_ of $\mathbf{R}^{n}$ is a subset $V$ of $\mathbf{R}^{n}$ satisfying ([source](https://textbooks.math.gatech.edu/ila/subspaces.html#subspaces-defn-of)):
	* **_Non-emptiness:_** The zero vector is in V
	* **_Closure under addition:_** If $u$ and $v$ are in $V$, then $u+v$ is also in $V$.
	* **_Closure under scalar multiplication:_** If $v$ is in $V$ and $c$ is in $\mathbf{R}$, then $cv$ is also in $V$.
* Subsets versus Subspaces ([source](https://textbooks.math.gatech.edu/ila/subspaces.html#bluebox-32)):
	* A *subset* of $\mathbf{R}^{n}$ is any collection of vectors whatsoever.
	* Therefore, any subspace is considered a subset, but not vice versa, as some subsets don't satisfy the three conditions of that define a subspace.


# Vector Span

[source](https://textbooks.math.gatech.edu/ila/spans.html#vectors-defn-span)

English definition: 

The _span_ of $v_{1},v_{2},\ldots,v_{k}$ is the collection of all [linear combinations](#Vector%20Space%20(Linear%20Combination%20of%20Vectors)) of $v_{1},v_{2},\ldots,v_{k}$, and is denoted $\mathrm{Span}\{v_1,v_2,\ldots,v_k\}$. 

Mathematical definition:

$$ 
\mathrm{Span}\{v_1,v_2,\ldots,v_{k}\} =
\begin{Bmatrix}
c_{1} v_{1} + c_{2} v_{2} + \cdots + c_{k} v_{k} \;|\; c_1,c_2,\ldots,c_k\;\;\text{in R}
\end{Bmatrix}
$$

We also say that $\mathrm{Span}\{v_1,v_2,\ldots,v_k\}$ is the subset _spanned by_ or _generated by_ the vectors $v_{1},v_{2},\ldots,v_{k}$.

Therefore, 

Drawings of spans ([source](https://textbooks.math.gatech.edu/ila/spans.html#paragraphs-9), I highly suggest checking out their interactive examples for clarification of the drawings below):

![|500](Media-Temp/Pasted%20image%2020231118140740.png)

![](Media-Temp/Pasted%20image%2020231118140819.png)

# Linear Independence

[source 1](https://textbooks.math.gatech.edu/ila/linear-independence.html#subsection-19), [source 2](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/linear-independence/v/linear-algebra-introduction-to-linear-independence)

Why is this concept useful? ([source](https://textbooks.math.gatech.edu/ila/linear-independence.html#p-274)):

One of the reasons for its usefulness is related to vector spans; Sometimes, a vector set could have one or more **redundant vectors** that will not affect the **span** of this set. For example:

![](Media-Temp/Pasted%20image%2020231118155103.png)

The vectors above are *linearly dependent* (explained below); in each of the sub figures, one vector is in the span of the other(s), so *it doesn't make the span bigger*. <mark style="background: #FF5582A6;">Therefore, the concept of linear dependency can help us find if a vector set has redundant vectors or not</mark>.

English definition of linearly (in)dependence:

Given a vector set $\{v_1,v_2,\ldots,v_k\}$ with a linear combination equal to $0$, which is mathematically represented like this:

$$c_{1} v_{1} + c_{2} v_{2} + \cdots + c_{k} v_{k} = 0$$

This vector set is:
* **linearly independent** if **all** the coefficients $c_{1}, c_{2}, \cdots, c_{k}$ are equal to $0$.
* **linearly dependent** otherwise.
	* In other words, linearly dependent if **at least one** coefficient is equal to $0$.

Example 1: 

can the following vector set: 
* be considered linearly independent?
* have a vector span in $\mathbf{R}^{3}$? 

$$ \left\{\begin{bmatrix}1\cr-1\cr2\end{bmatrix},\begin{bmatrix}2\cr1\cr3\end{bmatrix},\begin{bmatrix}-1\cr0\cr2\end{bmatrix}\right\}$$

The [system of equations](https://textbooks.math.gatech.edu/ila/systems-of-eqns.html#p-35) formed from the vector set above is [solved algebraically](https://www.khanacademy.org/test-prep/sat/x0a8c2e5f:untitled-652/x0a8c2e5f:heart-of-algebra-lessons-by-skill/a/gtp--sat-math--article--solving-system-of-linear-equations--lesson) in this [video](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/linear-independence/v/span-and-linear-independence-example).

Other solved examples (using the [determinant row opertations](https://textbooks.math.gatech.edu/ila/determinants-definitions-properties.html#det-defn-the-defn)) are mentioned [here](https://textbooks.math.gatech.edu/ila/linear-independence.html#bluebox-26).

# Vector Set of Collinear Vectors

[source 1](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/linear-algebra-parametric-representations-of-lines), [source 2](https://www.youtube.com/watch?v=PyPp4QvQY3Q)

First, recall the parametric equation form [here](Line%20Equations.md#Parametric%20Equation).

Now, let's define a **vector set** as the following:

$$ S=\left\{c\cdot\vec{r}\;\middle|\;c\in\mathbb{R}\right\}$$

Note: a *vector set* in this case will refer to [Collinear Vectors](#Collinear%20Vectors) that are on the same line only, like the left sub-figures here:

![](Media-Temp/Pasted%20image%2020231116051048.png)

Now, we can create another vector set $L$ whose vectors are collinear to the vectors in $S$ that are NOT on the same line (i.e., the right sub-figures above). The equation for $L$ can be defined as the following:

$$ L=\left\{\vec{x}+t\cdot\vec{r}\;\middle|\;t\in\mathbb{R}\right\}$$

The equation above can help us find a parametric equation form for the [Displacement Vector](#Displacement%20Vector), which had the following vector form:

$$\nabla\vec{r} = \vec{{r}_{2}} - \vec{{r}_{1}}$$

How? Let's deduce this with an example: 

Assume we have the following two [Position Vectors](#Position%20Vector):

$$
\begin{aligned}
\vec{r_{1}}&=
\left[\begin{matrix}{1}\cr{2}\end{matrix}\right] \cr\cr
\vec{r_{2}}&=
\left[\begin{matrix}{4}\cr{2}\end{matrix}\right] \cr\cr
\end{aligned}
$$

Therefore, the displacement vector will be:

$$
\nabla \vec{r} = \left[\begin{matrix}{4}\cr{2}\end{matrix}\right] - \left[\begin{matrix}{1}\cr{2}\end{matrix}\right] = \left[\begin{matrix}{3}\cr{0}\end{matrix}\right]
$$

Now, the vector set $S$ of $\nabla \vec{r}$ can be visualized like this:

![](Media-Temp/Pasted%20image%2020231116064613.png)

But we're not interested in this vector set, we're interested in the vector set $L$ that represents the path from $r_{1}$ to $r_{2}$, so to get this, we evaluate the following expression:

$$\begin{aligned}
L&=\left\{\vec{r_{1}}+t\cdot\nabla\vec{r}\;\middle|\;t\in\mathbb{R}\right\} \cr\cr
L&=\left\{\left[\begin{matrix}{1}\cr{2}\end{matrix}\right]+t\cdot\left[\begin{matrix}{3}\cr{0}\end{matrix}\right]\;\middle|\;t\in\mathbb{R}\right\} \cr\cr
\end{aligned}$$

## Parametric Representation of a Vector Equation

Now, convert the vector set into a parametric equation form like so:

$$\begin{aligned}
x&=1+3t \cr\
y&=2
\end{aligned}$$

But why do we care about constructing a parametric form in the first place?: 

Because now we can obtain any point on the vector set $L$ given a specific "time" $t$. For example, when $t=0$, $(x,y)=(1,2)$. When $t=0.5$, $(x,y)=(2.5,2)$. When $t=1$, $(x,y)=(4,2)$, and so on.

Side note: we can visually represent the vector set $L$ like the red line shown below:

![](Media-Temp/Pasted%20image%2020231116065711.png)


