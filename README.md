# Swift Expression
This app analyses the feeling from the user's photo using a trained machine learning image classification model and gives a Taylor Swift song and lyrics according to that feeling.

## ContentView.swift
This file is the main page when the apps opens. It has a NaviagtionStack with a ZStack with a maroon background, a Text with the title, a rectangle button start.

## ResultPage.swift
This is the screen with the results where there is the feeling, the user's photo, the song and the lyrics inside a scroll view. We check the label given by the trained model and compares with the different types of songs, extracted from a cvs file with all the songs and the lyrics.

## Songs.swift
This file contains all the songs and each lyrics in dictionaries separeted by feeling.

## CoreMLViewModel.swift
