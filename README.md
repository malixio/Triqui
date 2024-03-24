# Triqui
#Importar librerias
from tkinter import *
import random
#Funcion para definir turno
def next_turn(row, column):

    global player

    if buttons[row][column]['text'] == "" and check_winner() is False:

        if player == players[0]:

            buttons[row][column]['text'] = player

            if check_winner() is False:
                player = players[1]
                label.config(text=(players[1]+" Turno"))

            elif check_winner() is True:
                label.config(text=(players[0]+" Ganador"))

            elif check_winner() == "Empate":
                label.config(text="Empate!")

        else:

            buttons[row][column]['text'] = player

            if check_winner() is False:
                player = players[0]
                label.config(text=(players[0]+" Turno"))

            elif check_winner() is True:
                label.config(text=(players[1]+" Ganador"))

            elif check_winner() == "Empate":
                label.config(text="Empate!")
# Funcion para comprobar el ganador
def check_winner():

    for row in range(3):
        if buttons[row][0]['text'] == buttons[row][1]['text'] == buttons[row][2]['text'] != "":
            buttons[row][0].config(bg="navy")
            buttons[row][1].config(bg="navy")
            buttons[row][2].config(bg="navy")
            return True

    for column in range(3):
        if buttons[0][column]['text'] == buttons[1][column]['text'] == buttons[2][column]['text'] != "":
            buttons[0][column].config(bg="light grey")
            buttons[1][column].config(bg="light grey")
            buttons[2][column].config(bg="light grey")
            return True

    if buttons[0][0]['text'] == buttons[1][1]['text'] == buttons[2][2]['text'] != "":
        buttons[0][0].config(bg="light grey")
        buttons[1][1].config(bg="light grey")
        buttons[2][2].config(bg="light grey")
        return True

    elif buttons[0][2]['text'] == buttons[1][1]['text'] == buttons[2][0]['text'] != "":
        buttons[0][2].config(bg="light grey")
        buttons[1][1].config(bg="light grey")
        buttons[2][0].config(bg="light grey")
        return True

    elif empty_spaces() is False:

        for row in range(3):
            for column in range(3):
                buttons[row][column].config(bg="light grey")
        return "Empate"

    else:
        return False

#Funcion de espacion vacios
def empty_spaces():

    spaces = 9

    for row in range(3):
        for column in range(3):
            if buttons[row][column]['text'] != "":
                spaces -= 1

    if spaces == 0:
        return False
    else:
        return True
#funcion de nuevo juego
def new_game():

    global player

    player = random.choice(players)

    label.config(text=player+" Turno")

    for row in range(3):
        for column in range(3):
            buttons[row][column].config(text="",bg="#F0F0F0")

#llamado de la libreria tkinter
window = Tk()
window.title("Triqui")
players = ["X","O"]
player = random.choice(players)
window.config(bg="black")
buttons = [[0,0,0],
           [0,0,0],
           [0,0,0]]

label = Label(text=player + " Turno",bg= "black",fg= "snow" ,font=('consolas',40))
label.pack(side="top")

reset_button = Button(text="Limpiar",bg= "black" ,fg= "snow", border= 3 ,font=('consolas',20), command=new_game)
reset_button.pack(side="top")

frame = Frame(window)
frame.pack()

for row in range(3):
    for column in range(3):
        buttons[row][column] = Button(frame, text="",font=('consolas',40), width=5, height=2,
                                      command= lambda row=row, column=column: next_turn(row,column))
        buttons[row][column].grid(row=row,column=column)

window.mainloop)
