---
title: Computationally understanding Einstein's field equation in 1 hour. 
category: Physics 
excerpt: |    
  This post is trying to explain how to unwrap the Einstein's field equation into simple differential equations.  
feature_image: "https://unsplash.it/1300/400?random"
---

This post is trying to explain how to unwrap the Einstein's field equation into simple differential equations. When I studied general relativity, I spent quite some time in the geometrical structures instead of the physical signification, and I want to summarize the mathematical details here in the bottom-up way.   

<!-- more -->

So when you open Wikipedia and clicked into the page of [General Relativity](https://en.wikipedia.org/wiki/General_relativity) , the first equation you will encounter is the Einstein's field equations:

$$
G_{\mu\nu} \equiv R_{\mu\nu}-\frac{1}{2}R g_{\mu\nu}=\frac{8\pi G}{c^4}T_{\mu\nu}
$$

If you have the same background knowledge as I did, then probably you immediately recognize the $$G$$ and $$c$$ constants, but wtf are the other symbols with subscripts? And if you open an orthodox  GR textbook, you will probably revisit the equation in 8+ chapters, if you still haven't gotten lost in the first 7 chapters.  

 Well, totally understandable.  
 
 Having gone through all the obstacles(probably not entirely useless) and struggled with all the mathematical details, I want to take down these when I still remember them, at least as a refresher in the future.  
 
 So it's obvious, we need to know how $$R_{\mu \nu}$$, $$g_{\mu \nu}$$  and $$T_{\mu \nu}$$ looks like. $$R$$ in the equation may seem familiar, but it is actually a scalar variable derived from the $$R_{\mu \nu}$$ instead of radius. In summary, we need to know how to represent the three monsters.  
 
##### Preliminary:Building Platforms and Webtools  
  
###### Building Platforms:  
  
[Linux System](http://www.linuxandubuntu.com/home/10-basic-linux-commands-that-every-linux-newbies-should-remember)  Useful commands.

[Tensorflow](https://www.tensorflow.org/install/ "Tensorflow")  
Open-source machine-learning platform. Dependent Language: Python [Free]  
[PyTorch](http://pytorch.org/ "PyTorch")  
Succint and trouble-free building platform. Dependent Language: Python [Free]  
[C++](http://www.mlpack.org/)  
ML library written in C++. [Free]  
[Matlab](https://www.mathworks.com/solutions/machine-learning.html) / [MatConNet](http://www.vlfeat.org/matconvnet/)   
Using Matlab to build ML network.  [May be paid]  

[Python-Tutorial](https://www.liaoxuefeng.com/ "递归函数 - 廖雪峰的官方网站")  
A comprehensive website for python beginners.

###### Useful webtools:

[Github](https://github.com/) --[Github-Installation](https://www.howtoforge.com/tutorial/install-git-and-github-on-ubuntu-14.04/) / [Github-Usage](http://www.ruanyifeng.com/blog/2014/06/git_remote.html)    
Amazing collaborate platform, and good place to store your code.   
[Google VM](https://cloud.google.com/) -- [VM-Setup](https://haroldsoh.com/2016/04/28/set-up-anaconda-ipython-tensorflow-julia-on-a-google-compute-engine-vm/) / [GUI Support](https://medium.com/google-cloud/graphical-user-interface-gui-for-google-compute-engine-instance-78fccda09e5c)  
Three hundred dollars worth of credits free to use. But GPU is not supported then.  
[Notepad++](https://notepad-plus-plus.org/) --[Notepad++ -Plugin](https://sites.google.com/site/fstellari/nppplugins "Autofill and Autosave")  
Free editing software with multi-functional hightlight.  

##### Machine Learning  
  
[Machine Learning](https://see.stanford.edu/Course/CS229)   
Understand the basic concepts and category of machine learning.  
[Artificial Neural Network](http://pages.cs.wisc.edu/~bolo/shipyard/neural/local.html)  
Grasp some basic ideas about the composition of ANN.  
[Neural Network Playground](http://playground.tensorflow.org/)  
Have fun with the interactive design!   
[ANN](https://algobeans.com/2016/03/13/how-do-computers-recognise-handwriting-using-artificial-neural-networks/)  
A more user-friendly introduction with multiple illustrations.  

[Visualizing Backpropagation](http://colah.github.io/posts/2015-08-Backprop/)  
Understand backpropagation's core issue: partial derivative.   
[Visualizing Backpropagation - Part Two](https://mattmazur.com/2015/03/17/a-step-by-step-backpropagation-example/)  
Step-by-step backpropagation with numbers.  
[Visualizing optimizers](https://mattmazur.com/2015/03/17/a-step-by-step-backpropagation-example/)  
You may refer to individual papers for detailed explanation.    
[MNIST using ANN](https://www.tensorflow.org/get_started/mnist/beginners)  
Auxiliary Notes. Be sure to try running real programs!  
[Tensorboard Readme](https://github.com/tensorflow/tensorflow/blob/r1.1/tensorflow/tensorboard/README.md)  
Visualizing and monitoring the training process.  

  