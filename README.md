Chess book learning for any chess engine or human.

Repeatedly analyse games played until it finds move
where it disagress with game move or abs(score)>6.5,
then score all positions including analysis of previous
games at same time with one minmax search
and (re)create opening book

Analysis part currently tested only with Stockfish,
but only minor changes if any should be needed 
to use any engine for analysis.


PyChess library needed, for example Ubuntu:
sudo apt-get install pychess


tournamet.py: Will run tournament 2 games at time until
file pause.flag is created in same directory or 
given number of rounds has been reached.
Edit round.sh before running this or create bat file and give it as argument.
Example usage:
tournamet.py --name "Stockfish 8 Book learning" 100
tourname.py will use book_learning.py to do analysing and book updating.

tournamet.py --name "Stockfish 8 Book learning" --tournament_script round.bat 100
Same as above, but instead of round.sh wll use round.bat (copy round.sh and modify it)

tournamet.py --name "Stockfish 8 Book learning" --fen "rnbqkbnr/pppp1ppp/8/4p3/4P3/8/PPPP1PPP/RNBQKBNR w KQkq e6 0 2"
Will start from specified fen. In round.sh add -pgnin file_where_above_fen_is_in_header_and_no_moves.pgn

tournamet.py --name "Stockfish 8 Book learning" --nodes 10M --fixed_lines fixed_lines.dat
Will use use 10x more nodes in analysis than default 1M setting.
Will directly copy lines from fixed_lines.dat to book for specified colour overriding minmax analysis.
Format is colour and moves in uci format, for example:
w e2e4 e7e5 g1f3 b8c6 f1b5
b e2e4 e7e5 g1f3 b8c6



book_learning.py: Used to create opening book from games played by engine or human.
Example usage:
book_learning.py --pgn some_tournament.pgn --name "Stockfish 8 Book learning"
This will analyse positions by player named "Stockfish 8 Book learning" until it
disagrees or absolute score becomes too big. Evaluations are stored in evaluations.pos
and games in game.log . Book is stored in book_learning.bin .

book_learning.py --pgn some_tournament.pgn --name "Stockfish 8 Book learning" --fen "rnbqkbnr/pppp1ppp/8/4p3/4P3/8/PPPP1PPP/RNBQKBNR w KQkq e6 0 2"
Will start from specified fen.

book_learning.py --pgn some_tournament.pgn --name "Stockfish 8 Book learning" --nodes 10M --fixed_lines fixed_lines.dat
Will use use 10x more nodes in analysis than default 1M setting.
Will directly copy lines from fixed_lines.dat to book for specified colour overriding minmax analysis.
Format is colour and moves in uci format, for example:
w e2e4 e7e5 g1f3 b8c6 f1b5
b e2e4 e7e5 g1f3 b8c6

book_learning.py --help
will display help message with all options

round.sh also has more complete usage example
