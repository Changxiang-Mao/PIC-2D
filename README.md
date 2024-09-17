# PIC-2D
2D PIC simulation

# 1. Basic equations
Low index $i,j$ denotes number nodes and low index $p$ denotes number of particles. The number of nodes is $N_x,N_y$.
## 1.1 Gather
Suppose we have a field $E(\vec{x}),\vec{E}_{ij}$. For $p-th$ particle, its position is $x_p,y_p$, then

$$I={\rm int}\left(\frac{x_p-x_{\rm min}}{dx}\right),~J={\rm int}\left(\frac{y_p-y_{\rm min}}{dy}\right),~\Delta x=\frac{x_p-x_I}{dx},~\Delta y=\frac{y_p-y_J}{dy},$$

$$E_{px}=(1-\Delta x)(1-\Delta y)E_{x,ij}+\Delta x(1-\Delta y)E_{x,i+1,j}+(1-\Delta x)\Delta yE_{x,i,j+1}+\Delta x\Delta yE_{x,i+1,j+1}$$

$$E_{py}=(1-\Delta x)(1-\Delta y)E_{y,ij}+\Delta x(1-\Delta y)E_{y,i+1,j}+(1-\Delta x)\Delta yE_{y,i,j+1}+\Delta x\Delta yE_{y,i+1,j+1}$$

$$\vec{E}_ p=(1-\Delta x)(1-\Delta y)\vec{E}_ {ij}+\Delta x(1-\Delta y)\vec{E}_ {i+1,j}+(1-\Delta x)\Delta y\vec{E}_ {i,j+1}+\Delta x\Delta y\vec{E}_{i+1,j+1}$$




## 1.2 Scatter
Suppose we konw the position of a particle. We need to scatter the quantity of particle to surrounding nodes.

$$I={\rm int}\left(\frac{x_p-x_{\rm min}}{dx}\right),~J={\rm int}\left(\frac{y_p-y_{\rm min}}{dy}\right),~\Delta x=\frac{x_p-x_I}{dx},~\Delta y=\frac{y_p-y_J}{dy},$$

$$E_{x,ij}=(1-\Delta x)(1-\Delta y)E_{px},E_{x,i+1,j}=\Delta x(1-\Delta y)E_{px},E_{x,i,j+1}=(1-\Delta x)\Delta yE_{px},E_{x,i+1,j+1}=(1-\Delta x)(1-\Delta y)E_{px}$$

$$\vec{E}_ {ij}=(1-\Delta x)(1-\Delta y)\vec{E}_ {p},\vec{E}_ {i+1,j}=\Delta x(1-\Delta y)\vec{E}_ {p},\vec{E}_ {i,j+1}=(1-\Delta x)\Delta y\vec{E}_ {p},\vec{E}_ {i+1,j+1}=(1-\Delta x)(1-\Delta y)\vec{E}_{p}$$

## 1.3 Finite Difference Method
Possion equation is $\nabla^2\phi=-4\pi\rho$, which means

$$\frac{\phi_{i+1,j}+\phi_{i-1,j}-2\phi_{ij}}{dx^2}+\frac{\phi_{i,j+1}+\phi_{i,j-1}-2\phi_{ij}}{dy^2}=-4\pi\rho_{ij}$$

$$\frac{\phi_{i+1,j}+\phi_{i-1,j}}{dx^2}+\frac{\phi_{i,j+1}+\phi_{i,j-1}}{dy^2}-(\frac{2}{dx^2}+\frac{2}{dy^2})\phi_{ij}=-4\pi\rho_{ij}$$

$$\frac{\phi_{i+1,j}+\phi_{i-1,j}}{dx^2}+\frac{\phi_{i,j+1}+\phi_{i,j-1}}{dy^2}+4\pi\rho_{ij}=(\frac{2}{dx^2}+\frac{2}{dy^2})\phi_{ij}$$

$$\phi_{ij} = \left[\frac{\phi_{i+1,j}+\phi_{i-1,j}}{dx^2}+\frac{\phi_{i,j+1}+\phi_{i,j-1}}{dy^2}+4\pi\rho_{ij}\right]/(\frac{2}{dx^2}+\frac{2}{dy^2})$$

Now we have the potential, we can calculate the electric field, $$E=-\frac{\partial\phi}{\partial x}$$.

$$E_{x,ij}=-\frac{\phi_{i+1,j}-\phi_{i-1,j}}{2dx},~~~ E_{x,0j}=\frac{\phi_{2,j}-4\phi_{1,j}+3\phi_{0,j}}{2dx},~~~ E_{Nx-1,j}=-\frac{\phi_{Nx-3,j}-4\phi_{Nx-2,j}+3\phi_{Nx-1,j}}{2dx}$$

$$E_{y,ij}=-\frac{\phi_{i,j+1}-\phi_{i,j-1}}{2dy},~~~ E_{y,i0}=\frac{\phi_{i,2}-4\phi_{i,1}+3\phi_{i,0}}{2dy},~~~ E_{i,Ny-1}=-\frac{\phi_{i,Ny-3}-4\phi_{i,Nx-2}+3\phi_{i,Nx-1}}{2dy}$$


## 1.4 Leap frog method
The position of particles are in integer time step, and the velocity of particles are in half-integer time step.

$$\vec{v}_p^{i+1/2}=\vec{v}_p^{i-1/2}+\frac{q\vec{E}_p^i}{m}dt,~~~ \vec{x}_p^{i+1}=\vec{x}_p^i+\vec{v}_p^{i+1/2}dt$$


