import random
import math

def domino_set_create():
    all_pieces = []
    for i in range(0, 7):
        for x in range(i, 7):
            all_pieces.append([i, x])
    return all_pieces

def domino_set_mix(domino_set):
    return random.sample(domino_set, len(domino_set))

def computers_set(random_domino_set):
    return random_domino_set[:7]

def players_set(random_domino_set):
    return random_domino_set[7:14]

def stock_set(random_domino_set):
    return random_domino_set[14::]

def dubls(set_):
    dubls = []
    for x in set_:
        if x[0] == x[1]:
            dubls.append(x)
    return dubls

def start_snake(computers_dubls, players_dubls):
    if len(computers_dubls) > 0:
        max_computer = max(computers_dubls)
    else:
        max_computer = [-1, 0]
    if len(players_dubls) > 0:
        max_player = max(players_dubls)
    else:
        max_player = [-1, 0]
    if max_player == max_computer:
        start_game()
    else:
        return [max(max_player, max_computer)]

def start_player(start, computer_set, players_set):
    if start[0] in players_set:
        players_set.remove(start[0])
        status_ = "Status: Computer is about to make a move. Press Enter to continue..."
        return status_
    elif start[0] in computer_set:
        computer_set.remove(start[0])
        status_ = "Status: It's your turn to make a move. Enter your command."
        return status_

def start_design(stock_pieces, computer_pieces, player_pieces, domino_snake, status):
    print("=" * 70)
    print("Stock size:", len(stock_pieces))
    print("Computer size:", len(computer_pieces))
    print()
    print(domino_snake[0])
    print()
    print("Your pieces:")
    i = 1
    for _ in player_pieces:
        print(str(i) + ":" + str(_))
        i += 1
    print()
    print(status)

def start_game():
    """return: stock_pieces - list, comp_pi - list, play_pi - list, domino_snake - list, status - str"""
    start_set = domino_set_create()
    stock = domino_set_mix(start_set)
    stock_pieces = stock_set(stock)
    comp_pi = computers_set(stock)
    play_pi = players_set(stock)
    computer_dubls = dubls(comp_pi)
    player_dubls = dubls(play_pi)
    domino_snake = start_snake(computer_dubls, player_dubls)
    status = start_player(domino_snake, comp_pi, play_pi)
    start_design(stock_pieces, comp_pi, play_pi, domino_snake, status)
    return stock_pieces, comp_pi, play_pi, domino_snake, status

def moving(stock, set_pices, snake, move):
    moove = int(move)
    next_piceses = set_pices.pop(int(math.fabs(moove)) - 1)
    sign = moove / int(math.fabs(moove))
    if sign == -1:
        if next_piceses[1] == snake[0][0]:
            snake.insert(0, next_piceses)
        elif next_piceses[0] == snake[0][0]:
            next_piceses_orianted = [next_piceses[1], next_piceses[0]]
            snake.insert(0, next_piceses_orianted)
    else:
        if next_piceses[0] == snake[-1][-1]:
            snake.append(next_piceses)
        elif next_piceses[1] == snake[-1][-1]:
            next_piceses_orianted = [next_piceses[1], next_piceses[0]]
            snake.append(next_piceses_orianted)

def rules_check(move, set_pices, snake):
    next_piceses = set_pices[int(math.fabs(int(move))) - 1]
    sign = int(move) / int(math.fabs(int(move)))
    if sign == 1:
        if not snake[-1][-1] in next_piceses:
            return False
    elif sign == -1:
        if not snake[0][0] in next_piceses:
            return False
    return True     

def computers_choose(snake, comp_pi):
    nimbers_value = {}
    for number in range(7):
        counter = 0
        for piece in snake:
            counter += piece.count(number)
        for piece in comp_pi:
            counter += piece.count(number)
        nimbers_value[number] = counter
    pi_value = []
    picese_set = comp_pi.copy()
    for piece in comp_pi:
        value = nimbers_value[piece[0]] + nimbers_value[piece[1]]
        pi_value.append(value)
    while True:
        if len(picese_set) == 0:
            return "0"
        best_value = max(pi_value)
        index = pi_value.index(best_value)
        removed_value = pi_value.pop(index)
        chosed_piece = picese_set.pop(index)
        if snake[0][0] in [chosed_piece[0], chosed_piece[1]]:
            sign = "-"
            break
        elif snake[-1][-1] in [chosed_piece[0], chosed_piece[1]]:
            sign = ""
            break
    index = str(comp_pi.index(chosed_piece) + 1)
    chose = sign + index
    return chose

def bodi_of_game(stock_pieces, comp_pi, play_pi, domino_snake, status):
    if status == "Status: Computer is about to make a move. Press Enter to continue...":
        r = input()
        move = computers_choose(domino_snake, comp_pi)
        if move == "0":
            if len(stock_pieces) > 0:
                comp_pi.append(stock_pieces.pop())
                stop = 1
            else:
                status = "Status: It's your turn to make a move. Enter your command."
                return status
        else:
            moving(stock_pieces, comp_pi, domino_snake, move)
        status = "Status: It's your turn to make a move. Enter your command."
        return status
    elif status == "Status: It's your turn to make a move. Enter your command.":
        move = input()
        stop = 0
        while stop == 0:
            if move == "0":
                if len(stock_pieces) > 0:
                    play_pi.append(stock_pieces.pop())
                    stop = 1
                else:
                    stop = 1                   
            elif not (move.replace("-","").isdigit() and int(move) in list(range(-len(play_pi),len(play_pi) + 1))):
                print("Invalid input. Please try again.")
                move = input()
            elif rules_check(move, play_pi, domino_snake):
                moving(stock_pieces, play_pi, domino_snake, move)
                stop = 1
            else:
                print("Illegal move. Please try again.")
                move = input()
        status = "Status: Computer is about to make a move. Press Enter to continue..."
        return status
        
def bodi_design(stock_pieces, comp_pi, play_pi, snake, status):
    print("=" * 70)
    print("Stock size:", len(stock_pieces))
    print("Computer size:", len(comp_pi))
    print()
    if len(snake) <= 6:
        print(*snake, sep="")
    else:
        print(snake[0], snake[1], snake[2], "...", snake[-3], snake[-2], snake[-1], sep="")
    print()
    print("Your pieces:")
    i = 1
    for _ in play_pi:
        print(str(i) + ":" + str(_))
        i += 1
    print()
    print(status)

def draw_check(snake):
    end_number = snake[0][0]
    counter = 0
    for picese in snake:
        counter += picese.count(end_number)
    return counter == 8 and snake[0][0] == snake[-1][-1]
       
def stop_check(comp_pi, play_pi, snake, status):
    if status == "Status: Computer is about to make a move. Press Enter to continue...":
        if len(play_pi) == 0:
            status = "Status: The game is over. You won!"
        elif draw_check(snake):
            status = "Status: The game is over. It's a draw!"
    elif status == "Status: It's your turn to make a move. Enter your command.":
        if len(comp_pi) == 0:
            status = "Status: The game is over. The computer won!"
        elif draw_check(snake):
            status = "Status: The game is over. It's a draw!"
    return status

def finish_design(stock_pieces, comp_pi, play_pi, snake, status):
    print("=" * 70)
    print("Stock size:", len(stock_pieces))
    print("Computer size:", len(comp_pi))
    print()
    if len(snake) <= 6:
        print(*snake, sep="")
    else:
        print(snake[0], snake[1], snake[2], "...", snake[-3], snake[-2], snake[-1], sep="")
    print()
    print("Your pieces:")
    i = 1
    for _ in play_pi:
        print(str(i) + ":" + str(_))
        i += 1
    print()
    print(status)
    
stock_pieces, comp_pi, play_pi, domino_snake, status = start_game()
status = bodi_of_game(stock_pieces, comp_pi, play_pi, domino_snake, status)
while status[-1] == ".":
    bodi_design(stock_pieces, comp_pi, play_pi, domino_snake, status)
    status = bodi_of_game(stock_pieces, comp_pi, play_pi, domino_snake, status)
    status = stop_check(comp_pi, play_pi, domino_snake, status)
finish_design(stock_pieces, comp_pi, play_pi, domino_snake, status)
