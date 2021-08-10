# Distribution Derivation

# Exponential Family 
Q1 Suppose that an airplane engine will fail, when in flight, with
probability 1−p independently from engine to engine; suppose that the airplane will 
make a successful flight if at least 50 percent of its engines remain operative. 
For what values of p is a four-engine plane preferable to a two-engine plane?\
Answer\
$ {4 \choose 2}p^2(1-p)^2+{4 \choose 3}p^3(1-p)^1+{4 \choose 4}p^4(1-p)^0	\geq {2\choose 1}p(1 − p) + {2 \choose 2} p^2 \implies	p\geq2/3$\
Q2 Calculate Var(X) when X represents the outcome when a fair die is rolled\
Answer\
$E(X)=7/2, E(X^2)=91/6, Var(X)=91/6-(7/2)^2=35/12$\
Q3 If i = 4, find the probability that a total of 7 games are played. Also show
that this probability is maximized when p = 1/2\
Answer\
$P(7 games)={6 \choose3}p^3(1-p)^3 $\
$dp(7)/dp=60p^2(1-p)^2(1-2p) \implies p=1/2$



# Disease/Quality Test
A laboratory blood test is 95 percent effective in detecting a
certain disease when it is, in fact, present. However, the test also yields a “false
positive” result for 1 percent of the healthy persons tested. (That is, if a healthy
person is tested, then, with probability 0.01, the test result will imply he has the
disease.) If 0.5 percent of the population actually has the disease, what is the
probability a person has the disease given that his test result is positive?\
Answer\
$(0.95*0.005)/[(0.95+0.005)+(0.01)(0.995)]=95/294$

# Herebity
In a certain species of rats, black dominates over brown. Suppose that a
black rat with two black parents has a brown sibling.
(a) What is the probability that this rat is a pure black rat (as opposed to being
a hybrid with one black and one brown gene)?
(b) Suppose that when the black rat is mated with a brown rat, all five of their
offspring are black. Now, what is the probability that the rat is a pure black rat?
Answer\
(a) P(2 black genes | at least one black gene)=$(1/4)/(3/4)=1/3$\
(b) P(2 black genes | 5 black offspring)=$(1/3)/[1(1/3)+(1/2)^5(2/3)]$
