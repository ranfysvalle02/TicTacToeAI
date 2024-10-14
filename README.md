# TicTacToeAI

**Introduction**

In the rapidly evolving landscape of artificial intelligence, the **minimax algorithm** has long been a cornerstone of strategic decision-making. Originally designed for two-player games, its potential now extends far beyond the realm of entertainment. As generative AI and advanced robotics continue to push boundaries, minimax emerges as a powerful tool for developing intelligent systems capable of navigating complex and uncertain environments. 

Minimax is primarily a decision tree-based AI. It constructs a tree representing all possible game states and evaluates them recursively. This approach is well-suited for games with a finite number of states and actions.

Neural networks, on the other hand, are typically used for tasks involving pattern recognition, prediction, and classification. They are inspired by the structure and function of the human brain and learn from data through training. While neural networks can be used for game playing, they often require large amounts of data and training time to achieve competitive performance compared to algorithms like minimax.

**The Minimax Algorithm: A Strategic Foundation**
Just as minimax analyzes all potential future states to determine the best move, Doctor Strange evaluates countless possible outcomes in his quest to protect the universe. The two share a common goal: optimizing decisions by considering multiple future scenarios.

While Doctor Strange’s approach relies on magic, the underlying concept of optimizing decisions by anticipating outcomes is a common thread that ties minimax and Strange together.

At its core, the minimax algorithm is a recursive decision-making process that helps a player maximize their chances of winning while minimizing potential losses from an opponent's moves. By constructing a decision tree, minimax explores every possible move and its corresponding outcomes, allowing for optimal strategic planning. 

The algorithm constructs a decision tree where:
- **Maximizing Player**: The AI, aiming to maximize its score (win).
- **Minimizing Player**: The opponent, attempting to minimize the AI's score (prevent a loss).

At the leaves of this tree, terminal nodes (end states) are assigned values:
- Win = 1
- Loss = -1
- Draw = 0

The algorithm then backtracks through the tree:
- The maximizing player selects the maximum value from child nodes.
- The minimizing player selects the minimum value.

In a simple game of Tic Tac Toe, the AI uses the minimax algorithm to explore all possible moves, evaluating outcomes and counter-moves from the player. This enables the AI to choose the move that leads to the best possible outcome.

**A New Frontier: Minimax and Generative AI**

The synergy between minimax and generative AI is particularly exciting. Generative AI, with its ability to create new content and solutions, can augment the decision-making capabilities of minimax. Imagine a robotic system that not only predicts the consequences of its actions but also generates potential scenarios to adapt and optimize its strategies. This could revolutionize fields like autonomous vehicles and industrial robotics.

**Robotics: A Strategic Playground**

In the realm of robotics, minimax can be a game-changer. By enabling robots to anticipate and react to multiple variables in real-time, minimax can enhance their ability to:

* **Navigate complex environments:** From bustling cities to hazardous terrains, minimax can help robots make informed decisions to avoid obstacles and reach their goals.
* **Collaborate effectively:** In scenarios where multiple robots work together, minimax can facilitate strategic coordination and ensure efficient task completion.
* **Adapt to changing conditions:** By continuously evaluating potential outcomes, minimax can help robots adapt to unexpected challenges and make adjustments on the fly.


## Full Code
```python
class TicTacToe:
    def __init__(self):
        self.board = [[0 for _ in range(3)] for _ in range(3)]
        
    def print_board(self):
        for row in self.board:
            print(' | '.join('X' if cell == 1 else 'O' if cell == -1 else ' ' for cell in row))
            print('---------')

def check_winner(board):
    # Check rows and columns
    for i in range(3):
        if abs(sum(board[i])) == 3:  # Row check
            return board[i][0]
        if abs(sum(board[j][i] for j in range(3))) == 3:  # Column check
            return board[0][i]

    # Check diagonals
    if abs(board[0][0] + board[1][1] + board[2][2]) == 3:
        return board[1][1]
    if abs(board[0][2] + board[1][1] + board[2][0]) == 3:
        return board[1][1]

    return 0  # No winner

def is_draw(board):
    return all(cell != 0 for row in board for cell in row)

def minimax(board, depth, is_maximizing):
    winner = check_winner(board)
    if winner == 1:
        return 1  # AI wins
    elif winner == -1:
        return -1  # Opponent wins
    elif is_draw(board):
        return 0  # Draw

    if is_maximizing:
        best_score = float('-inf')
        for i in range(3):
            for j in range(3):
                if board[i][j] == 0:  # If the cell is empty
                    board[i][j] = 1  # AI move
                    score = minimax(board, depth + 1, False)
                    board[i][j] = 0  # Undo the move
                    best_score = max(score, best_score)
        return best_score
    else:
        best_score = float('inf')
        for i in range(3):
            for j in range(3):
                if board[i][j] == 0:  # If the cell is empty
                    board[i][j] = -1  # Opponent move
                    score = minimax(board, depth + 1, True)
                    board[i][j] = 0  # Undo the move
                    best_score = min(score, best_score)
        return best_score

def best_move(board):
    # First, check if the AI can win in the next move
    for i in range(3):
        for j in range(3):
            if board[i][j] == 0:  # If the cell is empty
                board[i][j] = 1  # AI move
                if check_winner(board) == 1:
                    return (i, j)  # Return winning move
                board[i][j] = 0  # Undo the move

    # Check if the player can win in the next move and block it
    for i in range(3):
        for j in range(3):
            if board[i][j] == 0:  # If the cell is empty
                board[i][j] = -1  # Pretend the opponent moves
                if check_winner(board) == -1:
                    board[i][j] = 0  # Undo the move
                    return (i, j)  # Block opponent's winning move
                board[i][j] = 0  # Undo the move

    # If no immediate win or block, find the best move using minimax
    best_score = float('-inf')
    move = (-1, -1)
    for i in range(3):
        for j in range(3):
            if board[i][j] == 0:  # If the cell is empty
                board[i][j] = 1  # AI move
                score = minimax(board, 0, False)
                board[i][j] = 0  # Undo the move
                if score > best_score:
                    best_score = score
                    move = (i, j)
    return move

def play_game():
    game = TicTacToe()
    print("Welcome to Tic Tac Toe!")
    print("You are 'O' and the AI is 'X'.")
    print("Enter your move as two numbers separated by a space (row and column) between 0 and 2.")

    # AI (X) makes the first move
    move = best_move(game.board)
    if move != (-1, -1):
        game.board[move[0]][move[1]] = 1  # AI makes a move

    while True:
        game.print_board()
        
        if is_draw(game.board):
            print("It's a draw!")
            break
        
        # Player (O) move
        while True:
            try:
                row, col = map(int, input("Enter your move (row col): ").split())
                if row < 0 or row > 2 or col < 0 or col > 2:
                    print("Row and column must be between 0 and 2. Please try again.")
                    continue
                if game.board[row][col] == 0:
                    game.board[row][col] = -1  # User makes a move
                    break
                else:
                    print("Cell already occupied. Try again.")
            except (ValueError, IndexError):
                print("Invalid move. Enter row and column as two numbers between 0 and 2.")

        if check_winner(game.board) == -1:
            game.print_board()
            print("You (O) win!")
            break
        
        # AI (X) move
        move = best_move(game.board)
        if move != (-1, -1):
            game.board[move[0]][move[1]] = 1  # AI makes a move
            if check_winner(game.board) == 1:
                game.print_board()
                print("AI (X) wins!")
                break

# Start the game
play_game()


```
