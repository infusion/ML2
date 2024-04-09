# ML2

**Def**: For any finite, non-empty set $S$, called the set of samples, any non empty set $X\neq\emptyset$ called the attribute space and any $x:S\to X$, the tuple $(S, X, x)$ is called unlabeled data.

For any $y:S\to\{0,1\}$ given in addition, the tuple $(S, X, x, y)$ is called labeled data.

**Def**: Let $(S, X, x, y)$ labeled data, $\Theta\neq\emptyset$, $f:\Theta\to\mathbb{R}^X$ (for any $\theta\in\Theta$, $f_\theta:X\to\mathbb{R}$) and $R:\Theta\to\mathbb{R}^+_0$ called a regularizer.

- For any $n\in\mathbb{N}_0$, the instance of the **Separability problem** is to decide if there exists a $\theta\in\Theta$ such that

$$R(\theta)\leq m$$

$$\begin{array}{c}
\forall s\in y^{-1}(1) : f_\theta(x_s)>0\\
\forall s\in y^{-1}(0) : f_\theta(x_s)\leq 0
\end{array}$$

- The instance of the **Separation problem** has the form 

$$\inf\limits_{\theta\in\Theta} R(\theta)$$

subject to 

$$\begin{array}{c}
\forall s\in y^{-1}(1): f(x_s)>0\\
\forall s\in y^{-1}(0): f(x_s)\leq 0
\end{array}$$

- For any $L:\mathbb{R}\times\{0,1\}\to\mathbb{R}_0^+$ called a loss function and any $\lambda\in\mathbb{R}^+_0$ called a regularization parameter, the instance of the **Supervised learning** problem has the form

$$\inf\limits_{\theta\in\Theta} \lambda R(\theta) + \frac{1}{|S|}\sum\limits_{s\in S} L(f_\theta(x_s), y_s)$$

$\lambda = \frac{1}{(|S|+1)R(\hat{\theta})}$

**Example**: For any $r\in\mathbb{R}$ and any $\hat{y}\in\{0,1\}$:

$$L(r, \hat{y})=\begin{cases}
      0, & \text{if}\ (\hat{y}=1\land r>0)\lor (\hat{y}=0\land r\leq 0) \\
      1, & \text{otherwise}
    \end{cases}$$
    
    
 Assumption: $\theta^*$ solves separation. 
 
- $\Rightarrow L=0$ (since constraints are satisfied)
- $\Rightarrow \forall \theta':L=0: R(\theta') =R(\theta^*)$

obj. value of $\theta^*$ for supervised learning

$$\lambda R(\theta^*) + 0 = \frac{R(\theta^*)}{(|S|+1)R(\hat{\theta})}$$

Let $\theta''\in\Theta$ obj. value of $\Theta''$ for 

$$\lambda R(\theta'')+0 = \frac{R(\theta'')}{(|S|+1)R(\hat{\theta})}$$



Def: Let $\Gamma = \left\{(v_0, v_1)\in 2^V\times 2^V : v_0\cap v_1 = \emptyset\right\}$ and $\Theta\in 2^\Gamma$. For any $\theta\in\Theta$, the $f_\theta:\{0,1\}^V\to\{0,1\}$ such that $\forall x\in\{0,1\}^V$

$$f(x) = \bigvee\limits_{(V_0, V_1)\in\theta} \prod\limits_{v\in V_0}(1-x_v)\prod\limits_{w\in V_1}x_w$$

is called the disjuncted normal form defined by $V$ and $\Theta$.

$$R_\ell(\theta) = \sum\limits_{(V_0, V_1)\in\theta} (|V_0|+|V_1|)$$


$$R_\alpha(\theta) = \max\limits_{V_0, V_1}\in\theta |V_0|+|V_1|$$