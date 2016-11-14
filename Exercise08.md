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

code
```
import pylab as pl
import math
class oscillatory:
    def __init__(self,g=9.8,l=9.8,q=0.5,F_D=1.465,O_D=2/3,time_step=3*math.pi/100,\
    total_time=100,initial_theta=0.2,initial_omega=0):
        self.g=g
        self.l=l
        self.q=q
        self.F=F_D
        self.O=O_D
        self.t=[0]
        self.initial_theta=initial_theta
        self.initial_omega=initial_omega
        self.dt=time_step
        self.time= total_time
        self.omega= [initial_omega]
        self.theta= [initial_theta]
        self.nsteps=int(total_time//time_step+1)
        self.tmpo=[0]
        self.tmpt=[0]
    def run(self):
        for i in range(self.nsteps):
            tmpo=self.omega[i]+(-1*(self.g/self.l)*math.sin(self.theta[i])-\
            self.q*self.omega[i]+self.F*math.sin(self.O*self.t[i]))*self.dt
            tmpt=self.theta[i]+tmpo*self.dt
            while(tmpt<(-1*math.pi) or tmpt>math.pi):
                if tmpt<(-1*math.pi):
                   tmpt+=2*math.pi
                if tmpt>math.pi:
                   tmpt-=2*math.pi
            self.omega.append(tmpo)
            self.theta.append(tmpt)
            self.t.append(self.t[i]+self.dt)
        for i in range(len(self.t)):
            if self.t[i]//(3*math.pi)>300:
                if ((2/3*self.t[i])%(2*math.pi))<=(2/3*self.dt*0.5)\
                or (2*math.pi-((2/3*self.t[i])%(2*math.pi)))<=(2/3*self.dt*0.5):
                    self.tmpo.append(self.omega[i])
                    self.tmpt.append(self.theta[i])   
    def show_results(self):
        font = {'family': 'serif',
                'color':  'darkred',
                'weight': 'normal',
                'size': 16,}
        pl.plot(self.t,self.theta)
        #pl.scatter(self.tmpt, self.tmpo)
        pl.title(r'$\theta$ versus t', fontdict = font)
        pl.xlabel(r't(s)')
        pl.ylabel(r'$\theta$(radian)')
        pl.xlim(0,100)
        pl.ylim(-4,4)
        pl.legend((['$F_D$=1.465']))
        pl.show()
a = oscillatory()
a.run()
a.show_results()
```


##感谢
熊沛雨、仲逸飞、谭善
