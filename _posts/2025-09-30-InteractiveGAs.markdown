---
layout: post
title:  "Interactive Genetic Algorithms"
date:   2025-09-30
categories: research GAs live mixed-initiative 
---

Hello, this is the live document on interactive genetic algorithms. I plan to edit this post as I gather more information about it. 

This post was last updated September 30th 2025. 

##  Interaction in Genetic Algorithm

What is deemed an "interactive genetic algorithm" is not clearly defined, and hard to differentiate from related terms such as "human-based genetic algorithms" or "human-in-the-loop genetic algorithm." While some suggest that "interactive genetic algorithm" refers specifically to algorithms where humans replace the selection function, in this post we will use the term to describe *any genetic algorithm in which humans participate throughout the evolutionary process." This could be in the form of replace or guiding the fitness function, but it can also refer to algorithms were humans contribute content or conduct other parts of the evolutionary process. This is distinct from "static" genetic algorithms where user preferences can only be set before evolution and the user cannot direct the process in any way. 

This blog post will go through several of the ways interaction has been implemented in genetic algorithms, but it is likely not an extensive list. I will be updating this post as I find new publications, but feel free to reach out to me if you know of algorithms not mentioned in this post. 


### User As Fitness Function 

The purest form of a interactive genetic algorithm, is one where the selection or fitness function is completely replaced by a human user. This was originally to take into account cases where it was not obvious how to create a good computational fitness function. Particularly in regards to design where the aesthetic quality is what is desired, evaluation by humans is particularly desired. A basic example of such an algorithm is given below. 

```
def human_fitness_ga(): 
  generate random population 
  while resources last:
    Show user population 
    Have user select N individuals from population 
    Cross-over and mutate selected individuals to replace population 

```

Alternatively, the user can provide a rating for each individual which then acts as a regular fitness function would. 

However, evolutionary algorithms require a significant amount of time to start to produce high quality outputs. This means that a human would have to make likely hundreds of evaluations, likely with only minor increments between steps, before they would generate individuals that suit their preferences. Not only is this highly inefficient, it can cause fatigue in this user. Genetic algorithms that completely replace selection with human evaluation are often designed to be toys rather then serious means of creation. The [casual creators framework](https://escholarship.org/uc/item/4kg8g9gd), describes design tools that focus on exploration and fun rather then out and includes several such examples. In fact "mutation shopping," the ability to view and choose from variants, is listed as a design pattern of casual creators. Another approach is to have smarter cross-over and mutation functions, such as [this paper](https://dl.acm.org/doi/pdf/10.1145/3583131.3590351) that used a large language model (LLM) to replace traditional genetic operators and online voting to replace the fitness function. 

### Users Guiding Fitness Functions 

Instead of humans completely taking over the fitness function, their preferences can be used to guide the fitness. This allows for user preference to be taken into account throughout evolution, but are not as slow and tedious as solely human driven selection.

An example of this is shown in [this paper](https://ieeexplore.ieee.org/abstract/document/9446649), which focused on generating 2D game levels. The user begins by creating an example artifact (game level), which is used as the initial population for the GA. Every N generations, the user was presented with the current population and could choose to "like" particular individuals in the population. In-between these selections, the fitness function evaluates how close an individual is to the previously liked individuals. 