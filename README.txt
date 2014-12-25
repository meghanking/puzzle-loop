Slither Link's Puzzle Loop is a game of wits, between you and the rules I will describe 
here.

The quote below is from Slither Link's exact description copied from their website:

"The rules are simple. You have to draw lines between the dots to form a single loop 
without crossings or branches. The numbers indicate how many lines surround it."


To accomplish this monumental task, the following wil explain how, coding wise, things 
needed to accomplish such game play by my implementation such as which function calls to 
make, how to construct a map, and specifying moves on the board.


If any questions, comments, or concerns, feel free to contact me:
	Meghan King
	meghantking67@gmail.com

using the subject: Slither's Puzzle Loop Question.



Content sections are in this order:
	Map Names
	Seeing the game rules
	Making a map
	Printing a map before gameplay
	Selecting a map to play
	Starting a game
		Different game types
	AI Game Timing
	Human Game
		Making a move
		Restarting game after exiting
		Winning the game


==========================================================================================
Map Names:
Each board is named with the number the are associated with, being

one
two
three
four
...
fifteen

To choose the board, which is talked about in "Selecting a map before gameplay" you do:
	
	(makegameboard 'one)
	...
	...
	(makegameboard 'fifteen)
	


==========================================================================================
Seeing the game rules:

	Game rules can be found in the README.txt file paired with the Silther implementation.
	
	Game rules can also be printed once the game is loaded by calling the function
	'showgamerules' which has no arguments
	
		CG-USER(27): (showgamerules)

		The output of this is omitted in this case.

==========================================================================================
Making a map:

	Maps are structured as a a list. Each sublist is the rows, in order from top to
	bottom, with their contents being each element (or tile) in the corresponding column 
	of that row. Tiles that have a number should be specified with that number 
	(0, 1, 2, 3, or 4). Tiles that have no number should be specified with the @ char.

	Once a map is made, the name of the map is added to a list of all the maps created, 
	called 'maplist'. The 'maplist' is returned each time a new map is created.
	To create a map, use the function 'makemap' which takes two arguments:
		1. the name of map
		2. the contents of the map in the correct form
		
	Please only input maps that have a proper solution.



	Example of making a map:

		(+ * + * +) 
		(* 1 * 0 *) 
		(+ * + * +) 
		(* 3 * @ *) 
		(+ * + * +) 
		(* 2 * @ *) 
		(+ * + * +) 

		The map above can be created by entering:

		CG-USER(17): (makemap 'mapexample '((1 0) (3 @) (2 @)))
		(MAP1 MAP2 MAP3 MAP4 MAP5 MAP6 MAPEXAMPLE)
		

==========================================================================================
Selecting a map to play:

	Many maps can be made, but only one map can be the game board at a time. 
	To select a game board, use the function 'makegameboard' with one arguement:
		1. the name of the map
		
			CG-USER(27): (makegameboard 'mapexample)
			
			(+ * + * +) 
			(* 1 * 0 *) 
			(+ * + * +) 
			(* 3 * @ *) 
			(+ * + * +) 
			(* 2 * @ *) 
			(+ * + * +) 
			"This is now the game map. Enter (slither) to start the game."
	
	Different Game Types:
    ======================================================================================	
    The answer you your prompt will determine the type of game you will play:
    
    	The first prompt is:
    	"Would you like the AI to solve this map?"
    	
    		Yes means AI, so you will not be able to input moves, and the AI will solve 
    		the board.
    		No means Human, so you will be inputting any 
    		
    	If you chose AI, the second prompt is:
    	"Will this be timed?"
    	
    		Yes:
    		This will allow for optimal times since printing is not a option until the 
    		final solution. To actual time this, instead of calling (slither), call 
    		(time (slither))
    		
    		No: This will lead to stuff being printed out every time the loop goes 
    		through.

	
==========================================================================================
Printing a map before gameplay:

	A map can be printed with either the contents that were input by the user, or in 
	the format seen in "Example of making a map".
	
	To print with the contents input by ther user, enter the name of the map.
	
			CG-USER(17): mapexample
			((1 0) (3 @) (2 @))

	To print with the contents in the playable format, use a function 'printmap' which 
	takes no arguments. 
	However, there MUST be a game board already set using 
	'makegameboard' function.

			CG-USER(37): (printmap)

			(+ * + * +) 
			(* 1 * 0 *) 
			(+ * + * +) 
			(* 3 * @ *) 
			(+ * + * +) 
			(* 2 * @ *) 
			(+ * + * +)


==========================================================================================
Starting a game:

	After selecting a map to play (see the section of the same name above for details),
	use the function 'slither' with no arguments. 
	However, there MUST be a game board already set using 'makegameboard' function.

			CG-USER(38): (slither)

			(+ * + * +) 
			(* 1 * 0 *) 
			(+ * + * +) 
			(* 3 * @ *) 
			(+ * + * +) 
			(* 2 * @ *) 
			(+ * + * +) 
			"Intersections are valid" 
			"Some tiles are not valid" 
			"Board is still incorrect or not completed." Make another move? y/n: 
			
AI Game:

	To time a game, use the function in where printing does not occur every loop and do
	the following. Instead of calling (slither), call (time (slither))

Human Game
	======================================================================================
	Making a move:

		After starting a game, you will be prompted if you would liek to make another 
		move.
		Entering the character y will allow you to enter a move.
		Entering anything else will allow you to exit the game.
	
				"Board is still incorrect or not completed." Make another move? y/n: y
				Your next move it: 
	
		To enter a move, specify the row number, column number, and the side you would 
		like the lined to be placed (T top, L left, B bottom, R right)
	
				Your next move it: 2 2 L
			
				(+ * + * +) 
				(* 1 * 0 *) 
				(+ * + * +) 
				(* 3 I @ *) 
				(+ * + * +) 
				(* 2 * @ *) 
				(+ * + * +) 
				"Some intersections are not valid" 
				"Some tiles are not valid" 
				"Board is still incorrect or not completed." Make another move? y/n
	
		This will draw a line in the place that you have specified: 
			the second row, second column, Left side
		
		This same move could have been accomplished with 2 1 R.


	======================================================================================
	Restarting a game after exit:

		A game that was currently being played, but you chose to make no more moves 
		(eitherby accident or on purpose) can be reset to the state you left it at by 
		using the function 'slither'
	
				CG-USER(23): (slither)

				(+ = + * +) 
				(* 2 * 2 *) 
				(+ * + * +) 
				(* 2 * 2 *) 
				(+ * + * +) 
				"Some intersections are not valid" 
				"Some tiles are not valid" 
				"Board is still incorrect or not completed." Make another move? y/n: 

	======================================================================================
	Winning a game:

		A game is won by completing the board following the Slither's Puzzle Loop rules.
		The game should correctly determine if you have completed the board successfully.
		A dialog box will ask you if you want to play another board. 
		, you will be prompted to ask the play another map.
		A list of all the map names will be printed, and you can enter which map you would 
		like to select.
	
			
				You've won! Do you want to play another board?
				Choose a map: map1 map2 map3 map4 map5 map6 mapexample
			
		Type in the map name, and the process starts all over again.
	
	
================================== Thanks for playing! ==================================