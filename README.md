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

The implementation of this LP in Julia programming language can be found in 
