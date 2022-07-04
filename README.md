# **shellpranks.sh**
## Bash/zsh shell pranks that print errors when attempting to run certain commands
---
## **Note:** This will make these commands unusable *in that shell* except for builtin commands such as `cd`.
---
## **DISCLAIMER**
We (@terminalcommandnewsletter), the maintainer of this project, are not liable for any damages caused by the commands listed below.
---
## **The Commands**
---
### Fake Sudo / Incorrect Password

This makes it so that typing the password into the sudo command always prints "Sorry, try again". After 3 attempts, the command exits.

```bash
sudo(){ if [[ $# -ne 0 ]]; then for each in {1..2}; do printf "Password:"; read -s; printf "\n"; sleep 0.3; printf "Sorry, try again.\n"; done; printf "Password:"; read -s; printf "\n"; sleep 0.7; printf "sudo: 3 incorrect password attempts\n"; else printf "usage: sudo -h | -K | -k | -V\nusage: sudo -v [-AknS] [-g group] [-h host] [-p prompt] [-u user]\nusage: sudo -l [-AknS] [-g group] [-h host] [-p prompt] [-U user] [-u user]\n            [command]\nusage: sudo [-AbEHknPS] [-C num] [-D directory] [-g group] [-h host] [-p\n            prompt] [-R directory] [-T timeout] [-u user] [VAR=value] [-i|-s]\n            [<command>]\nusage: sudo -e [-AknS] [-C num] [-D directory] [-g group] [-h host] [-p prompt]\n            [-R directory] [-T timeout] [-u user] file ...\n"; fi }
```
---
### Fake RM / Permission Denied

This makes it so that anytime rm is run, instead of deleting the file, the program prints "rm: cannot remove: permission denied"

```bash
rm(){ if [[ $# -ne 0 ]]; then for file in $*; do printf "rm: cannot remove '$file': Permission denied\n"; done; else printf "usage: rm [-f | -i] [-dIPRrvWx] file ...\n       unlink [--] file\n"; fi }
```
---
### Fake LS / Operation Not Permitted

This makes it so that anytime ls is run, instead of listing the contents of the directory, the program prints "ls: Operation not permitted"

```bash
ls(){ if [[ $# -ne 0 ]]; then for directory in $*; do if [[ $directory == */ ]]; then printf "ls: $directory: Operation not permitted\n"; else printf "ls: $directory/: Operation not permitted\n"; fi; done; else printf "ls: .: Operation not permitted\n"; fi }
```
---
### Fake CURL / Could Not Resolve Host

This makes it so that anytime curl is run, instead of making the request, the program prints "curl: (6) Could not resolve host"

```bash
curl(){ if [[ $# -ne 0 ]]; then printf "curl: (6) Could not resolve host: $1\n"; else printf "curl: try 'curl --help' or 'curl --manual' for more information\n"; fi }
```
---
### Fake CD / No Such File/Directory

This makes it so that anytime cd is run, instead of deleting the file, the program prints "cd: no such file or directory"

```bash
cd(){ if [[ $# -ne 0 ]]; then printf "cd: no such file or directory: $1\n"; fi }
```
---
### Fake SU / Incorrect Password

This makes it so that typing the password into the su command always prints "su: Sorry".

```bash
su(){ printf "Password:"; read -s; printf "\n"; sleep 0.3; printf "su: Sorry\n"; }
```