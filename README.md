Katya@ubuntu:~$ export GITHUB_USERNAME=Ekaterina06-choi
Katya@ubuntu:~$ cd ${GITHUB_USERNAME}/workspace
Katya@ubuntu:~/Ekaterina06-choi/workspace$ pushd .
~/Ekaterina06-choi/workspace ~/Ekaterina06-choi/workspace
Katya@ubuntu:~/Ekaterina06-choi/workspace$ source scripts/activate
Katya@ubuntu:~/Ekaterina06-choi/workspace$ git clone https://github.com/${GITHUB_USERNAME}/lab07 lab08
fatal: destination path 'lab08' already exists and is not an empty directory.
Katya@ubuntu:~/Ekaterina06-choi/workspace$ git clone https://github.com/${GITHUB_USERNAME}/lab07 lab08
Cloning into 'lab08'...
remote: Enumerating objects: 277, done.
remote: Counting objects: 100% (277/277), done.
remote: Compressing objects: 100% (149/149), done.
remote: Total 277 (delta 108), reused 269 (delta 105), pack-reused 0 (from 0)
Receiving objects: 100% (277/277), 1.34 MiB | 1.00 MiB/s, done.
Resolving deltas: 100% (108/108), done.
Katya@ubuntu:~/Ekaterina06-choi/workspace$ cd lab08
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ git submodule update --init
Submodule 'third-party/gtest' (https://github.com/google/googletest) registered for path 'third-party/gtest'
Cloning into '/home/Katya/Ekaterina06-choi/workspace/lab08/third-party/gtest'...
Submodule path 'third-party/gtest': checked out '58d77fa8070e8cec2dc1ed015d66b454c8d78850'
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ git remote remove origin
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab08
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ cat > Dockerfile <<EOF
FROM ubuntu:18.04
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ cat >> Dockerfile <<EOF

RUN apt update
RUN apt install -yy gcc g++ cmake
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ cat >> Dockerfile <<EOF

COPY . print/
WORKDIR print
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ cat >> Dockerfile <<EOF

RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install
RUN cmake --build _build
RUN cmake --build _build --target install
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ cat >> Dockerfile <<EOF

ENV LOG_PATH /home/logs/log.txt
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ cat >> Dockerfile <<EOF

VOLUME /home/logs
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ cat >> Dockerfile <<EOF

WORKDIR _install/bin
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ cat >> Dockerfile <<EOF

ENTRYPOINT ./demo
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ docker build -t logger .
[+] Building 28.6s (15/15) FINISHED                              docker:default
 => [internal] load build definition from Dockerfile                       0.1s
 => => transferring dockerfile: 490B                                       0.0s
 => [internal] load metadata for docker.io/library/ubuntu:18.04            0.0s
 => [internal] load .dockerignore                                          0.1s
 => => transferring context: 2B                                            0.0s
 => [ 1/10] FROM docker.io/library/ubuntu:18.04                            0.0s
 => [internal] load build context                                          2.4s
 => => transferring context: 29.16MB                                       2.3s
 => CACHED [ 2/10] RUN apt update                                          0.0s
 => CACHED [ 3/10] RUN apt install -yy gcc g++ cmake                       0.0s
 => [ 4/10] COPY . print/                                                  0.9s
 => [ 5/10] WORKDIR print                                                  0.3s
 => [ 6/10] RUN rm -rf _build && mkdir _build && cd _build && cmake .. -D  5.4s
 => [ 7/10] RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INS  1.6s 
 => [ 8/10] RUN cmake --build _build                                       2.6s 
 => [ 9/10] RUN cmake --build _build --target install                      1.7s 
 => [10/10] WORKDIR _install/bin                                           0.7s 
 => exporting to image                                                    12.3s 
 => => exporting layers                                                   12.2s 
 => => writing image sha256:3acc22c13e00b454a4a62cb0d445b173595c24a9e3129  0.0s 
 => => naming to docker.io/library/logger                                  0.0s 
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ docker images                  
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
logger       latest    3acc22c13e00   26 seconds ago   363MB
<none>       <none>    bd8159a52901   23 hours ago     363MB
ubuntu       18.04     f9a80a55f492   23 months ago    63.2MB
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ mkdir logs
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ docker run -it -v "$(pwd)/logs/:/home/logs/" logger
text1
text2
text3
<C-D>
/bin/sh: 1: ./demo: not found
text1: command not found
text2: command not found
text3: command not found
bash: syntax error near unexpected token `newline'
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ docker run -it -v "$(pwd)/logs/:/home/logs/" logger
/bin/sh: 1: ./demo: not found
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ docker inspect logger
[
    {
        "Id": "sha256:3acc22c13e00b454a4a62cb0d445b173595c24a9e3129a74a9f668c2fcdbdebf",
        "RepoTags": [
            "logger:latest"
        ],
        "RepoDigests": [],
        "Parent": "",
        "Comment": "buildkit.dockerfile.v0",
        "Created": "2025-04-28T16:06:45.932893041Z",
        "DockerVersion": "",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "LOG_PATH=/home/logs/log.txt"
            ],
            "Cmd": null,
            "Image": "",
            "Volumes": {
                "/home/logs": {}
            },
            "WorkingDir": "/print/_install/bin",
            "Entrypoint": [
                "/bin/sh",
                "-c",
                "./demo"
            ],
            "OnBuild": null,
            "Labels": {
                "org.opencontainers.image.ref.name": "ubuntu",
                "org.opencontainers.image.version": "18.04"
            }
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 362938591,
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/nxy4x0822sh0ibggphi45tv5q/diff:/var/lib/docker/overlay2/sexq10bvrqc23tmy9ud15ajkj/diff:/var/lib/docker/overlay2/xacgjl3p42la2ixhq5ehhtm0w/diff:/var/lib/docker/overlay2/pn4i9wm4a1dzrq6wzpmtm0u0f/diff:/var/lib/docker/overlay2/i9gossneof9tofq7iowbf2gkq/diff:/var/lib/docker/overlay2/q2hobklb54jbmxen5bma5jl22/diff:/var/lib/docker/overlay2/y7zkvf85kjkjeae9jiimfs0z3/diff:/var/lib/docker/overlay2/k4wt5ia1pinn5j3med5it6yry/diff:/var/lib/docker/overlay2/8c979223a0ce8144ff4daa6d10a17d9ac46332fb864dcf0b3ce3e53497b305c1/diff",
                "MergedDir": "/var/lib/docker/overlay2/owvsjivb0ke2z9i6dp5t5mkfb/merged",
                "UpperDir": "/var/lib/docker/overlay2/owvsjivb0ke2z9i6dp5t5mkfb/diff",
                "WorkDir": "/var/lib/docker/overlay2/owvsjivb0ke2z9i6dp5t5mkfb/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:548a79621a426b4eb077c926eabac5a8620c454fb230640253e1b44dc7dd7562",
                "sha256:e16d3219a05154dde6f227aafd57e5a2b985a15628629610ee78809ace8c1464",
                "sha256:fbdfe9d4c91d7375bd8044a876c2ef8e518f559bad60074a1a0802bd85515f57",
                "sha256:eb343279e4e37ddafd75dac8ed97ce1d17fc879c5c0a54228343dcb6d604985b",
                "sha256:5f70bf18a086007016e948b04aed3b82103a36bea41755b6cddfaf10ace3c6ef",
                "sha256:c8f0d9de46953225912a9325aa7f4435f30b246365ba9717bb7708adc681e1b5",
                "sha256:ad9009e99cb5b66e163c7ee5a6b384f0b7df0b8e83fd94180a621e97b1633014",
                "sha256:98a421cc0164d83268234fae77cacc9bc7623018d9018000457ea76f852c7ef1",
                "sha256:bd4a404fa6b70fb4a410f90d2a351951fc208d23e2e0121cfb6e7cda143b5353",
                "sha256:21d92e974111a449d8bb39b2ab364c105119517348f324fe05babfe64bbe64ff"
            ]
        },
        "Metadata": {
            "LastTagTime": "2025-04-28T16:06:58.235815067Z"
        }
    }
]
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ cat logs/log.txt
cat: logs/log.txt: No such file or directory
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ mkdir -p logs
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ touch logs/log.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ cat logs/log.txt
text1
text2
text3
<C-D>
text1: command not found
text2: command not found
text3: command not found
bash: syntax error near unexpected token `newline'
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ cat logs/log.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ docker run -it -v "$(pwd)/logs/:/home/logs/" logger
/bin/sh: 1: ./demo: not found
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ docker run -it -v "$(pwd)/logs/:/home/logs/" logger
/bin/sh: 1: ./demo: not found
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ mkdir -p logs
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ touch logs/log.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ cat logs/log.txt
text1
text2
text3
<C-D>
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ gsed -i 's/lab07/lab08/g' README.md
Command 'gsed' not found, did you mean:
  command 'msed' from deb mblaze (1.1-1)
  command 'gsd' from deb python3-gsd (3.3.0-1)
  command 'gted' from deb gnome-text-editor (47.0-1ubuntu2)
  command 'ssed' from deb ssed (3.62-8)
  command 'gsnd' from deb ghostscript (10.03.1~dfsg1-0ubuntu2.2)
  command 'sed' from deb sed (4.9-2build1)
  command 'gsec' from deb firebird3.0-utils (3.0.11.33703.ds4-2ubuntu2)
  command 'gsad' from deb gsad (22.8.0-1build2)
Try: sudo apt install <deb name>
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ sed -i 's/lab07/lab08/g' README.md
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ vim .travis.yml
Command 'vim' not found, but can be installed with:
sudo apt install vim        # version 2:9.1.0496-1ubuntu6.4, or
sudo apt install vim-gtk3   # version 2:9.1.0496-1ubuntu6.4
sudo apt install vim-motif  # version 2:9.1.0496-1ubuntu6.4
sudo apt install vim-nox    # version 2:9.1.0496-1ubuntu6.4
sudo apt install neovim     # version 0.9.5-7
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ sudo apt install vim
[sudo] password for Katya: 
Installing:                     
  vim

Installing dependencies:
  libsodium23  vim-runtime

Suggested packages:
  ctags  vim-doc  vim-scripts

Summary:
  Upgrading: 0, Installing: 3, Removing: 0, Not Upgrading: 4
  Download size: 9,424 kB
  Space needed: 42.7 MB / 78.4 GB available

Continue? [Y/n] Y
Get:1 http://ru.archive.ubuntu.com/ubuntu oracular/main amd64 libsodium23 amd64 1.0.18-1build3 [161 kB]
Get:2 http://ru.archive.ubuntu.com/ubuntu oracular-updates/main amd64 vim-runtime all 2:9.1.0496-1ubuntu6.5 [7,322 kB]
Get:3 http://ru.archive.ubuntu.com/ubuntu oracular-updates/main amd64 vim amd64 2:9.1.0496-1ubuntu6.5 [1,941 kB]
Fetched 9,424 kB in 3s (2,736 kB/s)
Selecting previously unselected package libsodium23:amd64.
(Reading database ... 204213 files and directories currently installed.)
Preparing to unpack .../libsodium23_1.0.18-1build3_amd64.deb ...
Unpacking libsodium23:amd64 (1.0.18-1build3) ...
Selecting previously unselected package vim-runtime.
Preparing to unpack .../vim-runtime_2%3a9.1.0496-1ubuntu6.5_all.deb ...
Adding 'diversion of /usr/share/vim/vim91/doc/help.txt to /usr/share/vim/vim91/d
oc/help.txt.vim-tiny by vim-runtime'
Adding 'diversion of /usr/share/vim/vim91/doc/tags to /usr/share/vim/vim91/doc/t
ags.vim-tiny by vim-runtime'
Unpacking vim-runtime (2:9.1.0496-1ubuntu6.5) ...
Selecting previously unselected package vim.
Preparing to unpack .../vim_2%3a9.1.0496-1ubuntu6.5_amd64.deb ...
Unpacking vim (2:9.1.0496-1ubuntu6.5) ...
Setting up libsodium23:amd64 (1.0.18-1build3) ...
Setting up vim-runtime (2:9.1.0496-1ubuntu6.5) ...
Setting up vim (2:9.1.0496-1ubuntu6.5) ...
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/ex (ex) in aut
o mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/rview (rview) 
in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/rvim (rvim) in
 auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vi (vi) in aut
o mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/view (view) in
 auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vim (vim) in a
uto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vimdiff (vimdi
ff) in auto mode
Processing triggers for man-db (2.12.1-3) ...
Processing triggers for libc-bin (2.40-1ubuntu3.1) ...
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ vim .travis.yml
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ git add Dockerfile
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ git add .travis.yml
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ git commit -m"adding Dockerfile"
[main 6a346de] adding Dockerfile
 1 file changed, 13 insertions(+)
 create mode 100644 Dockerfile
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ git push origin main
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
Enumerating objects: 280, done.
Counting objects: 100% (280/280), done.
Delta compression using up to 8 threads
Compressing objects: 100% (149/149), done.
Writing objects: 100% (280/280), 1.34 MiB | 12.86 MiB/s, done.
Total 280 (delta 109), reused 276 (delta 108), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (109/109), done.
remote: error: GH013: Repository rule violations found for refs/heads/main.
remote: 
remote: - GITHUB PUSH PROTECTION
remote:   —————————————————————————————————————————
remote:     Resolve the following violations before pushing again
remote: 
remote:     - Push cannot contain secrets
remote: 
remote:     
remote:      (?) Learn how to resolve a blocked push
remote:      https://docs.github.com/code-security/secret-scanning/working-with-secret-scanning-and-push-protection/working-with-push-protection-from-the-command-line#resolving-a-blocked-push
remote:     
remote:     
remote:       —— GitHub Personal Access Token ——————————————————————
remote:        locations:
remote:          - commit: 551d65ee097ceb8451ffc90c7355e7ef8cdb1a5d
remote:            path: README.md:2
remote:     
remote:        (?) To push, remove secret from commit(s) or follow this URL to allow the secret.
remote:        https://github.com/Ekaterina06-choi/lab08/security/secret-scanning/unblock-secret/2wMiLfO4WeFljsO84YbwUnD5iUK
remote:     
remote:     
remote:       —— GitHub Personal Access Token ——————————————————————
remote:        locations:
remote:          - commit: 1be8e0a6ff5d024f282bad2c4677b0cd4ff72915
remote:            path: lab03/README.md:3
remote:     
remote:        (?) To push, remove secret from commit(s) or follow this URL to allow the secret.
remote:        https://github.com/Ekaterina06-choi/lab08/security/secret-scanning/unblock-secret/2wMiLezoHi4o1dFhpecIw2f8Ixo
remote:     
remote: 
remote: 
To https://github.com/Ekaterina06-choi/lab08
 ! [remote rejected] main -> main (push declined due to repository rule violations)
error: failed to push some refs to 'https://github.com/Ekaterina06-choi/lab08'
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ git push origin main
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
Enumerating objects: 280, done.
Counting objects: 100% (280/280), done.
Delta compression using up to 8 threads
Compressing objects: 100% (149/149), done.
Writing objects: 100% (280/280), 1.34 MiB | 52.94 MiB/s, done.
Total 280 (delta 109), reused 276 (delta 108), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (109/109), done.
remote: error: GH013: Repository rule violations found for refs/heads/main.
remote: 
remote: - GITHUB PUSH PROTECTION
remote:   —————————————————————————————————————————
remote:     Resolve the following violations before pushing again
remote: 
remote:     - Push cannot contain secrets
remote: 
remote:     
remote:      (?) Learn how to resolve a blocked push
remote:      https://docs.github.com/code-security/secret-scanning/working-with-secret-scanning-and-push-protection/working-with-push-protection-from-the-command-line#resolving-a-blocked-push
remote:     
remote:     
remote:       —— GitHub Personal Access Token ——————————————————————
remote:        locations:
remote:          - commit: 551d65ee097ceb8451ffc90c7355e7ef8cdb1a5d
remote:            path: README.md:2
remote:     
remote:        (?) To push, remove secret from commit(s) or follow this URL to allow the secret.
remote:        https://github.com/Ekaterina06-choi/lab08/security/secret-scanning/unblock-secret/2wMiLfO4WeFljsO84YbwUnD5iUK
remote:     
remote: 
remote: 
To https://github.com/Ekaterina06-choi/lab08
 ! [remote rejected] main -> main (push declined due to repository rule violations)
error: failed to push some refs to 'https://github.com/Ekaterina06-choi/lab08'
Katya@ubuntu:~/Ekaterina06-choi/workspace/lab08$ git push origin main
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
Enumerating objects: 280, done.
Counting objects: 100% (280/280), done.
Delta compression using up to 8 threads
Compressing objects: 100% (149/149), done.
Writing objects: 100% (280/280), 1.34 MiB | 19.12 MiB/s, done.
Total 280 (delta 109), reused 276 (delta 108), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (109/109), done.
To https://github.com/Ekaterina06-choi/lab08
 * [new branch]      main -> main
