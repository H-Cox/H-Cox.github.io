---
layout: post
title: Ruby katas and TDD
date: 2018-05-12 00:00:00 +0300
description: My experiences with ruby and test driven development
img: croatiaislands.jpg
tags: [Ruby, TDD]
---

Test driven development (TDD) and the programming language Ruby were both alien to me in October 2017. However, this changed when I began to be mentored by an experienced Software Developer who I found through the [Manchester Gold][Manchester gold] mentoring programme. Recently, we have discussed the basic principles of TDD, and other software development practices, and put them into practise with Ruby. 

#### Ruby

Ruby was created by Yukihiro Matsumoto in Japan with the aim of being an easy to use, genuine object orientated scripting language. My first impressions of Ruby was that it does read very nicely. To get to grips with the syntax and learn a bit more about the language I completed the [Ruby Koans][RB Koans]. These challenges ease you into the language very nicely and feature a couple of small projects to complete along the way. You can find my completed version of the koans [here][my kaons].

#### Software development practices

Up until now, my programming process has evolved naturally with my personal experiences and needs as I have been self-taught rather than following a structured course. However, in an industry setting, or when your code needs to be dependable and usable by many different people or applications, software development practices have sprung up to define how best to produce the most effective and robust code. 

As an outsider to these practices, I wanted to gain an overview of the way things are done in modern development teams. Through independent research and discussion with my mentor I learnt about a variety of practices such as Extreme Programming, Agile and Scrum and discussed the actual code writing process in terms of test driven development (TDD).

#### The TDD process

The test driven development process has multiple parts:

1. Write a test which fails.
2. Implement the quickest or easiest solution which modifies your code such that all tests pass.
3. Refactor the code if possible so that it is easier to read, more efficient, etc.
4. Return to step 1 and write a new test, or finish here if you have no more relevant tests to do and the code is working.

In practice this is often completed in pairs, where one person may write the test, and the other then completes steps 2 and 3. To help me get a better grasp of the process I have completed a couple of common kata using the TDD method. These are a roman numerals kata and a bowling kata.

#### Roman numerals and bowling

The first kata I completed was the roman numerals kata which I did with my mentor in a pair programming style. Typically, they wrote a test and then I completed the code, which worked well as they are much more experienced with the process and software development in general. You can see the completed kata [here][roman]. This worked out really well and it was nice to be solving coding problems with another person.

The second kata I completed individually and the aim of it was to write a small program which could keep track of the score in a game of bowling. I used git to perform commits between each cycle of the TDD process (after I had written a failing test) and you can see the repository and each stage of the process I went through [here][bowling]. 

Completing the bowling kata was more challenging which was certainly due to the fact I had to do it individually but also because I actually defined the kata myself: input to the program was one bowl at a time, not a list of all bowls for the game. Nevertheless, I learnt a lot through making mistakes and looking back on it, in comparison to completions of similar kata I have seen online, I have some good take-aways to build on next time.

#### Lessons learnt

The main take-away for me was that I need more practice actually writing the tests. My solution to the bowling kata has 16 in total, and certainly a few of the ones I wrote could probably be removed or changed so that they are more efficient. Some of the solutions online only feature around 5 tests to ensure the code is working properly. Having said that, the tests I wrote were not all trivial, and having a set of tests to check the program operation did really make me appreciate how useful TDD would be in an environment where you need to keep updating or working on the code.

Furthermore, I am glad that now I can descibe the basic principles behind modern software development and if I was put infront of a Kanban board I could describe the basic workflow and determine what the team was up to. I didn't realise that software development teams would be so team-orientated and this is a big positive for me as I enjoy working with people to solve problems.

Photo: Islands near Zadar, Croatia

[Manchester gold]:http://www.careers.manchester.ac.uk/experience/mentoring/mangold/
[RB Koans]:http://rubykoans.com
[my kaons]:https://github.com/H-Cox/Ruby-Koans
[roman]:https://github.com/H-Cox/roman-numerals-kata
[bowling]:https://github.com/H-Cox/bowling-kata









