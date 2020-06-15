---
layout: post
title: Girl's Frontline Bingo Math
date: 2020-06-12 00:00:00 -0700
tags: [math, probability, girls_frontline, gacha]
math: true
---

![GFL AR TEAM](/assets/gfl/ar_team.jpg)
{:center: style="text-align: center"}
_Just cute girls with guns doing cute things. No crippling depression, PTSD, and implications of sexual abuse to see here._
[Source: GFL presskit](https://www.igdb.com/games/girls-frontline/presskit)
{:center}

About 3 months ago, I wanted to get into gacha games to understand why they are so popular. Gacha games
are named after Japanese vending machines called "Gachapons" that disperse random capsule toys. Their
defining characteristic is a lottery to obtain additional characters, costumes, etc. It's a mechanic
that you'll also see in other types of games nowadays as well, in the form of loot boxes or booster packs, but
the lottery is a big part of the experience in a gacha game. Gacha games have somewhat of a reputation that
they're money sinks, because rolls can be obtained via real money and getting what you really want typically
requires a lot more rolls than you can get for free.

<figure class="video_container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/uhgaRckDObQ?start=18"
          frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
          allowfullscreen>
  </iframe>
</figure>
{:center: style="text-align: center"}
_Watching other people go into the pits of gacha hell might be funner than actually doing it yourself. At the very
least, it's healthier for your wallet._ [^1]
{:center}

I had decided on a game called ["Girls Frontline"](https://en.wikipedia.org/wiki/Girls%27_Frontline), and I've been playing it ever since. In this game,
you are collecting android girls called "T-dolls", each representing a particular gun model, and sending them off
into battle in a post-apocalyptic world. There's a character for every anime trope you can think of, so everyone
can find something they like. For example, there's a mother-like model that represents the [M1903 Springfield](https://en.gfwiki.com/wiki/Springfield),
a sleepyhead model that represents the german [G11](https://en.gfwiki.com/wiki/G11), a [tsundere](https://www.urbandictionary.com/define.php?term=Tsundere)
[sniper rifle](https://en.gfwiki.com/wiki/WA2000),
and [a](https://en.gfwiki.com/wiki/M4A1) [whole](https://en.gfwiki.com/wiki/M16A1) [entire](https://en.gfwiki.com/wiki/ST_AR-15)
[team](https://en.gfwiki.com/wiki/M4_SOPMOD_II) representing just the M4/M16 weapon platform. [^2].

If you're into collectathons, cute girls, guns and/or post-apocalyptic war torn worlds, I recommend at least giving
the game a try. It's "free" after all (just be responsible with your money spending). But I'm not writing here to tell you
to play this game. I'm writing about a question that popped into my head while playing the game,
and the (over-)application of mathematics I went through to answer said question.

As of this writing, Girl's Frontline is running an "bingo event". There is a 6x6 grid of numbers, and you can earn
random pull tickets by doing missions that refresh daily. The numbers you pull are marked on your grid, and you
earn prizes each time you mark all the numbers on a line. You also earn bonuses if you reach thresholds of
the number of completed lines. The max bonus threshold is 14 lines, which can only be obtained if you mark the
entire grid (6 horizontal lines, 6 vertical lines, and 2 diagonal lines).

![Bingo Card](/assets/gfl/gfl_bingo.png){: style="margin: 0 auto; display: block"}
{:center: style="text-align: center"}
_My current bingo grid. Most of it is filled out and only 7 numbers remain. I've also filled out 3 lines._
{:center}

One quirk is that the random numbers can _repeat_. So you start off marking off the grid really quickly.
But later when you have half the grid filled, you'll find yourself getting repeat numbers over half the time.
This may seem like the classic tactic of hooking people in early just to upcharge them later when they're committed,
like how a drug dealer deals with addicts. But one can't even buy more tickets with cash, so I
can't even throw my money at it even if I wanted to! So naturally I wondered what my chances were to fill
in the whole grid by the time the event closes. If it was impossible to luck into filling the entire grid, then perhaps
I could do better things with my pulls like exchanging the pulls for other prizes directly.

## Using geometric distributions to get an average number of pulls

Let's ignore the bingo lines since I'm just interested in the time it takes to fill out the whole grid.
The question I'm then asking is:

**Given a set of 36 numbers, how many random pulls (with replacement) does it take draw each number at least once?**

Let's first look at smaller examples.

What if there's only 1 number to mark? The answer is clearly 1 pull.

So what if there's 2 numbers to mark? The number of pulls necessary is now a random number, which can vary from 2
at the luckiest, to arbitrarily large if you're really unlucky picking the same number repeatedly until you finally pick up the
second number. We can break the number of pulls down into two parts, the number of pulls it takes to get one
number (it doesn't matter which one), and then the number of pulls it takes to get the other one. The first part
is the amount of pulls it takes to get one of 2 out of 2 numbers, and the second part is the amount of pulls it takes
to get one of 1 out of 2 numbers.

$$
\begin{align}
    T(\text{Mark all 2 numbers}) &= T(\text{Mark any of 2 out of 2 numbers}) + T(\text{Mark any of 1 out of 2 numbers}) \\
    T'(2, 2)                     &= T(2, 2) + T(1, 2) 
\end{align}
$$

I introduced shorthand notation $$T(k, t)$$ to denote the time it takes to pull any one of $$k$$ out of $$t$$ numbers, and
$$T'(k, t)$$ as the total time it takes to pull $k$ unique numbers from $$t$$ numbers. $$T(k, t)$$
is a random number itself, so what is its distribution? Clearly $$T(2, 2)$$ is 1 with probability 1 (similarly for
any $$T(t, t)$$ for any $$t$$). Once $$ k < t $$ though, the time needed can vary randomly.

Let's consider $$T(k, t)$$, the time it takes to get any of k target numbers out of t total numbers. With probability $$k/t$$,
you will get a target number and the process ends. With probability $$(1 - k/t)$$,
you miss and you need to keep going. So for $$T(k, t)$$ to be exactly $$n$$ (that is, you needed exactly $$n$$ pulls
to get any one of $$k$$ target numbers of $$t$$ total numbers), you need to have missed on $$(n-1)$$ pulls and then finally
hit a target on the last pull. The probability of this happening is $$(1 - k/t)^{n-1}(k/t)$$.

So we have:

$$
    P(T(k, t) = n) = (1 - k/t)^{n-1}(k/t)
$$

If you're familiar with probability distributions, this is a [geometric distribution](https://en.wikipedia.org/wiki/Geometric_distribution) where the probability of a success is $$k/t$$.
The number of pulls it takes to fill out all 2 numbers turns out to be the sum of two random variables with geometric distributions.

We can extend this reasoning to the original problem of filling out a grid of 36 numbers. First, we have to hit any of 36 of 36 numbers.
Then we have to hit any of the remaining 35 of 36 numbers which takes time according to a geometric
distribution with success rate $$35/36$$. We repeat this process until we're left with trying to hit the last 1 of 36 numbers with a success
rate of just $$1/36$$ numbers.

We now have this breakdown of time it takes to fill out all 36 numbers as a sum of 36 random variables with geometric distributions.

$$
    T'(36, 36) = T(36, 36) + T(35, 36) + T(34, 36) + \ldots + T(2, 36) + T(1, 36)
$$

From here, it's pretty easy to get the average number of pulls necessary to fill the grid. The average of a sum of random variables
is the sum of the averages of those variables, by [linearity of expectation](https://en.wikipedia.org/wiki/Expected_value).

$$
    E[T'(36, 36)] = E[T(36, 36)] + E[T(35, 36)] + E[T(34, 36)] + \ldots + E[T(2, 36)] + E[T(1, 36)]
$$

The expected value of a geometric distribution with success rate $$p$$ is $$1/p$$. So $$E[T(n, t)] = t/n$$. We then have:

$$
\begin{align}
    E[T'(36, 36)] &= E[T(36, 36)] + E[T(35, 36)] + E[T(34, 36)] + \ldots + E[T(2, 36)] + E[T(1, 36)] \\
                  &= 36/36 + 36/35 + 36/34 + \ldots + 36/2 + 36/1 \\
                  &\approx 150.28
\end{align}
$$

![Expected number of pulls](/assets/gfl/pulls_expectation_line.jpg){: style="margin: 0 auto; display: block"}
{:center: style="text-align: center"}
_A visual representation of the time it takes to pull all 36 numbers. Drawn to scale of perceived time wasted due to just
drawing repeat numbers again and again._
{:center}

So it takes about 150 pulls on average to fill the entire 6x6 grid. The event runs for 21 days, and each day you can earn 9 pulls,
for a total of 189 pulls. So it seems that we have more than enough pulls available to be more likely than not to fill the entire grid.
But what is the actual probability of filling the entire grid assuming by the end of the event?

## Figuring the probability of filling the grid by some number of pulls

The question of the probability of filling the entire grid within some number of pulls $$m$$ is $$P(T(\text{Mark all 36 numbers}) \leq m)$$.
If we first tackle the question of the probability of getting it in exactly $$n$$ pulls, ($$P(T(\text{Mark all 36 numbers}) = n)$$), then
we can add the probabilities for exact pull times for up for all values $$n \leq m $$.

The probability distribution of sums of non-identically distributed random variables is rather annoying. Generally you have to go
through all possible way to split up the target value and add up a joint probability for each split.

Something horrendous like:

$$
    P(T'(36, 36) = n) = \sum_{\substack{n_1, n_2, \ldots, n_{36}}\\
                                                           n_1 + n_2 + \dots + n_{36} = n}
                                            P(T(36, 36) = n_1)*P(T(35, 36) = n_2)*\ldots*P(T(1, 36) = n_{36})
$$

I don't know if there's an easier way to express this. So instead, I made a program to calculate this value directly.
Conceptually, I broke down the formula into a recursion that starts with the base case of drawing just the first number, and then
builds up the calculation one step at a time using the value from accumulating up all the previous steps.

For example, let's say that we want to calculate the probability of the number of pulls to draw 36 numbers being $$n$$. Then for every way to
split up $$n$$ into two parts $$n_1$$ and $$(n-n_1)$$, we combine the probability of getting the first 35 numbers in exactly $$n_1$$ pulls
with the probability to get the 36th number in $$(n-n_1)$$ pulls. To get the probability getting the first 35 numbers in exactly $$n_1$$ pulls,
we would do a similar calculation, splitting up into all ways to get the first 34 numbers in some times and then the 35th number at the $$n_1$$
pull. And so on, so forth until we get to only 1 number which we already know to be a binomial distribution.

Here's the recursion in formulas:

$$
\begin{align}
    P(T'(1, 36) = n) &= P(T(36, 36) = n) \\
    P(T'(k, 36) = n) &= \sum_{n_1=1}^{n-1} P(T'(k-1, 36) = n_1) * P(T(36-k+1, 36) = n - n_1)
\end{align}
$$

Here's the [code](https://github.com/laganojunior/lalaheadpats_code/blob/master/gfl/bingo.py) if you want to see it. The probability of filling in the grid by 189 pulls turns out to be around 83.69%. This feels pretty
good, but there's still about a 1/6 chance that we might not fill the grid.

## Taking the pity system into account

Many gacha games have pity systems that alleviate the "feels bad" part of random draws, by giving you points per pull that you can trade in for what
you really want. In this bingo event, every single time you draw a repeat number, you get a pity point. With 10 pity points, you can pity pull
(for free!) whatever number you want. [^3]

From the previous section, we saw that we would need 150 pulls on average to fill the grid naturally. Since there's only 36 numbers, that's
114 extra pulls that would convert to pity points for about 11 targeted pity pulls along the way. It seems obvious that this should reduces
the number of pulls we need to fill the grid and increase the probability that we can fill the grid by the end of the event. But by how much
does the pity system help?

Let's assume we save our pity points until we collected enough pity points to fill out the remaining numbers, as opposed to spending the pity points
on random numbers along the way.

Suppose we've pulled enough unique numbers and enough pity points to finish the grid at exactly $$n$$ pulls. There are 2 cases:

* The last pull was a new number, and then we had enough pity points to pay for the remaining numbers.
* The last pull was not a new number, but the pity point obtained was the last one needed to have enough pity points to obtain the rest of the numbers.

Let's first consider the first case where the last pull was a new number, and it was the kth unique number. There were n pulls with only k unique numbers,
implying $$(n - k)$$ repeat numbers were drawn, which means that we obtained $$(n - k)$$ pity points. To finish the grid, we need to have obtained at
least $$(36 - k) * 10$$ pity points to get $$(36 - k)$$ pity pulls to fill out the rest of the grid. Clearly, we can't use more pity points than we obtain.
Also, the surplus of pity points left over can't be enough to obtain another pity pull because it implies we could have completed the grid earlier.
This gives us this constraint on the value of the number of naturally drawn unique numbers $$k$$.

$$
    0 \leq (n - k) - (36 - k) * 10 < 10
$$

Massaging this to isolate k gives:

$$
    \frac{10*36 - n}{9} \leq k < \frac{10*(36+1) - n}{9}
$$

Note that k is inside an interval of size $$\frac{10}{9}$$, which is just barely over 1, and k is an integer. This means that there are only at most 2
valid values for k, but usually just 1 valid value.

We already calculated the probability of getting the k value on pull $$n$$ on the previous section. The probability of finishing the grid
on pull $$n$$ when the last draw was a new number is then:

$$
     P(T_{\text{last_number_new}}'(36, 36) = n) = \sum_{\text{k valid}} P(T'(k, 36) = n)
$$

Now let's consider the 2nd case, where the last number is not a unique number.

Let's say that there were k naturally drawn unique numbers over n pulls, but the kth
number was not drawn exactly at the nth pull. Similarly to the first case, let's try to reason about what the value of k must be.
Again, we need to use (36 - k) * 10 pity points, and we've obtained (n - k) pity points. But now, these two values must be matched with
equality. If the number of pity points obtained is more than the number of pity points used, this implies that we had already enough pity points
to finish the grid without the extra pity point that the last pull earned.

This gives us this condition on the number of unique naturally drawn numbers k:

$$
\begin{align}
    (36 - k) * 10    &= (n - k) \\
    40 - \frac{n}{9} &= k
\end{align}
$$

Since k is an integer, this implies that there's a valid solution for $$k$$ only if n is divisible by 9. But if n is indeed divisible by 9, the count of
uniquely drawn numbers is determined. But we don't know when the kth unique number was drawn, except that it wasn't on the nth pull. Let's say that the kth unique number
was drawn in the mth pull, with m < n. Since only k unique numbers were drawn over n pulls, this means that the remaining (n - m) pulls were limited to the k
already drawn numbers. This happens with probability $$(k/36)^{(n-m)}$$. We can then add up all the cases over all valid values of the exact pull time $$m$$.

$$
    P(T_{\text{last_number_repeat}}'(36, 36) = n) = \sum_{m=1}^{m<n} P(T'(k, 36) = m) * (k/36)^{(n-m)}
$$

Adding up these 2 cases gives us the new probability distribution of the number of pulls needed to fill the grid with pity. Here's the [code](https://github.com/laganojunior/lalaheadpats_code/blob/master/gfl/bingo_with_pity.py) to do those calculations.

Using these formulas, the average number of pulls needed to fill the grid goes down to about 75 pulls, and it's a near certainty that we'll be able
to complete the grid within the max obtainable 189 pulls given in the event time. I guess I don't have to worry about not filling out the grid then!

Just for fun, here's a chart showing the probability distribution of the number of pulls needed.

![Distribution of needed with pity points](/assets/gfl/pity_pulls_distribution.jpg){: style="margin: 0 auto; display: block"}

There are very noticeable spikes at multiples of 9, particularly at values 63, 72, 81, and 90. The effect of the case where the last draw was not a unique number must
be quite large, and we know from before that this can only happen at multiples of 9. In fact, over half the time, you will be able to fill the entire grid exactly
on a multiple of 9. It's probably no accident then that the developers set the daily rate of pulls to 9.
This might have been a deliberate choice to get their players to feel good at the last pull of the day. I just thought this was an interesting phenomenon
that I saw from real sample data that corresponds with predictions from the probability model.

If you like this kind of fun use of math towards inane topics, and have any questions, comments, suggestions for other things to ponder about, or you just wanna say hi,
you can email me at me@lalaheadpats.com.

## Footnotes

[^1]:
    If this is the first time you're seeing an anime avatar streamer and you found yourself wanting more, I'm sorry to have pulled you down the hole that is
    vtubers and you'll have to deal with all the youtube recommendations. I got pulled in this hole around the same time I started playing Girls Frontline. The
    hole is very, very deep and I haven't found the bottom yet.

[^2]:
    If guns aren't your thing, there's also media for anthropomorphized [tanks](https://en.wikipedia.org/wiki/Girls_und_Panzer) and
    [warships](https://en.wikipedia.org/wiki/Azur_Lane). If you're into anything at all, some asian country has already [made it into a moe character](https://en.wikipedia.org/wiki/Moe_anthropomorphism).

[^3]:
    Technically, it's actually a rate of 10 pity points per repeat number and 100 points to get a pity pull, but I just wanted to simplify the numbers.