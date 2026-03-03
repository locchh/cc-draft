# Linux Commands

## Table of Contents

- [1. Navigation](#1-navigation)
- [2. Files](#2-files)
- [3. Directories](#3-directories)
- [4. Text Processing](#4-text-processing)
- [5. Permissions](#5-permissions)
- [6. User Management](#6-user-management)
- [7. Package Management](#7-package-management)
- [8. Help & Documentation](#8-help--documentation)
- [9. Archive](#9-archive)
- [10. Network](#10-network)
- [11. System Info](#11-system-info)
- [12. Process Management](#12-process-management)
- [13. Services](#13-services)
- [14. Session](#14-session)
- [15. Extras](#15-extras)
- [16. Git](#16-git)
- [17. Docker](#17-docker)
- [18. Kubernetes](#18-kubernetes)

## <a id="1-navigation"></a>1. Navigation [↑](#table-of-contents)

### `ssh` — Connect to a remote machine securely

```bash
ssh user@hostname
ssh user@192.168.1.1
ssh -p 2222 user@hostname        # custom port
```

### `ls` — List directory contents

```bash
ls                               # basic list
ls -l                            # long format with permissions
ls -a                            # show hidden files
ls -la /etc                      # combine flags on a path
```

### `pwd` — Print current working directory

```bash
pwd
```

### `cd` — Change directory

```bash
cd /etc                          # absolute path
cd ..                            # go up one level
cd ~                             # go to home directory
cd -                             # go to previous directory
```

### `clear` — Clear the terminal screen

```bash
clear
# shortcut: Ctrl+L
```

---

## <a id="2-files"></a>2. Files [↑](#table-of-contents)

### `touch` — Create empty file(s) or update timestamp

```bash
touch file.txt
touch file1.txt file2.txt
```

### `echo` — Print text or write to a file

```bash
echo "Hello World"
echo "text" > file.txt           # overwrite file
echo "text" >> file.txt          # append to file
```

### `nano` — Simple terminal text editor

```bash
nano file.txt
# Ctrl+O = save, Ctrl+X = exit
```

### `vim` — Advanced terminal text editor

```bash
vim file.txt
# i = insert mode, Esc = normal mode
# :wq = save & quit, :q! = quit without saving
```

### `cat` — Display file contents

```bash
cat file.txt
cat file1.txt file2.txt          # concatenate multiple files
```

### `shred` — Securely overwrite and delete a file

```bash
shred file.txt                   # overwrite in place
shred -u file.txt                # overwrite then remove
shred -n 5 file.txt              # overwrite 5 times
```

### `cp` — Copy files or directories

```bash
cp file.txt backup.txt
cp -r folder/ backup/            # copy directory recursively
```

### `mv` — Move or rename files

```bash
mv old.txt new.txt               # rename
mv file.txt /tmp/                # move to another directory
```

### `rm` — Remove files or directories

```bash
rm file.txt
rm -r folder/                    # remove directory recursively
rm -rf folder/                   # force remove (no prompts)
```

### `ln` — Create links between files

```bash
ln file.txt hardlink.txt         # hard link
ln -s file.txt symlink.txt       # symbolic (soft) link
```

### `less` — View file contents page by page

```bash
less file.txt
# Space = next page, b = back, /word = search, q = quit
```

### `head` — Show the first lines of a file

```bash
head file.txt                    # first 10 lines (default)
head -n 20 file.txt              # first 20 lines
```

### `tail` — Show the last lines of a file

```bash
tail file.txt                    # last 10 lines (default)
tail -n 20 file.txt              # last 20 lines
tail -f app.log                  # follow live output (great for logs)
```

### `cmp` — Compare two files byte by byte

```bash
cmp file1.txt file2.txt
```

### `diff` — Show line-by-line differences between two files

```bash
diff file1.txt file2.txt
diff -u file1.txt file2.txt      # unified format (easier to read)
```

### `find` — Search for files and directories

```bash
find . -name "*.txt"             # find .txt files from current dir
find /home -name "file.txt"      # find by name
find . -type d                   # find directories only
find . -mtime -7                 # modified in last 7 days
```

---

## <a id="3-directories"></a>3. Directories [↑](#table-of-contents)

### `mkdir` — Create a directory

```bash
mkdir myfolder
mkdir -p parent/child/grandchild # create nested directories
```

### `rmdir` — Remove an empty directory

```bash
rmdir myfolder
```

---

## <a id="4-text-processing"></a>4. Text Processing [↑](#table-of-contents)

### `sort` — Sort lines of a file

```bash
sort file.txt
sort -r file.txt                 # reverse order
sort -n numbers.txt              # numeric sort
```

### `grep` — Search for patterns in files

```bash
grep "pattern" file.txt
grep -r "pattern" ./             # search recursively
grep -i "pattern" file.txt       # case-insensitive
grep -n "pattern" file.txt       # show line numbers
```

### `awk` — Pattern scanning and text processing

```bash
awk '{print $1}' file.txt                   # print first column
awk -F: '{print $1}' /etc/passwd            # use : as delimiter
awk '/pattern/ {print}' file.txt            # print matching lines
```

---

## <a id="5-permissions"></a>5. Permissions [↑](#table-of-contents)

### `chmod` — Change file permissions

```bash
chmod 755 script.sh              # rwxr-xr-x
chmod +x script.sh               # add execute permission
chmod -R 644 folder/             # apply recursively
```

### `chown` — Change file owner and group

```bash
chown user file.txt
chown user:group file.txt
chown -R user:group folder/
```

---

## <a id="6-user-management"></a>6. User Management [↑](#table-of-contents)

### `whoami` — Show the current logged-in user

```bash
whoami
```

### `useradd` — Add a new user (low-level)

```bash
sudo useradd username
sudo useradd -m username         # also create home directory
sudo useradd -m -s /bin/bash username
```

### `adduser` — Add a new user (interactive, friendlier)

```bash
sudo adduser username
```

### `sudo` — Run a command as superuser

```bash
sudo apt update
sudo -i                          # open a root shell
```

### `su` — Switch to another user

```bash
su username
su -                             # switch to root
```

### `passwd` — Change user password

```bash
passwd                           # change your own password
sudo passwd username             # change another user's password
```

### `exit` — Exit current shell or session

```bash
exit
# shortcut: Ctrl+D
```

---

## <a id="7-package-management"></a>7. Package Management [↑](#table-of-contents)

### `apt` — Debian/Ubuntu package manager

```bash
sudo apt update                  # refresh package list
sudo apt upgrade                 # upgrade all installed packages
sudo apt install package-name
sudo apt remove package-name
sudo apt search keyword
```

---

## <a id="8-help--documentation"></a>8. Help & Documentation [↑](#table-of-contents)

### `finger` — Display info about a user

```bash
finger
finger username
```

### `man` — Display the manual page for a command

```bash
man ls
man grep
```

### `whatis` — Show a one-line description of a command

```bash
whatis ls
whatis grep
```

---

## <a id="9-archive"></a>9. Archive [↑](#table-of-contents)

### `zip` — Compress files into a zip archive

```bash
zip archive.zip file1.txt file2.txt
zip -r archive.zip folder/       # zip a whole directory
```

### `unzip` — Extract a zip archive

```bash
unzip archive.zip
unzip archive.zip -d /target/    # extract to a specific directory
```

---

## <a id="10-network"></a>10. Network [↑](#table-of-contents)

### `curl` — Transfer data from or to a URL

```bash
curl https://example.com
curl -O https://example.com/file.txt          # download file
curl -X POST -d '{"key":"val"}' https://api.example.com
```

### `ifconfig` — Show/configure network interfaces (legacy)

```bash
ifconfig
ifconfig eth0
```

### `ip address` — Show network interfaces (modern replacement for ifconfig)

```bash
ip address
ip addr show eth0
ip a                             # shorthand
```

### `resolvectl status` — Show DNS resolver status

```bash
resolvectl status
```

### `ping` — Test network connectivity to a host

```bash
ping google.com
ping -c 4 google.com             # send only 4 packets
```

### `netstat` — Show network connections and stats (legacy)

```bash
netstat -tuln                    # list listening ports
netstat -an                      # all connections
```

### `ss` — Show socket statistics (modern netstat)

```bash
ss -tuln                         # list listening ports
ss -s                            # summary statistics
```

### `iptables` — Configure kernel-level firewall rules

```bash
sudo iptables -L                 # list all rules
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -F                 # flush (clear) all rules
```

### `ufw` — Uncomplicated Firewall (easy iptables frontend)

```bash
sudo ufw enable
sudo ufw disable
sudo ufw status
sudo ufw allow 22                # allow SSH
sudo ufw deny 80                 # deny HTTP
```

---

## <a id="11-system-info"></a>11. System Info [↑](#table-of-contents)

### `uname` — Print system information

```bash
uname -a                         # all info
uname -r                         # kernel version only
uname -m                         # machine hardware name
```

### `neofetch` — Display system info with ASCII art logo

```bash
neofetch
```

### `cal` — Display a calendar

```bash
cal                              # current month
cal 2025                         # full year
cal 3 2025                       # specific month and year
```

### `free` — Show RAM and swap usage

```bash
free
free -h                          # human-readable (MB/GB)
```

### `df` — Show disk space usage

```bash
df
df -h                            # human-readable
df -h /home                      # specific mount point
```

### `env` — Display or modify environment variables

```bash
env                              # show all environment variables
env | grep HOME                  # filter specific variables
env VAR=value command            # run command with custom variable
env -i COMMAND                   # run command with empty environment
```

### `set` — Display or modify shell variables and functions

```bash
set                              # show all shell variables and functions
set | grep PATH                  # filter specific variables
set -x                           # enable debug mode (show commands)
set +x                           # disable debug mode
set -e                           # exit on error
```

---

## <a id="12-process-management"></a>12. Process Management [↑](#table-of-contents)

### `ps` — Snapshot of running processes

```bash
ps
ps aux                           # all processes with full details
ps aux | grep nginx              # find a specific process
```

### `top` — Live process monitor (built-in)

```bash
top
# q = quit, k = kill process, M = sort by memory
```

### `htop` — Interactive process monitor (better top)

```bash
htop
# F9 = kill, F6 = sort, q = quit
```

### `kill` — Send a signal to a process by PID

```bash
kill 1234
kill -9 1234                     # force kill (SIGKILL)
```

### `pkill` — Kill processes by name

```bash
pkill firefox
pkill -9 nginx                   # force kill by name
```

---

## <a id="13-services"></a>13. Services [↑](#table-of-contents)

### `systemctl` — Manage systemd services

```bash
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl status nginx
sudo systemctl enable nginx      # auto-start on boot
sudo systemctl disable nginx
```

---

## <a id="14-session"></a>14. Session [↑](#table-of-contents)

### `history` — Show command history

```bash
history
history 20                       # last 20 commands
history | grep ssh               # search history
!42                              # re-run command number 42
```

### `reboot` — Restart the system

```bash
sudo reboot
```

### `shutdown` — Shut down or schedule a shutdown

```bash
sudo shutdown now
sudo shutdown -h now             # halt immediately
sudo shutdown +10                # shutdown in 10 minutes
sudo shutdown -r now             # reboot immediately
```

---

## <a id="15-extras"></a>15. Extras [↑](#table-of-contents)

### `lazydocker` — Terminal UI for managing Docker containers

```bash
curl https://raw.githubusercontent.com/jesseduffield/lazydocker/master/scripts/install_update_linux.sh | bash
```

### `nvidia-smi` — Monitor NVIDIA GPU status and usage

```bash
nvidia-smi                       # snapshot of GPU usage
nvidia-smi -l 1                  # refresh every 1 second
nvidia-smi --query-gpu=name,memory.used,memory.total --format=csv
```

### `nvtop` — Interactive GPU process monitor (like htop for GPUs)

```bash
nvtop
# q = quit, F2 = setup, supports multi-GPU
```

### `glances` — All-in-one system monitor (CPU, RAM, disk, network)

```bash
glances
glances -w                       # run as web server (port 61208)
glances --export influxdb        # export metrics
```

---

## <a id="16-git"></a>16. Git [↑](#table-of-contents)

### `git init` — Initialize a new repository

```bash
git init
git init my-project
```

### `git clone` — Clone a remote repository

```bash
git clone https://github.com/user/repo.git
git clone https://github.com/user/repo.git my-folder
```

### `git status` — Show working tree status

```bash
git status
```

### `git add` — Stage changes

```bash
git add file.txt
git add .                        # stage all changes
git add -p                       # stage interactively (chunk by chunk)
```

### `git commit` — Save staged changes

```bash
git commit -m "your message"
git commit --amend               # edit last commit
```

### `git push` — Upload commits to remote

```bash
git push
git push origin main
git push -u origin feature-branch
```

### `git pull` — Fetch and merge from remote

```bash
git pull
git pull origin main
```

### `git branch` — Manage branches

```bash
git branch                       # list branches
git branch feature-x             # create branch
git branch -d feature-x          # delete branch
```

### `git checkout` / `git switch` — Switch branches or restore files

```bash
git checkout feature-x
git checkout -b new-branch       # create and switch
git switch main                  # modern alternative
```

### `git merge` — Merge a branch into current

```bash
git merge feature-x
git merge --no-ff feature-x      # preserve merge commit
```

### `git log` — Show commit history

```bash
git log
git log --oneline --graph        # compact visual tree
git log -n 10                    # last 10 commits
```

### `git diff` — Show changes

```bash
git diff                         # unstaged changes
git diff --staged                # staged changes
git diff main..feature-x         # between branches
```

### `git stash` — Temporarily save uncommitted changes

```bash
git stash
git stash pop                    # restore last stash
git stash list                   # show all stashes
```

### `git reset` — Undo commits or unstage files

```bash
git reset HEAD file.txt          # unstage a file
git reset --soft HEAD~1          # undo last commit, keep changes staged
git reset --hard HEAD~1          # undo last commit and discard changes
```

---

## <a id="17-docker"></a>17. Docker [↑](#table-of-contents)

### `docker ps` — List running containers

```bash
docker ps
docker ps -a                     # include stopped containers
```

### `docker images` — List local images

```bash
docker images
```

### `docker pull` — Download an image

```bash
docker pull ubuntu
docker pull nginx:1.25
```

### `docker run` — Create and start a container

```bash
docker run nginx
docker run -d -p 8080:80 nginx   # detached, port mapping
docker run -it ubuntu bash       # interactive shell
docker run --name myapp -d nginx
```

### `docker exec` — Run a command in a running container

```bash
docker exec -it container_name bash
docker exec container_name ls /app
```

### `docker stop` / `docker start` — Stop or start containers

```bash
docker stop container_name
docker start container_name
docker restart container_name
```

### `docker rm` / `docker rmi` — Remove containers or images

```bash
docker rm container_name
docker rm -f container_name      # force remove running container
docker rmi image_name
```

### `docker build` — Build an image from a Dockerfile

```bash
docker build .
docker build -t myapp:1.0 .
docker build -f Dockerfile.prod -t myapp:prod .
```

### `docker logs` — View container logs

```bash
docker logs container_name
docker logs -f container_name    # follow live logs
docker logs --tail 100 container_name
```

### `docker compose` — Manage multi-container apps

```bash
docker compose up
docker compose up -d             # detached
docker compose down
docker compose logs -f
docker compose ps
```

---

## <a id="18-kubernetes"></a>18. Kubernetes [↑](#table-of-contents)

### `kubectl get` — List resources

```bash
kubectl get pods
kubectl get pods -A              # all namespaces
kubectl get svc
kubectl get deployments
kubectl get nodes
```

### `kubectl describe` — Show detailed info about a resource

```bash
kubectl describe pod my-pod
kubectl describe svc my-service
kubectl describe node my-node
```

### `kubectl apply` — Create or update resources from a file

```bash
kubectl apply -f deployment.yaml
kubectl apply -f ./k8s/          # apply all files in a directory
```

### `kubectl delete` — Delete resources

```bash
kubectl delete pod my-pod
kubectl delete -f deployment.yaml
kubectl delete pod --all
```

### `kubectl logs` — View pod logs

```bash
kubectl logs my-pod
kubectl logs -f my-pod           # follow live logs
kubectl logs my-pod -c container # specific container in pod
```

### `kubectl exec` — Run a command inside a pod

```bash
kubectl exec -it my-pod -- bash
kubectl exec my-pod -- ls /app
```

### `kubectl port-forward` — Forward a local port to a pod

```bash
kubectl port-forward my-pod 8080:80
kubectl port-forward svc/my-service 8080:80
```

### `kubectl scale` — Scale a deployment

```bash
kubectl scale deployment my-app --replicas=3
```

### `kubectl rollout` — Manage rollouts

```bash
kubectl rollout status deployment/my-app
kubectl rollout undo deployment/my-app   # rollback
kubectl rollout restart deployment/my-app
```

### `kubectl config` — Manage kubeconfig and contexts

```bash
kubectl config get-contexts
kubectl config use-context my-cluster
kubectl config current-context
```
