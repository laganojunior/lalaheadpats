---
layout: post
title:  The Josie mixup using game theory
date: 2019-09-09 00:00:00 -0700
tags: [tekken, fighting_games, game_theory]
math: true
---

I love fighting games. They are the _best_ video games for anyone to just start watching
and enjoy the show. The rules are easy to pick up - 2 characters (or teams of characters) enter and
start beating each other up until the other's life bar depletes [Footnote]. The games are quick (usually only a few minutes),
fast-paced, and the aesthetics are designed to deliver a satisfying feeling to player and spectator alike.
Recent fighting games have added features mainly for the spectator experience, such as freeze frames,
flashy cinematics, and slow motion to further increase the hype and tension for players and spectators.

<figure class="video_container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/JzS96auqau0"
          frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
          allowfullscreen>
  </iframe>
</figure>

This is Evo moment #37. Two fighting game all-time greats Daigo Umehara and Justin Wong are facing each other on the biggest stage
and tournament for fighting games - [Evolution](https://en.wikipedia.org/wiki/Evolution_Championship_Series).
Daigo is in danger of losing to any hit, and Justin unleashes a super move that does a dozen hits, each of which would kill Daigo
if Daigo just simply stands there. Daigo successfully inputs the parry for each individual
hit of Justin's super move, and then does a full combo back to complete the unlikely comeback. All of this in front
of a crowd that slowly realizes the significance of the events on the screen and ends with a crescendo of utter madness and disbelief.

This is probably the most referenced and analyzed clip of all time from any fighting game, if not _any video game_.
Even if you have no idea what's going on, the energy from the crowd gives you the feeling that something amazing is going on and it's hard to not get caught up in the excitement. 
This clip is from 2004, and fighting games have only moved onto larger stages and production value. Here's a favorite
of mine that's from Evolution 2018. Here, the American player Terrelle "Lil Majin" Jackson takes on Korean giant Kim "JDCR" Hyunjin in Evolution 2018
in the Mandalay Bay Event Center in Las Vegas. While Lil Majin is a good player in his own right, JDCR is one of the greatest
players in the whole world, making the only American player left in the tournament a clear underdog especially when Lil Majin
loses the first game to JDCR in a best of 3. With the home crowd roaring behind his back, legendary commentary ("Look at the time!!! Look at it!!!"),
and the theatrics from wrestling lover Lil Majin, Lil Majin brings the game to a nail-biter where the tension and
excitement never drops. (I skipped to just before the 2nd game where the excitement begins to build).

<figure class="video_container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/wQq1dvf3nKI?start=506" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen>
  </iframe>
</figure>

Competitive fighting games are so exciting to watch from a spectator standpoint, but there's also a lot of depth
to fighting games than is evident from just what's visually on the screen. For the Evo moment 37 clip,
a person fluent in video games in general may read that Daigo just made a unlikely comeback after deflecting
a barrage of attacks from the attacker and that it was probably pretty hard to do. A player familiar with the game realizes that the
Daigo had to make over a dozen precisely timed button presses (within about 7 milliseconds),
having the mental awareness and fortitude to jump on the final hit to land a max damage combo for the comeback, _and_
had to start off the entire parry string _predicting_ when the attacker was going to even start since it's too
late to react to once the attack animation comes out. The clip has been analyzed several times from
several perspectives, you just have to search for "Evo moment #37" to find more insight on it. But here's a
[link to the wikipedia page](https://en.wikipedia.org/wiki/Evo_Moment_37) to start you off.

The amount of sub-second decisions, situation recognition over matchups between pairs over dozens of characters, and the amount of mental fortitude to execute what
you need to do under pressure is what makes them so rewarding to players willing to dedicate some time to getting good at a game.
I am not a good fighting game player, but that doesn't mean I can't appreciate the depth that's in fighting games.
Here I want to dig into a small situation in a fighting game I'm currently playing named "Tekken 7" using basic game
theory to give you a taste of what the layers of depth in a fighting game can look like. Maybe it would entice you to
be at least somewhat interested in fighting games (if the above clips weren't enough to pique your interest).

## Introducing Josie and her switch stance

In Tekken 7, I personally play a character named Josie. Continuing the long tradition of stereotypes
in fighting games, she's the perfect representation of a filipina. She's basically wearing the
Philippine flag. Her name is the equivalent of naming one's American daughter after George Washington.
She even cries when she wins, which if you ever watch an episode of any filipino show, you're aware
of any filipina's eagerness to give you a sob story if you hand her screen time.

[JOSIE]

Her game play style I would describe as being a nuisance to the opponent. She can force her opponents to be in situations
where they are heavily disincentived from attacking by threatening to do big damage if the opponent
is unfamiliar with the matchup or just makes a mistake trying to attack at the wrong time or distance. The result is that
the opponent learns to "not press buttons" (the first tip I would give to anyone learning to play against Josie!)
and then Josie relies on chipping away at her opponent slowly to death.

One of her most prominent tools is her "switch stance". After certain kicks, she pulls an Inigo Montoya
and leaves her right foot forward and suddenly all of her moves are incredibly powerful. However,
she can only stay in the stance for a short while because she gets tired and must move her right foot back
in order to conserve her energy.

[SWITCH STANCE]

Before explaining what her moves from switch stance are, I'll first go over some
Tekken notation and concepts to save myself some typing later. Tekken is a 4 attack button game on top
of basic up/down/left/right movement. Each of the 4 attack buttons roughly map to a limb of the body.

* 1 - Left Hand
* 2 - Right Hand 
* 3 - Left Foot
* 4 - Right Foot

So if I write switch 1, this is the attack that comes out when I press the 1 button while in switch
stance, which turns out to be a left elbow. Sometimes an attack involves pressing multiple buttons which
is denoted with "+". so 1 + 2 means pressing the the 1 and 2 buttons at the same time, and usually has to do
with the hands or upper body.

Attacking moves are generally classified as high, mid, and low. A defender can either guard standing or
ducking. A standing defender will block high and mid attacks and take no damage, but will get
hit by low attacks. A ducking defender will evade high attacks and block low attacks to take
no damage, but will get hit by mid attacks.

Ok, so back to looking at Josie's switch stance. When Josie is in switch stance, all 4 buttons lead to moves that are better than
average. After Josie goes into switch stance, she has such a head start over her opponent that all of her
moves will usually hit before an opponent's move connects if the opponent tries to attack back. This is known
as a "counter hit". Josie's switch 1, 2, and 3 (a high, mid, and low attack respectively) all stun her 
opponents on a counter hit, leading to a massively damaging combo. Switch 2 and 3 will generally beat any 
move from the defender except a jab, typically the fastest move available to a character. Switch 1 is
fast enough to even beat a jab for the counterhit combo! Switch 4 is another mid option that doesn't give
a counter hit combo, but does more slightly damage than a switch 2 in the case the opponent is just ducking.

[Illustrations of basic switch]

Low attacks in Tekken 7 are generally slow enough such that a defending ducking player can, after blocking, retaliate
with their own attack before the attacker can recover to block. This is known as a "block punish".
Using Josie as a reference for the defender, a defending Josie can respond with a kick for moderate
damage.

[Retaliation gif]

## A first game-theoretic look at the switch stance mixup game

We can lay out the options both players have and the resulting damage (rounded to the nearest multiple
of 5 damage) in a table [Footnote]. The rows are the attacker's options and the columns are the defender's options.
Positive numbers are damage given by the original attacker, and negative numbers are damage given by the defender
(like if the defender landed an attack in retaliation).

|                 | Stand   | Duck        | Jab  | Slow move |
|:-----           |:--------|:------      |:-----|:-----     |
| **Switch 1**    | 0       | 0           | 70   | 70        |
| **Switch 2**    | 0       | 15          | -5   | 70        |
| **Switch 3**    | 15      | -15         | -5   | 70        |
| **Switch 4**    | 0       | 20          | -5   | 20        |


If you reason about this table long enough, you may realize that the defending player has no reason to
ever try a slow move. A jab will result in better results most of the time and gives no worse
results in the case of a switch 1 from the attacker. If we assume that the defending player will not
then choose to do a slow move, then the attacking player will never choose to do a switch 2
because switch 4 will give no worse and sometimes better results over all the remaining defending player's options.

However, even we remove these worse options from consideration, it's not obvious what
either player should do. The best option depends on what the other player chooses. For example,
if the defending player chooses to just stand and guard, the attacking will want to do the low
attack. However, If the attacking player does a low attack, the defending player then wants to duck guard
and then retaliate with their own attack. But if the defending player ducks, then the attacker would
want to do a mid attack instead. If the attacker wants to a mid attack, the defender would want to stand
guard and we're back where we started. This is essentially a game of rock, paper, scissors and the
resulting guessing game is known in fighting games as a "mixup". So I'll call this game the switch stance
mixup game.

If you've ever played games of rock, paper, scissors, you would know that the best strategy is to
just randomize as best you can [FOOTNOTE?]. But here the probabilities to choose which option
isn't that obvious because the payoffs are different for each result. For example, if the defending player
chooses among the 3 options  of stand, duck, jab with even 1/3 probability, we get:


| Defender strategy probabilities |  0.33    |  0.33        | 0.33  | 0         |
|             | Stand   | Duck        | Jab  | Slow move | Expected damage (given defender strategy) |
|:-----       |:--------|:------      |:-----|:-----     | :-----      |
| **Switch 1**    | 0       | 0           | 70   | 70        |  23.33      |
| **Switch 2**    | 0       | 15          | -5   | 70        |   3.33      |
| **Switch 3**    | 15      | -15         | -5   | 70        |  13.33      |
| **Switch 4**    | 0       | 20          | -5   | 20        |   5         |


If the defender commits to these even probabilities, the attacker would just prefer switch 1 all the time
because that does the most expected damage out of all options. Then the defender again would want to change
their strategy in response. I then ask the question - ok, so when would the 2 players stop wanting to 
change their strategy? My intuition is that this would be strategy that players with repeated play
experience would tend towards.

A pair of strategies where the 2 players do not want to change their own strategy given the other player's
strategy is called a [Nash equilibrium](https://en.wikipedia.org/wiki/Nash_equilibrium). Nash equilibria
are well-studied concepts in game theory come in many different forms. Here we're going to look for
mixed Nash equilibria due to the need to do mixtures of strategies using probabilities. We can try to calculate the
Nash equilibria of this game by hand [Footnote], but I'm going to use a handy Nash equilibria solver [here](http://cgi.csc.liv.ac.uk/~rahul/bimatrix_solver/) [Footnote citation].
If you use the web solver yourself, and I do encourage you to, I'm setting the payoff matrix as the damage numbers for
the attacker and checking the box that this is a zero-sum game.

There turns out to be one nash equilibrium in this mixup game.

|                                    | Defender strategy probabilities |  0.648    |  0.278        | 0.074  | 0         |
| Attacker strategy probabilities    |             | Stand   | Duck        | Jab   | Slow move | Expected damage (given defender strategy) |
| :-----                             |:-----       |:--------|:------      |:----- |:-----     | :-----      |
| 0.136                              | **Switch 1**    | 0       | 0           | 70    | 70        |  5.189      |
|     0                              | **Switch 2**    | 0       | 15          | -5    | 70        |  3.796      |
| 0.346                              | **Switch 3**    | 15      | -15         | -5    | 70        |  5.189      |
| 0.519                              | **Switch 4**    | 0       | 20          | -5    | 20        |  5.189      |
| Expected damage (given attacker strategy) |      | 5.189   | 5.189       | 5.189 | 44.07     |             | 

The expected damage for each option with assigned non-zero probability for _either_ attacker and defender are the same (5.189).
The 2 strategies that have 0 probability assigned have "worse" expected damage for the respective players: Switch 2 has less
expected damage than the other attacker options, and a slow move has more expected damage (for the attacker) than any defender
option. So this is indeed a Nash equilibria as neither player can change their strategy to get a better result.

In this equilibrium, the defending player just stands there most of the time, ducking sometimes to catch the switch 3,
and rarely uses the jab to stop the switch 3 or 4. The attacking player mostly takes the safe option of doing the mid attack
switch 4 hoping the defender is ducking and doing the low attack switch 3 to try to incentivize ducking. From actual play,
this is indeed what happens when I play with real people that are somewhat new to the Josie matchup, at least after they
figure out they should generally stop trying to attack me in switch stance. But from the outside observer, it looks pretty
silly that I'm just usually doing a attack into their guard for no damage.

## The switch stance mixup game against a better defender

More advanced players will know that the options from switch stance aren't quite so safe as they initially appear. The defender
can duck while using the universal low parry on a switch 3 to knock the attacker on the ground and do a moderately damaging
combo to the attacker. At the same time, the defender can also duck switch 1 and then launch the attacker into the air for a big combo.
Switch 4 is also risky for the attacker because a defender can jab the attacker in the air for much more damage.

[Show options]

Changing these damage numbers in the payoff table and using the solver to recalculate the nash equilibrium, we get:

|                                    | Defender strategy probabilities |  0.677    |  0.156        | 0.167  | 0         |
| Attacker strategy probabilities    |             | Stand   | Duck        | Jab   | Slow move | Expected damage (given defender strategy) |
| :-----                             |:-----       |:--------|:------      |:----- |:-----     | :-----      |
| 0.087                              | **Switch 1**    | 0       | **-65**       | 70    | 70        |  1.510      |
| 0.813                              | **Switch 2**    | 0       | 15          | -5    | 70        |  1.510      |
| 0.101                              | **Switch 3**    | 15      | **-50**       | -5    | 70        |  1.510      |
| 0                                  | **Switch 4**    | 0       | 20          | **-40** | 20        |  -3.54      |
| Expected damage (given attacker strategy) |      | 1.510   | 1.510       | 1.510  | 70        |             |

Now the risk that switch 4 doesn't justify the additional damage over switch 2, so the attacker completely switches
to using switch 2 instead of switch 4. The attacker also does switch 1 and switch 3 less often since the defender
can punish the attacker with much more return damage. The overall result is still very similar, the defender is mostly
just standing there and the attacker is mostly futilely doing a mid attack on the standing guard for no damage _more often
than before_. The overall expected damage per mixup game has gone down from 5.189 to 1.510 damage for the attacker. From personal experience,
if I see that the defender is prepared to duck and launch me for doing switch 1 or 3, I do start reducing my use of switch 1 and 3 and just
do mid options to reduce my risk even if I'm just hitting his guard most of the time.

But this kind of sucks for me as the attacking Josie since I'm really not getting that much payoff for getting into the
switch mixup game in the first place. I might be better served by initiating a different mixup game or playing a different
kind of play style altogether. But the situation is not dire for a switch stance loving Josie, she actually has more options out of switch stance
by transitioning into another stance called "step in" or "crouch dash" in common Tekken parlance.

## Adding step in transitions as another layer of depth

If Josie inputs the forward direction during switch stance, she dashes into the opponent, transitioning into another stance called "step in".
While she's dashing, she ducks under defending jabs and she has at least 3 more moves [footnote]:

 * step in 3 - a low attack that does more damage than switch 3.
 * step in 2 - a mid attack that launches the defender high into the air for big damage.
 * step in 1 + 2 - a mid attack that can be followed up with another kick on the ground for moderate damage. However, the 1+2 attack is slow enough that a defender can jab
                   and still be able to block the attack afterward.

[Step in attacks]

However, more reward often comes with more risk. A defending josie can low block a step in 3 and block punish with a full combo.
A step in 2 that's guarded standing can be block punished by a moderately damaging combo. The step in 1+2 is completely safe and cannot be block punished.
On top of all that, a step in transition overall is slow enough such that the defender can actually sneak in a slower move that would have been
beaten before by any option from switch stance. There's enough time that the defender can do a launching move to do a full combo back onto the attacker,
so I'll just consider only the defender doing a launching move as the slower move of choice.

[Step in defending punish]

A further complication is that a defender that didn't commit to doing a move (either a jab or a launch) has enough time to choose to stand guard for switch moves
and then duck for the step in moves, and vice versa. So the defender effectively has 4 strategies for guarding, stand -> stand, stand -> duck,
duck -> stand, and duck -> duck. We're really adding on the layers of depth now!

Adding in these additional options for the attacker and defender and recalculating the nash equilibrium gives:

|                                    | Defender strategy probabilities   | [0.588, 0.439] |  [0.058, 0.208] | [0.149, 0]   | [0, 0.149]    | 0.159 | 0.045     |
| Attacker strategy probabilities    |                                   | Stand -> Stand | Stand -> Duck   | Duck -> Duck | Duck -> Stand | Jab   | Launch    | Expected damage (given defender strategy) |
| :-----                             |:-----                             |:--------       | :----           |:------       | :----         |:----- |:-----     | :-----      |
| 0.043                              | **Switch 1**                      | 0              | 0               | -65          | -65           | 70    | 70        |  4.579      |
| 0.404                              | **Switch 2**                      | 0              | 15              | 15           | 15            | -5    | 70        |  4.579      |
| 0.050                              | **Switch 3**                      | 15             | 0               | -50          | -50           | -5    | 70        |  4.579      |
| 0                                  | **Switch 4**                      | 0              | 0               | 20           | 20            | -40   | 20        |  -2.487     |
| 0                                  | **Step in 2**                     | -50            | 70              | 70           | -50           | 70    | -60       |  -6.426     |
| 0.153                              | **Step in 3**                     | 25             | -55             | -55          | 25            | 25    | -60       |  4.579      |
| 0.350                              | **Step in 1+2**                   | 0              | 35              | 35           | 0             | 0     | -60       |  4.579      |
| Expected damage (given attacker strategy) |                            | 4.579          | 4.579           | 4.579        | 4.579         | 4.579 | 4.579     |             |

The solver actually gives 2 extreme Nash equilibrium for the defending player. This is noted by the pairs of probabilities over the stand -> stand, stand -> duck,
duck->stand, and duck->duck options. This means that any convex mixture between the 2 strategies is also an Nash equilibrium. So there's really an infinite number
of Nash equilibria, but that's just an artifact of how the 4 guarding strategies is really just 2 different choices of ducking and standing vs. switch and step in.
We can simplify the result by looking at summing the probabilities of the defender standing or ducking at the beginning (for switch) and the end (for step in)
The result is that the defender is initially standing or ducking with probabilities 0.646 and 0.149 respectively. If the attacker
transitions into step in, the defender transitions into standing or ducking with probabilities 0.588 and 0.208 respectively.

This is a satisfying result from a gameplay perspective because the attacker still finds use of most options, even if it's just occasionally. (However, the risks for switch 4
and step in 2 turn out to be too risky to justify using them). The defender even finds themselves wanting to use a slow launching move sometimes to stop a step in, even
though it's risking eating counter hit combo from the attacking options in switch. Visually, the majority result is still the defender mostly just standing there and the attacker
seemingly futilely smashing mid attacks (in this case, switch 2 or step in 1+2) into the defender's guard. But the attacking Josie's expected damage has now increased
to 4.579 due to all of the additional options and possible mind games.

## Other things to look at later

This is just a quick look into a small part (the switch stance mixup game) into a single matchup (Josie vs. Josie) of a single fighting game (Tekken 7). Even for just this
mixup game, there's so many things that could change the numbers for each row and column and change the results of the analysis.

* **The stage being played on and location of the players.** Switch 4 can bounce the defender off a wall behind them, massively increasing the potential payoff of hitting the move.
  This would possibly make switch 4 a better option than switch 2 as the mid option of choice from switch.
* **The character the defender is playing.** Josie is only one of a handful of characters that can block punish step in 3 for a full combo and has above average block punishment
  damage in general. If the defender has worse payoffs for blocking these moves, the attacker would increase their use of these moves.
* **The knowledge and skill of the opposing player.** If the defender is unfamiliar with the matchup or does not consistently take full advantage of the attacker's vulnerabilities,
  then risky moves with large payoffs for the attacker such as switch 1 and step in 2 would be used more by the attacker.
* **People are bad at randomization.** Even if both players are trying to play the Nash equilibrium strategies (which is already unlikely), people are just bad at
  being random and inevitably would show patterns that the defender can take advantage of. There's a lot of mind games and conditioning in fighting games,
  and you'll see all the time in competitive play that people seemingly start knowing exactly what their opponent is going to do and afterwards win handily. As fight game
  professional player Infiltration would say, "Download Complete" [Footnote].

And there's so many different sub-games and situations for each character matchup! There's so much room for experiencing new things in fighting games, which is lot of the
fun in fighting games. I hope if you haven't tried getting into fighting games that this makes fight games seem a least a little bit more interesting. Just don't get caught up with trying to learn all the options at first like we did there and just have fun with pressing buttons.

However, This modeling has a disconnect with actual play. We've been implicitly trying to maximize our expected damage per mixup, and we're getting numbers of
~1 to ~5 damage per mixup. This is fine if players had near infinite pools of health and the games were infinitely long and we can justify using expected damage
by hiding by the law of large numbers. But in this game, combos do greater than 70 damage (or higher than 100 damage or even your full health bar
depending on the situation!) and health pools are only 170 health in total. It's possible that we only play a few instances of the mixup game, so the variance in payoffs matters 
quite a bit. Also once we get to lower healths, a 10 damage option might be just as good as a 70 damage option in terms of winning the game, even if the 70 damage option would 
typically carry more risk.

In my next post, I'll be tweaking the modeling to take into account repeated mixup games and how strategies change when health pools start decreasing. To do this, I'll briefly 
introduce the concept of "frame advantage" and what "taking turns" in fighting games looks like. It's an additional layer of depth found in the fundamentals of most fighting games and
also an additional layer of looking at turn-based game in game theory and some algorithms in programming. If you had any fun looking at fighting games through this lense of
mixed Nash equilibrium, I'm hoping that that follow-up will be fun for you as well.