#math #linear-algebra 

Main sources:
[khan academy: Unit 1: Vectors and spaces](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces)

# Vector Definition

<mark style="background: #FF5582A6;">It is something that has a magnitude and a direction</mark>.

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
  
  ![](Media-Temp/Pasted%20image%2020231104160540.png)
  
  Consequently, when we do operations on these vectors, like [adding vectors](#Vector%20Addition), we get a vector like this:
  
  ![](Media-Temp/Pasted%20image%2020231104160832.png)
  
  However, we may move these vectors' starting points (i.e., tails) to easily conceptualize these operations, for example:
  
  ![](Media-Temp/Pasted%20image%2020231104161011.png)
  
  Now the question is the following: "why is it allowed for us to move these vectors' starting points to anywhere we want in the coordinate plane?" 
  
  Answer: Because if we recall the [definition of a vector](#Vector%20Definition), we see that we only care about encoding two pieces of information: **magnitude** and **direction**. Therefore, the actual location of the vector in the plane does not matter.

# Vector Addition

Addition visualization ([interactive source](https://sciencepickleapps.com/VisuallyAddingVectorsV1-0-0/), from [this](https://sciencepickle.com/earth-systems/vectors-and-forces/adding-vectors/)):
![vector-addition](Attachments%20-%20Vectors/vector-addition.mp4)

Example: 

$$\vec{v}=\vec{red}+\vec{green}+\vec{blue}=\left[\begin{array}{c}{-9}\cr{3}\end{array}\right]+\left[\begin{array}{c}{2}\cr{3}\end{array}\right]+\left[\begin{array}{c}{2}\cr{0.2}\end{array}\right]=\left[\begin{array}{c}{-5}\cr{6.2}\end{array}\right]$$

# Vector Subtraction

Suppose you have these two vectors:

![](Media-Temp/Pasted%20image%2020231104155811.png)
(Adapted from [here](https://www.google.com/search?q=vector+subtraction&sca_esv=579447376&tbm=isch&sxsrf=AM9HkKnGtLJ6VqlC3AJLr_SJv37CNWgI9w:1699105968608&source=lnms&sa=X&ved=2ahUKEwix5sb9vqqCAxW_UKQEHatZBbEQ_AUoAXoECAQQAw&biw=1920&bih=911&dpr=1#vhid=V5qJxTe7D4HnZM&vssid=3981:1DaQEkvNT6JBSM))

Now, what if we want to subtract B from A? (i.e., A - B)?

Mathematical example:

$$A-B=\left[\begin{array}{c}{3}\cr{5}\end{array}\right]-\left[\begin{array}{c}{4}\cr{2}\end{array}\right]=\left[\begin{array}{c}{-1}\cr{3}\end{array}\right]$$

Now, this vector can be represented like this:

![](Media-Temp/Pasted%20image%2020231104162015.png)

Now, to intuitively grasp how subtraction works geometrically, there are two methods of moving the vector $A-B$:

* Method 1 ([source](https://www.onlinemathlearning.com/vector-subtraction.html)):
  
  ![](Media-Temp/Pasted%20image%2020231104162158.png)
  
  Applying this on the previous example:
  
  ![](Media-Temp/Pasted%20image%2020231104162448.png)
  
  So it's as if we're [adding](#Vector%20Addition) $A$ to $-B$ to get the emerged vector $A-B$:  
  
  ![](Media-Temp/Pasted%20image%2020231104162559.png)
  
  Final image which contains all of the previous images' steps:
  
  ![](Media-Temp/Pasted%20image%2020231104162712.png)
  
* Method 2: 
  
  Starting from this image:
  
  ![](Media-Temp/Pasted%20image%2020231104162015.png)
  
  Simply move the vector $A-B$ to be between $A$ and $B$:
  
  ![](Media-Temp/Pasted%20image%2020231104163010.png)
  
  Why is this logical? First, recall how we visualize [vector addition](#Vector%20Addition), then, recognize that what we're doing above is simply: $A=B+(A-B)$, so it's as if the vector $A$ emerged like the image above due to adding $B$ to $A-B$.

## Vector Subtraction Visual summary

![](Media-Temp/Pasted%20image%2020231104163904.png)

# Vector Multiplication

Multiplication visualization ([source](https://makeagif.com/gif/vector-multiplication-by-scalar-G4qCVh)):
![vector-scalar-multiplication](Attachments%20-%20Vectors/vector-scalar-multiplication.gif)

Formula of a scalar-multiplied vector's magnitude: $||c\cdot \vec v||=|c|\cdot ||\vec v||$ 

To get the reverse direction of a vector, add 180 to its direction.

Example ([source](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/e/scaling_vectors)):

![](Attachments%20-%20Vectors/Pasted%20image%2020231104110053.png)

Answer:

![](Attachments%20-%20Vectors/Pasted%20image%2020231104112518.png)

![](Attachments%20-%20Vectors/Pasted%20image%2020231104112617.png)


# Unit Vector

[source](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/intro-unit-vector-notation)

Definition: 
* **A vector that has a magnitude of 1** is a unit vector. 
* It is also known as Direction Vector.

Specifically, in cartesian coordinates, <mark style="background: #FF5582A6;">the unit vectors along the axis are denoted by i and j respectively</mark>. Their formulae:

$$\begin{aligned}
\hat{i}&=
\left[\begin{matrix}{1}\cr{0}\cr\end{matrix}\right] \cr\cr
\hat{j}&=
\left[\begin{matrix}{0}\cr{1}\cr\end{matrix}\right]
\end{aligned}$$


![](Media-Temp/Pasted%20image%2020231104154916.png)
([source](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/intro-unit-vector-notation))
