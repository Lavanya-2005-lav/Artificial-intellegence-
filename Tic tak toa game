import math

def print_board(board):
    print("\n")
    for row in board:
        print(" | ".join(row))
        print("-" * 9)
    print("\n")


def check_winner(board, player):
    for row in board:
        if all(cell == player for cell in row):
            return True

    for col in range(3):
        if all(board[row][col] == player for row in range(3)):
            return True

    if all(board[i][i] == player for i in range(3)):
        return True
    if all(board[i][2 - i] == player for i in range(3)):
        return True

    return False


def is_full(board):
    return all(cell != ' ' for row in board for cell in row)


def get_human_move(board):
    while True:
        try:
            move = input("Enter your move (row and column: 1 1): ")
            row, col = map(int, move.split())
            row -= 1
            col -= 1

            if row not in range(3) or col not in range(3):
                print("Please enter values between 1 and 3.")
                continue

            if board[row][col] != ' ':
                print("That cell is already taken. Try again.")
                continue

            return row, col
        except ValueError:
            print("Invalid input. Enter row and column numbers separated by a space.")


def minimax(board, depth, is_maximizing, human, computer):
    if check_winner(board, computer):
        return 1
    elif check_winner(board, human):
        return -1
    elif is_full(board):
        return 0

    if is_maximizing:
        best_score = -math.inf
        for i in range(3):
            for j in range(3):
                if board[i][j] == ' ':
                    board[i][j] = computer
                    score = minimax(board, depth + 1, False, human, computer)
                    board[i][j] = ' '
                    best_score = max(score, best_score)
        return best_score
    else:
        best_score = math.inf
        for i in range(3):
            for j in range(3):
                if board[i][j] == ' ':
                    board[i][j] = human
                    score = minimax(board, depth + 1, True, human, computer)
                    board[i][j] = ' '
                    best_score = min(score, best_score)
        return best_score


def get_best_move(board, human, computer):
    best_score = -math.inf
    move = None

    for i in range(3):
        for j in range(3):
            if board[i][j] == ' ':
                board[i][j] = computer
                score = minimax(board, 0, False, human, computer)
                board[i][j] = ' '
                if score > best_score:
                    best_score = score
                    move = (i, j)
    return move


def play_game():
    board = [[' ' for _ in range(3)] for _ in range(3)]
    human = 'X'
    computer = 'O'
    current_player = human  # Human starts first

    print("Welcome to Tic-Tac-Toe (You vs Unbeatable Computer)!")
    print_board(board)

    while True:
        if current_player == human:
            row, col = get_human_move(board)
        else:
            print("Computer is making a smart move...")
            row, col = get_best_move(board, human, computer)

        board[row][col] = current_player
        print_board(board)

        if check_winner(board, current_player):
            if current_player == human:
                print("🎉 You win!")
            else:
                print("💻 Computer wins!")
            break

        if is_full(board):
            print("It's a draw!")
            break

        # Switch turns
        current_player = computer if current_player == human else human


if __name__ == "__main__":
    play_game()
