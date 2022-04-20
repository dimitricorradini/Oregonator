# Oregonator
We attempt an explicit implementation of the Runge-Kutta 4th order integrator in order to approxi- mate solutions to the Oregonator model, invented in 1974 to describe the very weird (and beauti- ful) Belousov-Zhabotinsky reaction, which famously displays oscillating behaviour between differ- ent chemical species for some values of its parameters. At the heart of the model lie the following equations, which constitute a nonlinear system in three variables:


dX =k1*A*Y+k3*A*X-k2*X*Y-2k4X2 dt
dY = -k1 * A * Y - k3 * X * Y + f * k5 * B * Z dt 2
dZ = 2 * k2 * A * X - k5 * B * Z

Where X, Y, Z represent (molar) concentrations of the chemical species, and respectively, ki are kinetic rates, A and B are concentrations of other reagents (assumed as constant) and f is an adjustable stoichiometric factor.

We can apply RK4 to the aforementioned system: let us briefly recall how the algorithm works.
In order to discretize the equation system, we first select an adequate time interval (here named h). We proceed to compute the value of the derivative for each component at t=0 by direct application of the equations; this calculation is then used to estimate the value of the three components at t= h2
à la Euler, i.e. by considering the first order approximation and leveraging the properties of linear- ity. After this first step, we can input the obtained value for the components in the equation once more to estimate the derivatives at t= h2 , and subsequently use the result to again approximate the value of the solution at the center point of the interval. By inserting the result in the equation one more time and calculating the value of the derivative at t=h, we get the last ingredient of our recipe. Quantitatively, the following operations are executed:
Given
dx =f(x, t) dt
We can calculate t1= f(x, t)
x1= x(t) + h2 t1
t2=f(x1,t+h2 )
x2= x(t) + h2 t2
t3=f(x2,t+ h2 )
x3= x(t) + ht3 t4=f(x3,t+h)
Where x(t) is the state of the system at time t.
Finally, we can approximate the value of x(t+h) by computing
x(t+h) = x(t)+ h/6 (t1 +2 t2+2 t3+ t4)
It can be shown that the error in this approximation amounts to O(h4).
