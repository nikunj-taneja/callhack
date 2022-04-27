# Callhack

<b>Disclaimer:</b> This project was developed in collaboartion with Ahmad Rammah as part of an assignment for the CSC369 Operating Systems course taken at the University of Toronto taught by Prof. Bogdan Simion in Fall 2021. The starter code for this assignment was provided by Prof. Simion. 

Callhack is a very basic Linux kernel module that intercepts (hijacks) system calls. It implements a new system call named ``my_syscall`` which allows users to send commands from userspace, to intercept another pre-existing system call (like read, write, open, etc.). After a system call is intercepted, the intercepted system call logs a message first before continuing performing what it was supposed to do. 

The new system call ``my_syscall`` is defined as follows:
<br>
<br>
``int my_syscall(int cmd, int syscall, int pid);`` 
<br>
<br>
will serve as an interceptor and will receive the following commands from userspace:
* REQUEST_SYSCALL_INTERCEPT: intercept the system call  syscall
* REQUEST_SYSCALL_RELEASE: de-intercept the system call  syscall
* REQUEST_START_MONITORING: start monitoring process  pid  for system call ``syscall`` , i.e., add  ``pid``
to the  syscall 's list of monitored PIDs. A special case is that if  pid  is  0  then all processes are
monitored for ``syscall`` , but only root has the permission to issue this command.
* REQUEST_STOP_MONITORING: stop monitoring process ``pid`` for system call ``syscall``, i.e., remove ``pid`` 
from the ``syscall``'s list of monitored PIDs.
