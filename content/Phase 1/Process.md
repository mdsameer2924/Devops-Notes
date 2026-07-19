> in [[Linux]] everything is a Process

process refers to allocate resources and utilizing it to process the job. while linux [[Operating system]] assign each and every process to PID `Process ID` to unique indentity.    
whether it can be
- [[Process#Kernel process|Kernal Process]]
- [[Process#User Process|User Process]] 
- [[Process#Daemon Process|Daemon Process]]

## Kernel process
it's a process which managed by [[Architecture of Linux#Kernel|kernel]] itself most of the 
even [[Systemd 1]] is a example of [[Architecture of Linux#Kernel|kernel]] process which 

## User Process
it's a process which created and managed by a user, it might be a Application software or user script and command which running as a [[Background Process|background process]] either [[Foreground Process|foreground process]]

## Daemon Process
it's also known as [[Services in Linux]] which managed by [[Systemd 1]]. where Daemon means `background` + `process` means background process run.