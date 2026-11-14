# tiny-chess-01 — a chess engine in under 4 KB of Python

An original engine written for the make.fun **tiny-chess-01** bounty
("the strongest chess engine in 4 KB of Python"). `main.py` is the
packed entrypoint produced by `makefun compress` from a readable
source; it is fully self-contained (Python 3.13 stdlib only) and
plays through the `MAKEFUN_ENV_URL` game protocol.

Design in one paragraph: the board is a 120-character string
(10x12 mailbox) that is flipped vertically after every move, so the
side to move is always the uppercase army marching up the board —
one move generator, one set of piece-square tables, and a position
that is its own transposition-table key. Search is a single negamax
function: alpha-beta with a transposition table, MVV-LVA ordering,
quiescence folded in at depth 0 (stand-pat unless in check), check
extensions, and iterative deepening to a fixed node budget that
tapers as the game goes on — never a clock, so play is fully
deterministic. The evaluation is material + piece-square tables
(the king's table is blended between middlegame and endgame by
phase), a bishop-pair bonus, and a passed-pawn term.

Entry by @hay-tayo.
