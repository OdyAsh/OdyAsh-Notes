#math #linear-algebra 

sources:
[khan academy: Unit 1: Vectors and spaces](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces)

# Vector Definition

Basic vector characteristics:
* It is something that has a magnitude and a direction.
	* Intuitive example ([source](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/vector-introduction-linear-algebra)):
	  ![[Pasted image 20231103144158.png]]
* It has the following notation: $\vec{v}=\left(5,0\right)=\left[\begin{array}{c}{5}\cr{0}\end{array}\right]$ 
	* $5$ and $0$ are called ***components*** of a vector, while $\left(5,0\right)$ is called a ***2-tuple*** in a 2-D real coordinate space $\left(\mathbb{R}^2\right)$ ([source](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/real-coordinate-spaces)).
		* Side note 1: $\mathbb{R}^2$ is also called a ***set***, such that $\overrightarrow{x}\in\mathbb{R}^2$ is called "vector $\overrightarrow{x}$  belongs in the set $\mathbb{R}^2$"
		* Side note 2: it can also be represented using unit vectors $i$ and $j$ , as explained in the [Unit vector](#Unit%20vector) section.
* It can be [added](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/adding-vectors) and [multiplied (by scalers)](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/multiplying-vector-by-scalar)

## Vector Addition

Addition visualization ([interactive source](https://sciencepickleapps.com/VisuallyAddingVectorsV1-0-0/), from [this](https://sciencepickle.com/earth-systems/vectors-and-forces/adding-vectors/)):
![vector-addition](Attachments%20-%20Vectors/vector-addition.mp4)

Example: $\vec{v}=\vec{red}+\vec{green}+\vec{blue}=\left[\begin{array}{c}{-9}\cr{3}\end{array}\right]+\left[\begin{array}{c}{2}\cr{3}\end{array}\right]+\left[\begin{array}{c}{2}\cr{0.2}\end{array}\right]=\left[\begin{array}{c}{-5}\cr{6.2}\end{array}\right]$

## Vector Multiplication

Multiplication visualization ([source](https://makeagif.com/gif/vector-multiplication-by-scalar-G4qCVh)):
![vector-scalar-multiplication](Attachments%20-%20Vectors/vector-scalar-multiplication.gif)

Formula of a scalar-multiplied vector's magnitude: $||c\cdot \vec v||=|c|\cdot ||\vec v||$ 

To get the reverse direction of a vector, add 180 to its direction.

Example ([source](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/e/scaling_vectors)):
![](Media-Temp/Pasted%20image%2020231104110053.png)
Answer:
![](Media-Temp/Pasted%20image%2020231104112518.png)
![](Media-Temp/Pasted%20image%2020231104112617.png)


## Unit vector

