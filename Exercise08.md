#Exercise08 
####*熊毅恒 2014301020066*
------
##abstract

From the last work, we have used the method of the Euler-Cromer to solve the problem of the oscillatory motion and chaos. 
Now I want to have deeply consideration of the routes of the chaos. And we know that the routes of chaos have a relationship 
with the period doubling from the book. So I would like to use the bifurcation diagram and poincare section to do the consideration.
And I will try the bigger Fd to do the work to understand the relationship between chaos and period doubling. 
##background

We know the Euler-Cromer method. We will take the Euler-Cromer method into the oscillatory motion and chaos calculation: 
Newton’s second law for ideal pendulum with small angle: 
$$\frac{d^2\theta}{dt^2}=-\frac{g}{l}\theta$$
Write the second-order equations as two firest-order differential equations: 
$$\frac{d\omega}{dt}=-\frac{g}{l}\theta$$
$$\frac{d\theta}{dt}=\omega$$

Finite difference form with Euler-Cromer method: 
\omega_{i+1}=\omega_i-(g/l)\theta_i\Delta t
\theta_{i+1}=\theta_i+\omega_{i+1}\Delta t
t_{i+1}=t_i+\Delta t

Also to make the question more realistic,we can take some factors into consideration. 
We do not assume the small-angle approximation, and thus do not expand  term in .
We include friction of the form .
We add to our model a sinusoidal driving force . 
Putting all of these ingredients together, we have the equation of motion:

We can rewrite the two-order differential equation now as two first-order differential equations and obtian: 

Finite difference form with Euler-Cromer method: 

If  is out of the range , add or subtract  to keep it in this range. 
And for the pioncare section, we chose the time that : 

##mainbody
problem 3.18 : 
Calculate Piuncare sections for the pendulum as it undergose the period-doubling route to chaos. Plot ω versus θ, with one point plotted for each drive cycle, as in Figure 3.9. Do this for F_D=1.4, 1.44, and 1.465, using the other parameters as fiven in connection with Figure 3.10. You should find that after removing the points corresponding to the initial transient the attractor in the period-1 regime will contain only a single point. Likewise, if the behavior is period n, the attractor will contain n discrete points.

![二分之派](https://github.com/Guibeen/compuational_physics_N2014301020066/blob/master/images/07/3.12-%E4%BA%8C%E5%88%86%E4%B9%8B%E6%B4%BE.png)

而在同样条件下，当驱动力的大小使得白的周期刚好为驱动力周期整数倍时，去掉开始阶段的点，所得图像将变成数个孤立的点。

##正文

![](http://latex.codecogs.com/gif.latex?%5Cdpi%7B120%7D%20%5Cbg_white%20%5Ctheta-t)图像:

[代码1](https://github.com/Guibeen/compuational_physics_N2014301020066/blob/master/codes/08/18-1.py)

结果：

![1.35-1](https://github.com/Guibeen/compuational_physics_N2014301020066/blob/master/images/08/1.35-1.png)
![1.4-1](https://github.com/Guibeen/compuational_physics_N2014301020066/blob/master/images/08/1.4-1.png)
![1.44-1](https://github.com/Guibeen/compuational_physics_N2014301020066/blob/master/images/08/1.44-1.png)
![1.465-1](https://github.com/Guibeen/compuational_physics_N2014301020066/blob/master/images/08/1.465-1.png)
驱动力为1.35时，摆的频率和驱动力一致；当其幅度增加到1.4时刚刚开始进入两倍周期，只是两峰非常接近；1.44时，摆的周期变为驱动力的两倍；而幅度再增加到1.465时，摆的周期进一步增加到驱动力的四倍。
照此趋势，当驱动力幅度增加到某一值时，摆的周期将变为驱动力的无数倍，即不再是周期性运动，为混沌状态。

![](http://latex.codecogs.com/gif.latex?%5Cdpi%7B120%7D%20%5Cbg_white%20%5Comega-%5Ctheta)关系：

[代码2](https://github.com/Guibeen/compuational_physics_N2014301020066/blob/master/codes/08/18-2.py)

结果：

![](http://latex.codecogs.com/gif.latex?%5Cdpi%7B120%7D%20%5Cbg_white%20F_D%3D1.35)时：

![](https://github.com/Guibeen/compuational_physics_N2014301020066/blob/master/images/08/1.35-2.png)

![](http://latex.codecogs.com/gif.latex?%5Cdpi%7B120%7D%20%5Cbg_white%20F_D%3D1.4)时：

![](https://github.com/Guibeen/compuational_physics_N2014301020066/blob/master/images/08/1.4-2.png)

![](http://latex.codecogs.com/gif.latex?%5Cdpi%7B120%7D%20%5Cbg_white%20F_D%3D1.44)时：

![](https://github.com/Guibeen/compuational_physics_N2014301020066/blob/master/images/08/1.44-2.png)

![](http://latex.codecogs.com/gif.latex?%5Cdpi%7B120%7D%20%5Cbg_white%20F_D%3D1.465)时

![18-2](https://github.com/Guibeen/compuational_physics_N2014301020066/blob/master/images/08/18-2.png)

可见代码2的算法存在着一些问题，使得其图像不是孤立的点而变为直线。事实上由于π是无理数，计算机在计算式无法给出精确的数值。每次计算都会积累小的偏差，所以逐渐延长为线段。将算法做改进后，得出的点变为孤立的。

[代码3](https://github.com/Guibeen/compuational_physics_N2014301020066/blob/master/codes/08/18-3.py)

下图中显示的是![](http://latex.codecogs.com/gif.latex?%5Cdpi%7B120%7D%20%5Cbg_white%20F_D%3D1.2%2CF_D%3D1.4%2CF_D%3D1.44%2CF_D%3D1.465)对应的图像。

![](https://github.com/Guibeen/compuational_physics_N2014301020066/blob/master/images/08/%E5%80%8D%E5%91%A8%E6%9C%9F.png)

与前面相符，即驱动力幅值为1.4时刚开始分离，实际上应该是十分靠近的两点。幅值为1.44时，摆的周期变为驱动力的两倍，两个峰大小明显不同。幅值达到1.465时，摆的周期变为驱动力的四倍。

##感谢
熊沛雨、仲逸飞、谭善
