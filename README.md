Katya@ubuntu:~$ export GITHUB_USERNAME=Ekaterina06-choi
Katya@ubuntu:~$ export GITHUB_EMAIL=ekaterina.tsoy.2006@gmail.com
Katya@ubuntu:~$ export GITHUB_TOKEN=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
Katya@ubuntu:~$ alias edit=nano
Katya@ubuntu:~$ cd ${GITHUB_USERNAME}/workspace
Katya@ubuntu:~/Ekaterina06-choi/workspace$ source scripts/activate
Katya@ubuntu:~/Ekaterina06-choi/workspace$ mkdir ~/.config
mkdir: cannot create directory ‘/home/Katya/.config’: File exists
Katya@ubuntu:~/Ekaterina06-choi/workspace$ cat > ~/.config/hub <<EOF
> github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace$ git config --global hub.protocol https
Katya@ubuntu:~/Ekaterina06-choi/workspace$ mkdir projects/lab02 && cd projects/lab02
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ git init
Initialized empty Git repository in /home/Katya/Ekaterina06-choi/workspace/projects/lab02/.git/
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ git config --global user.name ${GITHUB_USERNAME}
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ git config --global user.email ${GITHUB_EMAIL}
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ git config -e --global
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ git pull origin main
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 1.45 KiB | 370.00 KiB/s, done.
From https://github.com/Ekaterina06-choi/lab02
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> origin/main
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ touch README.md
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	README.md

nothing added to commit but untracked files present (use "git add" to track)
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ git add README.md
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ git commit -m"added README.md"
[main 63b43b0] added README.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ git push origin main
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 294 bytes | 294.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/Ekaterina06-choi/lab02.git
   f2a6ccf..63b43b0  main -> main
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ git pull origin main
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 997 bytes | 997.00 KiB/s, done.
From https://github.com/Ekaterina06-choi/lab02
 * branch            main       -> FETCH_HEAD
   63b43b0..0bbcda0  main       -> origin/main
Updating 63b43b0..0bbcda0
Fast-forward
 file.gitignore | 4 ++++
 1 file changed, 4 insertions(+)
 create mode 100644 file.gitignore
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ git log
commit 0bbcda0d815116df29e13bc7948beb0e4de6bee2 (HEAD -> main, origin/main)
Author: Ekaterina06-choi <ekaterina.tsoy.2006@gmail.com>
Date:   Mon Mar 10 18:43:35 2025 +0300

    Create file.gitignore

commit 63b43b0cd9b31ee603e881d26b639a73a700bac0
Author: Ekaterina06-choi <ekaterina.tsoy.2006@gmail.com>
Date:   Mon Mar 10 15:41:19 2025 +0000

    added README.md

commit f2a6ccf65e4fb93ad5903121ee8c27c8b3529762
Author: Ekaterina06-choi <ekaterina.tsoy.2006@gmail.com>
Date:   Mon Mar 10 18:32:59 2025 +0300

    Initial commit
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ mkdir sources
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ mkdir include
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ mkdir examples
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ cat > sources/print.cpp <<EOF
> #include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ $ cat > include/print.hpp <<EOF
> #include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
$: command not found
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ cat > include/print.hpp <<EOF
> > #include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ cat > examples/example1.cpp <<EOF
> #include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ cat > examples/example2.cpp <<EOF
> #include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ edit README.md
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	examples/
	include/
	sources/

nothing added to commit but untracked files present (use "git add" to track)
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ git add .
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ git commit -m"added sources"
[main 9200f2a] added sources
 4 files changed, 32 insertions(+)
 create mode 100644 examples/example1.cpp
 create mode 100644 examples/example2.cpp
 create mode 100644 include/print.hpp
 create mode 100644 sources/print.cpp
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ git push origin main
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
Delta compression using up to 8 threads
Compressing objects: 100% (7/7), done.
Writing objects: 100% (9/9), 978 bytes | 88.00 KiB/s, done.
Total 9 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/Ekaterina06-choi/lab02.git
   0bbcda0..9200f2a  main -> main
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab02$ 

