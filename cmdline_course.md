---
layout: default
---
## Introduction

In this course we learned how to navigate the Unix system. We learned to use the Bash shell to use Unix/Linux systems through the terminal. First we learned the basics of navigating the terminal and progressed to more and more advanced uses including making small scripts and making our own configurations. We also learned some facts about programming languages and started to build a base knowledge for version contorl through git.
## Week 1: Introduction to Command-Line Environments

In the beginning, we got some basic info about Computer systems in general, mostly about Unix/Linux. We got to know differences between Windows and Unix files. We also got know the very basic commands for manipulating files in Unix/Linux shell such as:
* **cat** (read files)
* **mv** (move files)
* **cp** (copy files)

We also learned about datastreams within Unix and the basics of how to manipulate them. Essentially, how to get the output, input and error datastreams to behave like we want to.

## Week 2: Navigating Unix System

As the name suggest on the second week we learned to navigate through the Unix/Linux terminal using commands such as **cd** (navigating) and **ls** (listing files). We also gained info on user permission and how to manipulate them using **chmod** and we discussesd root access and sudo access. We also talked about **ssh** and **scp** protocols for connecting to remote servers for example.

## Week 3: Corpus Processing

This week we started talking more about data streams and how to manipulate them (redirect). This also lead nicely to the fact that we started now using what we have learned in a more linguistic context. We started making simple text processing commands by combining different kinds of commands into a line of commands. We worked with **tr**, (manipulating) **sed** (also manipulating/extracting) and **grep** (searching) which all were used for text processing. There were other commands aswell:
* **sort** (for sorting the results)
* **uniq** (for getting unique results)

A example of a chain of commands:  
```Bash
cat life_of_bee.txt | tr -s '\n\t\r ' '\n' | tr -dc "A-Za-z0-9'\n" | tr 'A-Z' 'a-z' | sort | uniq -c | sort -nr > life_of_bee.ic.freq
```  
This counted word frequencies in a text file life_of_bee.txt

## Week 4: Scripting and Unix Configuration Files

On fourth week we learned more about the "chains of command" and how to more use them more efficiantly by making them into a Script. Which is essiantially a saved command chain which can be used as much as you want. We also learned about configuring our enviroment. We learned about **PATH** (an address path that is looked through when looking for a script or command etc.). We also learned about .bashrc which is a config file that can be used for preconfiguring settings that are used on startup in our Shell enviroment.  
Here is an example from my own .bashrc file (with explanations added:
```Bash 
export JAVA_HOME=/homeappl/home/juusomih/jdk1.8.0_191 (Shows where to find Java)
export PROMPT_COMMAND="echo -n \[\$(date +%H:%M:%S)\]\ " (Modifies the Prompt in Bash)  
#Change history size  
HISTSIZE=10000 (Creates a bigger command history) 
HISTFILESIZE=20000 (Increases file size for the command history) 
  
alias solr="cd /homeappl/home/juusomih/nlpappcourse/solr-7.5.0" (script that navigates to my solr directory by simply typing solr) 
```
## Week 5: Installing and Running Programs  
On the fifth week we learned about using programming languages in paralel to our scripting and Bash skills. To do this we would **Make** file which you could say is a kind of an compiler in the sense that it combines all your scripts and programs and runs them at the same time. An example of a make file with bash scripts and a python program in it, Below:  

```Bash
BOOKS=alice christmas_carol dracula frankenstein heart_of_darkness life_of_bee moby_dick modest_propsal pride_and_prejudice tale_of_two_cities

FREQLISTS=$(BOOKS:%=results/%.freq.txt)
SENTEDBOOKS=$(BOOKS:%=results/%.sent.txt)
PARSEDBOOKS=$(BOOKS:%=results/%.parsed.txt)

all: $(FREQLISTS) $(SENTEDBOOKS) $(PARSEDBOOKS)

clean:
	rm -f results/* data/*no_md.txt

%.no_md.txt: %.txt
	python3 src/remove_gutenberg_metadata.py $< $@

results/%.freq.txt: data/%.no_md.txt 
	src/freqlist.sh $< $@

results/%.sent.txt: data/%.no_md.txt
	src/sent_per_line.sh $< $@

results/%.parsed.txt: results/%.sent.txt
	python3 src/parse.py $< $@

```
This make file runs three different scripts at the same time with command **make all** (can erased by **make clean**) and it goes through the sources (BOOKS) removes metadata from it, makes a frequency list files from them, makes a sentence per line files from all of them and makes a parsed files from them (in this case using python program, which only parses first 10 sentences in this case)  
## Week 6: Version Control
 During this week we learned the basic concepts of Version Control, how implement it into your development cycle. We used Git as our Version Control tool and Github was our hosting service for our repositories. 

 More specifically we learned about different git commands to use after we have created our repository.  
  >**Git status** to check on the situation in your repo  
  **Git add** to add new files for Git to follow (can be seen with Git Status)  
  **Git commit** to commit our changes into our repo (local)  
  **Git push** to push our commited files to the Global repo  

  We also learned to use branches as a actual developer would.
  
  This week also had my favorite comic out of all the weekly comics:  
  
![alt text](https://imgs.xkcd.com/comics/git.png "Git yay?")
 
 
## Week 7: Building Webpages using GitHub Pages
On the last week of the course we learned to make our own websites (with premade templates) to github.io. Indeed, if you are reading this it means I made the website work. We also learned to basics of Jekyll and how it interacts with github.io files. We also learned the basic syntax for markdown files (this one again) which we used to create this website that you are reading right now. Which is our final project for the course. During this final project we also used braching and Version control to internalize how a developer would use version control. 