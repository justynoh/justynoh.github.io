---
layout: page
title: OCR Sudoku solver
permalink: /projects/ocr-sudoku-solver/
---

_[back to projects](/projects/)_

As a term project for an introductory class to Python, I wrote an OCR Sudoku puzzle solver (see also the [github repo](https://github.com/justynoh/sudoku-solver)) which took as input a snapshot of a Sudoku puzzle and output a solution to the puzzle along with step-by-step explanations of each filled cell. I also made a YouTube video explaining the main features and algorithms behind the project.

There were two main components to the project. The first component was digitalizing the puzzle, which involved implementing a grid detection algorithm using OpenCV and an adaptive machine learning model using Tensorflow. For grid detection, I used a Hough lines transform in OpenCV to detect a grid of parallel and perpendicular lines. The angle of rotation was also used to assist the user to rotate their image such that the grid would be square with the window. Once the grid was detected, the image was segmented into 81 squares, each corresponding to a Sudoku cell. On each cell, a neural network written in Tensorflow was used for digit recognition. On the first use of the application, the neural network was initialized with parameters based on the MNIST handwritten digit dataset as a starting point for digit recognition. However, after the digits in the user's puzzle were recognized, users were prompted to correct the detected digits, which was then fed back as a training set into the neural network to adjust its parameters. This enabled the neural network to learn as the application was used more and more by the same user, so that the neural network would be tuned with a set of parameters unique to the user's handwriting.

The second component was the solver itself which used the rules of Sudoku as well as other deductive rules to determine most of the cells in the puzzle. In particular, the singleton search rule and unique cell search rule were implemented, explained below.

* The singleton search rule is based on the fact that a cell's fill is fixed if the union of the fills in its row, column and box make up the other eight digits.
* The unique cell search rule says that for each region (i.e. row, column or box) and for each digit not already in the region, a(n unfilled) cell must contain the digit if all other unfilled cells cannot contain the digit (due to their row, column or box already having that digit).

The steps were also stored during the solving process so that once the solver had found a solution, the steps to solve the Sudoku could be shown to the user as well.