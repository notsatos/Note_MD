## Expected Value 

If not specified otherwise, we let $(\Omega, \mathcal F, \mathbf P)$ be a probability space. Given a random variable $X \colon \Omega \to \mathbb R$ with $\Omega$ specifically finite, the *expectation of $X$* of defined by 
$$
\mathbf E[X] = \sum_{ z \in \Omega} X(z) \mathbf P (\{z \})
$$
Note that if every $\omega \in \Omega$ has the same probability, say, $p$, then $\mathbf E[X] = \sum_{\omega \in \Omega} X(\omega) \mathbf P( \{\omega \}) = p \sum_{\omega \in \Omega} X(\omega) $.

We can actually expand out this definition to the case where $\Omega$ is countable, i.e., if we write $\Omega = \{x_1, x_2, \ldots \}$, then 
$$\mathbf E[X] = \sum_{i=1}^\infty X(x_i) \mathbf P(\{x_i \}).$$

For example, consider $\Omega = \mathbb Z_{\geq 0 } \subset \mathbb R$, where $X$ is constant with value $1/2$ and the probability of each $n$ integer is $1/2^n$ (actually should check that this is a probability space), then 
$$\mathbf E[X] = \sum_{n \in \mathbb Z_{\geq 0}} X(n)\mathbf P(\{n \}) = \sum_{i \geq 0 } \frac{1}{2^{i+1}} = 2$$

*Example.* Let $\Omega$ consist of all possible outcomes of a single six-sided dice roll. Define $X \colon \Omega \to \mathbb R$ to be the value of the dice roll, which makes $X(\Omega) \subset \llbracket 1,6 \rrbracket $. Then for all $z \in \Omega$ (we're assuming a fair dice), $ \mathbf P (\{z \})=1/6$. Then the expectation of $X$ is given by 
$$ \mathbf E[X] = 1/6(1+\cdots +6)= \frac{1}{6} \frac{6(6+1)}{2} =42/12 = 3.5$$
```
import random 

nums = [1, 2, 3, 4, 5, 6]
count = 0
sum = 0 
for x in range (1,100): 
    count += 1 
    roll = random.choice(nums)
    sum += roll
expected_value  = sum/count 
print(float(expected_value))
```
According to a slightly different language, if $\Omega$ is of size, say, $n$, we can write $X(\Omega) = \{a_1, \ldots, a_n \}$ so that
$$\mathbf E[X] = \sum_{i=1}^n a_i \mathbf P(X=a_i).$$ 
Recall that $\mathbf P(X=a_i) := \mathbf P ( \{ \omega \in \Omega \colon X(\omega) = a_i \})$


*Definition.* The *variance* of a random variable $X$ on $(\Omega, \mathcal F, \mathbf P)$ is given by Var($X$) = $\mathbf E[X^2] - (\mathbf E[X])^2$. The *standard deviation* of $X$ is given by $\sqrt{\text{Var} (X) }$.

## Utilizing Linearity of Expectations 
This a short tidbit on a technique I've seen appear often. The general gist is that if you're trying to find out the expectation of a random variable $Y$, then sometimes it's best to do this by breaking up the random variable $Y$ into indicators (i.e. some sort of random variable that gives binary output). This process is best explained through some examples.


There's even this funny quote, "When I taught a probability class at Dartmouth College in 2013, I tried to convince my
students that linearity of expectation is how you solve all problems in probability."[1]
This is of course in reference to the fact that if $X,Y$ are random variables, then for any $c \in \mathbb R$, $\mathbf E(cX) = c \mathbf E(X)$ and $\mathbf E(X+Y) = \mathbf E(X) + \mathbf E (Y)$.

An observation I made earlier, which is obvious, is that the set of random variables, say, on $\Omega$ forms a $k$-vector space. I believe this should work with all fields $k$, but for simplicity, $k = \mathbb R$. (I also think there should be some restriction on $\Omega$, i.e. it's countable or finite, but I do not want to think about it right now.) This $k$-vector space is just the function space $\mathfrak v (\Omega ) = \mathbb R^{\Omega}$. This observation lets you describe the expectation $\mathbf E $ as a $k$-linear function, $\mathbf E \colon \mathfrak v (\Omega) \to \mathbb R$, $Y \mapsto \mathbf E[Y]$. In fact, a linear functional, i.e. an element in the dual space $\mathfrak v(\Omega)^\ast$. There's a lot to actually be said about $\mathfrak v(\Omega)$, which I will think about later on [2]. 


However, to think about it a little right now, $\mathfrak v(\Omega)$ is finite-dimensional if and only if $\Omega$ is finite (this is part of a more general fact about function spaces of $k = \mathbb R$). Now, by Rank-Nullity, $\dim (\ker (\mathbf E))+\dim (\text{im}(\mathbf E)) = 1$, but as $\text{im} (\mathbf E)$ is a subspace of $\mathbb R$, which is of dimension one, and of course has non-trivial image, we have $\text{im} (\mathbf E) = \mathbb R$, so $\dim (\ker (\mathbf E)) = 0$. Hence we can conclude that if $\mathbf E[X] = \mathbf E[Y]$ for any random variables $X,Y$, we must have that $X=Y$, by using that the kernel must be trivial.


*Exercise.* Suppose we flip a coin 10 times. What is the expected number of heads we get?

*Sol.* Define random variables $Y_i = 0 $ if the $i$-th flip is tails, $1$ if the $i$-th flips is heads. Then $Y = Y_1 + Y_2 + \cdots + Y_{10}$. Then, by linearity, $\mathbf E[Y] = \sum_{i = 1}^{10} \mathbf E[Y_i]$. The great utility of choosing this linearity is that in evaluating $\mathbf E[Y_i]$ we're able to think about the possibilities as binaries. That is, the expected value of $\mathbf E[Y_i] = 1/2 \cdot 1 + 0 \cdot 1/2 = 1/2$. Thus $\mathbf E[Y] = 1/2 \cdot 10 = 5$.

*Exercise.* There is a dinner party where n men check their hats. The hats are mixed up during
dinner, so that afterward each man receives a random hat. In particular, each man gets
his own hat with probability 1/n. What is the expected number of men who get their own
hat?

*Sol.* Define the random variables as $Y_i = 0 $ if the $i$-th person doesn't get their hat back, $1$ if the $i$-th person get their hat back. Then $Y = Y_1 + \cdots + Y_n$ counts the amount of people getting their hat back. We have $\mathbf E[Y_i] = 1/n \cdot 1 + 1/n \cdot 0$. By linearity, we have $\mathbf E[Y]  = \sum_{i = 1}^n \mathbf E[Y_i] = \sum_{i=1}^n (1/n) = n \cdot 1/n = 1$.

*Exercise.* Suppose you have 10 pairs of socks, with each pair being a different color. (So,
maybe you have a red pair, and a yellow pair, and so forth.) You put them all in the washing
machine. The washing machine eats four socks at random. What is the expected value for
the number of complete pairs that make it out alive?

*Sol.* 

## Problems and Solutions

(1) You draw one card from a standard deck of playing cards. If you pick a heart, you will win $10. If you pick a face card, which is not a heart, you win $8. If you pick any other card, you lose $6. Do you want to play? Explain.

Sol. A standard deck of playing cards as 52 cards and 13 distinct card variations. The probability of picking a heart is 13/52, the probability of picking a face which is not a heart is (4 $\cdot$ 3-3)/52 = 9/52. The probability of picking any other card is (52-13-8)/52 = 30/52. Thus the expected value is 
$$ \mathbf E[X] = \frac{13}{52} \cdot 10 + \frac{9}{52} \cdot 8 - \frac{30}{52} \cdot 6 = \frac{130+72-180}{52} > 0, $$
so this is a worthwhile game. 

(2) The world famous gambler from Philadelphia, Señor Rick, proposes the following game of chance. You roll a fair die. If you roll a 1, then Señor Rick pays you $25. If you roll a 2, Señor Rick pays you $5. If you roll a 3, you win nothing. If you roll a 4 or a 5, you must pay Señor Rick $10, and if you roll a 6, you must pay Señor Rick $15. Is Señor Rick loco for proposing such a game? Explain.

Sol. Random variable given by $X \colon 1 \mapsto 25, 2 \mapsto 5, 3 \mapsto 0, 4 \mapsto -10, 5 \mapsto -10, 6 \mapsto -15$. So,
$$\mathbf E[X] = 25 \frac{1}{6} + 5\frac{1}{6} -10 \frac{2}{6} -15 \frac{1}{6} = \frac{30 - 20-15}{6} < 0$$
so Rick is loco for proposing a bad game.

(3)You pay $10 to play the following game of chance. There is a bag containing 12 balls, five are red, three are green and the rest are yellow. You are to draw one ball from the bag. You will win $14 if you draw a red ball and you will win $12 is you draw a yellow ball. How much do you expect to win or loss if you play this game 100 times?

Sol. $X \colon R \mapsto 4, Y \mapsto 2, G \mapsto -10$. We have $\mathbf P (R) =5/12 $, $\mathbf P(G) = 3/12$, $\mathbf P(Y) = 4/12$. Thus 
$$\mathbf E[X] = 4 \frac{5}{12} + 2 \frac{4}{12} - 10 \frac{3}{12} = \frac{20 -8 -30 }{12} = \frac{-2}{12} = -1/6< 0 $$ 
so after 100 games, we expect a loss of $100 (1/6)$, approximately 16.60.

(4) At Tucson Raceway Park, your horse, Soon-to-be-Glue, has a probability of 1/20 of coming in first place, a probability of 1/10 of coming in second place, and a probability of 1⁄4 of coming in third place. First place pays $4,500 to the winner, second place $3,500 and third place $1,500. Is it worthwhile to enter the race if it costs $1,000?

Sol. $X \colon 1 \mapsto 1/20 , 2 \mapsto 1/10, 3 \mapsto 1/4$, and thus, assuming this is a race of consisting of twenty horses, $X(i) = -1000$, with probability 20/20 - $, $i > 3$. Thus $$\mathbf E[X] = 3500 \frac{1}{20} + 2500 \frac{2}{20} + 500 \frac{5}{20} -1000 \frac{8}{20} = \frac{11000-8000}{20}$$


(5) Your company plans to invest in a particular project. There is a 35% chance that you will
lose $30,000, a 40% chance that you will break even, and a 25% chance that you will make
$55,000. Based solely on this information, what should you do?

Sol. $\mathbf  E [X] = -30000\frac{35}{100} + 55000\frac{25}{100} > 0$ so you invest. 

(6) Throw a die. If you win $2 when the number is even and lose $1 when the number is odd, what is the
expected value? If you pay $1 to play the game, will you win in the long run?

Sol. $X  \colon e \mapsto 2, o \mapsto -1$, so $\mathbf E[X] = 3 \cdot 2 \frac{1}{6}  - 3 \cdot \frac{1}{6} = 3/6 = 1/2$.

(7) Someone is using a loaded die. The probability of rolling a “1” is ½ and the rest of the values have equal probabilities. Find the expected
value for rolling this die.

Sol. $\mathbf E[X] = 1 (1/2) + 2(1/6) + 3(1/6) + 4(1/6) = 1/2 + 1/3 + 1/2 + 2/3 = 1 + 1 = 2$.




## References
1. *Linearity of Expectation*, Simon Rubinstein-Salzedo,  https://sanjosemathcircle.org/handouts/2018-2019/20190405_handout.pdf

2. *Vector space of Random Variables*, https://www.randomservices.org/random/expect/Spaces.html
## CDF
Recall that if we're given some random variable $X \colon \Omega \to \mathbb R$ on a probability space $(\Omega, \mathcal F , \mathbf P)$ we have an associated function, called the *cumulative distribution function* (CDF), $F_X \colon \mathbb R \to [0,1]$ given by $F_X(y) = \mathbf P(X \leq y)$. 
We also denote the *distribution of $X$* as $\rho_X( (a,b]) = \mathbf P (\{\omega \in \Omega \colon X(\omega)  \in (a,b]\}) $.

*Proposition.* Let $(\Omega, \mathcal F, \mathbb P)$ be a probability space. If two random variables  $X$ and $Y$ have the same CDF, then they have the same distribution, i.e. $\rho_X(B) = \rho_Y(B)$ for any (Borel) measureable subset of $\mathbb R$

*Proposition.* Let $F_X \colon \mathbb R \to [0,1]$ be a CDF of a random variable $X$ on $(\Omega, \mathcal F, \mathbb P)$. Then:
- $F_X$ is an increasing function (not necessarily strictly increasing).
- $F_X$ is right continuous, i.e. for all $y \in \mathbb R$, $\lim_{x \to y^+} F_X(x)  = F_X(y)$