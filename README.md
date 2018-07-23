# Surakarta

Surakarta is, according to some reports, a traditional Indonesian board game. It is similar to chequers, but has some unique twists. Your goal, in this project, is to implement the functionality required to ensure that only legal moves are allowed by the Python-based version of Surakarta.

The Rules of Surakarta (adapted from Cyningstan):

The board consists of a six-by-six grid of lines, with two concentric circular tracks at each corner, as shown below. Pieces are placed on the points where lines intersect. Each player starts with twelve pieces (black or white tokens) that are placed on the intersections nearest that player.

Note: initially, we will work with a more compact four-by-four version of the Surakarta board, with a single circular track at each corner, as shown below. On this board, each player starts with only four pieces placed on the intersections nearest to that player. However, the functions you implement should also work for a six-by-six version of the board.

Players decide at random who moves first. In a turn, a player must make one of two types of move (passing is not allowed):

A normal move, in which a player moves one of their pieces from one intersection to an adjacent intersection, horizontally, vertically, or diagonally. Pieces may not jump over other pieces, and only one piece may occupy an intersection at any point in time. The circular tracks around each corner may not be used for normal moves.

A capture move, in which a player slides a piece along a straight line, around a circular track, and then further along a straight line, until it lands on an opposing piece, which is then removed from the board. Pieces making a capture move may move more than one intersection during such a move, but may not jump over other pieces. Note that a capture move must use at least one of the circular tracks, and may use more than one. Update: A capture move can start and/or end on the edge of the board; that is, it can move along a straight line of length zero!

A player wins when they have captured all of their opponent's pieces.

In this project, you will answer a number of questions that create functions needed to play the game of Surakarta.

Question 1: Implement a function make_move_normal(initial, move_start, move_end) that validates and executes if possible, a normal move.
Question 2: Implement a function make_move_capture(initial, move_start, move_end) that validates and executes if possible, a capture move.
Question 3: Implement a function make_move_sequence(initial, move_sequence) that validates a sequence of moves constituting part of a game.
Question 4: This question will require you to create a suite of test cases that can be used to test your make_move_capture function.

To make it simpler to define test cases for your function, the board state may be defined in terms of an N-by-N string specifying the state of the board; eg, for the four-by-four game, the string 'xxxx........oooo' specifies the initial board state.

Tip: To make the relationship between a string and the corresponding board state clearer, it may help to represent the string as follows:


'xxxx' +
'....' +
'....' +
'oooo'
Remember that + concatenates two strings.

In this representation 'x' represents a black piece, 'o' represents a white piece, and '.' represents an empty location. A string is unlikely to be the most convenient internal representation for the board state: a list of lists (a nested list) is a better choice.

You have been provided with three functions to assist with converting between board strings and board states; and drawing graphical representations of the board, which may assist with developing and debugging your code and test cases:

The function get_board_state(board_string) will return a board state based on the specified board string. Board strings must be 16 or 36 characters long, and the dimension of the board state returned will be four-by-four or six-by-six respectively.

>>> from reference import get_board_state
>>> get_board_state('xxxx........oooo')
[['x', '.', '.', 'o'], ['x', '.', '.', 'o'], ['x', '.', '.', 'o'], ['x', '.', '.', 'o']]

Note that you can obtain the value of a specific location from a board state (ie, black, white, or empty): the first index will be the x-coordinate (column) and the second index will be the y-coordinate (row).


>>> from reference import get_board_state
>>> board = get_board_state('xxxx........oooo')
>>> board[0][1]
'.'
>>> board[1][3]
'o'

The function get_board_string(board_state) will return a board string representation of the specified board state.

>>> from reference import get_board_string
>>> get_board_string([['x', '.', '.', 'o'], ['x', '.', '.', 'o'], ['x', '.', '.', 'o'], ['x', '.', '.', 'o']])
'xxxx........oooo'

The function draw_sura(board_string) will create a graphical representation of the board (as depicted in these instructions). You may pass a string of length 16 or 36, corresponding to a four-by-four or six-by-six board state respectively.

--------------------------------------------------------------------------------------------------------------------------------------

Q1

Write a function make_move_normal(board_string, start, end) that takes as input a string representation of the current board state, a tuple representing a the initial position of the piece to be moved (start), and a tuple representing the end position (end) the piece is to be moved to. This function will validate if the move is valid and if so, execute the move.

The function should return a string representation of the board reflecting the position of the pieces after the move if the move is valid, or None if the move is invalid.

Assumptions: Capture moves need not be considered for the purpose of this task (ie, they would be deemed invalid).

--------------------------------------------------------------------------------------------------------------------------------------

Q2

Write a function make_move_capture(board_string, start, end) that takes as input a string representation of the current board state, a tuple representing the initial position of the piece to be moved (start), and a tuple representing the end position (end) the piece is to be moved to. This function will validate if the move is valid and if so, execute the move.

The function should return a string representation of the board reflecting the position of the pieces after the move if the move is valid, or None if the move is invalid.

Assumptions: Normal moves need not be considered for the purpose of this task (ie, they would be deemed invalid).


>>> print(make_move_capture('xxxx........oooo', (0, 0), (0, 1)))
None
>>> print(make_move_capture('x.xx.x......oooo', (1, 1), (1, 3)))
'x.xx........oxoo'

--------------------------------------------------------------------------------------------------------------------------------------

Q3

Write a function make_move_sequence(board_string, move_sequence) that validates a sequence of moves constituting part of a game. This sequence may contain both normal and capture moves. This function should take as arguments a string representation of the initial board state, and a list of tuples containing the start and end coordinates corresponding to a sequence of successive moves.

The return value of this function is a string representation of the final board state (ie, after executing all moves in the sequence) if the sequence of moves are valid, or None if an invalid move is made at any point in the sequence.

Assumptions: It can be either black or white's turn for any initial given board state.


>>> print(make_move_sequence('xxxx........oooo', [((1, 0), (1, 1)), ((2, 3), (1, 2))]))
'x.xx.x...o..oo.o'
>>> print(make_move_sequence('x.xx.x...o..oo.o', [((1, 2), (2, 1)), ((1, 1), (1, 3))]))
'x.xx..o.....ox.o'
We have provided to you a reference implementation of the make_move_normal(board_string, start, end) function from Question 1 and make_move_capture(board_string, start, end) function from Question 2 that you can use here

---------------------------------------------------------------------------------------------------------------------------------------

Q4

Testing your implementation.

In addition to implementing your solution, you are also required to submit a suite of test cases that can be used to test your Question 2 make_move_capture function. You should aim to make your test cases as complete as possible. That is, it should be sufficient to pick up invalid moves. Your suite of test cases may assume that the input passed to your function will be of the correct type and will be well-formed, in that the first argument will be a string of the correct length, containing valid characters ('x', 'o', and '.'), and the second and third arguments will be tuples containing the coordinates of start and end coordinates. However, you should not assume that the moves described by these inputs are necessarily valid.

You should specify your test cases as a series of calls to the function test_make_move_capture((board_string, start, end), expected_return_value), where board_string and expected_return_value are board string representations of the initial and final boards, and start and end are 2-tuples of positions, as in Question 2. That is, you specify both the arguments and return value for make_move_capture as arguments to test_make_move_capture.

For example, using the first two examples from Question 2:


from testcase_tournament import test_fn as test_make_move_capture

test_make_move_capture(('xxxx........oooo', (0, 0), (0, 1)), None)
test_make_move_capture(('x.xx.x......oooo', (1, 1), (1, 3)), 'x.xx........oxoo')
