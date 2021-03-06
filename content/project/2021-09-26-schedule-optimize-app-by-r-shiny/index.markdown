---
title: Schedule optimize app by R shiny
summary: Customizable web app to optimize schedule working shifts 
cover:
  image: "cover.png"
author: Hai Vo
date: '2021-09-26'
slug: []
categories: []
tags: [Optimization, shiny, ompr]
---


## Why
![Screen shoot](app-screenshoot.png)

The problem is simple and straight forward: I want to assign a schedule of (n) staffs to work for (m) days, each day have (t) shifts.

Each worker provide a personal sheet which show their level of preference for each shift. Base on that data, the optimizer will try to arrange correspond schedule.

The preference are in the form of numeric number. For example: 3 for the best suite shift, 1 for less desire shift and "Busy" for the shift that they can not attend.

The objective of model is to maximize total preference while still satisfied several constraint.

I also want this program to have a nice user interface so that any people can understand and use it.

Link to app: [Shiny app](https://haivo.shinyapps.io/schedule-optimizer/)

Link to app source code: [Github](https://github.com/vohai611/shiny-schedule-assign) 
## How

So, there are two problem: 

1. Write and solve the model which accept user input: number of staff, day, shift and several optional constraints.

2. Build an interface that allow user provide input and download the result.

### The model

This kind of problem is categorized as "Integer programming" and is able to solve by most solver such that Excel solver, AMPL, Lingo ...

In R, there are a package `{ompr}` which allow user to write mixed integer linear programs directly in R on a mathematics way, it also possible to be program with. This package than provide an API to multiple solver: GLPK, CPLEX, ...

### Web app interface

`{shiny}` is exactly what I need. It provide a framework that makes it easy to build interactive web apps straight from R. The app could be host on shinyapps.io, dockerizing or on any server with the help of `{shinyserver}`.

## Summarise and future work

At the moment, the app only implement the below constraint:

1. [Default] People does not allow to work more than 1 shift a day

2. [Option] People are not allow to work two day in a row

3. [Option] Choose number of people per shift

There are multiple constraint can be add to the app such that:

- Limit number of shift assign to one people (upper and lower bound)

- Prioritize certain people o work together 

Thank you for your reading! If you want to give me any feedback, email me at haingocvo96@gmail.com. 


<style type="text/css">
h2 {
  color: #9EBA89;
}
</style>



