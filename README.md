# Degrees

- [Introduction](#introduction)
- [Distinctiveness and Complexity](#distinctiveness-and-complexity)
- [How To Run](#how-to-run)
- [User Guide](#user-guide)

-----------------------------------------------------------------------------
## Introduction

Inspired by the **Six Degrees** of Kevin Bacon game, this program finds the shortest path between two actors through movies they have starred in together. Each connection represents a movie where two actors appeared together.

-----------------------------------------------------------------------------
## Distinctiveness and Complexity

This project is solved using the **breadth-first search (BFS)** algorithm to find the shortest path between two actors:

   - As a search problem: 
      - States: Actors (people)
      - Actions: Movies that connect two actors
      - Initial and Goal States: The two actors the user is trying to connect

   - At the top of the degrees.py file, several data structures store information from the CSV files:
      - The `names` dictionary is a way to look up a person by their name: it maps names to a set of corresponding ids (because it’s possible that multiple actors have the same name).
      - The `people` dictionary maps each person’s id to another dictionary with values for the person’s name, birth year, and the set of all the movies they have starred in.
      - The `movies` dictionary maps each movie’s id to another dictionary with values for that movie’s title, release year, and the set of all the movie’s stars.

   - The user enters the source and target names. The `person_id_for_name` function retrieves the corresponding ID for any person (and handles prompting the user to clarify, in the event that multiple people have the same name).

   - The `shortest_path` function starts from the source, using  `neighbors_for_person` function, finds the (movie_id, person_id) pairs who starred with the source, adds the pairs to the `QueueFrontier` which is defined in `util.py`. The `ex_list` is a list to prevent the repetitive paths.

  - Using a `while loop`, the first (movie_id, person_id) pair in queueFrontier is removed. The  `neighbors_for_person` function finds the next (movie_id, person_id) pairs of connections, checked against the target, If the target is not reached and the path is not repetitive, new connections are added to the queuefrontier.

  - If queuefrontier is empty or the target actor is found, the loop breaks, returning either the shortest path or none if no connection exists.

-----------------------------------------------------------------------------
## How To Run

Follow these steps to set up and run the degrees.py:

- Navigate to the project directory: cd /workspaces/Degrees/degrees
- Run the program: python degrees.py
- Select and write one of the actor's full name from the people.csv in the small or large folder. Then press enter
- Select and write another actor's name from the same people.csv file and press enter
- If multiple actors have the same name, you are asked to enter the actor's id depending their birth year
- The program will display the shortest connection through movies

-----------------------------------------------------------------------------
## User Guide

The distribution code contains two sets of CSV data files: one set in the large directory and one set in the small directory. Each contains three files with the same names, and the same structure, but small is a much smaller dataset for ease of testing and experimentation.
You just need to open the file `stars.csv` and select two actors who you want to know the degree between them.
