# VulnerableCS
A collection of proof-of-concept exploitable applications in C#

## SQL Injection

  An application that connects to a MySQL database and checks if the username and password supplied by the user is valid. Can be exploited by essentially any injection vector. This is due to a lack of input sanitation.

## Buffer Overflow

  Demonstrates the rare case where a C# application is vulnerable to a buffer overflow. A couple of conditions must be met in order to perform a buffer overflow. This is due to CRL's garbage collection! It is well known that c# creates space on the heap instead of the stack. In order to order to force CRL to create the variable on the stack, 
[stackalloc](https://msdn.microsoft.com/en-us/library/cx9s2sy4.aspx)
must be used in the variable's definition. Because this is considered unsafe, you must first allow unsafe code in the project settings. The method must also be declared unsafe. [unsafe keyword](https://msdn.microsoft.com/en-us/library/chfa2zb8.aspx)


Before entering the loop, the memory location of the variable "number" is displayed...

![](http://imgur.com/pCu8tFD.jpg)


After running through the loop a single time, the memory looks like.

![](http://imgur.com/MW7SrMQ.jpg)

Running through a second time displays a memory profile of

![](http://imgur.com/8Q57e5k.jpg)

Note that the end of allocated memory has been reached. Any further addition will overrun the stack and cause a segmentation fault.

![](http://imgur.com/sDZwBdR.jpg)

Because of the particular conditions that must be met for this to happen, it is not practical and is extremely rare in the wild.

  
