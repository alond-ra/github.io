---
layout: post
title:  "Technical Log for Week 4 - Google Code Jam problems"
date:   2023-02-13 15:00:56 -0600
author: "Alondra Galvan"
tags:
categories: technical-log
---

## Group Log

**Apprentice 2023A**
Abraham Ramirez
Aldo Santiago
Alejandro Mendoza
Alondra Galvan
Gonzalo Martinez
Gustavo Higuera
Juan Sanchez
Oscar Garzon


##Foregone

**Overview:**
The problem requires us to find two numbers that, when added up, are equal to the amount of a lottery prize (a target number), but any of the generated numbers can’t contain the digit 4.

The first input line contains the number of test cases (or the number of targets). The next line contains the target number, one for each case defined. The algorithm takes the string target number, then traverses the string and each digit is evaluated. During the evaluation, each digit of our numbers A and B is generated, simultaneously. The output of the algorithm shows the solution for each defined case. This process is repeated for each case.


**Context:**
Oh no! The keyboard of the oversized check printer is broken and the 4 key does not work. Someone just won the Code Jam lottery and this check has to be printed out. For some reason, the prize amount always includes at least one “4”. What can we do? Let’s print out two oversized checks that add up to the prize amount and do not contain the digit 4! We are tasked to find this pair of numbers to print out the checks.

**Solution**
**Iterative String Solution:**
To solve this problem, we noticed that we have to focus only on the digit “4”, every other digit does not matter. We decided to add a 2 to each check when we find a 4, that way we can maintain the value of the prize amount. 

We decided to read the input as a string and declare two empty strings for our output, a and b. Now, we can loop through the string and check if the digit is a 4, if it is, then we concatenate a “2” to each string, but if it’s not a 4, then we concatenate that digit to the a string and a “0” to the b string. We have to add a 0 to the b string, since we have to take into account the place value of each digit. 

When we’re done looping through the string, we will have two strings that represent the amount for each check, we can then return them and show the output. We decided to use strings to represent the numbers, since in Test Case 3, the number of the prize can be as large as 10100, and some languages can’t represent integers that large.

This solution, in terms of Big-O Notation, is O(N), since we loop through the string only once. 

To solve this problem in LISP, we had to adjust to the particularities of the language. In LISP, everything is a single linked-list, so the best data structure to work with is a list. We read the input as a string and looped through it normally, but instead of defining empty strings, we defined empty lists and used the cons function to add the digits to the lists. By doing this, we got a list in reverse order, so we utilized the reverse function to print out the list in the correct order.

In order to develop the solution in Java, the input string had to be converted into a String Array. This way was possible to traverse the digits in an easy way with a for loop. The A and B numbers were defined as strings so we used the concat function to add each digit, and no conversion was needed for the output.

To solve this problem using Go, it was necessary to convert the input of the problem to a string and the two output numbers too because using a 64-bit integer It couldn't pass the test cases due to the length of the numbers. Also using strings we could concatenate the numbers of the solution and iterate through the digits of the input number.

On the other hand, to develop the solution in Python, the inputs are taken as a String from the beginning. Then, given the target number, N, even though it is a string, we can use list methods to count the numbers of 4’s it has (with N.count( ); to reduce the number of iterations that will be made) and to find its position (using N.find() inside a loop to find them all).

**Alternative Solutions:**
**Iterative Integer Solution:**
We also consider reading the input as an integer. Following the described methodology, we consider looping through the number with extra help from the mod operator. So, we divide the number into 10 and then we can take the mod as the digit we want to evaluate.

During the evaluation, we also have to verify if the digit equals four. In this case, we can assign a “2” value in string A and another “2” in string B. In case the digit is not equal to 4, we can generate a random number between 0 and 9, but also different from 4 and 6 in string A, and use the B = d - A equation for string B.

After this evaluation, we re-assign the target number, and the loop continues until there are no more digits to evaluate, meaning, the target equals zero.

In this way, we can obtain a pair of numbers that equals the target, A and B, and also, they do not always follow the same pattern but they can generate in a more dynamic way. However, we consider that this might have a cost in running time, and space in internal memory, because of the processes described above, and the conversion needed from String to Integer, and the other way around.


## Nesting Depth

**Overview**
This problem consists of inserting the minimum number of parentheses in a string of digits, so each digit with a value d is inside exactly d pairs of matching parentheses.

The first input line contains the number of tests required (in this case, the number of strings to be evaluated). The next line contains the string of numbers, one for each case. In this algorithm, a 0 is added at the beginning and at the end of the string, then it is traversed and two digits are compared. Based on this evaluation, closing and opening parenthesis are added to the string. This process is repeated for each case.



**Context**
Given a string of digits S, insert a minimum number of opening and closing parentheses into it, such that the resulting string is balanced and each digit d is inside exactly d pairs of matching parentheses. 

Given a string of digits S, find another string S', comprised of parentheses and digits, such that: 

* All parentheses in S' match some other parenthesis 
* Removing any and all parentheses from S' results in S 
* Each digit in S' is equal to its nesting depth 
* S' is of minimum length 

For example, the string “2110330” should produce the string “((2)11)0(((33)))0”. 



**Solution**

**Difference between digits solution:**
If we observe some examples of correct values for S', and we go over every digit in S', we can notice that every time the value of a digit changes in S', there must be a certain number of parentheses between the digits that are different consecutively. Further observing, the number of parentheses between every two consecutive different digits, is the difference between the values of these digits. If a digit D is lower than its consecutive D', there must be D' - D opening parentheses between them. If D is greater than D', there must be D - D' closing parentheses.


There is just one issue with this approach, the first digit in S has no digit before to compare and insert the necessary parentheses, and the last digit has no consecutive one, so we can simply add a zero at the beginning and at the end of S, and when finishing inserting the necessary parentheses, we remove the 0s.


This solution has a time complexity of O(N) since we only need to iterate S once and calculate a difference for each digit. 


In order to solve the problem in Java, the input string was converted in a String Array to traverse the digits in an easy way with a for loop. We use the compareTo function to compare the digits in their string form. This function returns a value depending on the lexicographically difference between two characters, in this case, considering them as numbers:


* x = 0, if they are equal.
* x < 0, if the first number is less than the second one.
* x > 0, if the first number is greater than the second one.


So, this way we also obtain the exact number of parentheses we have to add to the string. In addition, the repeat function was used to create the parenthesis string without having to recursively add each one of them


We also created two functions called addClosingParentheses and addOpeningParenthesis for a better structure within the code. The join function was used to convert the new array created during the algorithm to a string. 

Implementation in Python was pretty straightforward and only involved iteration of a string.


**Alternative Solutions:**
The alternative solution was practically the same as the first solution, just implementing a counter of the open parenthesis instead of adding zeros at the beginning and the end of the string.
With that in mind, we could compare the digits with the counter, and if the digits - openParenthesis > 0 we add the necessary parenthesis (the remaining) and increment the counter. Otherwise if digits - openParenthesis < 0, we close the |digits - openParenthesis| parentheses.
The time complexity of this alternative solution was the same, O(N) because we only need to iterate S once.

To implement this problem in Go, we used the alternative solution for simplicity, because adding and removing characters from a string in Go is not as simple as in Python or Java, and using the counter helps us with that without using slices or implementing push/pop functions.

To implement the alternative solution in Lisp we used tail recursion. Instead of implementing the operations in a for loop they were implemented in the parameters of the function. So each iteration is equivalent to the next recursive call. The complexity of the recursive implementation is the same as the iterative implementation because we used tail recursion. 





## You Can Go Your Own Way

**Overview**
This problem involves going through a maze, the starting position is at the left upper corner and the exit is at the right lower corner. Someone has already solved the maze, therefore we must find a path that does not repeat the steps she has made. 

Given a number T indicating the total number of test cases, followed by 2 lines per test case, the first one indicating the size of the square maze and the second one indicating the path that our childhood rival took, we need to find another path that does not use the same steps as our rival. For example, if our rival went from A to B, we can cross A or B, but we can’t go from A to B in the same order.




**Context**
We entered the world of the world's easiest maze, our starting position is at the left upper corner, and the exit is at the right lower corner, but we only have two types of movement, we can go to the south, or to the right, but no other direction. We have a life long childhood rival named Lydia that has already solved the maze, therefore, we can not take the same path as her, but we can cross it at some points. We are tasked to find a new way out of the maze.


**Solution**

**Iterative String Solution**
We noticed that the maze is always an N by N grid, knowing that, we know we can simply reverse Lydia’s path and we’re done. Since the created path will have N-1 E’s and N-1 S’s, it will always end up at the exit. To do this, first, we declare an empty string for the output, and then, read the input as a string and loop through the characters. If the character is an S, we concatenate an E to the output string and vice versa. When we’re done looping through the string, we can return our output string.

This solution, in terms of Big-O Notation, is O(N), since we loop through the string only once. 

To solve this problem in LISP, we adjusted the algorithm a little bit. As in the Foregone solution, we read the input as a string, used a list we created using the cons function and reversed it at the end using the reverse function. 

For the solution in Python, we simply declare an empty string and add (using the operator +) an ‘E’ or ‘S’ (as chars) whenever it is necessary as it is described in the first paragraph of this section.

In Java we simply need to iterate the input string and then add ‘E’ or ‘S’ as chars to a new string, helping us with the position. Also we use the Scanner function of Java.

To solve it using Go, it is declared an empty string to save the solution. Iterating from zero to N-1 and checking if in Lydia’s path there is a ‘S’ comparing the char at the position with 83 (the corresponding number to S in ASCII). If ther is a ‘S’, we add an ‘E’ to the solution string, otherwise, we ad an ‘S’.

**Alternative Solutions:**

**Possibility sets**
You can have a lot of possible solutions, but it needs to be equally long than 2N - 2, so you can build a set containing a lot of strings, discard the ones that are not possible, and select one of the remaining, but it is too slow and also uses a lot of memory. 

**Graph Search Trees:**
Another approach is to do a search tree, do some search in NlogN time, and find the possible ways to solve the maze. This approach is a bit faster than the previous, but the one that we implemented has a linear complexity.





## ESAb ATAd

**Overview**
This problem involves retrieving an array of bits stored inside a machine. To retrieve the information, we can query the machine and receive the bit we ask for, but this machine is subject to random quantum fluctuations and the information stored inside is changing every 10 queries. 

This problem happens to be an interactive problem, so the judge will be the system created by Google. It is responsible for sending the bits back and judging if our response is right or wrong. The input for our program consists of a single line containing T and B, where T represents the amount of test cases and B represents the size of the array, it is constant throughout the test cases. Then we will process each test case, we can do up to 150 queries before printing the array out. The judge will respond with a “Y” or “N”, if we get a “Y”, we continue with the next test case, if there is any, but, if we get an “N”, we must end the program.

**Context**
Last year, a research consortium had some trouble with a distributed database system that sometimes lost some data. They decided to store the data in a machine, where the data is stored in an array made up of bits. To obtain the information from the machine, you must make a query and receive the array bit by bit. There’s one problem though, this machine is subject to random quantum fluctuations, specifically after every 1st, 11th, 21th… query is sent. These fluctuations happen before the system sends the bit and there are four types of fluctuations that have equal chance of happening: 

* 25% of the time, the array is complemented: every 0 becomes a 1, and vice versa.
* 25% of the time, the array is reversed: the first bit swaps with the last bit, the second bit swaps with the second-to-last bit, and so on.
* 25% of the time, the array is complemented and reversed.
* 25% of the time, nothing happens to the array.

We are tasked to retrieve the data in whichever form it is, it doesn’t matter if it is fluctuated or not, we just have to be accurate by the time we give it. We can make up to 150 queries per test case.


**Solution**
Because we need to retrieve the whole data array of bits in its current state, for test cases with data arrays of length 10 we can simply query each bit and once we have all 10 bits we have the answer because no fluctuation occurred after the storing of the first bit.

For test cases with length greater than 10, fluctuations will occur after we have already stored some bits, so we need to identify what type of fluctuation occurred and update our local copy.

Identifying complements is easy if only this type of fluctuation could happen, similarly, if only a reversal could happen we need to identify a known bit with a symmetric pair that has a different value, for example if the left bit is 0, the right bit is 1, and after a fluctuation if these values change, it means we had a reverse operation. In this scenario both complement and reversal may happen individually or at the same time.

So, back to our bit with symmetric pair with different value, if it changes after a fluctuation, it means there was either a reversal or a complement, to know what exactly happened we need to identify another bit with a symmetric pair but this one with the same value, if after the fluctuation this bit does not change, it means we did not have a complement, if it does, then we had a complement.

That way we query for unknown bits when we know a fluctuation was not present, and only at the 11th, 21st, 31st, … queries we must spend some queries to ask for known bits and check how they changed as described above to know what exactly happened and update our local copy if necessary.

The implementation in Python involved the use of dictionaries to store information about the value of the bit, and information about its symmetric pair (if it has an equal or different value).

In Java the code is very ‘simple’ and readable, but it took hours of analysis to get to that point. Because Java is very verbose, it is kinda hard to get to a point without getting confused by too many words. Also it was kinda hard to test because of the type of problem. But at the end, it still is the same solution that many languages use, without the need of doing anything more.

Initially we tried to implement the first solution in Lisp but the language forced us to modify some things. Handling dictionaries in Lisp is complicated so we found out that it is not necessary to know if a pair is symmetric or asymmetric for each bit in the number. You only need to know one symmetric pair and one asymmetric pair. And if there are only asymmetric pairs you only need to know one pair, the case for only symmetric pairs is analogous. So instead of dictionaries we used two variables to store the values of the indexes of symmetric and asymmetric pairs, and an array to store the number bits we already knew. We also found out that if you only have asymmetric pairs then there are only two possible operations: complement or nothing. The other operations reduce to these two. If you only have symmetric pairs, it is analogous. With these two observations we were able to implement the solution in Lisp. The rest of our implementation is very similar to the original solution, after each 10 module 1 queries to Google we check the operation made to the number, update our array and keep asking for new bits until we know the value of the number.



**Alternative Solution:**
**Possibility Set:**
Another approach to the solution of the problem is creating a possibility set, every array describes a possible solution, and every time we check for a fluctuation we can eliminate the arrays that does not fit in the solution, analyzing this approach we can see that it uses a lot of memory and also is slower than ours, we can improve this using probability, but the computational effort it’s almost the same and it’s harder to implement.




***

## Individual Log

**Cryptopangrmas**

**Overview**
Given a list of numbers which each number is product of exactly two primes, the code should return a decrypted message. 

For the input of the program, we receive a line with the number of test cases (T), another line with the upper bond to the primes that letters were assigned (N) and the length of the list of numbers that form the encrypted message (L) and finally a line with the list of numbers (A). 

For the output, it is printed the number of case and the result (the decrypted message) in the format “Case #n: solution” where n is the number of case and solution is a string containing the decrypted message. 


**Context**
We only know that the message was encrypted as it follows: 

All spaces from the original message are erased. 

The original message contains all of the letters of the English alphabet at least once. 

A prime number is assigned to each letter of the alphabet in a way that the prime number assigned to ‘A’ is smaller than the prime number of ‘B’ and so on.  

Each number in the encrypted message is the product of the primes corresponding to two each consecutive letters in the original message; the first number in the encrypted message is the product of the prime assigned to the first letter in the original message with the prime assigned to the prime of the second letter of the original message. 

**Solution**
