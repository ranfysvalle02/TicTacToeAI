# TicTacToeAI
![](https://files.realpython.com/media/Build-an-AI-Game-Engine-for-Tic-Tac-Toe-in-Python_Watermarked.b90cdf84c417.jpg)
__Image credit to [Build a Tic-Tac-Toe Game Engine With an AI Player in Python](https://realpython.com/tic-tac-toe-ai-python/)__

**Introduction**

In the rapidly evolving landscape of artificial intelligence, the **minimax algorithm** has long been a cornerstone of strategic decision-making. Originally designed for two-player games, its potential now extends far beyond the realm of entertainment. As generative AI and advanced robotics continue to push boundaries, minimax emerges as a powerful tool for developing intelligent systems capable of navigating complex and uncertain environments. 

Minimax is primarily a decision tree-based AI. It constructs a tree representing all possible game states and evaluates them recursively. This approach is well-suited for games with a finite number of states and actions.

Neural networks, on the other hand, are typically used for tasks involving pattern recognition, prediction, and classification. They are inspired by the structure and function of the human brain and learn from data through training. While neural networks can be used for game playing, they often require large amounts of data and training time to achieve competitive performance compared to algorithms like minimax.

## From Minimax to Neural Networks: A Journey Through AI

**Minimax** and **neural networks** represent two distinct approaches to artificial intelligence, each with its own strengths and limitations. While minimax is well-suited for strategic game-playing, neural networks excel in pattern recognition and learning from data. Let's explore the key differences and potential synergies between these two AI paradigms.

**Minimax: A Strategic Decision Maker**

Minimax is a decision-making algorithm that recursively explores all possible game states, selecting the move that maximizes the player's chances of winning. It's a powerful tool for games like chess and Go, where the number of possible moves and outcomes is relatively limited.

**Neural Networks: Learning from Data**

Neural networks, inspired by the human brain, are composed of interconnected nodes (neurons) that process and learn from data. They are particularly effective at tasks like image recognition, natural language processing, and prediction. Neural networks learn by adjusting the weights between neurons through a process called backpropagation.

**Synergies Between Minimax and Neural Networks**

While minimax and neural networks may seem fundamentally different, there are opportunities for synergy:

1. **Hybrid Approaches:** Combining minimax with neural networks can create more powerful AI systems. For example, a neural network could be used to predict the outcome of a game state, and then minimax could be employed to select the best move based on the predicted outcomes.
2. **Learning from Minimax:** Neural networks can learn from the strategies generated by minimax algorithms. By training on a dataset of minimax-generated moves, a neural network can develop a better understanding of optimal gameplay.
3. **Improving Minimax with Neural Networks:** Neural networks can be used to improve the efficiency of minimax algorithms. For instance, a neural network could predict promising move sequences, reducing the number of states that need to be explored.

Both minimax and neural networks have their unique strengths and can be applied to a variety of AI tasks. By understanding their complementary nature, we can develop more powerful and versatile AI systems that can excel in both strategic decision-making and data-driven learning.

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

**Real-World Applications of Minimax Algorithm Beyond Robotics**

While the application of the minimax algorithm in robotics is fascinating, its potential extends far beyond this realm. Here are some intriguing case studies where this decision-making algorithm has been applied:

**1. Finance and Economics:** The world of finance and economics thrives on strategic decision-making. The minimax algorithm has found its place here, modeling and predicting market behavior to aid investors in making informed decisions. For instance, it can be used to determine the optimal pricing strategy for a product or service, taking into account all possible reactions from competitors and the market.

**2. Medical Diagnosis:** The healthcare sector is increasingly leveraging AI, particularly machine learning and decision tree algorithms like minimax, to improve diagnostic accuracy. These algorithms can analyze vast amounts of data to predict the likelihood of various diseases, thereby assisting doctors in making better-informed decisions about treatment plans.

**3. Environmental Management:** The minimax algorithm has a role to play in environmental management as well. It aids in making decisions that strike a balance between the needs of the environment and human activity. For example, it can help determine the optimal strategy for managing a forest, considering factors like timber production, biodiversity conservation, and carbon sequestration.

**4. Supply Chain and Logistics:** In the realm of supply chain management and logistics, the minimax algorithm can optimize routes and schedules. This can lead to cost reduction, improved efficiency, and minimization of the impact of disruptions.

**5. Cybersecurity:** The field of cybersecurity is another area where the minimax algorithm shines. It can be used to anticipate potential attacks and determine the best defense strategy. This involves predicting the moves of an attacker and deciding on the optimal response to minimize potential damage.

**6. Energy Management:** Minimax algorithms can be employed in energy management systems to optimize the use of resources and reduce costs. For example, they can help determine the optimal schedule for using and storing energy in a microgrid, considering factors like energy demand, production, and storage capacity.

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
