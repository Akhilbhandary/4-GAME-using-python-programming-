#INTERNPE INTERNSHIP 4TH ACTIVITY TO DO A 4 GAME USING PYTHON PROGRAMING 
THE DETAILED VIDEO IS BELOW ALONG WITH CODE 

https://github.com/user-attachments/assets/ae59653a-a65b-4980-ba96-1f51c6665c04

#THE PYHTON CODE 
import numpy as np

ROWS = 6
COLUMNS = 7
board = np.zeros((ROWS, COLUMNS), dtype=int)

def print_board(board):
   
    print(np.flip(board, 0))

def drop_piece(board, row, col, piece):
    board[row][col] = piece

def is_valid_location(board, col):
   
    return board[ROWS-1][col] == 0

def get_next_open_row(board, col):
    
    for r in range(ROWS):
        if board[r][col] == 0:
            return r

def winning_move(board, piece):
    
    for c in range(COLUMNS-3):
        for r in range(ROWS):
            if board[r][c] == piece and board[r][c+1] == piece and board[r][c+2] == piece and board[r][c+3] == piece:
                return True

    
    for c in range(COLUMNS):
        for r in range(ROWS-3):
            if board[r][c] == piece and board[r+1][c] == piece and board[r+2][c] == piece and board[r+3][c] == piece:
                return True

    
    for c in range(COLUMNS-3):
        for r in range(ROWS-3):
            if board[r][c] == piece and board[r+1][c+1] == piece and board[r+2][c+2] == piece and board[r+3][c+3] == piece:
                return True

    
    for c in range(COLUMNS-3):
        for r in range(3, ROWS):
            if board[r][c] == piece and board[r-1][c+1] == piece and board[r-2][c+2] == piece and board[r-3][c+3] == piece:
                return True

    return False

def play_game():
    
    game_over = False
    turn = 0

    while not game_over:
        
        print_board(board)

       
        if turn == 0:
            col = int(input("Player 1 (1-7): ")) - 1
            piece = 1
        else:
            col = int(input("Player 2 (1-7): ")) - 1
            piece = 2

        
        if is_valid_location(board, col):
           
            row = get_next_open_row(board, col)
            drop_piece(board, row, col, piece)

           
            if winning_move(board, piece):
                print_board(board)
                print(f"Player {piece} wins!")
                game_over = True

        
        turn += 1
        turn %= 2


play_game()
