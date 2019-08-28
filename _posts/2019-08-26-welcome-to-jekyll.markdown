---
layout: post
title:  Draft pod pairings
date:   2019-08-26 20:52:22 -0700
math: true
---

Last weekend, a group of friends and I went to MagicFest Las Vegas to play some games of magic.
After a long game of EDH, one of those friends (Jon) decided to sign up for a 8-player draft
prod of Core 2020. Another friend of ours (Eric) decided that he wanted to sign up for a different event.
Jon and I didn't think much of this at the time, thinking that perhaps Eric wanted to
maximize the possible payout of the group.

To understand this motivation, I'll go over the tournament structure. Each event takes 8 people
and seeds them into a single elimination tournament. Losing in the first game gets you 0 tickets.
Winning just 1 game gets you 20 tickets. Winning just 2 games gets you 200 tickets, and winning
all 3 games gets you 400 tickets. Given the top-heavy prizing structure, one can understand
wanting to maximize the chances of someone getting into the final game.

Perhaps as a form of karmic justice, Jon and I ended up being paired in the first game.
This guaranteed that one of us would be eliminated with 0 wins and thus leaving with 0 tickets.
I quipped that this at least made it impossible for us for both of us leaving with 0 tickets. Jon was understandably bummed that our potential for overall winnings was lessened.

But was it really the case that being matched in the first round ends up with lesser overall winnings
than if we were seed such that we wouldn't meet up until the final round? My intuition was that the
winnings were probably the same on average, and being matched in the first game just made that result
even more consistent. As we'll see, my intuition ends up being correct, under some assumptions.

# Set up

Let us just consider the setup of a 8 person single elimination tournament with the prizing structure
of:

| Wins | Tickets |
|:-----|:--------|
| 0    | 0       |
| 1    | 20      |
| 2    | 200     |
| 3    | 400     |
|=====

The details of the game played doesn't matter. Let's assume that for each game, each person has a
even 50% chance of winning. The game itself doesn't particularly matter, but I assure you that Magic:
The Gathering is a game of pure skill. Even if the game isn't actually a pure coin flip,
this model represents a situation where we're not quite sure what our skill level is compared
to the rest of the players, so we just assume that everyone is similarly skilled.
_(I'll revisit this assumption when I get to differing skill levels.)_

# Calculating probabilities for a single player

We can calculate expected winnings by going over each possible pair of games won, weighting the tickets
won for each possibility by probabilities of reaching it, and then adding it all up.

To calculate the probability of a pair of games, we treat each game as independent events so that
we just multiple the probability of winning and losing each game (due to my previous assumptions,
these probabilities are just 0.5). Note that we have to also account for the last game that the
person lost (if any).

For example, the individual probability of me winning particular game counts is:

$$
\begin{align*}
P(\text{winning exactly 0 games}) &= P(\text{losing first game}) \\
                           &= (0.5)^1 \\

P(\text{winning exactly 1 games}) &= P(\text{winning first game})P(\text{losing second game}) \\
                           &= (0.5)^2 \\
P(\text{winning exactly 2 games}) &= P(\text{winning first game})P(\text{winning second game})P(\text{losing third game}) \\
                           &= (0.5)^3 \\
P(\text{winning exactly 3 games}) &= P(\text{winning first game})P(\text{winning second game})P(\text{winning third game}) \\
                           &= (0.5)^3
\end{align*}
$$

Note that probability of winning exactly 2 games and the probability of winning exactly 3 games are the same due to the
game limit of 3.

# Probabilities if we were matched in the first round

For the case where Jon and I are matched up in the first round, there aren't many possibilities since one of
us is guaranteed to be eliminated in the first round. The calculations end up similar to calculating the
expected value for a single person, except that it's guaranteed that one of us wins at least 1 game`



| My wins | Jon wins | Probability         | Total Tickets | Weighted Tickets |
|:-----   |:-------- |:------              |:------------- |:---------------- |
| 1       | 0        | $$P(\text{I win exactly 1 game}) = (0.5)^2 = 0.25$$  | 20            |  5               |
| 2       | 0        | $$P(\text{I win exactly 2 games}) = (0.5)^3 = 0.125$$ | 200           |  25              |
| 3       | 0        | $$P(\text{I win exactly 3 gamew}) = (0.5)^3 = 0.125$$ | 400           |  50              |
| 0       | 1        | $$P(\text{Jon wins exactly 1 game}) = (0.5)^2 = 0.25$$  | 20            |  5               |
| 0       | 2        | $$P(\text{Jon wins exactly 2 games}) = (0.5)^3 = 0.125$$ | 200           |  25              |
| 0       | 3        | $$P(\text{Jon wins exactly 3 games}) = (0.5)^3 = 0.125$$ | 400           |  50              |
|=========+==========+=====================+===============+==================|
|         | Total    | $$1$$                   |               | 160          |


# Probabilities if we only meet in the final round

If Jon and I were seeded such that we would only meet in the final round, then we're both allowed to get wins.
The probabilities are calculated by multiplying the individual win probabilities together, but the final game
if Jon and I both reach it is treated as one event. Note that it is impossible for both Jon and I to end up with
just 2 wins each since after we get 2 wins each, we would play each other in the finals guaranteeing that one of
us end up with a 3rd win.


| My wins | Jon wins | Probability         | Total Tickets | Weighted Tickets |
|:-----   |:-------- |:------              |:------------- |:---------------- |
| 0       | 0        | $$P(\text{I win exactly 0 games})P(\text{Jon wins exactly 0 games}) \\ = (0.5)^1 * (0.5)^1 = 0.25$$  | 0            |  0               |
| 1       | 0        | $$P(\text{I win exactly 1 game})P(\text{Jon wins exactly 0 games}) \\= (0.5)^2 * (0.5)^1 = 0.125$$  | 20            |  2.5               |
| 2       | 0        | $$P(\text{I win exactly 2 games})P(\text{Jon wins exactly 0 games}) \\= (0.5)^3 * (0.5)^1 = 0.0625$$ | 200           |  12.5              |
| 3       | 0        | $$P(\text{I win exactly 3 games})P(\text{Jon wins exactly 0 games}) \\= (0.5)^3 * (0.5)^1 = 0.0625$$ | 400           |  25              |
| 0       | 1        | $$P(\text{I win exactly 0 games})P(\text{Jon wins exactly 1 game}) \\= (0.5)^1 * (0.5)^2 = 0.125$$  | 20            |  2.5               |
| 1       | 1        | $$P(\text{I win exactly 1 game})P(\text{Jon wins exactly 1 game}) \\= (0.5)^2 * (0.5)^2 = 0.0625$$  | 40            |  2.5              |
| 2       | 1        | $$P(\text{I win exactly 2 games})P(\text{Jon wins exactly 1 game}) \\= (0.5)^3 * (0.5)^2 = 0.03125$$ | 220           |  6.875              |
| 3       | 1        | $$P(\text{I win exactly 3 games})P(\text{Jon wins exactly 1 game}) \\= (0.5)^3 * (0.5)^2 = 0.03125$$ | 420           |  13.125              |
| 0       | 2        | $$P(\text{I win exactly 0 games})P(\text{Jon wins exactly 2 games}) \\= (0.5)^1 * (0.5)^3 = 0.0625$$  | 200            |  12.5               |
| 1       | 2        | $$P(\text{I win exactly 1 game})P(\text{Jon wins exactly 2 games}) \\= (0.5)^2 * (0.5)^3 = 0.03125$$  | 220            |  6.875               |
| 3       | 2        | $$P(\text{I win exactly 2 games})P(\text{Jon wins exactly 2 games})P(\text{I win final game}) \\= (0.5)^2 * (0.5)^2 * 0.5 = 0.03125$$ | 600           |  18.75     |
| 0       | 3        | $$P(\text{I win exactly 0 games})P(\text{Jon wins exactly 3 games}) \\= (0.5)^1 * (0.5)^3 = 0.0625$$  | 400            |  25               |
| 1       | 3        | $$P(\text{I win exactly 1 game})P(\text{Jon wins exactly 3 games}) \\= (0.5)^2 * (0.5)^3 = 0.03125$$  | 420            |  13.125               |
| 2       | 3        | $$P(\text{I win exactly 2 games})P(\text{Jon wins exactly 2 games})P(\text{Jon wins final game}) \\= (0.5)^2 * (0.5)^2 * 0.5 = 0.03125$$ | 600           |  18.75              |
|=========+==========+=====================+===============+==================|
|         | Total    | $$1$$                   |               | 160          |