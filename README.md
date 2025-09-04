# Snake_game
import os

# --- 1. Snake game code ---
snake_code = """
import curses
import random

screen = curses.initscr()
curses.curs_set(0)
height, width = screen.getmaxyx()
win = curses.newwin(height, width, 0, 0)
win.keypad(1)
win.timeout(100)

snake_x = width // 4
snake_y = height // 2
snake = [
    [snake_y, snake_x],
    [snake_y, snake_x - 1],
    [snake_y, snake_x - 2]
]

food = [height // 2, width // 2]
win.addch(food[0], food[1], curses.ACS_PI)

key = curses.KEY_RIGHT

while True:
    next_key = win.getch()
    key = key if next_key == -1 else next_key

    head = [snake[0][0], snake[0][1]]

    if key == curses.KEY_DOWN:
        head[0] += 1
    if key == curses.KEY_UP:
        head[0] -= 1
    if key == curses.KEY_LEFT:
        head[1] -= 1
    if key == curses.KEY_RIGHT:
        head[1] += 1

    snake.insert(0, head)

    if snake[0] == food:
        food = None
        while food is None:
            nf = [random.randint(1, height - 2), random.randint(1, width - 2)]
            food = nf if nf not in snake else None
        win.addch(food[0], food[1], curses.ACS_PI)
    else:
        tail = snake.pop()
        win.addch(tail[0], tail[1], ' ')

    if (snake[0][0] in [0, height] or
        snake[0][1] in [0, width] or
        snake[0] in snake[1:]):
        curses.endwin()
        print("Game Over!")
        break

    win.addch(snake[0][0], snake[0][1], curses.ACS_CKBOARD)
"""

