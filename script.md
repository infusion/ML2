# ML2

**Def**: For any finite, non-empty set $S$, called the **set of samples**, any non empty set $X\neq\emptyset$ called the **attribute space** and any $x:S\to X$, the tuple $(S, X, x)$ is called **unlabeled data**.

For any $y:S\to\{0,1\}$ given in addition, the tuple $(S, X, x, y)$ is called **labeled data**.

**Def**: Let $(S, X, x, y)$ labeled data, $\Theta\neq\emptyset$, $f:\Theta\to\mathbb{R}^X$ (for any $\theta\in\Theta$, $f_\theta:X\to\mathbb{R}$) and $R:\Theta\to\mathbb{R}^+_0$ called a **regularizer**.

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

- For any $L:\mathbb{R}\times\{0,1\}\to\mathbb{R}_0^+$ called a **loss function** and any $\lambda\in\mathbb{R}^+_0$ called a regularization parameter, the instance of the **Supervised learning** problem has the form

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

is called the **disjuncted normal form** defined by $V$ and $\Theta$.

$$R_\ell(\theta) = \sum\limits_{(V_0, V_1)\in\theta} (|V_0|+|V_1|)$$


$$R_\alpha(\theta) = \max\limits_{V_0, V_1}\in\theta |V_0|+|V_1|$$




**Def**.: For any set $S$ and any $\emptyset\notin\Sigma\subseteq 2^S$, the set $\Sigma$ is called a **cover** of $S$ iff 

$$\bigcup\limits_{\sigma\in\Sigma}\sigma=S$$

**Def**.: Let $S$ be any set, $\emptyset\notin\Sigma\subseteq 2^S$ and $m\in\mathbb{N}$. Deciding if there exists a $\Sigma'\subseteq\Sigma$ such that $\Sigma'$ covers $S$ and $|\Sigma'|\leq m$ is called the instance of the **Set-Cover problem** w.r.t. $S, \Sigma$ and $m$.

**Def**.: For any instance $(S', \Sigma, m)$ of SET-Cover, the Haussler Data induced by $(S', \Sigma, m)$ is labeled data $(S, X, x, y)$ such that

$$S=S'\uplus \{1\}$$

$$X = \{0,1\}^\Sigma$$

$$x:S\to X$$

$$\forall s\in S': x_\sigma^S = \begin{cases}
      0, & \text{if } s\in\sigma \\
      1, & \text{otherwise}
    \end{cases}$$

$$x^1 = (1, ..., 1) = 1^\Sigma$$

$y : S\to\{0,1\}$ such that $y_1=1$ and $\forall s\in S':y_s=0$.

Lemma: For any instance $(S', \Sigma, m)$ of SET-Cover, the Haussler Data ($S, X, x, y)$ and any $\Sigma'\subseteq\sigma$:

$$\bigcup\limits_{\sigma\in\Sigma} \sigma=S'\Leftrightarrow\forall s\in S':\prod\limits_{\sigma\in\Sigma'} x_\sigma^s = 0$$

Proof:

$$\begin{array}{rl}
&\bigcup\limits_{\sigma\in\Sigma} \sigma=S'\\
\Leftrightarrow &\forall s\in S'\exists\sigma\in\Sigma:s\in\sigma\\
\Leftrightarrow &\forall s\in S'\exists\sigma\in\Sigma':x_\sigma^s = 0\\
\Leftrightarrow &\forall s\in S' : \prod\limits_{\sigma\in\Sigma'}x_\sigma^s = 0
\end{array}$$


Thm: SET-Cover is polynomially reducible to SEPARABILITY w.r.t. DNFs regularized by depth/length.

Proof: The proof is for $R\in \{R_d, R_e\}$.

Let $(S', \Sigma, m)$ an instance of Set-Cover.
Let $T=(S, X, x, y)$ the Haussler Data w.r.t. $(S', \Sigma, m)$. We show: There exists a cover $\Sigma'\subseteq\Sigma$ of $S'$ with $|\Sigma'|\leq m$ iff there exists a DNF $\theta\in\Theta$ such that $R(\theta)\leq m$ and $\forall s\in S: f_\theta(x^s)=y^s$.

"$\Rightarrow$"  Let $\Sigma'\subseteq\Sigma$ a cover of $s'$ and $|\Sigma'|\leq m$ .

Let $V_0:=\emptyset$ and $\forall V_1=\Sigma'$ and $\Theta=\{(V_0, V_1)\}$.

Thus, $\forall\hat{x}\in X: f_\theta(\hat{x}) = \prod\limits_{\sigma\in\Sigma'} \hat{x}_\sigma$.

Firstly, $\forall s\in S': f_\theta(x_s) = 0$ (by Lemma) and $f_\theta(x^1) = f_\theta(1^\Sigma)=1=y_1$.

Thus, $f_\theta$ decides the Haussler Data correctly.

Secondly, $R(\theta)\leq R_e(\theta) = |\Sigma'|\leq m$.

Hence, $f_\theta$ solves the instance of Separability.

"$\Leftarrow$" Let $\theta\in\Theta$ be a DNF such that $R(\theta)\leq m$ and such that $\forall s\in S: f_\theta(x^s) = y_s$.

There exist $(\Sigma_0, \Sigma_1)\in\Theta$ such that $\Sigma_0=\emptyset$ because $1=y_1=f_\theta(x^1)=f_\theta(1^\Sigma)$.

Moreover,

$\begin{array}{rl}
&\forall s\in S': f_\theta(x^s) = y_s=0\\
&\forall s\in S': \bigvee\limits_{(\Sigma_0, \Sigma_1)\in\theta}\prod\limits_{\sigma\in\Sigma_0}(1-x_\sigma^s)\prod\limits_{\sigma'\in\Sigma_1}x_\sigma^{s'}=0\\
&\forall s\in S': \forall(\Sigma_0, \Sigma_1)\in\Theta:\prod\limits_{\sigma\in\Sigma_0}(1-x_\sigma^s)\prod\limits_{\sigma'\in\Sigma_1}x_\sigma^{s'}=0
\end{array}$

Thus, for $(\emptyset, \Sigma_1)$ in particular:

$\forall s\in S': \prod\limits_{\sigma'\in\Sigma_1}x_{\sigma'}^s=0$

By the lemma: $\bigcup\limits_{\sigma'\in\Sigma_1} \sigma=S'$

Example: $S':=\{a,b,c\}, \Sigma:=\{\{a,b\}, \{c\}, \{a,c\}\}, m:= 2$.

$S=S\uplus \{1\} = \{a,b,c,1\}$
$X = \{0,1\}^\Sigma$

TABELLE VON BLATT






**Def.:** Let $(S, X, x, y)$ labeled data, $\Theta\neq\emptyset$, $f:\Theta\to\mathbb{R}^X$ and $R:\Theta\to\mathbb{R}_0^+$ called **regularizer**

1) For any $m\in\mathbb{N}_0$, the instance of the **partial separability problem** is to decide if there exist $\theta, \theta'\in\Theta$ such that: $R(\theta)+R(\theta')\leq m$

$\forall s\in y^{-1}(1) : f_\theta(x^s) > 0$

$\forall s\in y^{-1}(0) : f_{\theta'}(x^s) > 0$

$\forall \hat{x}\in X : f_{\theta}(\hat{x}) \leq 0\lor f_{\theta'}(\hat{x})$


2) The instance of the **partial separation problem** has the form

$$\inf\limits_{\theta, \theta'\in\Theta} R(\theta)+R(\theta')$$

subject to

$\forall s\in y^{-1}(1) : f_\theta(x^s) > 0$

$\forall s\in y^{-1}(0) : f_{\theta'}(x^s) > 0$

$\forall \hat{x}\in X :f_{\theta}(\hat{x})\leq 0\lor f_{\theta'}(\hat{x})\leq 0$

3) For any $L:\mathbb{R}\times \{0,1\}\to\mathbb{R}_0^+$ called a **loss function** and any $\lambda\in\mathbb{R}_0^+$, the instance of the **supervised partial learning problem** has the form

$\inf\limits_{\theta, \theta'\in\Theta} \lambda(R(\theta) + R(\theta')) + \frac{1}{|y^{-1}(1)|}\sum\limits_{s\in y^{-1}()1} L(f_\theta(x^s), 1) + \frac{1}{|y^{-1}(0)|}\sum\limits_{s\in y^{-1}(0)} L(f_\theta(x^s), 1)$






Recap:

Def: $V\neq\emptyset$ finite. $\Gamma = \{(v_0, v_1)\subseteq 2^V\times 2^V | V_0\cap V_1=\emptyset\}$

$\Theta=2^\Gamma$. For any $\theta\in\Theta$, the DNF defined by $\theta$ is the form 

$$\bigvee\limits_{(v_0,v_1)\in\theta}\prod\limits_{v\in V_0}(1-x_v)\prod\limits_{w\in V_1}x_w$$

Def: For any labeled data $(S, X; x, y)$ with $x=\{0,1\}^V$, $\Theta\neq\emptyset$ and family $f:\Theta:R^X$ and any $R:\Theta\to\mathbb{R}^+_0$, the instance of the PARTIAL SEPARABILITY PROBLEM is to decide if there exists $\theta, \theta'\in\Theta$ such taht the following condition hold:

$$R(\theta) + R(\theta')\leq m$$

$$\forall s\in y^{-1}(1) : f_\theta(x_s) > 0$$

$$\forall s\in y^{-1}(0) : f_{\theta'}(x_s) > 0$$

$$\forall \hat{x}\in X : f_\theta(\hat{x})\leq 0\lor f_{\theta'}(\hat{x})\leq 0$$


Lemma: For any instance $(S', \Sigma, m)$ of SET-COVER, consider the instance of PARTIAL-SEPARABILITY wrt. the family $f:\Theta\to\mathbb{R}^\Sigma$ of DNFs, $R\in\{R_l, R_d\}$ (length und depth regularizer), the Haussler Data $(S, X, x, y)$ and the bound $2m$ (for $R_l$) and $m+1$ (for $R_d$).

1) Then, the function $h:2^\Sigma\to\Theta^2$ such that for any $\Sigma'\subset\Sigma, h(\Sigma')=(\theta,\theta')$ suh that the two conditions hold:

$$\theta:= \{(\emptyset, \{\sigma\}):\sigma\in\Sigma'\}$$

$$\theta':= \{(\Sigma', \emptyset)\}$$

has the following properties:

a) $h(\Sigma')$ is computable in time $O(\text{poly}(|\Sigma'|)$

b) If $\Sigma'$ is a solution to the instance of SET COVER, then $(\theta, \theta')$ (two DNFs) is a solution to the instance of PARTIAL-SEPARABILITY.

2) Moreover, any function $g:\Theta^2\to2^\Sigma$ such that for any $\theta,\theta'\in\Theta$:

$$g(\theta,\theta') = \arg\min\limits_{\{\Sigma'=\Sigma_0',\Sigma_1'\}} |\Sigma'|$$

with $\Sigma_0' = \bigcup\limits_{(\Sigma_0,\Sigma_1)\in\Theta'}\Sigma_0$, (all negated variables in $\theta'$)

$\Sigma_1' \in\{\Sigma_1\subseteq\Sigma | (\emptyset, \Sigma_1)\in\Theta\}$


has the following properties:

a) $g(\theta, \theta')$ is computable in time $O(\text{poly}(R_l(\theta)+R_l(\theta')))$

b) If $(\theta, \theta')$ is a solution to the instance of PARTIAL-SEPARATION, then $g(\theta, \theta')$ is a solution to the instance of SET-COVER.

----------

Let $s\in  S$ such that $y_s=0$ (same as $s\in S'$). Then, $f_{\theta'}(x_s)=\bigvee\limits_{\sigma\in\Sigma'}(1-x_s(\sigma))$.

$\Sigma'$  solves SET-COVER.$\Rightarrow\exists\sigma\in\Sigma':s\in\Sigma$. $\Rightarrow x_s(\sigma)=0$ (by constr. of Haussler Data). Thus, $f_{\theta'}(x_s)=1$. Moreover $f_\theta(1^\Sigma)=0$.

Furthermore: $f_\theta(\hat{x})=\prod\limits_{\sigma\in\Sigma'}\hat{x}(\sigma)$




