---
layout:     post
title:      Python Project Review
subtitle:   Data Visualization
date:       2018-11-13
author:     Lance
header-img: img/bg.jpg
catalog: true
tags:
    Python
    Git
---

## Content
You can git clone learning project data_visualization here: 
```shell
git clone https://github.com/lance-lh/data_visualization.git
```
_1. simple plot_
```python
import matplotlib.pyplot as plt

input_values = [1,2,3,4,5]
squares = [1,4,9,16,25]
plt.plot(input_values,squares,linewidth=5)

plt.title("Square Numbers", fontsize=24)
plt.xlabel("Value",fontsize=14)
plt.ylabel("Square of label",fontsize=14)

plt.tick_params(axis='both',labelsize=14)
plt.show()
```        
        
_2. scatter_
```python
import matplotlib.pyplot as plt

x = list(range(1,1001))
y = [x_value**2 for x_value in x]

# colormap

plt.scatter(x,y,c=y,cmap=plt.cm.Blues,edgecolors='none',s=10)

plt.title("Square Numbers", fontsize=24)
plt.xlabel("Value",fontsize=14)
plt.ylabel("Square of label",fontsize=14)

plt.tick_params(axis='both',which='major',labelsize=14)  
plt.axis([0,1100,0,1100000])
# plt.show()
plt.savefig('squares_plot.png',bbox_inches='tight') # save png
```

_3. random walk_  
1). rw_visual.py  

```python
import matplotlib.pyplot as plt
from random_walk import RandomWalk

while True:
    rw = RandomWalk(50000)
    rw.fill_walk()

    plt.figure(dpi=128,figsize=(10,6))

    point_numbers = list(range(rw.num_points))
    plt.scatter(rw.x_values,rw.y_values,c=point_numbers,cmap=plt.cm.Blues,edgecolor='none',s=1)

    plt.scatter(0,0,c='green',edgecolors='none',s=100)
    plt.scatter(rw.x_values[-1],rw.y_values[-1],c='red',edgecolors='none',s=100)

    plt.axes().get_xaxis().set_visible(False)
    plt.axes().get_yaxis().set_visible(False)
    plt.show()

    keep_running = input("Make another walk?(y/n): ")
    if keep_running == 'n':
        break
```
2). random_walk.py
```python
from random import choice

class RandomWalk():

    def __init__(self,num_points=5000):
        self.num_points = num_points
        self.x_values = [0]
        self.y_values = [0]

    def fill_walk(self):
        while len(self.x_values) < self.num_points:
            x_direction = choice([1,-1])
            x_distance = choice([0,1,2,3,4])
            x_step = x_direction * x_distance

            y_direction = choice([1,-1])
            y_distance = choice([0,1,2,3,4])
            y_step = y_direction * y_distance

            if x_step == 0 and y_step == 0:
                continue

            next_x = self.x_values[-1] + x_step
            next_y = self.y_values[-1] + y_step

            self.x_values.append(next_x)
            self.y_values.append(next_y)
```
*4. bar*  
1). die.py
```python
from random import randint

class Die():
    '''a class represented dice'''

    def __init__(self,num_sides=6):
        '''dice has 6 sides'''
        self.num_sides = num_sides

    def roll(self):
        '''return a random value within [1,6]'''
        return randint(1,self.num_sides)
```
2). die_visual.py
```python
from die import Die
import pygal

die_1 = Die()
die_2 = Die(10)

results = []

for roll_num in range(50000):
    result = die_1.roll() + die_2.roll()
    results.append(result)
# print(results)

frequencies = []
max_result = die_1.num_sides + die_2.num_sides
for value in range(2,max_result+1):
    frequency = results.count(value) 
    frequencies.append(frequency)

hist = pygal.Bar()

hist.title = "Results of rolling a D6 and a D10 dice 50000 times."
hist.x_labels = ['2','3','4','5','6','7','8','9','10','11','12','13','14','15','16']
hist.x_titles = "Results"
hist.y_title = "Frequency of Result"

hist.add('D6 + D10',frequencies)
hist.render_to_file('die2and10_visual.svg')

```
_5. read data from CSV_
```python  
import csv  
filename = 'death_valley_2014.csv'
with open(filename) as f:
    reader = csv.reader(f)
    header_row = next(reader)
```    
_6. read data from json_
```python
import json

filename = 'population_data.json'
with open(filename) as f:
    pop_data = json.load(f)
```     
_7. convert info into python dict_
```python
import requests
import pygal
from pygal.style import LightColorizedStyle as LCS, LightenStyle as LS

# call Github API and store response

url = 'https://api.github.com/search/repositories?q=language:python&sort=stars'
r = requests.get(url)
print("Status code:",r.status_code)

response_dict = r.json()    # convert info into python dict

print("Total respositories:",response_dict['total_count'])

repo_dicts = response_dict['items']   # items is a list but contain many dicts  

print("Repositories returned:",len(repo_dicts)) # how many repos

print("\nSelected information about each repository:")
names, plot_dicts = [],[]
for repo_dict in repo_dicts:
    names.append(repo_dict['name'])

    plot_dict = {
        'value':repo_dict['stargazers_count'],
        'label': str(repo_dict['description']),
        'xlink': repo_dict['html_url']
        }
    plot_dicts.append(plot_dict)

my_style = LS('#333366',base_style=LCS)

my_config = pygal.Config()
my_config.x_label_rotation = 45
my_config.show_legend = False
my_config.title_font_size = 24
my_config.label_font_size = 14
my_config.major_label_font_size = 18
my_config.truncate_label = 15
my_config.show_y_guides = False
my_config.width = 1000

chart = pygal.Bar(my_config,style=my_style)
chart.title = 'Most-Starred Python Projects on Github'
chart.x_labels = names

chart.add('',plot_dicts)
chart.render_to_file('python_repos.svg')
```        

## Reference  
- [Python Crash Course](https://ehmatthes.github.io/pcc/)  