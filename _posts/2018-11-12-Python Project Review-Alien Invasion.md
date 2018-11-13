---
layout:     post
title:      Python Project Review
subtitle:   Alien Invasion
date:       2018-11-12
author:     Lance
header-img: img/bg.jpg
catalog: true
tags:
    Python
    Pygame
    Git
---

## Content
You can git clone learning project alien_invasion here: 
```shell
git clone https://github.com/lance-lh/alien_invasion.git
```
_1. class_
```python
class Alien(Sprite):
    def __init__(self,ai_settings,screen):
        super(Alien, self).__init__()
        self.screen = screen
        self.ai_settings = ai_settings
```        
        
_2. load image_
```python
self.image = pygame.image.load('images/alien.bmp')
```

_3. get rectangular method_
```python
self.rect = self.image.get_rect() # rect method (center,centerx,middle,left,right...)
```

*4. draw one image onto another*
```python
  # blit(dest_image, location) location is obtained by rect method
  
  
self.screen.blit(self.image, self.rect) 
```
_5. initialize game_
```python    
def run_game():  # initialize the game, screen object,setting
    
    
    pygame.init()
    ai_settings = Settings()
    screen = pygame.display.set_mode(
        (ai_settings.screen_width,ai_settings.screen_height))  # define a tuple which indicates screen size, width:1200, height:800.
        
    pygame.display.set_caption("Alien Invasion")
```    
_6. Group_
```python
    bullets = Group()
     aliens = Group()
```     
_7. rect method_
```python
# create a bullet rectangular at (0,0) and then move it to proper location


        self.rect = pygame.Rect(0,0,ai_settings.bullet_width, ai_settings.bullet_height)
        self.rect.centerx = ship.rect.centerx
        self.rect.top = ship.rect.top
        
    def draw_bullet(self):
        '''paint bullet in the screen'''
        pygame.draw.rect(self.screen,self.color,self.rect)
```        
_8. Pygame font_
```python
self.font = pygame.font.SysFont(None,48)
```

_9. score to image_
```python
    def prep_score(self):
        '''score to image'''
        rounded_score = int(round(self.stats.score, -1))
        score_str = "{:,}".format(rounded_score)
        self.score_image = self.font.render(score_str,True,self.text_color,self.ai_settings.bg_color)

        # put score image on the top right of screen
        
        
        self.score_rect = self.score_image.get_rect()
        self.score_rect.right = self.screen_rect.right - 20
        self.score_rect.top = 20
```      
  
_10. reset game status_
```python
self.reset_stats()
```

_11. quit game_
```python
import sys

def check_keydown_events(event,ai_settings,screen, ship,bullets):
    if event.key == pygame.K_RIGHT:
        ship.moving_right = True

    elif event.key == pygame.K_LEFT:
        ship.moving_left = True

    elif event.key == pygame.K_SPACE:
        fire_bullet(ai_settings,screen,ship,bullets)
    elif event.key == pygame.K_q:
        sys.exit()
```        

_12. collision check_
```python
def check_bullet_alien_collisons(ai_settings,screen,stats,sb,ship,aliens,bullets):
    '''respond to collision between aliens and bullets'''
    # delete crashed bullets and aliens
    
    collissions = pygame.sprite.groupcollide(bullets,aliens,True, True)  # return a dict , key is a bullet and value is an alien

    if collissions:
        for aliens in collissions.values():
            stats.score += ai_settings.alien_points * len(aliens)
            sb.prep_score()
        check_high_score(stats,sb)

    if len(aliens) == 0:
        # delete existing bullets and create new aliens
        
        bullets.empty()
        ai_settings.increase_speed()

        # level up
        
        stats.level += 1
        sb.prep_level()

        create_fleet(ai_settings,screen,ship,aliens)
```

## Reference  
- [Python Crash Course](https://ehmatthes.github.io/pcc/)  
- [Pygame documentation](https://www.pygame.org/docs/) 