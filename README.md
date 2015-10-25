# pylbfgs
the python implementation of [lib:LBFGS](http://www.chokkan.org/software/liblbfgs/index.html)
##usage
```python
from lbfgs import *
def new_Evaluate(w, g, n, step):
...
def progress(x, g, fx, xnorm, gnorm, step, n, k, ls):
...
param = lbfgs_parameters(new_Evaluate, progress)
lb = lbfgs(N, x, fx, param)
ret = lb.do_lbfgs()
```
##API

```python
class lbfgs:
```
```python
def __init__(self, n, x, ptr_fx, lbfgs_parameters):
```

**n**	The number of variables.  
**x**	The array of variables. A client program can set default values for the optimization and receive the optimization result through this array.  
**ptr_fx**	The pointer to the variable that receives the final value of the objective function for the variables. This argument can be set to NULL if the final value of the objective function is unnecessary.  
**proc_evaluate**	The callback function to provide function and gradient evaluations given a current values of variables. A client program must implement a callback function.  
**proc_progress**	The callback function to receive the progress (the number of iterations, the current value of the objective function) of the minimization process. This argument can be set to NULL if a progress report is unnecessary.  
instance	A user data for the client program. The callback functions will receive the value of this argument.  
**param**	The pointer to a structure representing parameters for L-BFGS optimization. A client program can set this parameter to NULL to use the default parameters.  

```python
class lbfgs_parameters:
```
```python
def __init__(self, proc_evaluate, proc_progress, m=6, Linesearch=backtrack, epsilon=1e-5, ftol=1e-4, wolfe=0.9, max_linesearch=10, min_step=1e-20, max_step=1e20):
```

**m**: the number of corrections to approximate the inverse hessian matrix  
**Linesearch**: the Linesearch method  
**epsilon**: epsilon for the convergence test  
**ftol**: A parameter to control the accuracy of the line search routine.The default value is 1e-4. This parameter should be greaterthan zero and smaller than 0.5.  
**wolfe**: A coefficient for the Wolfe condition.The default value is 0.9. This parameter should be greater the ftol parameter and smaller than 1.0.  
**min_step**: The minimum step of the line search routine.  
**max_step**: The maximum step of the line search routine.  

see more details:
http://www.chokkan.org/software/liblbfgs/index.html