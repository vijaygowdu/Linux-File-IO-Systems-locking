# Linux-File-IO-Systems-locking
Ex07-Linux File-IO Systems-locking
# AIM:
To Write a C program that illustrates files copying and locking

Name: K Vijay

regno:212223040236
# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux IO Systems locking

### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:

## 1.To Write a C program that illustrates files copying 
```
#include <unistd.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdlib.h>
int main()
{
char block[1024];
int in, out;
int nread;
in = open("filecopy.c", O_RDONLY);
out = open("file.out", O_WRONLY|O_CREAT, S_IRUSR|S_IWUSR);
while((nread = read(in,block,sizeof(block))) > 0)
write(out,block,nread);
exit(0);}
```
## output

![WhatsApp Image 2024-05-08 at 19 55 00_71126963](https://github.com/vijaygowdu/Linux-File-IO-Systems-locking/assets/147473788/ba5bff94-c9e1-42bd-b8a7-f7ddc0667471)

![WhatsApp Image 2024-05-08 at 19 55 18_fece21d5](https://github.com/vijaygowdu/Linux-File-IO-Systems-locking/assets/147473788/46341f1e-4b1c-4842-8b80-91c26ebd492b)

![WhatsApp Image 2024-05-08 at 19 55 34_005e3962](https://github.com/vijaygowdu/Linux-File-IO-Systems-locking/assets/147473788/8b5ce0ca-d0f4-44a4-b969-ba32cd5b97bd)


## 2.To Write a C program that illustrates files locking
```
#include <fcntl.h>
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <sys/file.h>
int main (int argc, char* argv[])
{ char* file = argv[1];
 int fd;
 struct flock lock;
 printf ("opening %s\n", file);
 /* Open a file descriptor to the file. */
 fd = open (file, O_WRONLY);
// acquire shared lock
if (flock(fd, LOCK_SH) == -1) {
    printf("error");
}else
{printf("Acquiring shared lock using flock");
}
getchar();
// non-atomically upgrade to exclusive lock
// do it in non-blocking mode, i.e. fail if can't upgrade immediately
if (flock(fd, LOCK_EX | LOCK_NB) == -1) {
    printf("error");
}else
{printf("Acquiring exclusive lock using flock");}
getchar();
// release lock
// lock is also released automatically when close() is called or process exits
if (flock(fd, LOCK_UN) == -1) {
    printf("error");
}else{
printf("unlocking");
}
getchar();
close (fd);
return 0;
}
```
## OUTPUT
![WhatsApp Image 2024-05-08 at 19 57 11_7c9c0348](https://github.com/vijaygowdu/Linux-File-IO-Systems-locking/assets/147473788/6cffb692-79f1-4699-8f5a-2241a0ca08ea)

## RESULT:
The programs are executed successfully.
