# OOP Tic Tac Toe project from [the Odin Project](https://www.theodinproject.com/courses/ruby-programming/lessons/oop)

### Helpful resources:

* [Creating a Tic Tac Toe Game with Ruby](https://codequizzes.wordpress.com/2013/10/25/creating-a-tic-tac-toe-game-with-ruby/)
* [Introduction to Ruby](https://learn.co/tracks/introduction-to-ruby)
* [Ruby/wiki/Справочник](https://ru.wikibooks.org/wiki/Ruby/%D0%A1%D0%BF%D1%80%D0%B0%D0%B2%D0%BE%D1%87%D0%BD%D0%B8%D0%BA/Enumerable#Enumerable#all?)
* [Ruby-Doc.org](https://ruby-doc.org/)
* [Object-oriented Programming in 7 minutes](https://www.youtube.com/watch?v=pTB0EiLXUC8)

### Videos:
  * [Welcome to Tic Tac Toe Display Board](https://www.youtube.com/watch?v=eTHFavSQQkY)
  * [Building out the board.rb class](https://www.youtube.com/watch?v=AD50ztTWW8Q)
  * [ Building out the player, human, and the beginning of the game class.](https://www.youtube.com/watch?v=pd6RFZp3QHg)
  * [Building your first of many ruby gems with dB](https://www.youtube.com/watch?v=NF_btGRGVnk)


### Inroduction to Ruby creating Tic Tac Toe:

Name of solution | Project on github
--- | --- 
Reading Error Messages | [reading-error-messages-ruby](https://github.com/Anna-Myzukina/ruby-lecture-reading-error-messages-ruby-intro-000) 
TDD, Rspec, and Learn | [intro-to-tdd-rspec-and-learn-ruby](https://github.com/Anna-Myzukina/intro-to-tdd-rspec-and-learn-ruby-intro-000)
Debugging/my first ruby gem | [frgom](https://github.com/Anna-Myzukina/frgom)
Interpolation Super Power | [interpolation-super-power-ruby](https://github.com/Anna-Myzukina/interpolation-super-power-ruby-intro-000)
Tic Tac Toe Play Loop | [play-loop-ruby](https://github.com/Anna-Myzukina/ttt-9-play-loop-ruby-intro-000)
Tic Tac Toe Current Player | [current-player-ruby](https://github.com/Anna-Myzukina/ttt-10-current-player-ruby-intro-000)
Tic Tac Toe Game Status | Here win combinations [game-status-ruby](https://github.com/Anna-Myzukina/ttt-game-status-ruby-intro-000)
solution | my project
OO Tic Tac Toe | [oo-tic-tac-toe-ruby](https://github.com/Anna-Myzukina/oo-tic-tac-toe-ruby-intro-000)
### Main logic of this game/ A turn of Tic Tac Toe is composed of the following routine:

1. Asking the user for their move by position 1-9.
  * You can imagine the pseudocode for the #turn method:

          ask for input
          get input
          convert input to index
          if index is valid
            make the move for index
            show the board
          else
            ask for input again until you get a valid input
          end
1. Receiving the user input.
1. Convert position to an index.
1. If the move is valid, make the move and display the board to the user.
1. If the move is invalid, ask for a new move until a valid move is received.

class TicTacToe
  attr_accessor :board

  def initialize
    @board = [" ", " ", " ", " ", " ", " ", " ", " ", " "]
  end

  WIN_COMBINATIONS = [
  [0, 1, 2],
  [3, 4, 5],
  [6, 7, 8],
  [0, 3, 6],
  [1, 4, 7],
  [2, 5, 8],
  [6, 4, 2],
  [0, 4, 8]
]

  def display_board
    puts " #{@board[0]} | #{@board[1]} | #{@board[2]} "
    puts " ----------- "
    puts " #{@board[3]} | #{@board[4]} | #{@board[5]} "
    puts " ----------- "
    puts " #{@board[6]} | #{@board[7]} | #{@board[8]} "
  end

  def input_to_index(input)
    input.to_i - 1
  end

  def move(position, token='X')
    @board[position] = token
  end

  def position_taken?(input)
    @board[input] == "X" || @board[input] == "O"
  end

  def valid_move?(input)
    input.between?(0, 8) && !position_taken?(input)
  end


  def turn
    puts "Choose a spot between 1-9"
    spot = gets.strip
    spot = input_to_index(spot)
    if valid_move?(spot)
      move(spot, current_player)
    else
      turn
    end
    display_board
  end

  def turn_count
    taken = 0
    @board.each do |i|
      if i == "X" || i == "O"
        taken += 1
      end
    end
    return taken
  end

  def current_player
    player = nil
    if turn_count() % 2 == 0
      player = 'X'
    else
      player = 'O'
    end
    return player
  end


  def won?
    WIN_COMBINATIONS.detect do |combo|
      @board[combo[0]] == @board[combo[1]] &&
      @board[combo[1]] == @board[combo[2]] &&
      position_taken?(combo[0])
    end
  end

  def full?
    turn_count == 9
  end

  def draw?
    !won? && full?
  end

  def over?
    won? || full? || draw?
  end

  def winner
    won = ""
    if winner = won?
      won = @board[winner.first]
    end
  end

  def play
    until over?
      turn
    end

    if won?
      winner = winner()
      puts "Congratulations #{winner}!"
    elsif draw?
      puts "Cat's Game!"
    end
  end
end

game = TicTacToe.new
game.play
