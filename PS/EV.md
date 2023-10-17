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

## CDF
Recall that if we're given some random variable $X \colon \Omega \to \mathbb R$ on a probability space $(\Omega, \mathcal F , \mathbf P)$ we have an associated function, called the *cumulative distribution function* (CDF), $F_X \colon \mathbb R \to [0,1]$ given by $F_X(y) = \mathbf P(X \leq y)$. 
We also denote the *distribution of $X$* as $\rho_X( (a,b]) = \mathbf P (\{\omega \in \Omega \colon X(\omega)  \in (a,b]\}) $.

*Proposition.* Let $(\Omega, \mathcal F, \mathbb P)$ be a probability space. If two random variables  $X$ and $Y$ have the same CDF, then they have the same distribution, i.e. $\rho_X(B) = \rho_Y(B)$ for any (Borel) measureable subset of $\mathbb R$

*Proposition.* Let $F_X \colon \mathbb R \to [0,1]$ be a CDF of a random variable $X$ on $(\Omega, \mathcal F, \mathbb P)$. Then:
- $F_X$ is an increasing function (not necessarily strictly increasing).
- $F_X$ is right continuous, i.e. for all $y \in \mathbb R$, $\lim_{x \to y^+} F_X(x)  = F_X(y)$