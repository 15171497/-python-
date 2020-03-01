# -python-
90行代码实现python贪吃蛇
"""
作者：“python趣味爱好者”微信公众号。
转载请附上公众号信息
在公众号后台回复game1,game2,game3,game4.......获取更多原创小游戏。
玩法说明：
             上下左右移动：按键盘的上下左右。
             """

import pygame
import sys
from pygame.locals import*
import numpy as np
from random import randint
pygame.init()

rect_width=20
size=width,height=800,500
COLOR=(0,255,255)#蛇的颜色
x_rect=int(width/rect_width)
y_rect=int(height/rect_width)#长宽格子有多个

speed=[0,1]
bg=(255,0,0)
screen=pygame.display.set_mode(size)
pygame.display.set_caption("python趣味爱好者")
snake_new=[3,4]
font=pygame.font.Font(None,20)
food_live=1#食物的生命是否存在
Food=[12,18]#食物所在的坐标

ground=np.zeros([x_rect,y_rect])#整条蛇占据的矩阵，0是没有。

snake=[[5,5],[5,6],[5,7]]
food0=1
def get_rect(row,column):#计算应该在哪里画方格，以右上角为点。
    x1=rect_width*row
    y1=rect_width*column

    return (x1,y1,rect_width,rect_width)

#pygame.draw.rect(screen,COLOR,get_rect(row,column),0)

def move_snake(speed,food1):
    global snake_new

    k1=snake[0][0]+speed[0]
    k2=snake[0][1]+speed[1]
    snake_new=[k1,k2]
    snake.insert(0,snake_new)
    if food1==1:#如果吃到了食物就不用管了
        pass
    else:
        del snake[-1]#没吃到食物就删除最后一项
        
def meet_food(snake_pos,food_pos):
    global food0
    global food_live
    if snake_pos[0]==food_pos:
        food_live=0
        food0=1
       
    else:
        food0=0
     
    

def draw_snake(snakebody):
    for i in snakebody:
        pygame.draw.rect(screen,COLOR,get_rect(i[0],i[1]),0)



def draw_food(x,y):
    pygame.draw.rect(screen,COLOR,get_rect(x,y),0)
    
while True:
    for event in pygame.event.get():
        if event.type==pygame.QUIT:
            sys.exit()
        
        if event.type==KEYDOWN:
            if event.key==K_LEFT:
                speed=[-1,0]
            if event.key==K_RIGHT:
                speed=[1,0]
            if event.key==K_UP:
                speed=[0,-1]
            if event.key==K_DOWN:
                speed=[0,1]

    if food_live:
        pass
    else:
        Food=[randint(0,x_rect-1),randint(0,y_rect-1)]#随机生成食物的位置。
        food_live=1


   
    meet_food(snake,Food)
        

    move_snake(speed,food0)


    screen.fill(bg)
    #pygame.draw.rect(screen,(23,56,78),get_rect(10,10),0)
 
    draw_snake(snake)
    draw_food(Food[0],Food[1])
    
    pygame.display.flip()
    pygame.time.delay(180)

