# Linux-File-IO-Systems-locking
Ex07-Linux File-IO Systems-locking
# AIM:
To Write a C program that illustrates files copying and locking

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

int main() {
    char block[1024];
    int in, out;
    int nread;

    in = open("filecopy.c", O_RDONLY);
    out = open("file.out", O_WRONLY | O_CREAT, S_IRUSR | S_IWUSR);

    while ((nread = read(in, block, sizeof(block))) > 0)
        write(out, block, nread);

    exit(0);
}
```






## 2.To Write a C program that illustrates files locking
```
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>
#include <sys/file.h>

int main(int argc, char* argv[])
{
    if (argc < 2) {
        printf("Usage: %s <filename>\n", argv[0]);
        return 1;
    }

    char* file = argv[1];
    int fd = open(file, O_RDWR | O_CREAT, 0666);
    if (fd == -1) {
        perror("open failed");
        return 1;
    }

    if (flock(fd, LOCK_SH) == -1) {
        perror("shared lock failed");
    } else {
        printf("Acquiring shared lock using flock\n");
    }

    getchar(); // wait for Enter
    if (flock(fd, LOCK_EX | LOCK_NB) == -1) {
        perror("exclusive lock failed");
    } else {
        printf("Acquiring exclusive lock using flock\n");
    }

    getchar(); // wait for Enter
    if (flock(fd, LOCK_UN) == -1) {
        perror("unlock failed");
    } else {
        printf("Unlocking\n");
    }

    close(fd);
    return 0;
}
```



## OUTPUT

<img width="500" height="185" alt="Screenshot from 2025-10-26 22-56-43" src="https://github.com/user-attachments/assets/2530ad19-738d-44c1-8e39-2b4fc0678b01" />

<img width="879" height="1105" alt="image" src="https://github.com/user-attachments/assets/52883bea-b7f5-4af8-a30c-e10713006b1c" />








# RESULT:
The programs are executed successfully.
