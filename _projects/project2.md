---
layout: post
title: Roman Numeral Conversion in MIPs
description: A program that converts Roman Numeral string inputs to Decimal & Binary Values!
---

Objective
============

In this project, I developed a stronger understanding of how data is represented, stored, and manipulated at the processor level by creating a MIPS program that takes Roman Numerals as a form of string input, converts the values into binary and decimal, and prints the output as ASCII characters.

Implementation
============

The implementation process was divided into two steps. In the first step, I design what the program's functionality would look like and provide pseudocode to aid in visualizing how it would process user input. In the second step, I developed the code.

### Design ###

When thinking about edge-cases for this program, I considered the following:

~~~
a.	M is an invalid character
b.	No more than 3 consecutive identical Roman Numerals
c.	Only 1 'I' 'X' 'C' can be used as the leading numeral in part of 
	a subtraction pair. [Not needed as already implemented by d,e,f]
d.	'I' can only be placed before V and X [ or 0x0000]
e.	'X' can only be placed before L and C [ or 0x0000]
f.	'C' can only be placed before D	      [ or 0x0000]
g.	'D' 'L' 'V' can only appear once
~~~

To plan for my program, I developed some partial pseudocode that would allow me to gain a better understanding of how my program would flow and handle not only the aforementioned error and edge cases, but also how it would progress with long computations. The pseudocode follows:

~~~
> Program prompts the user for a Roman Numeral Input

> Program accesses the user's input

> Program checks for possible errors [A, B, C, D, E, F, G] within the user's input	

	> Program encounters an error
		- Program will display an error message
		- Program will return to the main prompt
	
	> Program encoutners no error
		1. Program takes the length of the Roman Numeral and stores in a reg (r)
		
		2. Program decodes the Roman Numerals (represented as Hex characters)
		   to decimal
			
			>> Loop
			a. Program takes with the first Roman Numeral (i) 
			b. Program converts (i) to a decimal representation		
			c. Program adds (i) to the total running sum (s)
			d. Program increments (i++)
			e. Program compares (i) to (i++)
				e.1: if (i) > (i++), then Program does (s) - (i++)
				e.2: if (i) < (i++), then Program does (s) + (i++)
			f. Program increments (i++)
			g. Program decrements (r--)
			h. Program compares length
				h.1 if (r) is = 0, Program exits
				h.2 if (r) is != 0, Program loops back to a.
		
		3. Program decodes the decimal representation to binary
			
			>> Loop
			* Program starts with a reg hold a 2 power (2P) *
			a. Program takes (s)
			b. Program takes (s) & (2P)
				c.1 If (s) - (2P) then...
					c.1.i 	'1' is inputted into a binary register (b)
					c.1.ii 	(2P) gets divided by 2
					c.1.iii	(b) gets shifted to the left by 4B
				c.2 if (s) !- (2p) then..
					c.1.i 	'0' is inputted into a binary register (b)
					c.1.ii 	(2P) gets divided by 2
					c.1.iii	(b) gets shifted to the left by 4B
			d. Program checks to see if (s) is 0
				d.1 If (s) = 0, then program exits
				d.2 If (s) != 0, then program jumps back to a.
		
		4. Program outputs the base 2 representation of the Roman Numeral
			
			>> Loop
			* Program gets the length of (l) *
			a. Program goes to (b)
			b. Program goes to the first value of (b) called (k)
			c. Program prints (k)
			d. Program increments(k++)
			e. Program decrements (l--)
				f.1 If (l) = 0, Program terminates
				f.2 If (l) != 0, Program jumps to a.
		
		5. Program Exits
			li	$v0 10
			syscall
~~~

### Develop ###

The final program code is posted on my GitHub and can be found [here](https://github.com/jimmy-franknedy/Website_Code/blob/main/Roman%20Numeral%20Conversion%20in%20MIPs/Lab4.asm){:target="_blank"}.

Evaluation
============

When testing the program for bugs, I considered the following:

1. Invalid Roman Numeral Inputs
2. Short & Long Roman Numeral Inputs
3. Addition & Subtraction Roman Numeral Computations

Conclusion
============

Through the course of this program, not only was I developing my MIPS programming skillset and gaining a deeper understanding of how data was stored and manipulated at the processor level, but I was also learning how to create functions that would allow my program to run more efficiently (recalling the notion of divide-and-conquer).