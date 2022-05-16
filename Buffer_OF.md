
# Buffer Overflow Attack

## 1(Section 3.4): Binaries a32.out and a64.out[32 and 64 bit]
When we compile the “make” file from shellcode, then it will generate two binaries a32.out and a64.out. After running these binaries, it opens a new shell as shown below.
!<img width="410" alt="image" src="https://user-images.githubusercontent.com/92758859/168507830-58a8ac3f-ea1d-4779-ae30-8f04a780f2d0.png">

 

## 2.(Section 4): Functioning of stack.c.
 “bof()” is the function in stack.c program. It contains a character buffer of size 100 (BUF_SIZE) and a strcpy() function. From the file 517 bytes of data is read by the main function which is  "badfile", and then copies the data to a buffer of size 100. Here, there is a buffer overflow. We will place the code in "badfile", when the program reads from that file, the code is loaded into the string array. The program copies string to the target buffer, the code will be stored on the stack. Now, we want the program to jump to the code. We can overwrite the return address field. Here, if the address of the “bad file” is known, then we can use this address to overwrite the return address field. When the function bof() returns, it will redirect to the new address, where the code is stored.
Section 5.1 – Distance between the buffer's start address and the location of the stored return address
We have calculate the Distance by “gdb” command.
![image](https://user-images.githubusercontent.com/92758859/168507872-5dd81478-2ba3-460e-8f04-2c9e467527c6.jpeg)

 
## 3.(Section 5.2) – The Final contents of exploit.py after modifications
![image](https://user-images.githubusercontent.com/92758859/168507764-2454c429-4a65-4c10-a40c-ed840be53303.jpeg)

 

Section 5.2 – Explanation of how the values used in your exploit.py were decided.
To create or produce a new shellcode w have used the code from the pdf provided. We need to put the shellcode somewhere in the payload. There was a change in the code which is : “start = 517 - len(shellcode)”. 517 is the total bytes data that will be copied. The return address is set to “ret = 0xffffcb78 + 200”, because, the address 0xffffcb78 was identified using the debugging method and the stack frame of the function bof() may be different when the program runs inside gdb as opposed to running directly. The gdb may cause the stack frame to be allocated deeper than it would be when the program runs directly. The first address may direct to address higher than 0xffffcb78 + 8. As stated by the result of gdb, the return address field initializes from offset 112.   
## 4.(Section 5.2)– Successful Attack
<img width="468" alt="image" src="https://user-images.githubusercontent.com/92758859/168507743-96736fef-5b1e-4d4f-ab87-ee4c917d92aa.png">

 
 (Completed till task 3, Due to exams and less time available couldn’t do all of them.)
