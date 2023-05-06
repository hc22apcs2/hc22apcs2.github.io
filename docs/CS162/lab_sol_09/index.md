---
layout: post
title: CS162 - Lab 09 Solutions
parent: Introduction to Computer Science II
--- 

{% include toc.md %}

# Lab 09 - Binary File IO
{: .no_toc}

* **Source:** [PDF file](Lab09_Binary_File_IO.pdf)

## 3.1 - Integer Array – Load & Save

Write a small program with $2$ features (the program should create menu options to allow user to choose one of them).
1. User enters an array of integers from keyboard. The program will save the array to a binary file.
2. User loads an array of integers from a binary file. The program will find the median and output to console.

**Format of input.bin:**
- $1$st number: $n$, number of elements in the array.
- Next $n$ numbers: elements in the array.

* **Solution:** [https://ideone.com/WcATe5](https://ideone.com/WcATe5)

## 3.2 - Date Array – Load & Save

Write a small program with $2$ features (the program should create menu options to allow user to choose one of them).

3. User enters an array of dates from keyboard. The program will save the array to a binary file.
4. User loads an array of dates from a binary file. The program will find the newest date and output to console.

Format of input.bin:

- $1$st number: $n$, number of elements in the array.
- Next $3n$ numbers: elements in the array.

* **Solution:** [https://ideone.com/RR45st](https://ideone.com/RR45st)

## 3.3 - Copy file

Use command prompt argument and binary file IO techniques to create a `MYCOPYFILE` program.

User will enter:

```bash
MYCOPYFILE -s path_of_source_file -d path_of_destination
```

The destination file will have same name as the source file.

**For example:**
```bash
MYCOPYFILE -s D:/film.mkv -d D:/Level1/Level2/Level3
```

* **Solution:** [https://ideone.com/zBGEG1](https://ideone.com/zBGEG1)

## 3.4 - Split file

Use command prompt argument and binary file IO techniques to create a `MYSPLITFILE` program.

User will enter:
```bash
MYSPLITFILE -s path_of_source_file -d path_of_destination -numpart x
```
`x` is a positive integer number, number of splitted parts.
OR
```bash
MYSPLITFILE -s path_of_source_file -d path_of_destination -sizeapart x
```
`y` is a positive integer number (in bytes), size of a splitted part.

For example:
```bash
MYSPLITFILE -s D:/film.mkv -d D:/Level1/Level2/Level3 -numpart 3
```
OR
```bash
MYSPLITFILE -s D:/film.mkv -d D:/Level1/Level2/Level3 -sizeapart 1000000
```
Names of splitted parts are: `film.mkv.part01`, `film.mkv.part02`, `film.mkv.part03` $\ldots$

* **Solution:** [https://ideone.com/qT6NOb](https://ideone.com/qT6NOb)

## 3.5 - Merge file

Use command prompt argument and binary file IO techniques to create a `MYMERGEFILE` program.

User will enter:
```bash
MYMERGEFILE -s path_of_part01 -d path_of_destination
```

The program will find all `*.part01`, `*.part02`, `*.part03` $\ldots$ files and merge into a single file.
The program will print errors if there is any part does not exist.

For example:
```bash
MYMERGEFILE -s D:/Level1/Level2/Level3/film.mkv.part01 -d D:/NewLevel
```

* **Solution:** [https://ideone.com/MvdXva](https://ideone.com/MvdXva)

## 3.6 - Bitmap File

* **Input:** width and height of the flag of England
* **Output:** the BMP file of the flag of England
* **Source:** [https://en.wikipedia.org/wiki/Flag_of_England](https://en.wikipedia.org/wiki/Flag_of_England)
* **Solution:** Soon or **NEVER**.