# Problem
> Read Deep Learning: An Introduction for Applied Mathematicians. Consider a network as defined in (3.1) and (3.2). Assume that $n_L = 1$, find an algorithm to calculate $\nabla_x{a^{[L]}(x)}$

## Solution
The network in the paper can be defined by:
- Input Layer: $a^{[1]} = x \in \mathbb{R}^{n_1}$
- Hidden Layer: $a^{[l]} = \sigma(W^{[l]}a^{[l-1]} + b^{[l]}) \in \mathbb{R}^{n_l}$
- Output Layer: $a^{[L]} = \sigma(W^{[L]}a^{[L-1]} + b^{[L]}) \in \mathbb{R}$

Define $z^{[l]} = W^{[l]}a^{[l-1]} + b^{[l]}$.

So we rewrite $a^{[l]} = \sigma(W^{[l]}a^{[l-1]} + b^{[l]}) = \sigma(z^{[l]})$

Define $\delta_j^{[l]} = \frac{\partial a^{[L]}}{\partial z_j^{[l]}}$.
- For the output layer ($l = L$):
    Since $a^{[L]} = \sigma(z^{[L]})$, we get $\delta^{[L]} = \sigma'(z^{[L]})$ 
- For the hidden layer $(l = L - 1, ..., 2)$:
Apply the chain rule and after computation, we get
    $\delta^{[l]}=\left(\left(W^{[l+1]}\right)^{T} \delta^{[l+1]}\right) \circ \sigma^{\prime}\left(z^{[l]}\right)$




### Algorithm
1. For $l$ in $2, 3, ..., L$ do
2. Compute $z^{[l]} = W^{[l]}a^{[l-1]} + b^{[l]}$ and $a^{[l]} = \sigma(z^{[l]})$
3. end for
4. Let $\delta^{[L]} = a^{[L]} = 1$
5. For $l$ in $L - 1, L - 2, ..., 1$ do
6. Compute $\delta^{[l]}=\left(\left(W^{[l+1]}\right)^{T} \delta^{[l+1]}\right) \circ \sigma^{\prime}\left(z^{[l]}\right)$
7. end for
8. Output $\nabla_x{a^{[L]}(x)} = \delta^{[1]}$