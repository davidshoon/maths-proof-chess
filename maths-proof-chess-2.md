# Proof that if a God's algorithm exists for Chess, it's drawn.

By David Shoon

2023-01-10

## Summary of proof

1. Zermelo's theorem.
2. Definition of a God's algorithm
	a. God's algorithm can exist if Chess is a finite move game.
	b. Implementation of God's algorithm.
	c. Sub-optimal play
	d. Material reduction algorithm
	e. 1st player cannot initiate a sub-optimal play leading to a long-term win, from the beginning.
3. Assumption: white or black will win, i.e. no draw, is false. (Proof by contradiction)
4. Final notes

## 1. Zermelo's theorem.
	
`https://en.wikipedia.org/wiki/Zermelo%27s_theorem_(game_theory)`

```

When applied to chess, Zermelo's Theorem states "either White can force a win, or Black can force a win, or both sides can force at least a draw"

...

Conclusions of Zermelo's theorem

Zermelo's work shows that in two-person zero-sum games with perfect information, if a player is in a winning position, then that player can always force a win no matter what strategy the other player may employ. Furthermore, and as a consequence, if a player is in a winning position, it will never require more moves than there are positions in the game (with a position defined as position of pieces as well as the player next to move).[1] 

```

## 2. Definition of a God's algorithm

### a. God's algorithm can exist if Chess is a finite move game.

Given the 50 move rule of chess: One has to take a piece or move a pawn.
	
1. The number of moves a pawn can make is finite (it can only move forward and reach the end of the board.)
2. Taking a piece is finite. There are limited number of pieces.
	
Therefore, chess is a finite move game.
	
If it's a finite move game, all possible combinations of moves can be calculated by a "God's algorithm".

Therefore, God's algorithm can exist in Chess.

### b. Implementation of God's algorithm.

God's algorithm for chess can be broken into two parts, given Zermelo's theorem:

1. Sub-optimal play leading to a long-term win, is always nullified.
2. Material reduction algorithm.

### c. Sub-optimal play

If a sub-optimal play (such as a piece sacrifice) could lead to a checkmate, it would be a series of "forced" moves (e.g. threats on king), such that any alternative leads to a checkmate even faster. 

However, given God's algorithm can exist, all sub-optimal plays are nullified, as a subset of all possible plays. (The reasoning: it's assumed God's algorithm would "see" the sub-optimal play and counter it first, as long as it has the ability to counter -- NB: This is proven to always be true, written below, in "1st player cannot initiate a sub-optimal play leading to a long-term win, from the beginning").

Thus, sub-optimal play does not lead to victory, and Zermelo's theorem holds.

### d. Material reduction algorithm

A very simple material reduction algorithm follows:

1. Trading piece for piece reduces material, thus ensuring whoever has the advantage maintains the advantage, as long as it doesn't lead to a sub-optimal play leading to a long-term win.

2. We know that sub-optimal play leading to a long-term win can't exist under God's algorithm. (Proof by contradiction of the definition of God's algorithm.)

Therefore, the material reduction algorithm is the quickest path for God's algorithm.

Corollary: The material reduction algorithm will lead to a "insufficient material" situation, that is, draw, as long as no sub-optimal play can be forced from the beginning (first move) of the game.

NB: Positional (number of squares under control) is also reduced using this algorithm, and assuming the remaining chess piece structure does not lead to a sub-optimal play leading to a long-term win, (i.e. God's algorithm holds under Zermelo's theorem), then positional play is also reduced to "zero". i.e. draw.

### e. 1st player cannot initiate a sub-optimal play leading to a long-term win, from the beginning.

The only situation where sub-optimal play can be "forced" from the beginning, is if the 1st move of the game allows this to occur.

i.e. if you can take a piece in the 1st move by the 1st player or threaten the king in the 1st move by the 1st player.

Since you can't do that under regular chess (as the pieces are on the first two rows), or even under Fischer360 chess, you cannot force a sub-optimal play leading to a long-term win.

Proof by induction:

1. sub-optimal play advantage at move 1 = zero. (No way to force a sub-optimal play, due to the structure of the opening of the chess pieces on the chess board, at move = 1). 

2. sub-optimal play advantage at move X (where X >= 2) = zero. (always nullifiable given God's algorithm, i.e. being to look ahead infinite depth).

3. sub-optimal play advantage at move X + 1 = zero. (God's algorithm would've already analysed the move X + 1 in the move X, and since it has no advantage in move X, then in move X + 1 it would also have no advantage.)

Thus, sub-optimal play cannot lead to a win under God's algorithm, and thus 1st player has no advantage.

(NB: This proof by induction shows that for any sub-optimal play that leads to a long-term win, it must be forced on move 1.)


## 3. Assumption: white or black will win, no draw, is false. (Proof by contradiction)

Let's assume that white or black will win. i.e. no draw.

e.g. f(x) = (-1)^n, where n is the final move such that the result is either 1 (white wins) or -1 (black wins).

For this function to work, it requires:
	- there is sufficient material to checkmate the king.
	
However, under definition of God's algorithm, it will reduce to insufficient material, where it is drawn.

Thus, proof by contradiction. Therefore, chess is a drawn game under God's algorithm with Zermelo's theorem.

i.e. the stricter subset of Zermelo's theorem is proven for Chess under God's algorithm.


## 4. Final notes

Currently, computer chess engines utilise pruned trees. That is, they're imperfect algorithms, due to space (memory) and cpu-time constraints. They are not God's algorithm.

i.e. they may prune branches of the search space such that there exists sub-optimal play leading to a long-term win.

Thus, humans playing against computer chess engines, are still able to win or draw, through the use of sub-optimal play. i.e. Zermelo's theorem does not hold as expected.

i.e. "if a player is in a winning position, then that player can always force a win no matter what strategy the other player may employ" (as per Zermelo's theorem) does not hold against computer chess engines.

In the near future, I will publish some chess games I've made with novel openings against Stockfish 15.1 chess engine such that sub-optimal play actually led to a draw, when the engine played against itself, and where sub-optimal plays have led to a win against crafty chess engine (where human defeated the computer).

However, under God's algorithm and Zermelo's theorem, none of those sub-optimal games would've been drawn or won.

It should be noted however, imperfect algorithms with sufficient depth (such that certain sub-optimal plays are "detected" and nullified), and that it utilises the material reduction algorithm, would reduce the probability of a sub-optimal play leading to a long-term win.

This is because the ability for the long-term win diminishes as the material advantage is traded off, which leads to the best case of a draw. (i.e. the quicker the algorithm reduces the combinatorial space for both sides, the better likelihood of forcing a draw, and avoiding sub-optimal plays leading to a win for the opponent.)

That is, the worst-case mathematical model is this:

Let's assume the chess game opens with 16 pieces of the best possible piece (i.e. queen). A queen has 32 squares it can control.

Therefore, 32^n, where n is the number of pieces, is the combinatorial space. i.e. You have 16 queens, then n = 16, i.e. 32^n = 32^16.

By reducing the number of pieces, then the graph is an inverse exponential i.e. 32^(n - x), where x is the number of pieces taken.
