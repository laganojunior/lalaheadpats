---
layout: post
title:  A poke at fighting games with game theory part 2 - taking turns
date: 2019-09-22 00:00:00 -0700
tags: [tekken, fighting_games, game_theory]
math: true
---

In my [previous post](/2019/09/22/poke-at-fighting-games-with-game-theory.html), I introduced
a small sub-game in the fighting game "Tekken 7" and did some analysis on the resulting
strategies of the 2 players using game theory and Nash equilibria. I'm going to be extending
on that topic here, so I recommend browsing through that post first if you haven't already.

In that post, I was structuring the game's outcome on damage values, so I was implicitly 
assuming that players were trying to just maximize damage (or minimize damage from the 
defender's perspective). So if we were to extend this to multiple plays, it would be
as if the 2 players were just playing an infinite game of damage tug-of-war.

But fighting games don't actually play like this. Health bars are finite and every point
of damage leads closer to the someone winning the round. Someone being at low enough health
absolutely affects both players' strategies since some lines of play can lead to a player
shortly winning. In Tekken 7, player health bars start at 170, and when combos can lead
to 60-76 damage (or even more depending on the situation), a player may only end up making few
effective decisions, so we can't assume everything washes up in the long run over
repeated subgames.

There's also the question of what do _turns_ even mean in a fighting game? I hinted at the
concept of turns a bit from the previous post when I introduced the step in transition
as an option from Josie's switch stance. Since the defender had the ability to make another
decision in the step in transition, it almost resembled a turn-based game where there
was potentially two turns. I didn't present it as a turn-based game then, but I'll be
breaking that game into separate turns in this post.

But the concept of turns extends to more than that in fighting games. Like, who even
gets to be the attacker in the first place? What happens in the next subgame, do the
attacker and defender just switch places to make the game fair? A fighting game is fast
and frantic and it may seem that the concept of turns doesn't apply at all. But if you
watch any tournament commentary, they'll say phrases like "taking/stealing/losing their turn"
. Or they'll something more indirect such as "got caught pressing buttons" or
"fell for the frame trap" which really just means someone tried taking their turn when
it really wasn't.

In this post, I'll briefly go over:

* what turn taking in fighting games look like by covering the concept of "frame advantage"
* making up a game with interconnected subgames using frame advantage to reason about transitions
* solving the overall game via computer program and looking at the result

## Frame advantage

If you spend any time trying to get into fighting games, you'll probably hear the word
"frame"-something at some point. "Frame advantage", "Frame-perfect", "Frame trap",
"1 frame link" etc. are phrases that just thrown around casually in fighting game commentary. 
But what is a "frame" even?

In fighting games, a frame comes from your computer screen displaying motion as a series
of still images (each of which is called a frame) in rapid succession that gives the 
illusion of motion. The standard for many games is 60 frames per second (60 fps),
so each frame only shows up for about $$1000 / 60 \approx 16.7ms$$. For fighting games, the
frames per second is often a fixed value, so a frame is used as a convenient unit for time.

Since frames are unit of times, they can be used to express how
_fast_ things are. For example, some moves are faster than others
in fighting games. A move that is faster will hit before a 
slower move. Using the lens of frames, the faster move would have _fewer_ frames to hit before
the slower move.

For example, in Tekken 7, jabs are 10 frames. These are generally the fastest moves in the
game. The kick I used to show the switch transition for Josie (downforward (df) 4) in the
previous post takes 14 frames to come out. So a jab will beat the switch transition 
kick every time if they both start at the same time.

[ Illustration of josie getting beat on switch kick ]

Note that this only true if the two attacks started out _at the same time_. If the switch
transition kick started 5 frames before the jab, then the switch transition kick would
hit first instead.

[ Illustration of switch kick winning instead ]

Generally speaking, humans can't react in the timescale of ~5 frames. So the question of
whether the switch kick or jab would hit first still seems effectively random if the
players can just start at any arbitrary frame they choose. But there are situations where
we _can_ reason about when the 2 players can start attacking. This is where the
concept of "frame advantage" comes in.

Every attack has 3 distinct phases, a startup, an active part (the part where the attack
hits, which is sometimes just a single frame), and a recovery period. An attacker typically
can only attack again once the recovery period ends. If the defender blocks the attack, they
are placed into a recovery state called "block stun" and they cannot attack until the block
stun period ends. Similarly, if the defender get hits by the attack instead, they are placed
into a recovery period called "hit stun" and they cannot attack until the hit stun period 
ends.

[ Illustration of the hit/block stun ]

The attacker recovery period and the defender's recovery don't have to end at the same time!
If the attacker recovery period ends before the defender's recovery period does, then if the
attacker and the defender try to start the same attack at the same time they can first can,
the attacker's attacker will hit first. This situation gives the attacker the "frame 
advantage".

The difference in when the recovery periods ends in usually expressed in frames in
favor of the attacker. So if an attacker's recovery period ends 2 frames before the 
defender's recovery period ends, then the move would be noted as "+2" and the move is 
generally noted as "+". Similarly, if the defender's recovery period ends 2 frames before the 
attacker's recovery period ends, then the 
move would be noted as "-2" and generally noted as "-". Moves typically have different frame 
properties depending on whether the move was blocked, hit the defender, or counter-hit the 
defender (meaning the move hit the defender while the defender was starting up another move). 
For example, a move could be -2 on block, +5 on hit, and + 10 on counterhit all giving 
different follow-up situations.

The resulting frame advantage is typically within +/- 10 frames which is still 
faster than human reaction. However, the startup + recovery period of the attack adds about 
20 frames of visual information before the recoveries end. This gives both players enough 
time to read the situation and make a decision on what to do immediately after the recovery
depending on what the frame advantage is.

[Illustration of the 1 jab frame advantage]

To connect this more with the previous post, I mentioned that some moves are slow enough
if blocked that the defender can retaliate with a move before the attacker can recover,
resulting in a "block punish". In this situation, the frame advantage is _so negative_
that the defender can recover, get through an attack's startup, and hit the attacker
all before the original attacker's recovery period ends. For example, Josie's step in 3
is -13 frames on block, and Josie's launching move from a duck is 13 frames on startup,
which means that Josie can block punish a step in 3 from another attacker Josie with
a launching combo [Footnote].

As a general rule of thumb in Tekken 7, most mid/high attacks are + on hit and - on block.
Many quick low attacks are - on hit. Any moves that are + on block are considered good
because they can often be looped by the attacker such that the defender has to take a risk
to stop the loop which opens up more options for the attacker. For pretty much any
fighting game that is played at all, people have gone through
the effort of measuring the frame properties of all moves through various hit/block
situations. I'll be using the frame numbers (for Josie) in
[rbnorway](http://rbnorway.org/josie-t7-frames/) as a reference in this post.

Core-A-Gaming also made a video on frame advantage and other concepts for beginners, I
recommend [checking out that channel as well](https://www.youtube.com/watch?v=_R0hbe8HZj0).

## Converting frame advantage to turns and transitions

So how does the concept of frame advantage relate to the concept of turns? We'll be
considering the player who has the positive frame advantage as taking the turn as the
"attacker". This is because the player with negative frame advantage would be taking a risk
to do anything other than just block, because any move from a negative frame advantage
would lose from a jab from the attacker.

But in the specific game that we considered in the previous post (the Josie v Josie matchup,
particularly the subgame from switch stance), does _any_ frame advantage grant the attacker 
the ability to go into switch stance? The answer is no. The transition attacker that I used
in the last post takes 14 frames to start [Footnote], and an opposing jab takes only 10 frames
to hit. So if the attacker's frame advantage is less than 4 frames, the defender can jab to
prevent an attacker that's always trying to go into switch stance.

But how does the attacker get into switch stance from the first place? Let's assume that
that the attacker is in a minor frame advantage, and just keeps using the basic jab. The
jab is 10 frames, and is +1 on block. Therefore, the defender can't just try to jab all the 
time because they'll just get hit by an attacking jab. In fact, Josie's jab is +8 on hit, so
if the defender gets hit by a jab, the attacker can then go into switch stance without 
worrying the defender interrupting with their own jab. Therefore the defender has a reason
to just stand there and block, which gives the window for the attacker to just go straight
into switch stance instead. This basic interaction with the jab is so much of the basis
of the offensive game in Tekken 7 that Tekken great JDCR [made a video just on how important
the jab is](https://www.youtube.com/watch?v=7bzQboSDHjU).

Turns aren't so absolute though. The defender can avoid the attackers jab to not get
into block stun in the first place, for example by ducking and doing a jab from a ducking
position (a "duck jab"). If the defender successfully counters an attacker's jab in this way,
the defender then secures the frame advantage (and thus the "turn" for themselves).
This kind of move is sometimes referred to as "stealing the turn" or just a "challenge".
However, a duck jab is risky because the attacker can instead do a low parry combo to the
defender.

I can construct a subgame which I call the "minor advantage game" (for frame advantages < 4)
with these options, with these abstract outcomes.

|                 | Stand   | Jab         | Duck Jab |
|:-----           |:--------|:------      |:-----    |
| Jab             | jab is blocked, +1                         | jab hits, +8           | defender jab hits, +6 for defender       |
| Duck/Low Parry       | defender can see the duck and then be able to jab first       | defender has committed to jab which attacker is now ducking, attacker can now jab first            | attacker does combo to defender      |
| Switch          | go to switch                        | defender jab hits, +8 for defender         | defender jab hits, +6 for defender       |
{:center: style="text-align: center"}
_Minor advantage game with abstracted outcomes_
{:center}

To govern the transitions more concretely, I'll assume these rules [Footnote]:

* Any player will not try to challenge from a frame disadvantage of -4 frames or lower. The 
player with frame advantage attacker goes into switch stance and the other player blocks the kick that goes into switch. Note that this means that the kick to transition into switch will _never_ itself hit.
* Any time a player is comboed or is otherwise knocked onto the ground, the position is reset
to a minor advantage for the player that did the combo or knocked down the other player.

So we can express this game with direct transitions into other games:

|                 | Stand   | Jab         | Duck Jab |
|:-----           |:--------|:------      |:-----    |
| Jab             | attacker minor advantage game  | attacker jab hits, attacker switch game           | defender jab hits, defender switch game |
| Duck/Low Parry       | defender minor advantage game | attacker minor advantage game   | attacker combo, attacker minor advantage game |
| Switch          | attacker switch                        | defender jab hits, defender switch         | defender jab hits, defender switch  |
{:center: style="text-align: center"}
_Minor advantage game with direct subgame transitions_ 
{:center}

I can do the same for the game I presented in the last blog post. I'll go ahead and split the
game up into 2 separate subgames for the switch and step in subgames.

|                 | Stand       | Duck/Low Parry    | Jab      | Launch |
|:-----           |:--------    |:------  |:-----    |:-------|
| Switch 1        | blocked, defender switch | defender combos attacker, defender minor advantage | attacker combos defender, attacker minor advantage | attacker combos defender, attacker minor advantage |
| Switch 2        | blocked, defender switch | hit, attacker switch | defender hits, defender switch | attacker combos defender, attacker minor advantage |
| Switch 3        | hit, defender minor advantage | defender combos attacker, defender minor advantage | defender hits, defender minor advantage | attacker combos defender, attacker minor advantage |
| Switch 4        | blocked, defender switch | hit knockdown, attacker minor advantage | defender hits, defender switch | attacker combos defender, attacker minor advantage |
| Step in         | attacker step in | attacker step in | attacker step in | defender combos attacker, defender minor advantage |

{:center: style="text-align: center"}
_Switch game with direct subgame transitions_
{:center}

For the step in sub game, I'll be adding a few more options that I didn't include in the last 
post. I'll be allowing the defender to also jab after seeing the attacker committing to a 
step in, which can interrupt a attacking step in 3 and float combo an attacking 1+2 as the
attacker is jumping during that attack. Step in 2 will duck under the jab and launch the 
defender for a combo. As an additional option to beat the jab, the attacker
now has has access to step in 4, which is a fast mid kick that can be timed to beat the jab 
timing required to interrupt the step in 3 or 1+2. [Footnote]

|                 | Stand       | Duck    | Jab      |
|:-----           |:--------    |:------  |:-----    |
| Step in 2       | defender combos attacker, defender minor advantage | attacker combos defender, attacker minor advantage | attacker combos defender, attacker minor advantage |
| Step in 3       | hit, attacker switch   | defender combos attacker, defender minor advantage | defender hits, defender switch  |
| Step in 4       | blocked, defender switch | hit, attacker switch    | hit, attacker switch |
| Step in 1+2     | blocked, attacker minor advantage | hit knockdown, attacker minor advantage    | defender combos attacker, defender minor advantage |

{:center: style="text-align: center"}
_Step in game with direct subgame transitions_
{:center}

## Calculating win probabilities and chaining subgames into bigger games

One of the problems with the previous post's model is that I was just using damage values without any consideration
for remaining health and players actually _winning the game_ through depleting the other player's health pool. Let's consider
a situation where both players have only 5 health (so any hit would win the game) and one player is in switch stance (so we're playing
the switch subgame). Furthermore, let's assume that this is the last turn of the game, and that if both players are both alive
by then, the player with the higher health total will win the game. If both players have the same health (which must happen in the
scenario where both players have 5 health), then the winner of the game is chosen by a coin flip.

We can then make a payoff matrix where the values are the probability of winning for the attacker instead of damage values:

| Switch (5, 5, 1)| Stand       | Duck/Low Parry    | Jab      | Launch |
|:-----           |:--------    |:------            |:-----    |:-------|
| Switch 1        | 0.5         | 0                 | 1        |       1|
| Switch 2        | 0.5         | 1                 | 0        |       1|
| Switch 3        | 1           | 0                 | 0        |       1|
| Switch 4        | 0.5         | 0                 | 1        |       1|
| Step in         | 0.5         | 0.5               | 0.5      |       0|

We can solve for this game's nash equilibrium similarly to the previous post. We get that this as a solution:

|                   | Defender strategy | 0.231       | 0.385             | 0.385    |      0 |                                |
| Attacker strategy | Switch (5, 5, 1)  | Stand       | Duck/Low Parry    | Jab      | Launch |  Value given defender strategy |
| :----             |:-----             |:--------    |:------            |:-----    |:-------| :---------------------------   |
|          0.406    | Switch 1          | 0.5         | 0                 | 1        |       1|     0.501                      |
|          0.203    | Switch 2          | 0.5         | 1                 | 0        |       1|     0.501                      |
|              0    | Switch 3          | 1           | 0                 | 0        |       1|     0.231                      |
|          0.203    | Switch 4          | 0.5         | 0                 | 1        |       1|     0.501                      |
|          0.189    | Step in           | 0.5         | 0.5               | 0.5      |       0|     0.501                      |
|                   | Value given attacker strategy  | 0.500 | 0.500 | 0.500 | 0.813 |

So we get that the value of this switch subgame at (attacker health, defender health, turns left) = (5, 5, 1) to be about 0.500. We can do a similar calculation
for the minor advantage subgame at (attacker health, defender health, turns left) = (5, 5, 1).

|                   | Defender strategy              |   1         |   0               | 0        |                                |
| Attacker strategy | Minor Advantage (5, 5, 1)      | Stand       | Jab               | Duck Jab |  Value given defender strategy |
| :----             |:-----                          |:--------    |:------            |:-----    | :---------------------------   |
|          0.3      | Jab                            | 0.5         |  1                | 0        |  0.5                           |                          
|          0.618    | Duck/Low Parry                 | 0.5         | 0.5               | 1        |  0.5                           |
|          0.083    | Switch                         | 0.5         |  0                | 0        |  0.5                           |                        
|                   | Value given attacker strategy  | 0.5         | 0.609             | 0.618    |                                |

This is only 1 of many solutions because the game collapses to the defender just standing there 100% of the time, which just makes the game a draw
and coin flip no matter what the attacker does, except the attacker needs to choose a strategy such that the defender doesn't want to do anything else.
The end result is that the game is an overall draw.

So now let's consider the step in game where (attacker health, defender health, turns left) = (5, 5, 2). We're still in sudden death mode,
but we're allowing for another subgame after this one in case nothing hit. We get a payoff matrix that depends on the values on possible future
games. Note that if the turn passes to the defender, we have to invert the probability back to the perspective of the attacker. For example, if a
transition to another game would have the defender winning 75% in that other game, the attacker's payoff here for going into that transition would be 25%.

| Step in (5, 5, 2) | Stand                      | Duck              | Jab      |
|:-----             |:--------                   |:------            |:-----    |
| Step in 2         | 0                          |  1                | 1        |
| Step in 3         | 1                          |  0                | 0        |
| Step in 4         | 1 - switch (5, 5, 1)       |  1                | 1        |
| Step in 1+2       | minor advantage (5, 5, 1)  |  1                | 0        |

The 2 subgame values are the values we just already calculated earlier! We can plug those in, and then solve for the Nash equilibria for this game.

|                       | Defender Strategy | 0.667                            | 0.127             | 0.207    |                               |
| Attacker Strategy     | Step in (5, 5, 2) | Stand                            | Duck              | Jab      | Value given defender strategy |
| :----                 |:-----             |:--------                         |:------            |:-----    | :---------------------------  |
|   0                   | Step in 2         | 0                                |  1                | 1        |    0.334                      |
|   0.333               | Step in 3         | 1                                |  0                | 0        |    0.667                      |
|   0.667               | Step in 4         | 1 - switch (5, 5, 1) = 0.5       |  1                | 1        |    0.667                      |
|   0                   | Step in 1+2       | minor advantage (5, 5, 1) = 0.5  |  1                | 0        |    0.461                      |
|                       | Value given attacker strategy | 0.667                | 0.667             | 0.667    |

So the Nash equilibrium probability of the attacker winning from step in (5, 5, 2) is about 2/3s. We can use the same idea to solve the smaller
games with low health values and low turns left to construct payoff matrices for the subgames with higher healths (using damage values for health
transitions) and solving those Nash equilibria as well. This should give us a Nash equilibria for any starting health values and turn count that we
may want [Footnote about subgame perfect Nash Equilibria].

So to solve the entire game, we first define some base rules that encodes turns running out, or either player running out of health.

$$
\text{any_game}(x, y, t \leq 0) =
\begin{cases}
    1 & \text{if } x > y \\
    0 & \text{if } y < x \\
    0.5 & \text{otherwise}
\end{cases}
$$

$$
\text{any_game}(x \leq 0 , y, t \geq 1) = 0 \\
\text{any_game}(x , y \leq 0, t \geq 1) = 1
$$

To solve any other game, we define the payoff matrix dependent on the values of other subgames and get the Nash equilibrium value. Note that if
the turn passes the defender, we have to switch the values after accounting for any damage that may have been taken. We use the transition rules
we defined earlier when talking about frame advantage and transitions. Note that since the turn counter is always decreasing, the game must end
at some point leading us to one of the base rules we defined just above.

| Minor Advantage (ma) (x, y, t) | Stand             | Jab                     | Duck Jab                   |
|:-----                          |:--------          |:------                  |:-----                      |
| Jab                            | ma(x, y, t-1)     | sws(x, y-5, t-1)        | 1 - sws(y, x-5, t-1)       |
| Duck/Low Parry                 | 1 - ma(y, x, t-1) | ma(x, y, t-1)           | ma (x, y-50, t-1)          |
| Switch                         | sws(x, y, t-1)    | 1 - sws(y, x-5, t-1)    | 1 - sws(y, x-5, t-1)       |

| Switch (sws) (x, y, t) | Stand                | Duck                    | Jab                   | Launch                |
|:-----                  |:--------             |:------                  |:-----                 | :-----                |
| Switch 1               | 1 - sws(y, x, t-1)   | 1 - ma(y, x-65, t-1)    | ma(x, y-70, t-1)      |  ma(x, y-70, t-1)     |
| Switch 2               | 1 - sws(y, x, t-1)   | sws(x, y-15, t-1)       | 1 - sws(y, x-5, t-1)  |  ma(x, y-70, t-1)     |
| Switch 3               | 1 - ma(y-15, x, t-1) | 1 - ma(y, x-50, t-1)    | 1 - sws(y, x-5, t-1)  |  ma(x, y-70, t-1)     |
| Switch 4               | 1 - sws(y, x, t-1)   | ma(x, y-20, t-1)        | 1 - ma(y, x-40, t-1)  |  ma(x, y-20, t-1)     |
| Step in                | stp(x, y, t-1)       | stp(x, y, t-1)          | stp(x, y, t-1)        |  1-ma(y, x-70, t-1)   |

| Step in (stp) (x, y, t) | Stand                 | Duck                    | Jab                   |
|:-----                   |:--------              |:------                  |:-----                 |
| Step in 2               | 1 - sws(y, x-50, t-1) | ma(x, y-70, t-1)        | ma(x, y-70, t-1)      |
| Step in 3               | sws(x, y-25, t-1)     | 1 - ma(y, x-55, t-1)    | 1 - sws(y, x-5, t-1)  |
| Step in 4               | 1 - sws(y, x, t-1)    | sws(x, y-15, t-1)       | sws(x, y-15, t-1)     |
| Step in 1+2             | ma(x, y, t-1)         | ma(x, y-20, t-1)        | 1 - ma(y, x-40, t-1)  |