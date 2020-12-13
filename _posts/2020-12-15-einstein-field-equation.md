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
 
 ##### From scalars to tensors  
 
 So it's obvious, we need to know how $$R_{\mu \nu}$$, $$g_{\mu \nu}$$  and $$T_{\mu \nu}$$ looks like. $$R$$ in the equation may seem familiar, but it is actually a scalar variable derived from the $$R_{\mu \nu}$$ instead of radius. In summary, we need to know how to represent the three "monsters".   
 
 Let's talk about their variations from a scalar function, step by step. Firstly, what the $$\mu \nu$$ represent? They are just indices from$$\{0 1 2 3\}$$, where 0 represent the "time" component, and 1 to 3 is the "space component". The slightest variation from a scalar function is a vector function, say $$U_{\mu}$$, which is the four-velocity of a particle. It is worth knowing that the two variables follow Einstein's notation, and when you see two identical indices(presumably one lower, one upper as explained next), they represent the summation of all the four possible cases.   
  
 Next, The lower and upper location. This is why it is called a (0-2) tensor, instead of just a matrix: The minimum amount of rules you need to know includes that,  

     (1) In GR, the symbols appearing in the super-scripts(sub-scripts) should match exactly those on the other side of the equation, expressions with different structures cannot be equal(0 can be any structure).   

     (2) Symbol with a super-script behaves like the coordinate function, like $$x^{\mu}$$. That with a lower-script is a one-form. (No need to shift your focus to it if you haven't learnt it.). 

     (3) If you need to move a symbol downward, you need to multiply the tensor by the metric tensor $$g_{\mu\, \nu}$$, that is, $$F^{\mu}_{\gamma} g_{\mu \nu}=F_{\nu \gamma}$$. (The sequence matters, but we will ignore it here.)   

     (4)(Optional) You can contract a tensor by having another tensor with symbol in the other-script. Such as, $$T_{\mu\nu}U^{\mu}V^{\nu} $$ is the inner product of the T-matrix with the two column vectors.   

 To visualize the tensor(say the (0-2) case), you can somewhat understand it as a bundle of 16 scalar functions. It can be seen as picking the corresponding $$\mu\, \nu$$ in the row vector shown below sequentially, and also in the corresponding $$U^{\mu}V^{\nu} $$ column vector, and add up all variations. From this we can see why the super/sub-script matters.

Pic 1

##### The metric and the stress-energy tensor  
 
 Before getting into the pure mathematical definition, let's get a little knowlege about the two symbols $$g_{\mu \nu}$$ and $$T_{\mu \nu}$$

  

  