---
layout: post
title:  Draft pod pairings
date:   2019-08-29 00:00:00 -0700
tags: [magic, math]
math: true
---

![Las Vegas](/assets/draft_pods/las_vegas.jpg)
{:center: style="text-align: center"}
_Las Vegas, the perfect place to stay inside all day and play card games_
[Source: Pixabay](https://www.pexels.com/photo/aerial-photography-of-city-during-evening-161772/)
{:center}

Last weekend, a group of friends and I decided to make the several hour trek to Las Vegas to ....
play [Magic: The Gathering](https://en.wikipedia.org/wiki/Magic:_The_Gathering) at MagicFest Las Vegas.
We didn't sign up for the main tournament, we just went around spending money on cards and fan paraphernalia
and to sign up for some of the side tournaments. Generally, the side tournaments were structured as 8 person
single elimination tournaments with a somewhat top heavy prize distribution.

| Wins | Tickets |
|:-----|:--------|
| 0    | 0       |
| 1    | 20      |
| 2    | 200     |
| 3    | 400     |

One of those friends, Jon, and I decided to sign up for one of the side tournaments together. Another
friend, Eric, didn't want to risk playing with us and decided to sign up for a different event.
Jon and I pondered about this, and figured that perhaps he just wanted to maximize our group winning
potential (or just doesn't like playing with us, who knows really).

Perhaps as a form of karmic justice, Jon and I ended up being paired in the first game.
This guaranteed that one of us would be eliminated with 0 wins and thus leaving with 0 tickets.
I quipped that this also guaranteed us at least one win and some tickets.
Jon was understandably bummed that one of us would be leaving early and our potential for overall
winnings was lessened. Eric was also nearby and remarked at the sad state of our luck before
returning to his tournament to trounce on his opponents.

![Tournament bracket illustration](/assets/draft_pods/tournament_illustration.png)
{:center: style="text-align: center"}
_Comparing potential winnings between matching in the first round vs. matching in the final round_
{:center}


My intuition at the time was that our expected winnings was probably the same either way, and that
perhaps we would even prefer to be matched with each other in the first round for consistency.
But, Eric ended up winning several hundred tickets over the weekend. My victory over Jon in this
game was the only win that either Jon or I got over the weekend. So perhaps Eric was right all along
and we should all be taking advice from him.

But I don't like [focusing too much on what ended up happening](https://en.wikipedia.org/wiki/Outcome_bias).
I prefer to console myself by reasoning about what my expected results should have been. So let's try to
answer the question:

__Would we prefer to get matched in the first round or matched in the finals?__

For my first stab at modeling the problem, I'll assume that everyone at the convention is
about the same skill level so that the probability of anyone winning a particular game is an
even 50% for each player. Under these conditions, it doesn't particularly matter when I face Jon
(or even if face Jon at all!). The probability of me winning a game is a constant 50%.

Let's first consider the expected value of just my winnings. The probability of me winning exactly
0, 1, 2, or 3 games is straightforward to calculate. We just have to
multiply the probabilities of winning the desired amount of games and the probability of losing
the last game if applicable.

| Wins | Tickets | Probability | Weighted Tickets |
|:-----|:--------|:------      |:-----            |
| 0    | 0       | $$P(\text{losing a game})=0.5$$     | 0                |
| 1    | 20      | $$P(\text{winning a game})P(\text{losing a game})=0.5^2$$   | 5                |
| 2    | 200     | $$P(\text{winning a game})^2P(\text{losing a game}) = 0.5^3$$   | 25 |
| 3    | 400     | $$P(\text{winning a game})^3 = 0.5^3$$  | 50 |
|==================================================|
|      | Total/Expected Value | $$1.0$$ | 80 |

So the expected value of tickets I win is 80. Similarly, Jon's expected value of tickets won
is also 80. So what's the expected value of the sum of the tickets won between ourselves if we're
in the same tournament? It turns out that the expectations just add due to the
[linearity of expectation](https://en.wikipedia.org/wiki/Expected_value#Linearity).

$$ E[\text{My tickets} + \text{Jon's tickets}] = E[\text{My tickets}] + E[\text{Jon's Tickets}] $$

So our expected total ticket is 160[^1]. This works even though the amount of tickets we win individually aren't independent!
For example if we were to face each other in the first game, if I were to end up with 20 tickets (or any value more
than 0), then Jon must have 0 tickets. Expected value sums don't care about the individual terms being independent
or not. That's one of the fun properties I remember from college probability, and why my first intuition is that
it all didn't really matter in the first place.

Since the probabilities for winning a single game is constant, the overall expected value is the same whether
we face each other in the first round or if we would only face each other in the final round. Therefore, we
shouldn't really care if we face each other in the first round. Don't believe me? Just try out writing out
all the possibilities and add it up. I'll leave that as an exercise for the reader.

But wait, Magic is a game of skill, _right_?! Otherwise, this game couldn't have lasted
[_over 25 years_](https://magic.wizards.com/en/content/magics-25th-anniversary-25-year-timeline).
If player skills vary such that the win probabilities are dependent on who's playing, then the above calculations break down.
If Jon and I would beat everyone else at the convention, then we would prefer to not face each other
until the finals so we can guarantee getting 600 tickets total. Conversely, if Jon and I can't beat
anyone else at the convention, then we would instead prefer to match with each other in the first game so that
we can walk away with 20 tickets instead of nothing.

Let's assume then that Magic is a game of pure skill and that all players can be ordered in a line such that players
will beat everyone else behind them in the line 100% of the time. We can then represent player
skill as the percentage of players they would beat in a game of magic. The tournament is then seeded with Jon,
I, and 6 other randomly chosen players.

Let $$x$$ be my skill and $$y$$ be Jon's skill. That is, I would beat a randomly chosen
person with probability $$x$$ and Jon would beat a randomly chosen person with probability $$y$$.
For the sake of not duplicating logic, let's also assume that $$ x > y $$. I _did_ beat Jon after all
in this tournament. However, similar logic follows in the case of $$ x < y $$.

![Skill Line](/assets/draft_pods/skill_line.png)

In this setting, the probability of winning does change when and if I face Jon. So let's first
consider the case where we match up in the first round. I am guaranteed to win the first round.
In the 2nd game, I would have to beat the winner of 2 random people. Generally speaking, this winner
has higher skill than a random person because this winner beat someone else. I would beat this winner
if and only if I would have been able to beat both of them, that is my skill is greater than the max skill
of the 2 players. If those 2 players have skills $$z_1$$ and $$z_2$$ respectively:

$$
\begin{align*}
  P(x > max(z_1, z_2)) &= P(x > z_1\text{ and }x > z_2) \\
                       &= P(x > z_1)P(x > z_2) \\
                       &= x^2
\end{align*}
$$

So I would win that game with probability $$x^2$$. Similarly, if I make it to the third game, I would
have to beat the best player out of 4 randomly chosen people. The probability of me winning the final
game if I reach it is then $$x^4$$.

Overall, my expected value for tickets in the case of being matched with Jon in the first round is

| Wins | Tickets | Probability | Weighted Tickets |
|:-----|:--------|:------      |:-----            |
| 1    | 20      | $$ 1 - x^2 $$   | $$ 20*(1-x^2) $$   |
| 2    | 200     | $$ x^2*(1 - x^4) $$ | $$ 200*x^2*(1-x^4) $$ |
| 3    | 400     | $$ x^2*x^4 $$ | $$ 400*x^2*x^4 $$  |
|==================================================|
|      | Total/Expected Value | $$1$$ | $$20 + 180 x^2 + 200 x^6$$ |

Since Jon is guaranteed is to lose the first game and get 0 tickets, this is our overall expected
value of total tickets.

$$
  E[\text{total tickets if matched in the first round}] = 20 + 180 x^2 + 200 x^6
$$

Now let's consider the case where we would only face each other in the finals. I will win the
first game with probability $$x$$. For the second game, I would need to beat the better of 2 random
players and win with probability $$x^2$$. For the third game, I would need to beat the best
of 3 random players and Jon. Since I'm already better than Jon, this is the same of me beating the best of
3 random players, so the probability of me winning the 3rd game is $$x^3$$. My expected value of tickets
in the case of meeting Jon only possibly in the finals is:

| Wins | Tickets | Probability | Weighted Tickets |
|:-----|:--------|:------      |:-----            |
| 0    | 0       | $$ 1 - x $$   | $$ 0 $$   |
| 1    | 20      | $$ x*(1 - x^2) $$   | $$ 20 * x*(1-x^2) $$   |
| 2    | 200     | $$ x*x^2*(1 - x^3) $$ | $$ 200*x*x^2*(1-x^3) $$ |
| 3    | 400     | $$ x*x^2*x^3 $$ | $$ 400*x*x^2*x^3 $$  |
|==================================================|
|      | Total/Expected Value | $$1$$ | $$ 20 x + 180 x^3 + 200 x^6  $$ |

Similarly, in the first round, Jon would have to beat a random player with probability y. Then if he reaches
the second round, he needs to beat the better of 2 random players with probability y^2. If Jon wins 2 rounds,
then he would have to face me or someone who is better than me, so he has no chance of winning the final round.
Jon's expected tickets in the case he doesn't have to face me until the finals is:

| Wins | Tickets | Probability | Weighted Tickets |
|:-----|:--------|:------      |:-----            |
| 0    | 0       | $$ 1 - y $$   | $$ 0 $$   |
| 1    | 20      | $$ y*(1 - y^2) $$   | $$ 20 * y*(1-y^2) $$   |
| 2    | 200     | $$ y*y^2 $$ | $$ 200*y*y^2 $$ |
|==================================================|
|      | Total/Expected Value | $$1$$ | $$ 20 y + 180 y^3 $$ |

With linearity of expectation, we can just add these expected values to get the expected total

$$
    E[\text{total tickets if possibly matched only in the final round}] = 20 x + 180 x^3 + 200 x^6 + 20 y + 180 y^3
$$

So when do we want to be matched up only in the final round? That's when the expected value of tickets
of being matched only in the final round exceeds the expected value of tickets of being matched in the first round.

$$
\begin{align*}
20 x + 180 x^3 + 200 x^6 + 20 y + 180 y^3 &> 20 + 180 x^2 + 200 x^6 \\
                           y * (20 + 180 y^2) &> (1-x)*(20 + 180 x^2)   \\
\end{align*}
$$

The left side is the expected value of tickets that Jon gets trying to win tickets on his own. The right side represents
the marginal expected tickets I get if I get a free win from Jon compared to if I had to beat
a random person in the first game[^2]. So we would prefer to not be matched with each other if we believe that
Jon would get more tickets by himself than we would if he gives me a free win.

We can graph over the valid values for $$x$$ and $$y$$ to get a better understanding of when this happens

![Expected Value Difference Graph](/assets/draft_pods/graph1.png)

As expected, around $$(1, 1)$$, we would prefer to match at the final round to maximize winnings.
Around $$(0, 0)$$ we would prefer to match up in the first round to take the free win. What was interesting
to me was the behavior when Jon is a below average player. There's a large area where even if I was pretty good,
I would still prefer to match with Jon in the first round because we get more tickets overall if I get a free win
compared to leaving Jon to try to win tickets on his own. It's only when I get closer to
elite skill levels that I don't get as much value taking the free win from Jon than Jon would get winning
tickets on the other side of the bracket. However, when Jon is an above average player, also implying that I am
an above average player as well, we would prefer to split up in the bracket the vast majority of the time.

In conclusion, if you and a friend sign up for a MagicFest side tournament to get as much tickets as possible
and both of you are above average players, then you would prefer to get seeded in separate sides of the tournament bracket.
Otherwise, if _either_ of you are below average players, then it's likely you want to pair up in the first round
instead! [Since everyone believes they're an above average player](https://en.wikipedia.org/wiki/Dunning%E2%80%93Kruger_effect),
this means that everyone should want to match up on opposite sides of the bracket.

Now I'm ignoring the fact that Magic isn't quite a game of pure skill, so there's room for allowing
for differing player skill affecting win probabilities, which would allow Jon to win games against
me and perhaps change the overall calculus. But that's an exercise for perhaps another day.

[^1]:
    I could have also reached this result by noting that the total tickets won in the tournament
    is 640 and that each of the 8 participants have equal probabilities of reaching any result. So the
    expected value of winnings per participant is $$640/8 = 80$$. But this approach extends better to
    the rest of this writing.

[^2]:
    The $$200x^6$$ terms disappears because it shows up in both sides. It's related to the marginal
    additional tickets of me making to and playing the final game. Regardless of whether I face Jon in the first game or in
    the finals, I end up having to be better than 6 random people to get to and win in the finals.