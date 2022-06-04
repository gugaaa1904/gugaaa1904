# EXERCISE 3 SECOND PART
# Program that asks user intervals of integer numbers


import random, sys

BLANK = '  '

def main():
    print('''Sliding Tile Puzzle

            1  2  3  4  5
            6  7  8  9  10
            11 12 13 14 15 
            16 17 18 19 20
            21 22 23 24
            ''')
    input('Press Enter to begin...')

    gameBoard = getnewpuzzle()

    while True:
        for i in range(40):
            displayBoard(gameBoard)
            makeRandomMove(gameBoard)

            if gameBoard == getNewBoard():
                print('You won!')
                sys.exit()


def getNewBoard():
    return [['1 ', '6 ', '11', '16', '21'], ['2 ', '7 ', '12', '17', '22'],
            ['3 ', '8 ', '13', '18', '23'], ['4 ', '9 ', '14', '19', '24'],
            ['5 ', '10', '15', '20', BLANK]]


def displayBoard(board):
    labels = [board[0][0], board[1][0], board[2][0], board[3][0], board[4][0],
              board[0][1], board[1][1], board[2][1], board[3][1], board[4][1],
              board[0][2], board[1][2], board[2][2], board[3][2], board[4][2],
              board[0][3], board[1][3], board[2][3], board[3][3], board[4][3],
              board[0][4], board[1][4], board[2][4], board[3][4], board[4][4]]
    boardToDraw = """
+------+------+------+------+------+
|      |      |      |      |      |
|  {}  |  {}  |  {}  |  {}  |  {}  |
|      |      |      |      |      |
+------+------+------+------+------+
|      |      |      |      |      |
|  {}  |  {}  |  {}  |  {}  |  {}  |
|      |      |      |      |      |
+------+------+------+------+------+
|      |      |      |      |      |
|  {}  |  {}  |  {}  |  {}  |  {}  |
|      |      |      |      |      |
+------+------+------+------+------+
|      |      |      |      |      |
|  {}  |  {}  |  {}  |  {}  |  {}  |
|      |      |      |      |      |
+------+------+------+------+------+
|      |      |      |      |      |
|  {}  |  {}  |  {}  |  {}  |  {}  |
|      |      |      |      |      |
+------+------+------+------+------+
""".format(*labels)
    print(boardToDraw)


def findBlankSpace(board):
    for x in range(5):
        for y in range(5):
            if board[x][y] == '  ':
                return (x, y)


def askForPlayerConfirmation(board):
    response = input('>').upper()
    if response == "YES":
        return makeRandomMove(board)
    elif response == "QUIT":
        sys.exit()
    input(f"Enter YES if the user would like to make 40 random moves or QUIT if you want to quit:  {response} ")


def makeMove(board, move):
    bx, by = findBlankSpace(board)

    if move == 'W':
        board[bx][by], board[bx][by+1] = board[bx][by+1], board[bx][by]
    elif move == 'A':
        board[bx][by], board[bx+1][by] = board[bx+1][by], board[bx][by]
    elif move == 'S':
        board[bx][by], board[bx][by-1] = board[bx][by-1], board[bx][by]
    elif move == 'D':
        board[bx][by], board[bx-1][by] = board[bx-1][by], board[bx][by]


def makeRandomMove(board):
    blankx, blanky = findBlankSpace(board)
    validMoves = []
    if blanky != 4:
        validMoves.append('W')
    if blankx != 4:
        validMoves.append('A')
    if blanky != 0:
        validMoves.append('S')
    if blankx != 0:
        validMoves.append('D')

    makeMove(board, random.choice(validMoves))


def getnewpuzzle(moves=40):
    board = getNewBoard()

    for i in range(moves):
        makeRandomMove(board)
    return board

if __name__ == '__main__':
    main()




