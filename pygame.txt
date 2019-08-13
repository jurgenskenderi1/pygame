import pygame
from pygame.locals import *
pygame.init()
window = pygame.display.set_mode ((300, 325))
#Krijojm dritaren
title="Tic-Tac-Toe"
pygame.display.set_caption(title)
winner = None
#Ketu ruhet fituesi
grid = [ [ None,None,None ], \
         [ None,None,None ], \
         [ None,None,None ] ]
#Vektoret per ruajtjen e cdo levizje 
X0 = "X"
#Kush fillo levizjen e par(i cili eshte X)
running = 1
while (running == 1):
    pygame.display.set_mode ((300, 325))
def initBoard(window):
#rregullojm backgroundin
    background = pygame.Surface (window.get_size())
    background = background.convert()
    background.fill ((250, 250, 250))

    pygame.draw.line (background, (0,0,0), (100,0), (100, 300), 2)
    pygame.draw.line (background, (0,0,0), (200,0), (200, 300), 2)
    pygame.draw.line (background, (0,0,0), (0,100), (300, 100), 2)
    pygame.draw.line (background, (0,0,0), (0,200), (300, 200), 2)

    return background
def drawStatus (board):
    #djflkajfds
    #========================
    #===
    #---

    #_----
    global X0, winner

    #kkdaf
    if (winner is None):
        message = X0 + "'s turn"
    else:
        message = winner + " won!"

        #lskdald======-=-=
    font = pygame.font.Font(None, 24)
    text = font.render(message, 1, (10, 10 ,10))

    #ksadjsafjsakhf
    board.fill ((250, 250, 250), (0, 300, 300, 25))
    board.blit(text, (10, 300))
    drawStatus (board)
    window.blit (board, (0, 0))
    pygame.display.flip()
def boardPos (mouseX , mouseY):
    if (mouseY < 100):
        row = 0
    elif (mouseY < 200):
        row = 1
    else:
        row = 2
    return (row, col)
def drawMove (board, boardRow, boardCol, Piece):
    centerX =((boardCol) * 100) + 50
    centerY =((boardRow) * 100) + 50
    if (Piece == '0'):
        pygame.draw.circle (board, (0,0,0), (centerX, centerY), 44, 2)
    else:
        pygame.draw.line (board, (0,0,0), (centerX - 22, centerY - 22,) \
                         (centerX + 22, centerY + 22), 2)
        pygame.draw.line (board, (0,0,0), (centerX + 22, centerY - 22), \
                         (centerX - 22, centerY + 22), 2)
        grid [boardRow][boardCol] = Piece
while (running == 1):
    for event in pygame.event.get():
        if event.type is QUIT:
            running = 0
        elif event.type is MOUSEBUTTONDOWN:
            showBoard(window, board);
def clickBoard(board):
    global grid, X0
    (mouseX, mouseY) = pygame.mouse.get_pos()
    (row, col) = boardPos (mouseX, mouseY)

    if ((grid[row][col] == "X") or (grid[row][col] == "0")):
        return
    drawMove (board, row, col, X0)
    if (X0 == "X"):
        X0 = "0"
    else:
        X0 = "X"
def gameWon(board):
    global grid, winner
    for row in range (0, 3):
        if ((grid [row][0] == grid[row][1] == grid[row][2]) and \
            (grid [row][0] is not None)):
            winner = grid[row][0]
            pygame.draw.line (board, (250,0,0), (0, (row + 1)*100 - 50), \
                              (300, (row + 1)*100 - 50), 2)
            break
        if (grid[0][0] == grid[1][1] == grid[2][2]) and \
           (grid[0][0] is not None):
            winner = grid[0][0]
            pygame.draw.line (board, (250,0,0), (50, 50), (250, 250), 2)

        if (grid[0][2] == grid[1][1] == grid[2][0]) and \
           (grid[0][2] is not None):
            winner = grid[0][2]
            pygame.draw.line (board, (250,0,0), (250, 50), (50, 250), 2)
