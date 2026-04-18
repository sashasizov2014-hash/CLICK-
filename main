import pygame as p
from random import randint
from time import time

p.init()

RED = (255, 0, 0)
GREEN = (0, 255, 51)
BlUE = (0, 0, 255)
ORANGE = (255, 123, 0)
WHITE = (255, 255, 255)
YELLOW = (255, 255, 0)
LIGHT_GREEN = (200, 255, 200)
LIGHT_RED = (250, 128, 114)
BLACK = (0, 0, 0)
DARK_BLUE = (0, 0, 100)
LIGHT_BLUE = (200, 255, 255)

scene = p.display.set_mode((500, 500))
scene.fill(LIGHT_BLUE)

clock = p.time.Clock()

class Area():
    def __init__(self, x=0, y=0, width=10, height=10, s_color=None):
        self.rect = p.Rect(x, y, width, height)
        self.fill_color = s_color
    
    def color(self, new_color):
        self.fill_color = new_color

    def fill_card(self):
        p.draw.rect(scene, self.fill_color, self.rect)

    def outline(self, frame_color, thickness):
        p.draw.rect(scene, frame_color, self.rect, thickness)
    
    def collidepoint(self, x, y):
        return self.rect.collidepoint(x,y)

class Label(Area):
    def set_text(self, text, f_size=20, t_color=BLACK):
        self.image = p.font.SysFont('verdane', f_size).render(text, True, t_color)
    
    def draw(self, shift_x=0, shift_y=0):
        self.fill_card()
        scene.blit(self.image, (self.rect.x + shift_x, self.rect.y + shift_y))

card_list = []
x = 50
for i in range(4):
    card = Label(x, 100, 70, 100, YELLOW)
    card.set_text('CLICK!', 25)
    card.outline(DARK_BLUE, 10)
    card_list.append(card)
    x += 100

text_score = Label(0, 0, 60, 25, LIGHT_BLUE)
text_score.set_text('Счёт', 40)
text_score.draw()

score = Label(0, 30, 60, 25, LIGHT_BLUE)
score.set_text('0', 40)
score.draw(15)

text_time = Label(400, 0, 70, 25, LIGHT_BLUE)
text_time.set_text('Время', 40)
text_time.draw()

timer = Label(400, 30, 60, 25, LIGHT_BLUE)
timer.set_text('0', 40)
timer.draw(15)

start_time = time()
cur_time = start_time

points = 0 
wait = 0
while True:
    new_time = time()
    if new_time - cur_time >= 1:
        timer.set_text(str(int(new_time - start_time)), 40)
        timer.draw(15)
        cur_time = new_time

    if new_time - start_time >= 10:
        game_ower = Label(0,0, 500, 500, LIGHT_RED)
        game_ower.set_text('You are IDIOT))))', 40)
        game_ower.draw(150, 200)
        break

    if points >= 10:
        game_ower = Label(0,0, 500, 500, LIGHT_GREEN)
        game_ower.set_text('You ban!! But you are IDIOT((((', 40)
        game_ower.draw(100, 200)
        break

    if wait == 0:
        wait = 25
        r_click = randint(1, 4)
        for i in range(4):
            card_list[i].color(YELLOW)
            if i+1 == r_click:
                card_list[i].draw(10,40)
            else:
                card_list[i].fill_card()
    else:
        wait -= 1

    for event in p.event.get():
        if event.type == p.MOUSEBUTTONDOWN and event.button == 1:
            x,y = event.pos
            for i in range(4):
                if card_list[i].collidepoint(x,y):
                    if i+1 == r_click:
                        card_list[i].color(GREEN)
                        points +=1
                    else:
                        card_list[i].color(RED)
                        points -= 1
                    card_list[i].fill_card()
                    score.set_text(str(points), 40)
                    score.draw(15)


    p.display.update()
    clock.tick(40)

p.display.update()
