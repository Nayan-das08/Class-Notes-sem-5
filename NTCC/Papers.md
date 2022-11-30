>Chapter - [[_NTCC 2nd yr]]

# 1. Lagaris et. al.
## Artificial Neural Networks for solving Partial Order Differential Equations
Presents a technique to solve initial value and various boudnary value differential equation problems with the help of Artificial Neural Networks (ANN). The said approach is applicable for ODEs, systems of ODEs and PDEs. 

The authors pose the problem of solving the PDE with the constraints given in the form of initial and boundary conditions as a mere optimization problem where the Left-Hand side of differential equation is minimized over discrete values of domain set, keeping Right-Hand side of the differential equation zero. 

The **trial solution**, or a general form of solution is formed with the output of a feedforward network with trainable parameters - weights and biases of the neural network. The trial function also needs to satisfy the **IC and BCs**. For that, the terms corresponding to the IC and BCs are added separately to the trial solution formula. 

The error or loss function for the model is designed such that for the discrete points on the domain the loss function gives the corresponding error value of the required derivatives from the actual derivative function. This value is subsituted in the trial solution gives value of predicted function solution. They have employed th eQuasi-Newton BFGS optimizer to optimize the loss function. 

The paper shows examples of the method being applied on ODEs and PDEs with some **IC and BCs**. The accuracy of the model is obtained via computation of deviation of predicted solution from the actual solution obtained from the function describing the differential. This deviation when plotted for the model shows that the deviation  is very low for points in the domain but increases slightly and gradually as it moves away from the region of domain. It should be noted that the size of training set is very small (about 10 equidistant points in the domain). The model shows similar accuracy when compared with Finite Element Method (FEM), a numerical method for solving PDEs.

One of the most important feature of this approach is that there is no need for any labelled dataset containing solutions of differential equations at various points as this model gets its set of actual solutions from the function defining the differential.


---


# 2. Raissi et. al.
## Physics Informed Deep Learning: Data-driven Solutions of Nonlinear Partial Differential Equations
This paper presents *Physics Informed Neural Networks (PINNs)*, which are trained to solve **supervised learning tasks** while respecting any physical law described by a PDE. 

It exploits the Universal Approximation Theorem, i.e. a  feedforward neural network with a single hidden layer and a finite number of neurons can approximate any continuous function and autodifferentiation. These are used to manipulate the parameters of the model and obtain a Physics Informed Neural Network. 

They have created a supervised model which requires labelled data containing solutions at various points over the domain. Such a dataset is obtained using spectral methods to solve the PDEs.

The main goal is to optimize the loss function which is a combination of several terms of *Mean Squared Error* concerning various points over the domain. These terms include error of solutions predicted by the model at the **initial condition**, **boundary conditions** and the function giving the physical information in the form of the value of differential equation at various points of training set. 

This gives excellent results when compared with actual solution plots at various time co-ordinates. They've also tabulated error with respect to number of points used for supervised learning and number of collocation points used for minimizing the differential equation function.

The paper shows examples of this method for Burger's equatoin and Schrodinger's equation.


---


# 3. Moseley et. al.
## Solving the wave equation with physics-informed deep learning
The authors implement the PINN model on 2D acoustic wave equation. 

The labelled data obtained from Finite Difference method and other spectral methods is used to train the model for the boundary and initial conditions

One limitation observed with PINN is that the model has to be trained again for any new constraint.

The model is tested over different values of parameters governing the 2D acoustic equation like density and velocity

The model was able to predict the state of the wave i.e. the solution of the concerned equation accurately and were able to infer many physical phenomena like transmission, reflection, compression and expansion of waves in various interfaces. 


---


# 4. Chengping Rao et. al.
## Physics informed deep learning for computational elastodynamics without labeled data
This is application of PINNs for elastodynamic PDE porblems. 

1. Lagaris et. al.
2. Raissi et. al.
3. Universal Approx theorem
4. Atuodiff
5. Raissi
6. Moseley
7. Guo (1d wave)
8. Rao (elasto)
9. Beck (study)
10. sirignano (DGM)
11. SciANN
12. Tensorflow
13. Keras
14. Numpy
15. RMSprop
16. Matplotlib



Raissi 
	PINN other examples
Moseley et. al.
	PINN on 2d wave eqn
Guo et. al. 
	PINN on 1D wave equation, kdv-burger's eqn, kdv eqn
Rao et. al. 
	elastodynamics
Beck et. al.
	other Deep Learning based approximation techniques
Sirignano et. al. 
	Monte Carlo and other numerical approaches
Haghighat et. al.
	SciANN
