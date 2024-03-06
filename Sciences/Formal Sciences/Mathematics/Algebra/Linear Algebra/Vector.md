
Main sources:
[khan academy: Unit 1: Vectors and spaces](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces)

# Vector Definition

<mark style="background: #FF5582A6;">It is something that has a magnitude and a direction</mark>.

Technically, we should say "a mathematical object" instead of "something".

It is also called a [Euclidean vector](https://en.wikipedia.org/wiki/Euclidean_vector).

Intuitive example ([source](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/vector-introduction-linear-algebra)):

![](Attachments%20-%20Vector/Pasted%20image%2020231104130417.png)

# Vector Mind Map

[source 1: sites.oxy.edu](https://sites.oxy.edu/ron/math/214/)

![](Attachments%20-%20Vector/Pasted%20image%2020231202143025.png)

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
  
  ![](Attachments%20-%20Vector/Pasted%20image%2020231104160540.png)
  
  Consequently, when we do operations on these vectors, like [adding vectors](#Vector%20Addition), we get a vector like this:
  
  ![](Attachments%20-%20Vector/Pasted%20image%2020231104160832.png)
  
  However, we may move these vectors' starting points (i.e., tails) to easily conceptualize these operations, for example:
  
  ![](Attachments%20-%20Vector/Pasted%20image%2020231104161011.png)
  
  Now the question is the following: "why is it allowed for us to move these vectors' starting points to anywhere we want in the coordinate plane?" 
  
  Answer: Because if we recall the [definition of a vector](#Vector%20Definition), we see that we only care about encoding two pieces of information: **magnitude** and **direction**. Therefore, the actual location of the vector in the plane does not matter.

## Magnitude (i.e., Length) Notation

The notation $\lVert \hat{v} \rVert$ can be read as: "the length (or magnitude) of vector $\hat{v}$".

Regarding [product](#Vector%20Product%20Types) notations ([source: math exchange](https://math.stackexchange.com/questions/1901618/difference-between-multiplication-dot-product-and-cross-product-symbols#:~:text=Often%2C%20the%20exact%20same%20symbol%20is%20used.%20You%20have%20to%20pay%20attention%20to%20context)): You have to pay attention to **context**:
* When you see $x \times y$, then:
	* If $x, y$ _are vectors_, it's [cross product](#Cross%20Product%20(i.e.,%20Vector%20Product)).
	* if $x,y$ _are numbers (i.e., scalars)_, it's multiplication.
* When you see $x \cdot y$, then:
	* If $x, y$ _are vectors_, it's [dot product](#Dot%20Product%20(i.e.,%20Scalar%20Product)).
	* if $x,y$ _are numbers (i.e., scalars)_, it's multiplication.

# Vector Addition

## Triangle Law of Vector Addition

Addition visualization ([interactive source](https://sciencepickleapps.com/VisuallyAddingVectorsV1-0-0/), from [this](https://sciencepickle.com/earth-systems/vectors-and-forces/adding-vectors/)):
![vector-addition](Attachments%20-%20Vector/vector-addition.mp4)

Example: 

$$\vec{v}=\vec{red}+\vec{green}+\vec{blue}=\left[\begin{array}{c}{-9}\cr{3}\end{array}\right]+\left[\begin{array}{c}{2}\cr{3}\end{array}\right]+\left[\begin{array}{c}{2}\cr{0.2}\end{array}\right]=\left[\begin{array}{c}{-5}\cr{6.2}\end{array}\right]$$

Note: If the example above adds 2 vectors only, then the method of addition above is called [the triangle law of vector addition](https://byjus.com/physics/triangle-law-of-vector-addition/#:~:text=Triangle%20law%20of%20vector%20addition%20states%20that%20when%20two%20vectors,direction%20of%20the%20resultant%20vector.).

## Parallelogram Law of Vector Addition

[source](https://www.khanacademy.org/math/precalculus/x9e81a4f98389efdf:vectors/x9e81a4f98389efdf:vector-add-sub/v/parallelogram-rule-for-vector-addition#:~:text=The%20parallelogram%20rule%20says%20that,same%20point%20as%20the%20vectors.)

The parallelogram rule says that if we place two vectors so they have the same initial point, and then complete the vectors into a parallelogram, then ***the sum of the vectors is the directed diagonal*** that starts at the same point as the vectors.

Example:

step 1:

![](Attachments%20-%20Vector/Pasted%20image%2020231110175351.png)

step 2:

![](Attachments%20-%20Vector/Pasted%20image%2020231110175424.png)

step 3: start from step 1, then move a to b instead:

![](Attachments%20-%20Vector/Pasted%20image%2020231110175522.png)

step 4: merge steps 2 and 3:

![](Attachments%20-%20Vector/Pasted%20image%2020231110175612.png)

Step 5: draw the diagonal (which is the result of a + b):

![](Attachments%20-%20Vector/Pasted%20image%2020231110180525.png)

# Vector Subtraction

Suppose you have these two vectors:

![](Attachments%20-%20Vector/Pasted%20image%2020231104155811.png)
(Adapted from [here](https://www.google.com/search?q=vector+subtraction&sca_esv=579447376&tbm=isch&sxsrf=AM9HkKnGtLJ6VqlC3AJLr_SJv37CNWgI9w:1699105968608&source=lnms&sa=X&ved=2ahUKEwix5sb9vqqCAxW_UKQEHatZBbEQ_AUoAXoECAQQAw&biw=1920&bih=911&dpr=1#vhid=V5qJxTe7D4HnZM&vssid=3981:1DaQEkvNT6JBSM))

Now, what if we want to subtract B from A? (i.e., A - B)?

Mathematical example:

$$A-B=\left[\begin{array}{c}{3}\cr{5}\end{array}\right]-\left[\begin{array}{c}{4}\cr{2}\end{array}\right]=\left[\begin{array}{c}{-1}\cr{3}\end{array}\right]$$

Now, this vector can be represented like this:

![](Attachments%20-%20Vector/Pasted%20image%2020231104162015.png)

Now, to intuitively grasp how subtraction works geometrically, there are two methods of moving the vector $A-B$:

* Method 1 ([source](https://www.onlinemathlearning.com/vector-subtraction.html)):
  
  ![](Attachments%20-%20Vector/Pasted%20image%2020231104162158.png)
  
  Applying this on the previous example:
  
  ![](Attachments%20-%20Vector/Pasted%20image%2020231104162448.png)
  
  So it's as if we're [adding](#Vector%20Addition) $A$ to $-B$ to get the emerged vector $A-B$:  
  
  ![](Attachments%20-%20Vector/Pasted%20image%2020231104162559.png)
  
  Final image which contains all of the previous images' steps:
  
  ![](Attachments%20-%20Vector/Pasted%20image%2020231104162712.png)
  
	* Side note: this method (i.e., a + (-b)) is used as a first step in subtracting vectors using the [Parallelogram Rule of Adding Vectors](#Parallelogram%20Law%20of%20Vector%20Addition) ([detailed video](https://www.khanacademy.org/math/precalculus/x9e81a4f98389efdf:vectors/x9e81a4f98389efdf:vector-add-sub/v/subtracting-vectors-with-parallelogram-rule))
	  
* Method 2: 
  
  Starting from this image:
  
  ![](Attachments%20-%20Vector/Pasted%20image%2020231104162015.png)
  
  Simply move the vector $A-B$ to be between $A$ and $B$:
  
  ![](Attachments%20-%20Vector/Pasted%20image%2020231104163010.png)
  
  Why is this logical? First, recall how we visualize [vector addition](#Vector%20Addition), then, recognize that what we're doing above is simply: $A=B+(A-B)$, so it's as if the vector $A$ emerged like the image above due to adding $B$ to $A-B$.
	* Side note: this method gives the same visual result as the one in the [Triangle Law of Vector Addition](#Triangle%20Law%20of%20Vector%20Addition).

### Vector Subtraction Visual summary

![](Attachments%20-%20Vector/Pasted%20image%2020231104163904.png)

# Vector Product Types

[source 1: Wikipedia](<https://en.wikipedia.org/wiki/Product_(mathematics)#Products_in_linear_algebra>)

* In mathematics, a product is the result of a multiplication of factors.
* In linear algebra, there exists many different kinds of products. Some of these types include:
	* Scalar multiplication
	* Dot (scalar) product
	* Cross product

## Vector Scalar Multiplication

Multiplication visualization ([source](https://makeagif.com/gif/vector-multiplication-by-scalar-G4qCVh)):
![vector-scalar-multiplication](Attachments%20-%20Vector/vector-scalar-multiplication.gif)

Formula of a scalar-multiplied vector: $c \cdot \vec v$

Formula of a scalar-multiplied vector's length (i.e., magnitude): $||c\cdot \vec v||=|c|\cdot ||\vec v||$. Noting that the formula to get the vector's length (i.e., $||\vec v||$) is mentioned in the dot product's [Vector Length Formula](#Vector%20Length%20Formula) section.


To get the reverse direction of a vector, add 180 to its direction.

Example ([source](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/e/scaling_vectors)):

![](Attachments%20-%20Vector/Pasted%20image%2020231104110053.png)

Answer:

![](Attachments%20-%20Vector/Pasted%20image%2020231104112518.png)

![](Attachments%20-%20Vector/Pasted%20image%2020231104112617.png)

## Dot Product (i.e., Scalar Product)

[source 1: gatech](https://textbooks.math.gatech.edu/ila/dot-product.html), [source 2: KA article](https://www.khanacademy.org/math/multivariable-calculus/thinking-about-multivariable-function/x786f2022:vectors-and-matrices/a/dot-products-mvc), [source 3 (amazing): Looking Glass Universe's YT video](https://www.youtube.com/watch?v=BcxfxvYCL1g), [source 4: KA video](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/dot-cross-products/v/vector-dot-product-and-vector-length)

***Important note***: even though [dot product](#Dot%20Product%20(i.e.,%20Scalar%20Product)) and [cross product](#Cross%20Product%20(i.e.,%20Vector%20Product)) sub sections are mentioned here (under [Vector Product Types](#Vector%20Product%20Types) section), ***I highly recommend understanding the other sections*** (until [Basis of a Subspace](#Basis%20of%20a%20Subspace) section) ***and then coming back to these 2 sub sections***. Specifically, these sections:
* [Unit Vector (UV)](#Unit%20Vector%20(UV))
* TODO

### Dot Product Intuitive Definition

* <mark style="background: #FF5582A6;">The dot product is a fundamental way to combine two vectors</mark>. ([source: KA article](https://www.khanacademy.org/math/multivariable-calculus/thinking-about-multivariable-function/x786f2022:vectors-and-matrices/a/dot-products-mvc#:~:text=The%20dot%20product%20is%20a%20fundamental%20way%20we%20can%20combine%20two%20vectors.%20Intuitively%2C%20it%20tells%20us%20something%20about%20how%20much%20two%20vectors%20point%20in%20the%20same%20direction.))
* Intuitively, it tells us something about <mark style="background: #FF5582A6;">how much two vectors point in the same direction</mark>.
* It is an operation which answers the following question:
	* "How much does one of these vectors overlap with the other?" ([source: LGU's YT video; 00:53](https://youtu.be/BcxfxvYCL1g?t=53))

Now, other intuitive definitions can be understood once we establish the following conceptual idea: 
* When comparing two vectors "a" and "b", we can define "a" as: 
	* *a bit in the same direction of "b"* **added to** *a bit that's perpendicular to "b"* ([source: 1:00 to 1:50](https://youtu.be/BcxfxvYCL1g?t=56))
	* Visualization:
	  
	  ![](Attachments%20-%20Vector/Pasted%20image%2020231226074819.png)
	  
* Now, here's a GIF visualization of how that "x" part decreases as the angle between "a" and "b" increases:
  
  ![dot-product-int-def-1](Attachments%20-%20Vector/dot-product-int-def-1.gif)
  
* Note that this "x" part will become negative once the angle between them is greater than 90°.

Applications of the dot product are mentioned in [Dot Product Use Cases](#Dot%20Product%20Use%20Cases) section.

### Dot Product Definition and Properties

The _dot product_ of two vectors $x,y$ in $\mathbf{R}^{n}$ is a scalar $c$, such that:

$$ x\cdot y=\begin{pmatrix}x_1 \cr x_2 \cr\vdots \cr x_n\end{pmatrix}\cdot\begin{pmatrix}y_1 \cr y_2 \cr \vdots \cr y_n\end{pmatrix} = x_1y_1+x_2y_2+\cdots+x_ny_n = c$$

Side note: Thinking of $x,y$ as [column vectors](#Row%20and%20Column%20Vectors), this is the same as $x^T y$.

Properties of the Dot Product: 

Let $x,y,z$ be vectors in Rn and let $c$ be a scalar. Then:
1. _Commutativity:_ $x \cdot y = y \cdot x$.
2. _Distributivity with addition:_ $(x+y) \cdot z=x \cdot z+y \cdot z$.
3. _Distributivity with scalar multiplication:_ $(cx) \cdot y=c(x \cdot y)$.


### Dot Product Use Cases

After understanding the [intuitive definitions of dot product](#Dot%20Product%20Intuitive%20Definition), here are some of its applications:

Use case 1:  Dot product is used to:
* Measure the angles between vectors.
* Compute the length of a vector $\lVert \hat{v} \rVert$.
	* Side note: the [Unit Vector (UV)](#Unit%20Vector%20(UV)) formula uses the [Vector Length](#Vector%20Length), so the dot product also helps in calculating the unit vector.

Use case 2 (which relies on use case 1): Dot product is used to find the closest point $z$ on a [subspace](#Basis%20of%20a%20Subspace) $V$ to a given point $x$, like so:

![](Attachments%20-%20Vector/Pasted%20image%2020231216033600.png)

If you try to visualize different $x$ points outside of $V$ and their corresponding $z$ points inside of $V$, you'll notice that the ***two points are always orthogonal (or perpendicular) to the subspace***. Other visualizations that shows different $x, z$ points: ([source 1](https://www.google.com/search?sca_esv=591385191&sxsrf=AM9HkKmo3v3dTUiCoPIhw5l1OgfGhpoGJg:1702690640799&q=visualizing+orthogonality+between+a+point+and+a+vector+subspace&tbm=isch&source=lnms&sa=X&ved=2ahUKEwiSlbr26JKDAxUjQ6QEHR16DXAQ0pQJegQICBAB&biw=1920&bih=911&dpr=1#vhid=g6SoGh16yZz-WM&vssid=3981:4waPAfA0SI_VvM), [source 2](https://www.researchgate.net/publication/220419352_Proactive_Threshold_Cryptosystem_for_EPC_Tags/figures?lo=1))

![](Attachments%20-%20Vector/Pasted%20image%2020231216034755.png) ![](Attachments%20-%20Vector/Pasted%20image%2020231216034824.png)

### Vector Length

#### Vector Length Intuition

Suppose you have a [position vector](#Position%20Vector) $\begin{pmatrix}3 \cr 4\end{pmatrix}$ in $\mathbf{R}^{2}$. Then, we can easily calculate the length of this vector using Pythagorean theorem:

$$ \lVert x \rVert= \left\lVert\begin{pmatrix}x_1 \cr x_2\end{pmatrix}\right\rVert = \sqrt{x_1^2+x_2^2} = \sqrt{3^2+4^2}=5$$

Visualization:

![](Attachments%20-%20Vector/Pasted%20image%2020231216045140.png)

<mark style="background: #FFF3A3A6;">Note that the length of a vector is the length of the arrow; if we think in terms of points, then the length is its distance from the origin</mark>.

Great, but what if we have $\mathbf{R}^{n}$ instead of $\mathbf{R}^{2}$ ? Then, the equation above will just be expanded; this is shown in the next [sub-section](#Vector%20Length%20Formula).

#### Vector Length Formula

<mark style="background: #FF5582A6;">Fact 1.1</mark>: The _length_ of a vector $x$ in $R^n$ is the number:

$$||x||=\sqrt{x\cdot x}=\sqrt{x_1^2+x_2^2+\cdots+x_n^2}$$

Why? Because the dot product of a vector with itself (i.e., self-dot product):

$$ x\cdot x = \begin{pmatrix}x_1 \cr x_2 \cr \vdots \cr x_n\end{pmatrix}\cdot\begin{pmatrix}x_1 \cr x_2 \cr \vdots \cr x_n\end{pmatrix}=x_1^2+x_2^2+\cdots+x_n^2 
$$

Squaring both sides of fact 1.1, we get <mark style="background: #FF5582A6;">fact 1.2</mark>:

$$||x||^2 = x\cdot x = \left(\sqrt{x_{1}^{2}+x_{2}^{2}+\ldots+x_{n}^{2}}\right)^{2}$$

Therefore, the most important 3 statements of this section (which are equivalent to each other):
* <mark style="background: #FF5582A6;">The length of a vector is the square root of its self-dot product</mark>.
	* Fact 1.1
* <mark style="background: #FF5582A6;">The squared length of a vector is its self-dot product</mark>.
	* Fact 1.2
* There's no such thing called "self-dot product". It's just a term I made up :]. It should be "dot product with itself" instead.

Fact 2: If $x$ is a vector and $c$ is a scalar, then $||c\cdot x||=|c|\cdot ||x||$. This is also mentioned in [Vector Scalar Multiplication](#Vector%20Scalar%20Multiplication) section. Unfortunately, I find difficulty translating this fact into English, but hopefully the mathematical example below will help you understand why the fact is accurate:

$$\begin{aligned}
||c\cdot x|| &= \left\lVert -2 \cdot \begin{pmatrix} 3 \cr 4 \end{pmatrix} \right\rVert \cr &= \sqrt{4(-3)^2+4(-4)^2} \cr &= \sqrt{36+64} = 10 \end{aligned}$$

Now, let's solve the same example using fact 2:

$$\begin{aligned}
||c\cdot x|| = |c|\cdot ||x|| &= 2 \left\lVert \begin{pmatrix} 3 \cr 4 \end{pmatrix} \right\rVert \cr &= 2\sqrt{(-3)^2+(-4)^2} \cr &= 2\sqrt{9+16} = 10 \end{aligned}$$


#### Vector Length Exercises

[Source 1: example below the highlighted paragraph](https://textbooks.math.gatech.edu/ila/dot-product.html#p-1399) 

Example 1: Suppose that $x=\begin{pmatrix}3 \cr 4\end{pmatrix}$, $y=\begin{pmatrix}-3 \cr -4\end{pmatrix}$. What is $\lVert 2x+3y \rVert$?

Solution: Using [vector addition](#Vector%20Addition) and [fact 1.1 of vector length formula](#Vector%20Length%20Formula):

$$\begin{aligned}\lVert 2x+3y \rVert &= 
\left\lVert 
\begin{pmatrix}6 \cr 8\end{pmatrix}
+
\begin{pmatrix}-9 \cr -12\end{pmatrix}
\right\rVert \cr &= \left\lVert \begin{pmatrix} -3 \cr -4\end{pmatrix} \right\rVert
\cr &= \sqrt{(-3)^2+(-4)^2}\cr &=5\end{aligned}$$

Example 2: Suppose that $\lVert x \rVert=2$, $\lVert y \rVert=3$, and $x \cdot y=-4$. What is $\lVert 2x+3y \rVert$?

Solution: from [fact 1.2](#Vector%20Length%20Formula), we can compute the term as follows:

$$ \begin{aligned}\lVert2x+3y\rVert^2&=(2x+3y)\cdot(2x+3y)\cr&=4x\cdot x+6x\cdot y+6x\cdot y+9y\cdot y\cr&=4\lVert x\rVert^2+9\lVert y\rVert^2+12x\cdot y\cr&=4\cdot4+9\cdot9-12\cdot4=49.\end{aligned}$$


Another example of calculating the vector length is shown in [Exercise Explanation of The UV Formula](#Exercise%20Explanation%20of%20The%20UV%20Formula) sub-section.

### Distance between Points

[source 1: 6.1 in gatech's textbook](https://textbooks.math.gatech.edu/ila/dot-product.html#p-1405)

Mandatory prerequisites:
* Understand that in general ([source 1: BYJU's](https://byjus.com/physics/difference-between-distance-and-displacement/#:~:text=The%20complete%20length%20of%20the,the%20minimum%20path%20between%20them.&text=To%20calculate%20distance%2C%20the%20direction%20is%20not%20considered.), [source 2: KA](https://www.khanacademy.org/science/mechanics-essentials/xafb2c8d81b6e70e3:how-to-analyze-car-crashes-using-skid-mark-analysis/xafb2c8d81b6e70e3:turning-a-race-into-a-snapshot/a/relative-motion-review-article#:~:text=Distance%20is%20the%20length%20of%20the%20path%20taken%20by%20an,and%20where%20it%20ended%20up.)):
	* Distance is the **complete length** of the path between any two points. 
	* Displacement is the **direct length** between any two points when measured along the minimum path between them.
* Understand that in Linear Algebra, specifically between vectors, **a lot** of articles will use the term "distance", when they are actually referring to "displacement", including this sub-section :].
	* Interchanging the two words is technically correct ONLY IF the **actual path** between two points/vectors was the **minimum path**.
		* Then the distance between these two points/vectors will be the same as their displacement.
	* So, we'll always make the assumption that **actual path = minimum path**, unless explicitly mentioned otherwise, and will therefore use the term "distance" instead of "displacement". 

Optional prerequisites:
* Understand that a "point" on the coordinate plane is essentially a [Position Vector](#Position%20Vector).
* Understand that a [Displacement Vector](#Displacement%20Vector) is essentially the difference between two position vectors.

Now, a <mark style="background: #FF5582A6;">definition</mark>: The **distance** between two points $x$ and $y$ in $\mathbb{R}^n$ is the length of the vector from $x$ to $y$:

$$ \operatorname{dist}(x,y)=\|y-x\|.$$

### Orthogonal and Perpendicular Vectors

[source 1: 6.1 in gatech's textbook](https://textbooks.math.gatech.edu/ila/dot-product.html#subsection-69)

Definition: Two vectors $x,y$ in $\mathbb{R}$ are _orthogonal_ and perpendicular* if $x \cdot y=0$.

\*Caveat: check [this](https://math.stackexchange.com/questions/2406260/difference-between-perpendicular-orthogonal-and-normal#:~:text=In%20linear%20algebra%2C%20%22perpendicular%22%20is%20mentioned%20for%20non%20zero%20vectors%20whereas%20%22orthogonality%22%20is%20for%20zero%20and%20non%20zero%20vectors.%20We%20say%20a%20zero%20vector%20is%20orthogonal%20to%20some%20vector%2C%20not%20perpendicular.%20%22Normal%22%20is%20perpendicular%20to%20every%20vector%20on%20the%20plane) answer to understand the difference between "orthogonal", "perpendicular", and "normal", and [this](https://allthedifferences.com/whats-the-difference-between-orthogonal-normal-and-perpendicular-when-dealing-with-vectors/) article for in-depth differences. however, most of the time, the terms are interchanged.

Notation: $x \perp y$ means $x \cdot y = 0$.

Note: Since $0 \cdot x = 0$ for any vector $x$, ***the zero vector is orthogonal to every vector*** in $\mathbb{R}^n$.

Recap: if we have this triangle of vector lengths:

![](Attachments%20-%20Vector/Pasted%20image%2020231216093727.png)

Then, if $x \perp y$, we'll have $\alpha=90\degree$. Therefore, the Pythagorean theorem can be applied, leaving us with this summary:

$$ x\perp y\quad\Longleftrightarrow\quad x\cdot y=0\quad\Longleftrightarrow\quad||y-x||^2=||x||^2+||y||^2$$

The motivation behind the summary above is the usage of the law of cosines in $\mathbb{R}^2$:

$$ ||y-x||^2=||x||^2+\|y\|^2-2||x||\,||y||\cos\alpha$$

In particular, when the conditions below become true:

$$\alpha=90\degree \Longleftrightarrow \cos(\alpha)=0 \Longleftrightarrow ||y-x||^2=||x||^2+||y||^2$$

Then, we will have the following algebraic motivation:

$$ \begin{aligned}x\text{ and }y \text{ are perpendicular}&\Longleftrightarrow||x||^2+||y||^2=||y-x||^2\cr&\Longleftrightarrow x\cdot x+y\cdot y=(y-x)\cdot(y-x)\cr&\Longleftrightarrow x\cdot x+y\cdot y=y\cdot y+x\cdot x-2x\cdot y\cr&\Longleftrightarrow x\cdot y=0.\end{aligned}$$

I highly suggest trying to solve the advanced exercises [here](https://textbooks.math.gatech.edu/ila/dot-product.html#bluebox-86). Note, mandatory prerequisites to solve them:
* [Systems of Linear Equations](https://textbooks.math.gatech.edu/ila/systems-of-eqns.html)
	* Which includes an important [section](https://textbooks.math.gatech.edu/ila/systems-of-eqns.html#subsection-3) that talks about [Parametric Representation of a Vector Equation](#Parametric%20Representation%20of%20a%20Vector%20Equation)
* [Row Reduced Echelon Form (RREF) of a Matrix and its steps](https://textbooks.math.gatech.edu/ila/row-reduction.html)
* [Span of a Vector Set (Vector Span)](#Span%20of%20a%20Vector%20Set%20(Vector%20Span))
* TODO: understand how the first example referenced above is solved and explain it here.

TODO: other sections that will lead to vector and scalar projection sections.

## Projection of Vectors

main sources:
* [the meaning of the dot product YT video](https://www.youtube.com/watch?v=BcxfxvYCL1g)
* [Projection of Vectors article](https://emedia.rmit.edu.au/learninglab/content/v5-projection-vectors)
* [The main math stack exchange answer](https://math.stackexchange.com/questions/3919139/why-do-we-divide-by-the-length-squared-when-projecting-a-vector#:~:text=I%20think%20there%27s%20a%20misunderstanding%20of%20the%20dot%20product) to "Why do we divide by the length squared when projecting a vector?" post
	* Side note: you can view this answer simultaneously with the above article.

TODO: write here from the sources above

## Cross Product (i.e., Vector Product)



# Vector Forms

[KA source](https://www.khanacademy.org/math/algebra-home/alg-vectors/alg-magnitude-direction/a/vector-forms-review)

Different vector forms:

![](Attachments%20-%20Vector/Pasted%20image%2020231110203104.png)

![](Attachments%20-%20Vector/Pasted%20image%2020231110203317.png)


# Vector Types

[Useful source](https://byjus.com/maths/types-of-vectors/)

## Unit Vector (UV)

[source](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/intro-unit-vector-notation)

### Standard Coordinate Vectors Definition

Definition: 
* <mark style="background: #FF5582A6;">A vector that has a magnitude of 1 is a unit vector.</mark>
* It is also known as Direction Vector.

Specifically, in cartesian coordinates, <mark style="background: #FF5582A6;">special, coordinate unit vectors along the axis are denoted by i and j respectively</mark>. Their formulae (in $\mathbb{R}^2$):

$$\begin{aligned}
\hat{i}&=
\left[\begin{matrix}{1}\cr{0}\cr\end{matrix}\right] \cr\cr
\hat{j}&=
\left[\begin{matrix}{0}\cr{1}\cr\end{matrix}\right]
\end{aligned}$$

Visualization:

![](Attachments%20-%20Vector/Pasted%20image%2020231106155417.png)
([source](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/intro-unit-vector-notation))

These vectors can be generalized to more dimensions. For example, in $\mathbb{R}^3$, we have the following *standard coordinate vectors*:


$$\begin{aligned}
\hat{i}&=
\left[\begin{matrix}{1}\cr{0}\cr{0}\cr\end{matrix}\right] \cr\cr
\hat{j}&=
\left[\begin{matrix}{0}\cr{1}\cr{0}\cr\end{matrix}\right] \cr\cr
\hat{k}&=
\left[\begin{matrix}{0}\cr{0}\cr{1}\cr\end{matrix}\right] \cr\cr
\end{aligned}$$


### General UVs Definition

If a vector $\vec{v}$ is not a [coordinate vector](#Standard%20Coordinate%20Vectors%20Definition), then it's a general unit vector, and is denoted by $\left|\left|\vec{v}\right|\right|$. 

Visualization:
![](Attachments%20-%20Vector/Pasted%20image%2020231107092101.png)


and its equation:

$$\hat{u}=\frac{\vec{v}}{\left|\left|\vec{v}\right|\right|}$$

such that:

$$||\hat{u}||=1$$

where:

$\hat{u}$ = normalized vector (i.e., unit vector)
$\vec{v}$ = non-zero vector
$\left|\left|\vec{u}\right|\right|$ = norm (or length) of $\vec{u}$, which is equal to 1, since it is a "unit" vector.
$\left|\left|\vec{v}\right|\right|$ = norm (or length) of $\vec{v}$

Important note: [based on](#Vector%20Length%20Formula) the [dot product](#Dot%20Product%20(i.e.,%20Scalar%20Product)) operation, we can extend the above unit vector definition like this:

$$||\hat{u}||=\sqrt{\hat{u} \cdot \hat{u}}=1$$

### Exercise Explanation of The UV Formula

[source](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/e/unit-vector)

Important note: To understand how the length of a vector (i.e., $\left|\left|\vec{v}\right|\right|$) is calculated, kindly check out the [dot product](#Dot%20Product%20(i.e.,%20Scalar%20Product)) section.

![](Attachments%20-%20Vector/Pasted%20image%2020231110171537.png)

![](Attachments%20-%20Vector/Pasted%20image%2020231110171639.png)

Making sure that this unit vector has a magnitude of 1:

![](Attachments%20-%20Vector/Pasted%20image%2020231110174904.png)

Visualizing the answer:

![](Attachments%20-%20Vector/Pasted%20image%2020231110174941.png)

### Intuitive Explanation of The UV Formula

From [vector scalar multiplication](#Vector%20Scalar%20Multiplication) rule, we have $c \cdot \hat u = \vec v$ 

dividing both sides by $c$:

$$\hat{u}=\frac{\vec{v}}{c}=\frac{\vec{v}}{\left|\left|\vec{v}\right|\right|}$$

Such that $c$ must be equal to $\left|\left|\vec{v}\right|\right|$ in order to get a vector $\hat{u}$ of a unit length equal to1.

Essentially, we're saying that:
* vector multiplication formula: multiply a scalar by a small vector to get a big vector
* unit vector formula: divide a big vector by a scalar to get a small vector
	* the "small vector" here has to have a magnitude of  1 (i.e., unit vector)


## Collinear Vectors

Definition ([source](https://unacademy.com/content/jee/study-material/mathematics/all-about-collinear-vectors/#:~:text=Whenever%20any%20two%20provided%20vectors,or%20parallel%20to%20one%20another.)):
* Two (or more) vectors are said to be collinear if they are parallel to each other.
* Examples:
  
  ![](Attachments%20-%20Vector/Pasted%20image%2020231110194740.png)

## Position Vector

[source 1](https://www.physicsread.com/displacement-vector/#:~:text=And%20when%20the%20position%20of%20a%20point%20is%20represented%20in%20vector%20form%2C%20it%20is%20called%20a%20position%20vector.), [source 2](https://www.nagwa.com/en/explainers/505138303596/), [source 3](https://byjus.com/physics/position-and-displacement-vectors/#what-is-a-position-vector), [KA video explanation](https://www.khanacademy.org/math/ap-calculus-bc/bc-advanced-functions-new/bc-9-4/v/position-vector-valued-functions)

Definition: It is the position of a point when it is represented in a vector form:
  
![](Attachments%20-%20Vector/Pasted%20image%2020231110205330.png)

([source](https://www.google.com/search?q=position+vector+vs+non+position+vector&tbm=isch&ved=2ahUKEwifteSbjLqCAxXpmCcCHeaVBH0Q2-cCegQIABAA&oq=position+vector+vs+non+position+vector&gs_lcp=CgNpbWcQAzoECCMQJ1DKCFi8H2D8H2gCcAB4AIABzAGIAfUWkgEGMC4xOS4ymAEAoAEBqgELZ3dzLXdpei1pbWfAAQE&sclient=img&ei=8XpOZd_4JOmxnsEP5quS6Ac&bih=923&biw=1920&hl=en#vhid=MR7wlvEObohfDM&vssid=3981:11csnMkTDlQ9jM))

noting that $\vec O$ always signifies that the start of the vector is the origin point $(0,0)$.


## Displacement Vector

[source](https://www.physicsread.com/displacement-vector/)

For example, you traveled from point **A** to point **B**. And if you look at your journey path, you will see that your total displacement is **AB**:

![](Attachments%20-%20Vector/Pasted%20image%2020231110204352.png)

And if you express this displacement in vector form, it is called displacement vector:

$$ \vec{s}=\overrightarrow{AB}$$

this displacement vector is not dependent on that curvy path; It just depends on your initial and final position.

The displacement vector can also be defined as the [change in](../../Math%20Jargon.md#"Change%20in...") position vectors:

![](Attachments%20-%20Vector/Pasted%20image%2020231110210612.png)
([source](https://www.google.com/search?q=displacement+vector&tbm=isch&ved=2ahUKEwisjoWej7qCAxV8sicCHeFiBCsQ2-cCegQIABAA&oq=disp&gs_lcp=CgNpbWcQARgAMgQIIxAnMgQIIxAnMgcIABCKBRBDMgcIABCKBRBDMgsIABCABBCxAxCDATIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEOgYIABAIEB46CAgAELEDEIMBOggIABCABBCxAzoKCAAQigUQsQMQQ1DsBFiwCGCSDmgAcAB4AIABnAGIAeMFkgEDMC41mAEAoAEBqgELZ3dzLXdpei1pbWfAAQE&sclient=img&ei=G35OZeyUJ_zknsEP4cWR2AI&bih=923&biw=1920#imgrc=Sm0W1jTIiJDh4M))

Formula:

$$\overrightarrow{AB} = \overrightarrow{OB} - \overrightarrow{OA}$$

or:

$$\nabla \vec{r} = \vec{r}_2 - \vec{r}_1$$

## Row and Column Vectors

[source 1: 2.3 Matrix equations in gatech's textbook](https://textbooks.math.gatech.edu/ila/matrix-equations.html#matrixeq-row-column-prod)

A row vector $x$ is a matrix with one row and $n$ columns.

A column vector $y$ is a matrix with $n$ rows and 1 column.

The product (i.e., [dot product](#Dot%20Product%20(i.e.,%20Scalar%20Product))) of $x$ and $y$ is a scalar $c$ such that:

$$ x \cdot y = x^T y =  \begin{pmatrix}x_1&x_2&\cdots&x_n\end{pmatrix}\begin{pmatrix}y_1 \cr y_2 \cr \vdots \cr y_n\end{pmatrix} = x_1y_1+x_2y_2+\cdots+x_ny_n = c
$$

Note: If you don't understand $x^T y$, kindly check the definition of the transpose operation [here](https://textbooks.math.gatech.edu/ila/determinants-definitions-properties.html#definition-42), and the row-column rule for matrix multiplication [here](https://textbooks.math.gatech.edu/ila/matrix-multiplication.html#matrix-mult-row-column), then notice how we need to apply the transpose operation to make the column vector $x$ a row vector, so that the matrix multiplication rule can be applied.

### The Column Vector Assumption

In most text books (or other resources), whenever a vector $v$ is mentioned, it is often implicitly defined as a [column vector](#Row%20and%20Column%20Vectors), unless explicitly defined as a [row vector](#Row%20and%20Column%20Vectors). Either way, you should deduce the definition from the context of the resource you're reading.

# Vector Equation of a Line

[source 1](https://www.nagwa.com/en/explainers/350134612051/#:~:text=This%20form%20of%20the,vector%20of%20the%20line.), [source 2](https://youtu.be/hWhs2cIj7Cw?t=1191)

instead of writing the [displacement vector](#Displacement%20Vector) in the "change in position vectors" formula, we can rewrite it in the following equation form:

![](Attachments%20-%20Vector/Pasted%20image%2020231123161524.png)

So again, the math equation will be:

$$ \vec{r}=\vec{r}_0+t\vec{d}$$

Since ⃑𝑟 is dependent on the value of the scalar 𝑡 , we often write this equation as:

$$\vec{r}(t)=\vec{r}_0+t\vec{d}$$

Note that if we have two distinct points $A (x_1,y_1)$ and $B (x_2,y_2)$ on the line, we can find the direction vector $\vec{d}$ by calculating the vector $AB$:

$$\overrightarrow{AB} = (x_2 - x_1 \;,\; y_2 - y_1)$$

Read additional notes [here](https://www.nagwa.com/en/explainers/350134612051/#:~:text=of%20this%20explainer.-,Key%20Points,-The%20position%20vector).

# Vector Set of Collinear Vectors

[source 1](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/linear-algebra-parametric-representations-of-lines), [source 2](https://www.youtube.com/watch?v=PyPp4QvQY3Q)

First, recall the parametric equation form [here](Algebraic%20Equations.md#Parametric%20Equation).

Now, let's define a **vector set** as the following:

$$ S=\left\lbrace c \cdot \vec{r} \; \middle| \; c \in \mathbb{R} \right\rbrace$$

Note: a *vector set* in this case will refer to [Collinear Vectors](#Collinear%20Vectors) that are on the same line only, like the left sub-figures here:

![](Attachments%20-%20Vector/Pasted%20image%2020231116051048.png)

Now, we can create another vector set $L$ whose vectors are collinear to the vectors in $S$ that are NOT on the same line (i.e., the right sub-figures above). The equation for $L$ can be defined as the following:

$$ L=\left\lbrace\vec{x}+t\cdot\vec{r}\;\middle|\;t\in\mathbb{R}\right\rbrace$$

The equation above can help us find a parametric equation form for the [Displacement Vector](#Displacement%20Vector), which had the following vector form:

$$\nabla \vec{r} = \vec{r}_2 - \vec{r}_1$$

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

![](Attachments%20-%20Vector/Pasted%20image%2020231116064613.png)

But we're not interested in this vector set, we're interested in the vector set $L$ that represents the path from $r_{1}$ to $r_{2}$, so to get this, we evaluate the following expression:

$$ \begin{aligned}
L&=\left\lbrace\vec{r_{1}}+t\cdot\nabla\vec{r}\;\middle|\;t\in\mathbb{R}\right\rbrace \cr\cr
L&=\left\lbrace\left[\begin{matrix}{1}\cr{2}\end{matrix}\right]+t\cdot\left[\begin{matrix}{3}\cr{0}\end{matrix}\right]\;\middle|\;t\in\mathbb{R}\right\rbrace \cr\cr
\end{aligned}$$

## Parametric Representation of a Vector Equation

A vector set $L$:

$$L=\left\lbrace\left[\begin{matrix}{1}\cr{2}\end{matrix}\right]+t\cdot\left[\begin{matrix}{3}\cr{0}\end{matrix}\right]\;\middle|\;t\in\mathbb{R}\right\rbrace$$

can be converted into a parametric equation form like so:

$$\begin{aligned}
x&=1+3t \cr\
y&=2
\end{aligned}$$

But why do we care about constructing a parametric form in the first place?: 

Because now we can obtain any point on the vector set $L$ given a specific "time" $t$. For example, when $t=0$, $(x,y)=(1,2)$. When $t=0.5$, $(x,y)=(2.5,2)$. When $t=1$, $(x,y)=(4,2)$, and so on.

Side note: we can visually represent the vector set $L$ like the red line shown below:

![](Attachments%20-%20Vector/Pasted%20image%2020231116065711.png)



# Vector Space (Linear Combination of Vectors)

a vector space is a set whose elements, often called vectors, may be added together and multiplied by numbers called scalars. ([source](https://en.wikipedia.org/wiki/Vector_space))

A **linear combination of vectors** has the same definition of a **vector space**.

Mathematically, it can be defined like this ([source 1](https://textbooks.math.gatech.edu/ila/vectors.html#definition-15), [source 2](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/linear-combinations/v/linear-combinations-and-span)):

Let $c_1,c_2,\ldots,c_k$ be scalars, and let $v_1,v_2,\ldots,v_k$ be vectors in $\mathbf{R}^n$. The vector in $\mathbf{R}^{n}$ :

$$ c_1\nu_1+c_2\nu_2+\cdots+c_k\nu_k$$

is called a _linear combination_ of the vectors $v_1,v_2,\ldots,v_k$, with _weights_ or _coefficients_ $c_1,c_2,\ldots,c_k$.

kindly follow the interactive example at [source 1](https://textbooks.math.gatech.edu/ila/vectors.html#definition-15) to see how **any vector on the plane in $\mathbf{R}^2$ can be obtained as a linear combination of $v_1,v_2$** ***with suitable coefficients***:

![](Attachments%20-%20Vector/Pasted%20image%2020231118134707.png)



# Vector Subspace

[source 1](https://textbooks.math.gatech.edu/ila/subspaces.html#subspaces-defn-of), [source 2](https://brilliant.org/wiki/vector-space/%20%22vector%20space%22), [source 3](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/subspace-basis/v/linear-subspaces)

* Quick definition: A **subspace** is a *special* [vector space](#Vector%20Space%20(Linear%20Combination%20of%20Vectors)) that is entirely contained within another [vector space](https://brilliant.org/wiki/vector-space/ "vector space"). ([source](https://brilliant.org/wiki/subspace/#:~:text=A%20subspace%20is%20a%20vector,4%2C%20C2%2C%20etc.))
	* The word "special" is used as it requires 3 characteristics mentioned below. 
	* As a subspace is defined _relative_ to its containing space, both are necessary to fully define one; for example, $\mathbf{R}^2$ is a subspace of $\mathbf{R}^3$, but also of $\mathbf{R}^4$, etc.
* Formal definition: A _subspace_ of $\mathbf{R}^n$ is a subset $X$ of $\mathbf{R}^n$ satisfying ([source](https://textbooks.math.gatech.edu/ila/subspaces.html#subspaces-defn-of)):
	* **_Non-emptiness:_** The zero vector is in $X$
	* **_Closure under addition:_** If $u$ and $v$ are in $X$, then $u+v$ is also in $X$.
	* **_Closure under scalar multiplication:_** If $v$ is in $X$ and $c$ is in $\mathbf{R}$, then $c\cdot v$ is also in $X$.
* Subsets versus Subspaces ([source](https://textbooks.math.gatech.edu/ila/subspaces.html#bluebox-32)):
	* A *subset* of $\mathbf{R}^n$ is any collection of vectors whatsoever.
	* Therefore, any subspace is considered a subset, but not vice versa, as some subsets don't satisfy the three conditions of that define a subspace.


# Vector Space vs Set vs Subset vs Subspace

A [vector space](#Vector%20Space%20(Linear%20Combination%20of%20Vectors)) $V$ is a set of vectors constructed from pre-defined vector operations (i.e., vector addition and scalar multiplication). 

A vector set $V$ is a set of vectors that are **not necessarily** constructed from pre-defined vector operations.

Therefore, any vector space is a vector set, but not vice versa.

A vector subset $X$ is a set of vectors that is a part of a bigger vector set (or a vector space) $V$. 

A [vector subspace](#Vector%20Subspace) $X$ is a vector space that has [special characteristics](#Vector%20Subspace), and is a part of a bigger vector space $V$. Note: $V$ must be a vector space in this case, not a vector set.

Therefore a vector subset is a more general (and relaxed) definition of a vector subspace, as the former's definition applies to both vector sets and vector spaces, while the latter's definition applies to vector spaces only.

# Span of a Vector Set (Vector Span)

[source](https://textbooks.math.gatech.edu/ila/spans.html#vectors-defn-span)

English definition: 

The _span_ of $v_1,v_2,\ldots,v_k$ is the collection of all [linear combinations](#Vector%20Space%20(Linear%20Combination%20of%20Vectors)) of $v_1,v_2,\ldots,v_k$, and is denoted as $\mathrm{Span}\lbrace v_1,v_2,\ldots,v_k \rbrace$. 

Mathematical definition:

$$ 
\mathrm{Span}\lbrace v_1,v_2,\ldots,v_k\rbrace =
\begin{Bmatrix}
c_1 v_1 + c_2 v_2 + \cdots + c_k v_k \;|\; c_1,c_2,\ldots,c_k\;\;\text{in R}
\end{Bmatrix}
$$

We also say that $\mathrm{Span}\{v_1,v_2,\ldots,v_k\}$ is the subset _spanned by_ or _generated by_ the vectors $v_1,v_2,\ldots,v_k$.

## Visualizing Spans

Drawings of spans ([source](https://textbooks.math.gatech.edu/ila/spans.html#paragraphs-9), I highly suggest checking out their interactive examples for clarification of the drawings below):

![|500](Attachments%20-%20Vector/Pasted%20image%2020231118140740.png)

![](Attachments%20-%20Vector/Pasted%20image%2020231118140819.png)

## Correct Terminology

'Vector span' is really not a valid terminology. You can talk about ***the span of a vector set*** but not 'vector span'.

## Vector Space vs Vector Span

[source 1](https://math.stackexchange.com/questions/3786958/what-is-the-difference-between-vector-space-and-vector-span), [source 2](https://www.reddit.com/r/learnmath/comments/6rrf21/difference_between_the_span_of_a_set_of_vectors/)

TLDR; they are the same thing, but we can say that the vector span has the notion of generating/spanning vectors to create a vector space $S$ that is inside a vector space $V$.

In-depth explanation:

A [vector space](#Vector%20Space%20(Linear%20Combination%20of%20Vectors)) is a set of vectors constructed from pre-defined vector operations (i.e., vector addition and scalar multiplication). 

To see how a vector space is related to a vector span, let's define a vector space $V$ which is equal to all of the vectors in $\mathbf{R}^3$.

Now, within that vector space $V$, we can take any subset of vectors, and ask about its span.

Example 1: 

Assume $X$ is a subset of vectors (i.e., a smaller vector space inside of $V$) with the following definition:

$$X=\left\lbrace 
c_1 \begin{bmatrix} 1\cr 0\cr 0 \end{bmatrix}
+
c_2 \begin{bmatrix} 0\cr 1\cr 0 \end{bmatrix}
\;\middle|\; 
c_1 ,\; c_2 \in \mathbb{R} 
\right\rbrace$$

Now we can ask about the span of $X$. In other words, <mark style="background: #FF5582A6;">we can ask about the set of all vectors of V that can be reached using only the vectors in X and the vector space operations of V</mark>.

So for the example above, the span of $X$ is actually all of the vectors in $\mathbf{R}^2$, as the third component of both vectors in the definition above is set to 0, so $X$ only spans the x-y coordinate space (not the x-y-z coordinate space). Visualization of this span ([source](https://www.google.com/search?q=vector+spanning+r2+plane&sca_esv=585006090&tbm=isch&sxsrf=AM9HkKk9OPrKUSx8lvSnwJJ8KYzQZZnYJQ:1700812917821&source=lnms&sa=X&ved=2ahUKEwj9367uldyCAxWW7qQKHX0wD_gQ_AUoAXoECAMQAw&biw=1920&bih=923&dpr=1#imgrc=KOWgby21v1AbbM)):

![](Attachments%20-%20Vector/Pasted%20image%2020231124100224.png)


Example 2:

Assume $Y$ is a "subset" of vectors of $V$ with the following definition:

$$Y=\left\lbrace 
c_1 \begin{bmatrix} 1\cr 0\cr 0 \end{bmatrix}
+
c_2 \begin{bmatrix} 0\cr 1\cr 0 \end{bmatrix}
+
c_3 \begin{bmatrix} 0\cr 0\cr 1 \end{bmatrix}
\;\middle|\; 
c_1 ,\; c_2 ,\; c_3 \in \mathbb{R} 
\right\rbrace$$

Here, the span of $Y$ is all of the vectors in $\mathbf{R}^3$, so we can say that $\mathrm{Span}\lbrace Y \rbrace = \mathrm{Span}\lbrace V \rbrace$.

Therefore, we can deduce from the two examples above the following statement:

The span of a set of vectors is actually a vector space, and vice versa.

To summarize, a span of a set of vectors $\mathrm{Span}\lbrace S \rbrace$ is a mathematical notation we use to find which vectors in the vector space $V$ can be reached/generated/spanned by a vector space $S$, which is contained in $V$. Dummy visualizations of this:

When $S=X$:

![](Attachments%20-%20Vector/Pasted%20image%2020231124103541.png)

When $S=Y$:

![](Attachments%20-%20Vector/Pasted%20image%2020231124103621.png)


## Vector Subspace vs Vector Span

Note the "tldr summary" at the start of the previous section ([Vector Space vs Vector Span](#Vector%20Space%20vs%20Vector%20Span)):

> we can say that the vector span has the notion of generating/spanning vectors to create a vector space $S$ that is inside a vector space $V$.

Notice that when we say:

> a vector space $S$ that is inside a vector space $V$.

This is the exact definition of a [vector subspace](#Vector%20Subspace) (given that $S$ has special characteristics).

Therefore, we can say that Spans are Subspaces and Subspaces are Spans ([source](https://textbooks.math.gatech.edu/ila/subspaces.html#subspaces-spans-are-subspaces)):

If $v_1,v_2,\cdots,v_p$ are any vectors in $\mathbf{R}^n$, then $\mathrm{Span}\lbrace v_1,v_2,\ldots,v_p \rbrace$ is a subspace of $\mathbf{R}^n$. 

Moreover, any subspace of $\mathbf{R}^n$ can be written as a span of a set of $p$ [linearly independent vectors](#Linear%20Independence) in $\mathbf{R}^n$ for $p \leq n$.

The proof of this can be shown [here](https://textbooks.math.gatech.edu/ila/subspaces.html#subsection-24).

## Span Examples

first example ([source](https://slideplayer.com/slide/13391998/)):

Given the following vector set $S$:

$$S = \left\lbrace
\begin{bmatrix} 1\cr 0\cr 1 \end{bmatrix}, 
\begin{bmatrix} 1\cr 1\cr 1 \end{bmatrix}, 
\begin{bmatrix} 1\cr 1\cr 2 \end{bmatrix} 
\right\rbrace$$

Does this set span $\mathbf{R}^3$? In other words, is every vector in $\mathbf{R}^3$ a linear combination of the vectors in $S$?

Answer:

$$
\begin{bmatrix} x\cr y\cr z \end{bmatrix} = 
c_1 \begin{bmatrix} 1\cr 0\cr 1 \end{bmatrix}
+
c_2 \begin{bmatrix} 1\cr 1\cr 1 \end{bmatrix}
+
c_3 \begin{bmatrix} 1\cr 1\cr 2 \end{bmatrix}
$$

Which can be rewritten as:

$$\begin{aligned}
x &= 1c_1 + 1c_2 + 1c_3 \cr
y &= 0c_1 + 1c_2 + 1c_3 \cr
z &= 1c_1 + 1c_2 + 2c_3 \cr
\end{aligned}$$

Which can be rewritten as:

$$\begin{pmatrix} 
1&1&1&\vdots&x\cr
0&1&1&\vdots&y\cr
1&1&2&\vdots&z\cr
\end{pmatrix}$$


performing [row operations](https://textbooks.math.gatech.edu/ila/row-reduction.html#paragraphs-5), we get:

$$\begin{pmatrix}
1&0&0&\vdots&x-y\cr
0&1&0&\vdots&y-z+x\cr
0&0&1&\vdots&z-x\cr
\end{pmatrix}$$

Which can be rewritten as:

$$\begin{pmatrix}
c_1&&&=&x-y\cr
&c_2&&=&y-z+x\cr
&&c_3&=&z-x
\end{pmatrix}$$

Therefore, whatever you substitute for x, y, and z, you will be able to find $c_1$, $c_2$, and $c_3$. Example:

suppose $x=5$, $y=3$, and $z=4$, then we will see that:

$$\begin{pmatrix}
c_1&&&=&5-3=2\cr
&c_2&&=&3-4+5=4\cr
&&c_3&=&4-5=-1\cr
\end{pmatrix}$$

Therefore:

$$
\begin{bmatrix} x\cr y\cr z \end{bmatrix} = 
\begin{bmatrix} 5\cr 3\cr 4 \end{bmatrix} =
2 \begin{bmatrix} 1\cr 0\cr 1 \end{bmatrix}
+
4 \begin{bmatrix} 1\cr 1\cr 1 \end{bmatrix}
+
(-1) \begin{bmatrix} 1\cr 1\cr 2 \end{bmatrix}
$$

# Linear Independence

[source 1](https://textbooks.math.gatech.edu/ila/linear-independence.html#subsection-19), [source 2](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/linear-independence/v/linear-algebra-introduction-to-linear-independence)

Why is this concept useful? ([source](https://textbooks.math.gatech.edu/ila/linear-independence.html#p-274)):

One of the reasons for its usefulness is related to [vector spans](#Correct%20Terminology); Sometimes, a vector set could have one or more **redundant vectors** that will not affect the [span of this set](#Span%20of%20a%20Vector%20Set%20(Vector%20Span)). For example:

![](Attachments%20-%20Vector/Pasted%20image%2020231118155103.png)

The vectors above are *linearly dependent* (explained below); because in each of the sub figures, one vector is in the span of the other(s), so *it doesn't make the span bigger*. <mark style="background: #FF5582A6;">Therefore, the concept of linear dependency can help us find if a vector set has redundant vectors or not</mark>.

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
* span all the vectors in $\mathbf{R}^{3}$? 

$$ \left\lbrace
\begin{bmatrix} 1\cr -1\cr 2 \end{bmatrix}, 
\begin{bmatrix} 2\cr 1\cr 3 \end{bmatrix}, 
\begin{bmatrix} -1\cr 0\cr 2 \end{bmatrix} 
\right\rbrace$$

The [system of equations](https://textbooks.math.gatech.edu/ila/systems-of-eqns.html#p-35) formed from the vector set above is [solved algebraically](https://www.khanacademy.org/test-prep/sat/x0a8c2e5f:untitled-652/x0a8c2e5f:heart-of-algebra-lessons-by-skill/a/gtp--sat-math--article--solving-system-of-linear-equations--lesson) in this [video](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/linear-independence/v/span-and-linear-independence-example).

Other solved examples (using the [row operations](https://textbooks.math.gatech.edu/ila/row-reduction.html#paragraphs-5)) are mentioned [here](https://textbooks.math.gatech.edu/ila/linear-independence.html#bluebox-26).

Additionally, look at the basis of a subspace's [example section](#Examples%20for%20Finding%20a%20Subspace's%20Basis); you'll find end-notes regarding linear dependency.

# Basis of a Subspace

[source 1](https://textbooks.math.gatech.edu/ila/dimension.html), [source 2](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/subspace-basis/v/linear-algebra-basis-of-a-subspace)

English definition: 

A "basis" is a **set** of *vectors* where:
* These *vectors* are [linearly independent](#Linear%20Independence).
* This **set** [spans](#Span%20of%20a%20Vector%20Set%20(Vector%20Span)) a [subspace](#Vector%20Subspace) $V$.

Mathematical Definition:

* Let $V$ be a subspace of $\mathrm{R}^n$. 
* A ***basis of $V$*** is a set of vectors: $X = \{v_1,v_2,\cdots,v_m\}$, such that:
	* $X \subset V$
	* $V = \mathrm{Span} \left\{ X \right\}$
	* $X$ is linearly independent

The "basis theorem" talks about the set of vectors applicable to be called "basis of a subspace", and it states the following:
* **Any** $m$ **linearly independent** vectors in a subspace $V$ **form a basis** for $V$.
* **Any** $m$ vectors **that span** $V$ **form a basis** for $V$.

## Dimension of a Subspace

[source 1: gatech](https://textbooks.math.gatech.edu/ila/dimension.html#dimension-defn-dimension)

The **dimension of a subspace** $V$ is the **number of vectors in any basis** of $V$, and is written as $Dim\,(V)$.



## Examples for Finding a Subspace's Basis

Example 1 ([source: math.stackexchange.com](https://math.stackexchange.com/questions/948178/finding-a-basis-for-a-subspace-in-bbb-r4)):

Let:

$$
v_1 = 
\begin{bmatrix} 2 \cr -1 \cr 2 \cr 1 \end{bmatrix}
,
v_2 =
\begin{bmatrix} 1 \cr 0 \cr 1 \cr 0 \end{bmatrix}
,
v_3 =
\begin{bmatrix} 1 \cr 1 \cr 1 \cr -1 \end{bmatrix}
,
v_4 =
\begin{bmatrix} 1 \cr -1 \cr 1 \cr -1 \end{bmatrix}
$$

Find a basis for the subspace of $\mathbb{R}^4$ spanned by the set $\left\{v_1,v_2,v_3,v_4\right\}$, and mention its dimension.

Answer:

Optional: convert to augmented matrix:

$$
\left(
\begin{array}{cccc|c}
2 & 1 & 1 & 1 & 0 \cr 
-1 & 0 & 1 & -1 & 0 \cr
2 & 1 & 1 & 1 & 0 \cr
1 & 0 & -1 & -1 & 0 \cr
\end{array} \;
\right)
$$

Side note: the above step is optional as we're dealing with a homogenous system of equation. Check [here](https://textbooks.math.gatech.edu/ila/solution-sets.html#solnsets-no-augment) for details.

Convert to matrix:

$$
\left(
\begin{matrix} 
2 & 1 & 1 & 1 \cr 
-1 & 0 & 1 & -1 \cr
2 & 1 & 1 & 1 \cr
1 & 0 & -1 & -1
\end{matrix} \;
\right)
$$

Change this matrix to reduced row echelon form (detailed steps are mentioned at the end):

$$\left( \;
\begin{matrix} 
1 & 0 & -1 & 0 \cr 
0 & 1 & 3 & 0
\cr 0 & 0 & 0 & 1 
\cr 0 & 0 & 0 & 0
\end{matrix} \; 
\right)$$

Now, assuming the matrix columns represents the coefficients $a, b, c, d$ respectively, and by seeing rows 1, 2, and 3, we see that $a=c, b=-3 \, c, d=0$ respectively. 

Therefore, $v_3$ is dependent on $v_1, v_2$, while $v_1, v_2, v_4$ (i.e., columns 1, 2, and 4) are linearly independent on each other.

Therefore, the basis $B$ is:

$$B = \left\{v_1, v_2, v_4 \right\}$$

Such that $Dim\,(B) = 3$ (as there are 3 vectors in $B$). 

Side note 1: the [steps done](https://textbooks.math.gatech.edu/ila/row-reduction.html#p-107) to get a reduced row echelon form can be seen [here](https://textbooks.math.gatech.edu/ila/demos/rrinter.html?mat=2,1,1,1:-1,0,1,-1:2,1,1,1:1,0,-1,-1&ops=s0:3,r0:1:1,r0:-2:2,r0:-2:3,s1:2,r1:-1:3,m2:-1.2,r2:1:0,r2:-3:1&cur=0), where you can keep clicking the big right arrow to visualize each step. Alternatively, you can look at the end of that page to directly see the steps.

Side note 2: From this result, we can deduce that the set of vectors $v_1, v_2, v_3, v_4$ is a [linear dependent](#Linear%20Independence) vector set.

Other examples are mentioned in [this](https://www.youtube.com/watch?app=desktop&v=kfVI7Tp98WM) and [this](https://www.youtube.com/watch?app=desktop&v=YYQQo6-lx68) video.

