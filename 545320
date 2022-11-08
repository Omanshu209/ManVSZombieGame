
import pygame
import random

pygame.init()

win = pygame.display.set_mode((500,480))

pygame.display.set_caption("Game!")

walkRight = [pygame.image.load('R1.png'), pygame.image.load('R2.png'), pygame.image.load('R3.png'), pygame.image.load('R4.png'), pygame.image.load('R5.png'), pygame.image.load('R6.png'), pygame.image.load('R7.png'), pygame.image.load('R8.png'), pygame.image.load('R9.png')]

walkLeft = [pygame.image.load('L1.png'), pygame.image.load('L2.png'), pygame.image.load('L3.png'), pygame.image.load('L4.png'), pygame.image.load('L5.png'), pygame.image.load('L6.png'), pygame.image.load('L7.png'), pygame.image.load('L8.png'), pygame.image.load('L9.png')]

bg = pygame.image.load('bg3i.jpg')
char = pygame.image.load('standing.png')
win_p=pygame.image.load('win.jpg')
lose_p=pygame.image.load("lose.jpg")

clock = pygame.time.Clock()

score=0

music=pygame.mixer.music.load("bgmusic2.mp3")
pygame.mixer.music.play(-1)
b_sound=pygame.mixer.Sound("bullet.mp3")
h_sound=pygame.mixer.Sound("hit.mp3")
c_sound=pygame.mixer.Sound("click.mp3")
l_sound=pygame.mixer.Sound("Fail.mp3")
hitm_sound=pygame.mixer.Sound("hitm.mp3")
w_sound=pygame.mixer.Sound("Win.mp3")

class player(object):
    def __init__(self,x,y,width,height):
        self.x = x
        self.y = y
        self.width = width
        self.height = height
        self.vel = 5
        self.isJump = False
        self.left = False
        self.right = False
        self.walkCount = 0
        self.jumpCount = 10
        self.standing = True
        self.hitbox=(self.x+20,self.y+10,26,50)

    def draw(self, win):
        if self.walkCount + 1 >= 27:
            self.walkCount = 0

        if not(self.standing):
            if self.left:
                win.blit(walkLeft[self.walkCount//3], (self.x,self.y))
                self.walkCount += 1
            elif self.right:
                win.blit(walkRight[self.walkCount//3], (self.x,self.y))
                self.walkCount +=1
        else:
            if self.right:
                win.blit(walkRight[0], (self.x, self.y))
            else:
                win.blit(walkLeft[0], (self.x, self.y))
        self.hitbox=(self.x+20,self.y+10,26,50)
        if keys[pygame.K_s]:
            pygame.draw.rect(win,(0,255,0),self.hitbox,2)
        
    def hit(self):
         if score>=-24:
         	self.x=5
         	self.walkCount = 0
         	font1 = pygame.font.SysFont('comicsans', 100)
         	text = font1.render('-5', 1, (255,0,0))
         	win.blit(text, (250 - (text.get_width()/2),200))
         	pygame.display.update()
         	i=0
         	while i < 100 :
         	    pygame.time.delay(10)
         	    i += 1
         	    for event in pygame.event.get():
         	             if event.type == pygame.QUIT:
         	             	 i = 301
         	             	 pygame.quit()


class projectile(object):
    def __init__(self,x,y,radius,color,facing):
        self.x = x
        self.y = y
        self.radius = radius
        self.color = color
        self.facing = facing
        self.vel = 8 * facing

    def draw(self,win):
        pygame.draw.circle(win, self.color, (self.x,self.y), self.radius)


class enemy(object):
    walkRight = [pygame.image.load('R1E.png'), pygame.image.load('R2E.png'), pygame.image.load('R3E.png'), pygame.image.load('R4E.png'), pygame.image.load('R5E.png'), pygame.image.load('R6E.png'), pygame.image.load('R7E.png'), pygame.image.load('R8E.png'), pygame.image.load('R9E.png'), pygame.image.load('R10E.png'), pygame.image.load('R11E.png')]
    
    walkLeft = [pygame.image.load('L1E.png'), pygame.image.load('L2E.png'), pygame.image.load('L3E.png'), pygame.image.load('L4E.png'), pygame.image.load('L5E.png'), pygame.image.load('L6E.png'), pygame.image.load('L7E.png'), pygame.image.load('L8E.png'), pygame.image.load('L9E.png'), pygame.image.load('L10E.png'), pygame.image.load('L11E.png')]
    
    def __init__(self, x, y, width, height, end):
        self.x = x
        self.y = y
        self.width = width
        self.height = height
        self.path = [x, end]
        self.walkCount = 0
        self.vel = 3
        self.hitbox=(self.x+17,self.y+2,31,57)

    def draw(self, win):
        self.move()
        if self.walkCount + 1 >= 33:
            self.walkCount = 0
        
        if self.vel > 0:
            win.blit(self.walkRight[self.walkCount//3], (self.x,self.y))
            self.walkCount += 1
        else:
            win.blit(self.walkLeft[self.walkCount//3], (self.x,self.y))
            self.walkCount += 1
        self.hitbox=(self.x+17,self.y+2,31,57)
        if keys[pygame.K_s]:
            pygame.draw.rect(win,(0,255,0),self.hitbox,2)
            
    def move(self):
        if self.vel > 0:
            if self.x < self.path[1] + self.vel:
                self.x += self.vel
            else:
                self.vel *= -1
                self.x += self.vel
                self.walkCount = 0
        else:
            if self.x > self.path[0] - self.vel:
                self.x += self.vel
            else:
                self.vel = self.vel * -1
                self.x += self.vel
                self.walkCount = 0
                
    def hit(self):
        print('hit')

def redrawGameWindow():
    if score<100 and score>=-24 :
	    win.fill((150,150,255))
	    win.blit(bg, (0,0))
	    text=font.render("Score:: "+str(score),1,(0,255,0))
	    text2=font2.render("Made By OMANSHU",1,(0,220,220))
	    text3=font3.render("MOVE LEFT::LEFT KEY",1,(120,200,175))
	    text4=font4.render("MOVE RIGHT::RIGHT KEY",1,(120,200,175))
	    text5=font5.render("JUMP::UP KEY",1,(120,200,175))
	    text6=font6.render("TELEPORT:: T",1,(120,200,175))
	    text7=font7.render("SHOOT BULLETS::SPACE KEY",1,(120,200,175))
	    text8=font8.render("RESET:: R",1,(120,200,175))
	    text9=font9.render("SCORE>=100:: YOU WIN",1,(255,255,120))
	    text10=font10.render("SCORE<= --25:: YOU LOSE",1,(255,255,120))
	    text11=font11.render("DISPLAY HITBOX:: S",1,(120,200,175))
	    win.blit(text11,(20,80))
	    win.blit(text10,(370,60))
	    win.blit(text9,(370,50))
	    win.blit(text8,(20,70))
	    win.blit(text7,(20,60))
	    win.blit(text6,(20,50))
	    win.blit(text5,(20,40))
	    win.blit(text4,(20,30))
	    win.blit(text2,(400,520))
	    win.blit(text3,(20,20))
	    win.blit(text,(370,20))
	    pygame.draw.rect(win,(150,150,255),(15,15,185,77),2)
	    pygame.draw.rect(win,(150,155,255),(365,47,165,25),2)
	    pygame.draw.rect(win,(255,165,0),(60,420,5,50))
	    man.draw(win)
	    goblin.draw(win)
	    goblin2.draw(win)
	    goblin3.draw(win)
	    for bullet in bullets:
	        bullet.draw(win)
	    
    if score>=100:
        pygame.mixer.music.stop()
        w_sound.play()
        win.fill((150,150,255))
        win.blit(win_p,(0,0))
        text1B=font1B.render("REPLAY [ R ]",1,(120,200,175))
        win.blit(text1B,(105,340))
            
    if score<=-25:
        hitm_sound.stop()
        pygame.mixer.music.stop()
        l_sound.play()
        win.fill((150,150,255))
        win.blit(lose_p,(0,0))
        text1B=font1B.render("REPLAY [ R ]",1,(120,200,175))
        win.blit(text1B,(175,425))	
    
    pygame.display.update()


#mainloop
font=pygame.font.SysFont("comicsans",40,True)
font2=pygame.font.SysFont("comicsans",20,True,True)
font3=pygame.font.SysFont("comicsans",15,True)
font4=pygame.font.SysFont("comicsans",15,True)
font5=pygame.font.SysFont("comicsans",15,True)
font6=pygame.font.SysFont("comicsans",15,True)
font7=pygame.font.SysFont("comicsans",15,True)
font8=pygame.font.SysFont("comicsans",15,True)
font1B=pygame.font.SysFont("comicsans",50,True)
font9=pygame.font.SysFont("comicsans",15,True)
font10=pygame.font.SysFont("comicsans",15,True)
font11=pygame.font.SysFont("comicsans",15,True)
man = player(5, 410, 64,64)
goblin = enemy(75, 415, 64, 64, 250)
goblin2=enemy(250, 415, 64, 64, 490)
goblin3=enemy(50,415,64,64,490)
shootLoop=0
bullets = []
run = True
while run:
    clock.tick(27)
    
    if man.hitbox[1] < goblin.hitbox[1] + goblin.hitbox[3] and man.hitbox[1] + man.hitbox[3] > goblin.hitbox[1]:
        if man.hitbox[0] + man.hitbox[2] > goblin.hitbox[0] and man.hitbox[0] < goblin.hitbox[0] + goblin.hitbox[2]:
            hitm_sound.play()
            man.hit()
            score -= 5
            
    if man.hitbox[1] < goblin2.hitbox[1] + goblin2.hitbox[3] and man.hitbox[1] + man.hitbox[3] > goblin2.hitbox[1]:
        if man.hitbox[0] + man.hitbox[2] > goblin2.hitbox[0] and man.hitbox[0] < goblin2.hitbox[0] + goblin2.hitbox[2]:
            hitm_sound.play()
            man.hit()
            score -= 5
            
    if man.hitbox[1] < goblin3.hitbox[1] + goblin3.hitbox[3] and man.hitbox[1] + man.hitbox[3] > goblin3.hitbox[1]:
        if man.hitbox[0] + man.hitbox[2] > goblin3.hitbox[0] and man.hitbox[0] < goblin3.hitbox[0] + goblin3.hitbox[2]:
            hitm_sound.play()
            man.hit()
            score -= 5
    
    if shootLoop>0:
    	shootLoop+=1
    if shootLoop>3:
    	shootLoop=0

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            run = False
        if event.type==pygame.MOUSEBUTTONDOWN:
            man.isJump = True
            man.right = False
            man.left = False
            man.walkCount = 0
        
    for bullet in bullets:

         try:
         	if bullet.y-bullet.radius<goblin.hitbox[1]+goblin.hitbox[3] and bullet.y+bullet.radius>goblin.hitbox[1]:
         		if bullet.x+bullet.radius>goblin.hitbox[0] and bullet.x-bullet.radius<goblin.hitbox[0]+goblin.hitbox[2]:
         			h_sound.play()
         			goblin.hit()
         			score+=1
         			bullets.pop(bullets.index(bullet))
         	if bullet.y-bullet.radius<goblin2.hitbox[1]+goblin2.hitbox[3] and bullet.y+bullet.radius>goblin2.hitbox[1]:
         	    if bullet.x+bullet.radius>goblin2.hitbox[0] and bullet.x-bullet.radius<goblin2.hitbox[0]+goblin2.hitbox[2]:
         	    	h_sound.play()
         	    	goblin2.hit()
         	    	score+=1
         	    	bullets.pop(bullets.index(bullet))
         	if bullet.y-bullet.radius<goblin3.hitbox[1]+goblin3.hitbox[3] and bullet.y+bullet.radius>goblin3.hitbox[1]:
         		if bullet.x+bullet.radius>goblin3.hitbox[0] and bullet.x-bullet.radius<goblin3.hitbox[0]+goblin3.hitbox[2]:
         			h_sound.play()
         			goblin3.hit()
         			score+=1
         			bullets.pop(bullets.index(bullet))
         except:
         	f=1
         if bullet.x < 510 and bullet.x > 75:
         	bullet.x += bullet.vel
         else:
         	bullets.pop(bullets.index(bullet))

    keys = pygame.key.get_pressed()
    
    if man.x>13 and man.x<23 and man.y>370:
    	man.x=12
    	
    if man.x>29 and man.x<40 and man.y>370:
    	man.x=41
    	

    if keys[pygame.K_SPACE] and shootLoop==0:
        b_sound.play()
        if man.left:
            facing = -1
        else:
            facing = 1
            
        if len(bullets) < 5:
            bullets.append(projectile(round(man.x + man.width //2), round(man.y + man.height//2), 6, (255,255,100), facing))
        shootLoop=1

    if keys[pygame.K_LEFT] and man.x > man.vel:
        man.x -= man.vel
        man.left = True
        man.right = False
        man.standing = False
    elif keys[pygame.K_RIGHT] and man.x < 500 - man.width - man.vel:
        man.x += man.vel
        man.right = True
        man.left = False
        man.standing = False
    elif keys[pygame.K_t]:
    	man.x=random.randint(10,490)
    else:
        man.standing = True
        man.walkCount = 0
        
    if keys[pygame.K_r]:
    	pygame.mixer.music.play(-1)
    	c_sound.play()
    	score=0
    if not(man.isJump):
        if keys[pygame.K_UP]:
            man.isJump = True
            man.right = False
            man.left = False
            man.walkCount = 0
    else:
        if man.jumpCount >= -10:
            neg = 1
            if man.jumpCount < 0:
                neg = -1
            man.y -= (man.jumpCount ** 2) * 0.5 * neg
            man.jumpCount -= 1
        else:
            man.isJump = False
            man.jumpCount = 10
            
    redrawGameWindow()

pygame.quit()
