# Swarms-Course-Projects

## HW1 - A point mass goes down a parabola then falls freely
- For interactive notebook, go to https://colab.research.google.com/drive/12gTb8SFlF5goO58rhXWqk-Ulhv4A8K08?usp=sharing
- We have a rectanglular area in $2D$ of size $l\times h$ along axes $\boldsymbol{x}$ and $\boldsymbol{y}$, of which the lower left corner is placed at $\left(-\frac{l}{2}, 0\right)$. The walls of the rectangle are not penetrable, which define the ***playground*** of this simulation. 
We release a number of $n$ circular unactuated objects in the playground and simulate the motion of these objects. We highlight an additional rule that the bounding walls boost/nerf the velocity of the circular objects by $p_x\% \text{ and } p_y\%$, *i.e.*, if an object collides with a vertical wall with a velocity vector of $\boldsymbol{v} = \left[v_x, v_y\right]$, then its velocity becomes $\left[-\left(1+\frac{p_x}{100}\right)v_x, v_y\right]$ after the impact. The objects can collide with each other while perserving their momentum and kinetic energy up to a maximum impact force.
