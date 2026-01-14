# Signaling Local Hidden Variable Model


The no-signalling principle is a fundamental assumption in Bell-inequality experiments. Nonetheless, experimental imperfections lead to apparent signalling beyond what is expected from finite-sample statistics. 
In the paper [Link], we propose a modified signalling local hidden variable model (SLHV) that allows bounded and operationally quantifiable amounts of signalling 


$$
p(a,b|x,y)=\sum_{\lambda} q_{\lambda} D^A_{\lambda}(a|x,y) D^B_{\lambda} (b|x,y)
$$

where $\lambda$ is a local hidden variable distirbuted according to $q_{\lambda}$ and $D^{A}_{\lambda}$ is the deterministic assignment the maps the outcome $a$ to settings $x$ and $y$ and similarly for Bob. 

The average ontological amount of signalling for Alice and Bob is is bounded by the set of signalling parameters $\alpha^{ax}\_{yy’}$  and $\beta^{by}\_{xx’}$

$$
\begin{align}\nonumber
&\sum_{\lambda} 	q_{\lambda} |D^A_{\lambda}(a|x,y)-D^A_{\lambda}(a|x,y') | \leq \alpha^{ax}_{yy'}, \\
&\sum_{\lambda} 	q_{\lambda} |D^B_{\lambda}(b|x,y)-D^B_{\lambda}(b|x',y) | \leq \beta^{by}_{xx'},
\end{align} 
$$

The membership of a given distribution $p(a,b|x,y)$ to such SLHV model can be determined by the following linear program (LP) 


$$
\begin{aligned}
		&\max _{ \{ q_{\lambda} \} } &&\quad v \\
		&\text{s.t.} && \quad v\ p(a,b\lvert x,y) + \frac{1-v}{n_{A}n_{B}} = \sum_{\lambda} q_{\lambda} D^{A}_{\lambda}(a|x,y)D^{B}_{\lambda}(b|x,y) \quad \forall a,b,x,y, \\
		&  && \sum_{\lambda} q_{\lambda}=1,\\ 
		& && q_{\lambda}\geq 0 \quad \forall \lambda, \\
		& && \sum_{\lambda} q_{\lambda} |D^{A}_{\lambda}(a|x,y) -D^{A}_{\lambda}(a|x,y')|\leq \alpha^{ax}_{yy'} \quad \forall a,x,y,y', \\
		& && \sum_{\lambda} q_{\lambda} |D^{B}_{\lambda}(b|x,y) -D^{B}_{\lambda}(b|x',y)| \leq \beta^{by}_{xx'} \quad \forall b,y,x,x'.\\
	\end{aligned}
$$

The linear program calculates the white-noise visbility $v$ of the distribution, if $v<1$ the distribution does not belong to the SLHV.

The implementation of this LP in Julia programming language can be found in the file Important_functions.jl. 

The function **calculate_visibility** takes as an input the probability distribution and the allowed signalling parameters $\alpha$, $\beta$ and returns as an output the visibility $v$. It is optional to provide the determinstic strategies for the function as the function is programmed to calculate them automatically if not provided. 

Furthermore, we provide and implementation of the Dual LP 

$$
	\begin{aligned}
		&\min_{\{c_{abxy}\}, \mu, \atop
				\{d_{axyy'}\},\{ e_{byxx'}\}} && 1-\mu +\sum_{a,b,x,y} c_{abxy} p(a,b|x,y)+ \sum_{a,x,y,y'} d_{axyy'} \alpha^{ax}_{yy'} + \sum_{b,y,x,x'} e_{byxx'} \beta^{by}_{xx'} \\
		&\text{s.t.} && \\
		&&& 1 + \sum_{a,b,x,y} c_{abxy} \left(p(a,b\lvert x,y) - \frac{1}{n_{A}n_{B}}\right) = 0, \\ 
		&&& \sum_{a,b,x,y} c_{abxy} D^{A}_{\lambda}(a|x,y) D^{B}_{\lambda}(b|x,y)   \quad + \sum_{a,x,y,y'} d_{axyy'} R^{ax}_{yy'\lambda} + \sum_{b,y,x,x'} e_{byxx'} T^{by}_{xx'\lambda} \geq \mu \quad \forall \lambda ,  \\
		&&& d_{axyy'} \geq 0 \quad \forall a,x,y,y', \\
		&&& e_{byxx'} \geq 0 \quad  \forall b,y,x,x',
	\end{aligned}
$$

The implementation can also be found in the file Important_functions.jl. The function calculate_visibility_dual takes the same input as calculate_visibility but returns on top of $v$, the coefficients $c_{abxy}$, $d_{axyy’}$ and $e_{byxx’}$ and the parameter $\mu$. Those can be used to construct inequalities for the SLHV model when $v<1$.

