---
layout: post
title:  "Volatile keyword used in C programming"
date:   2015-07-08 04:37:49
categories: volatile, keyword, programming
banner_image: ""
featured: false
comments: true
---

Embedded Programmers are often asked about “volatile” keyword. I have tried explaining it in this article.So let’s start off with the definition.What does volatile keyword mean to C compiler? It meas “dont perform any sort of optimisation please. Specifically, reload the variable every time I access it”.
Eg:

<pre>
fun()
{
volatile int IamVolatile;
int IamNotVolatile;
int temp;
temp = IamVolatile; /* Fetches from the actual memory address.*/
temp = IamNotVolatile; /* Fetches from the actual memory address. */
…
…
temp = IamNotVolatile; /* Compiler MIGHT optimise this line. It MIGHT not go and fetch 
from memory address of ‘IamNotVolatile’…Runtime Performance optimistaion!.*/

temp = IamVolatile; /* Fetches from the actual memory address */

}
</pre>

From the Programmer perspective ”volatile” variable is the one that can change unexpectedly. But why do you need this at all?If “IamVolatile” were to be a hardware register whose value is dependent on external h/w,there is no way we can do something in C without “volatile”.Here is a list of potential candidates for “volatile”:

1>Hardware registers.
2>Variables referenced in an ISR(interrupt service routine) and main code.
3>Variables shared across tasks in OS based Code.
4>Variables used across SetJump/Longjumps.

The point is where ever compiler tends to make optimisation due to of lack of static analysis shortcoming, it is potential candidate if need be.

“volatile” used along with other C keywords:

1> extern volatile unsigned int externalvar; /* volatile variable outside a module.*/

2> volatile const unsigned int PSW; /* An example is a read-only status register. It is volatile because it can change unexpectedly. It is const because the program should not attempt to modify it. */
3> volatile int* ptr; /*”ptr” points to VOLATILE memory.*/
Following is the scenario of excessive usage of volatile which introduces bugs in software:

<pre>
main()
{

volatile unsigned char *sptr = (unsigned char *) (0×1000);

unsigned int res;

res = acessserialportandMulBy3(sptr);

}

/* read serial port and return cube of it */
unsigned int acessserialportandMulBy3(volatile unsigned char *p)
{

unsigned int res;

res = ((*sptr) * (*sptr) * (*sptr) );

return res;

}
</pre>

I leave it to you to find the bug in the above code.

Technorati Tags: Software Development, Volatile, Cprogramming, Usage of volatile, Embedded