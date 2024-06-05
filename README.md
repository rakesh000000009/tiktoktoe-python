
def constBoard(board):
    print("current state of board: \n \n");
    for i in range (0,9):
            if ((i>0) and (i%3) == 0):
                print("\n");
            if (board [i] == 0):
                print("_ ", end= " ");
            if (board [i] == 1):
                print("O ", end= " ");
            if (board [i] == -1):
                print("X ", end= " ");
    print("\n \n ");

def user1Turn(board):
    pos = int(input("enter X position from 1 t0 9: "));
    if (board[pos-1] != 0):
        print("wrong move!");
        exit(0);
    board[pos-1] = -1;

def user2Turn(board):
    pos = int(input("enter O position from 1 t0 9: "));
    if (board[pos-1] != 0):
        print("wrong move!");
        exit(0);
    board[pos-1] = 1;

def analyseboard(board):
    cb = [[0,1,2], [3,4,5], [6,7,8], [0,3,6], [1,4,7], [2,5,8], [0,4,8], [2,4,6]];
    for i in range (0,9):
        if(board[cb[i][0]] != 0 and
          board[cb[i][0]] == board[cb[i][1]] and
          board[cb[i][0]] == board[cb[i][2]]):
            return board[cb[i][0]];
    exit(0);

def minmax(board, player):
    x = analyseboard(board);
    if(x != 0):
        return x*player;
    pos = -1;
    value = -2;
    for i in range (0,9):
        if(board[i] == 0):
            board[i] = player;
            score = -minmax(board, -player);
            board[i] = 0;
            if(score>value):
                value = score;
                pos = i;
            if(pos == -1):
                break;
            return value;

def compTurn(board):
    pos = -1;
    value = -2;
    for i in range (0,9):
        if(board[i] == 0):
            board[i] = 1;
            score = -minmax(board, -1);
            board[i] = 0;
            if(score>value):
                value = score;
                pos = i;
    board[pos] = 1;

def main():
    choice = int(input("enter 1 for single player, 2 for multi player :"));
    board = [0,0,0,0,0,0,0,0,0];
    if (choice == 1):
        print ("computer:O, your:X");
        player = int(input("choose your turn (1)st or (2)nd :"));
        for i in range (0,9):
            if (analyseboard(board) != 0):
                break;
            if((i+player)%2 == 0):
                compTurn(board);
            else:
                constBoard(board);
                user1Turn(board);
    else:
        for i in range(0,9):
            if (analyseboard(board) != 0):
                break;
            if (i%2 == 0):
                constBoard(board);
                user1Turn(board);
            else:
                constBoard(board);
                user2Turn(board);

    x = analyseboard(board);
    if (x == 0):
        constBoard(board);
        print("draw!");
    if (x == 1):
        constBoard(board);
        print("O win!");
    if (x == -1):
        constBoard(board);
        print("X win!");

