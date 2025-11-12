# Linux-Process-API-fork-wait-exec-

# Ex02-OS-Linux-Process API - fork(), wait(), exec()

# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:

### C Program to create new process using Linux API system calls fork() and getpid() , getppid() and to print process ID and parent Process ID using Linux API system calls

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>  

int main() {
    int pid = fork();

    if (pid == 0) { 
        printf("I am child, my PID is %d\n", getpid()); 
        printf("My parent PID is: %d\n", getppid()); 
        sleep(2); 
    } 
    else if (pid > 0) { 
        printf("I am parent, my PID is %d\n", getpid()); 
        wait(NULL); 
    } 
    else {
        printf("Fork failed!\n");
        return 1; // Error in fork
    }

    return 0;
}
```
## OUTPUT:

![WhatsApp Image 2025-11-12 at 21 52 17_4772602c](https://github.com/user-attachments/assets/8fabaaa4-eb92-4d22-8a0a-9544f0a75429)


### C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    int status;
    
    printf("Running ps with execl\n");
    if (fork() == 0) {
        execl("ps", "ps", "-f", NULL);
        perror("execl failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)) {
        printf("Child exited with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    
    printf("Running ps with execlp (without full path)\n");
    if (fork() == 0) {
        execlp("ps", "ps", "-f", NULL);
        perror("execlp failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)) {
        printf("Child exited for execlp with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    
    printf("Done.\n");
    return 0;
}
```

## OUTPUT:

![WhatsApp Image 2025-11-12 at 21 52 52_575ee9a8](https://github.com/user-attachments/assets/3270ab6d-9561-4ed0-a730-abab4028882b)



# RESULT:
The programs are executed successfully.
