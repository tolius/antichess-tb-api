# Antichess tablebase API

This is an API for reading data from the [antichess](https://en.wikipedia.org/wiki/Antichess) endgame tablebase with DTW (Depth To Win) metric.

The API represents 3 functions:
1. **antichess_tb_init** should be called once at the very beginning. If initialisation is successful, the function returns 0.
2. **antichess_tb_add_path** should be called once before probing, specifying the path to the folder where all tablebase files are located. If all files are successfully loaded, the function returns 0.
3. **antichess_tb_probe_dtw** is used for probing antichess positions:
- ***white_squares***/***black_squares*** should have values from 0 (a1), 1 (b1), etc. to 63 (h8).
- ***white_pieces***/***black_pieces*** should have values from 1 to 6 for PNBRQK (only the least significant three bits are taken into account).
- ***num_white_pieces***/***num_black_pieces*** should be 1+1, 1+2, 1+3, 2+1, 2+2, or 3+1.
- ***ep_square*** specifies the *en passant* target square (16...23 or 40...47) or any other value outside these ranges if there are none.
In case of an error, the function returns a negative value indicating the error code. If one side wins, the function returns 0. In case of a cursed win or a blessed loss (because of the 50-move rule), the function returns 1. In case of a draw, the function returns 2.
If there are no errors, the function sets the value of ***dtw***. The absolute value of ***dtw*** is equal to the number of plies before the win. The value is positive if the side to move wins, or negative if the side to move loses. ***dtw*** = 0 if it is a draw or the side to move has no legal moves.

## License

This code is released under the GPLv3+ license.

The following code is used in the program:
- [Syzygy](https://github.com/mcostalba/Stockfish/tree/master/src/syzygy) (modified)
- [Multi-Variant Stockfish](https://github.com/ddugovic/Stockfish/tree/146269195b1b6a5e9d1121d9fd5767668a48a2a6) (modified)
- Dictzip from [dictd 1.12.1](https://sourceforge.net/projects/dict/) with [Tvangeste's tweaks](https://github.com/Tvangeste/dictzip-win32/tree/bb996c999e9f437b1abb98d941a0a7a98ba82f67) (modified)
- [zlib 1.3.0.1](https://github.com/madler/zlib/tree/643e17b7498d12ab8d15565662880579692f769d)
