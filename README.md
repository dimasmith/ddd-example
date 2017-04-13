DDD Example - Snooker League
============================

# Domain
I want to maintain (imaginary) Ukrainian professional Snooker league.
There are few aspects that are interesting to track:
* Tournament calendar;
* Player rankings;
* Player statistics;
* Match and tournament statistics;

# Ranking and Tournaments

Snooker league provides set of tournaments and calculate player rankings based on players performance on tournament.
`Tournament` is an annual event where players participate and earn ranking points for wins.
Set of tournaments are grouped into `Season`.
Season usually spans for a year (most often is starts on September and ends on May).

Each season there are 96 `Players` participating.
They are trying to achieve maximum amount of ranking points.
`Ranking points` adds up for two latest seasons (points of previous seasons are discarded).
Player who has most ranking points after the end of season becomes a `Champion`.
Ranking points are added for each `Match` won during tournament.
Later stage wins brings more points to winner.
Actual amount of points for winning a match differs for each tournament.

All details regarding ranking and tournaments are managed by `League Managers`.

## Tournament
Tournament spans for a few days thus having start and end date.
Tournament consist of stages going one after another.
Progressing to later stage is done on play-off basis.
Two player plays match.
Winners goes to the next stage and loser is out of tournament.
Last winner becomes tournament champion and gets most ranking points.

### Seeded players
Depending on tournament size few highest-ranked players are participating without going through qualification.
Those players starting in later stages thus it is easier for them to get more ranking points.
There are 16 `seeded players` for `small` tournaments and 32 for `large` ones.
Seeded players starts their games with ones who passed qualification.

### Qualification
Players who are not seeded are going through qualification.
Pairs of players in qualification are formed in random order.
Progressing for each round of qualification gives exactly the same amount of ranking points.
For small tournaments there are 80 player who are not seeded.
Thus it is impossible to form normal play-off grid of them.
16 players are randomly selected to participate only in last round of qualification.
It is easier for them to go to later stages but they're missing opportunity to win additional points in qualification.

### Ranking update
Rankings are updated after tournament finishes.
Those updates are taken into account when seeding for next tournament.
Even if player through the course of qualification earns more points than currently seeded player it does not change seeding for ongoing tournament.
Tournament must not take place in the same time.
No time overlapping allowed.

### Tournament grid
Placement __todo: add details__

## Match
Match is a game between two players.
One player wins match, other one looses.
Match consists of `Frames`.
Each won frame adds one point to players `Match Score`.
Match has pre-defined winning score.
E.g. Match to 10 wins ends when either of players won 10 frames.
Each match in the same tournament stage has the same length.
Matches of different stages, however, may have different length (usually final match is longest one).
Match can also be `conceded` by one of players.
Player who conceded match loses it.
It can be a technical reason to end match before it goes full length (e.g. one of players cannot proceed because of health state or as result of disqualification).
Referee then should decide who is the winner.

More details on match rules can be found [here](https://en.wikipedia.org/wiki/Rules_of_snooker).

## Frame
Frame is part of match where player should pot balls and got `frame score` to win.
Players tries to pot balls by taking turns at the table.
If player pot the ball he should try to pot another one.
Each potted ball add points to player score.
__todo: add pot succession rules__
Amount of points depends on ball colour:
* Red - 1
* Yellow - 2
* Green - 3
* Brown - 4
* Blue - 5
* Pink - 6
* Black - 7
Few consecutive successful pots are called `Break`.
Break ends when player fails to pot (misses).
Player can earn foul for various things __todo: add foul descriptions__
Each type of foul adds certain amount of points to opponent of player who conducted foul.
Frame ends when there are no balls on table or one of player `conceded frame`.
When no balls left on table and score is even black ball returned to table and players play until first foul or pot.
This situation is called `respot black`.
In certain situations when there are no chance to proceed frame normally players may decide to `rerack frame`.
Balls are then returned to initial position and frame starts afresh.

## Player performance
Player performance is a set of metrics calculated during each frame:
* Break sizes;
* Century and highest breaks;
* Pot success ratio;
* Safety shots success ratio;
* Average and maximum time it took player to make a shot;
Performance metrics is calculated for each frame (depending on technical ability to track it).
Player performance may than be aggregated by match, tournament, career e.t.c.
It is also possible to sum up performance for tournament or season.

## Turn
Players play frames by taking turns.
Each turn may result in:
* Break;
* Miss;
* Foul;

# Application use-cases

## Organizing tournament
League manager creates new tournament.
He selects tournament type (`small` or `large`).
Tournament grid with all stages is created by system.

League manager assigns ranking points for winning each stage as well as ranking points
for winning round of qualification.
He also sets start and end dates for each stage.
System should check that stage dates does not overlap neither in one tournament nor with other ones.

After tournament stages are set-up tournament is announced.

### Tournament start
After previous tournament is ended and ranking is updated, System fills grid of current tournament with players.
When grid is filled tournament becomes ready to start.

#### Adding new tournament before
Let's assume we have Kyiv Masters scheduled for Jul 15 with previous tournament being Odessa Cup
ended on June 22. After Odessa Cup is ended Kyiv Masters grid is filled with players.
Then new tournament - Lviv Trophy is added on Jun 30 - Jul 7.
Grid for Kyiv Masters should be then recalculated after Jul 7 according to ranking after Lviv Trophy.

Minimal time between tournaments is 5 days.

## Denouncing tournament
Tournament can be cancelled at any time before it ends.
Tournament becomes deleted from system and any results are discarded.


# Build using Jenkins
I add this comment purely to test hook.
