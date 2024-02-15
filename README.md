# HW-5_1

'''
CSC-103, Professor Auerbeck, Fred P Vella
Homework 5-1
'''

# For Homework 5-1, we will create a graph using two of the 
# four graphs available of a graph illustrating a random set
# Of Pokemons height, weight, and number of games they
# Participated in and it will be presented as a single data set. 

# First, we will import all necessary data functions and 
# Variables necessary for this operation. 

import pandas as pd
import seaborn as sb
import matplotlib.pyplot as plt
import warnings

# Next, we will filter our warnings so they are fit towards
# Our coding/graphing project. 

warnings.filterwarnings("ignore", "use_inf_as_na")

# Sequentially, we will read all necessary csv files in. 

po = pd.read_csv('data/pokemon.csv')
px = pd.read_csv('data/pokemon_species.csv')
pg = pd.read_csv('data/poke_by_game.csv')

ddr = px.sample(6)['identifier']

xpe = (po.merge(pg, how='left', left_on='species'
              , right_on='species', suffixes=('_spec', '_exp')))

# After that, we determined the sample size and determined 
# How best to arrange the selected data sets. 

xpe = xpe[['identifier', 'generation_id', 'experience']]

dpl = xpe['identifier'].isin(ddr)

# Sequentially, we created variables that guide our data set for 
# The coming graphs and data entries of the pokemon. 

# Following that, we will create a subplot function with 
# Names of specific pokemons for the graph/graphs in question. 

e = xpe[dpl][['identifier', 'generation_id', 'experience']]

fig, ax = plt.subplots()
ids = ['bulbasar', 'spuirtle', 'mewtwo']

# Lastly, we will create the graph itself. This is is done with 
# The newdat function as well as other function such as lineplot
# This graph should show us the pokemon trends in games played
# Based on the variables identifier, generation_id and experience.

for i in ddr:
    dpl = xpe['identifier'].isin([i])
    newdat = xpe[ddr][['identifier', 'generation_id', 'experience']]
    sb.lineplot(data=newdat, x='generation_id', y='experience', legend="brief", label=str(i))
    
plt.ticklabel_format(style='plain', axis='y')
