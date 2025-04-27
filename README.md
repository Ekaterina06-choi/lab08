Katya@ubuntu:~$ export GITHUB_USERNAME=Ekaterina06-choi
Katya@ubuntu:~$ eport GITHUB_EMAIL=ekaterina.tsoy.2006@gmail.com
Command 'eport' not found, did you mean:
  command 'port' from snap port (1.10.0)
  command 'epost' from deb ncbi-entrez-direct (19.2.20230331+dfsg-3)
See 'snap info <snapname>' for additional versions.
Katya@ubuntu:~$ export GITHUB_EMAIL=ekaterina.tsoy.2006@gmail.com
Katya@ubuntu:~$ alias edit=nano
Katya@ubuntu:~$ alias gsed=sed
Katya@ubuntu:~$ cd ${GITHUB_USERNAME}/workspace
Katya@ubuntu:~/Ekaterina06-choi/workspace$ pushd .
~/Ekaterina06-choi/workspace ~/Ekaterina06-choi/workspace
Katya@ubuntu:~/Ekaterina06-choi/workspace$ source scripts/activate
Katya@ubuntu:~/Ekaterina06-choi/workspace$ git clone https://github.com/${GITHUB_USERNAME}/lab05 projects/lab06
Cloning into 'projects/lab06'...
remote: Enumerating objects: 261, done.
remote: Counting objects: 100% (261/261), done.
remote: Compressing objects: 100% (155/155), done.
remote: Total 261 (delta 100), reused 236 (delta 84), pack-reused 0 (from 0)
Receiving objects: 100% (261/261), 1.31 MiB | 947.00 KiB/s, done.
Resolving deltas: 100% (100/100), done.
Katya@ubuntu:~/Ekaterina06-choi/workspace$ cd projects/lab06
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ git remote remove origin
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab06
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ gsed -i '/project(print)/a\
set(PRINT_VERSION_STRING "v\${PRINT_VERSION}")
' CMakeLists.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ gsed -i '/project(print)/a\
set(PRINT_VERSION\
  \${PRINT_VERSION_MAJOR}.\${PRINT_VERSION_MINOR}.\${PRINT_VERSION_PATCH}.\${PRINT_VERSION_TWEAK})
' CMakeLists.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ gsed -i '/project(print)/a\
set(PRINT_VERSION_TWEAK 0)
' CMakeLists.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ gsed -i '/project(print)/a\
set(PRINT_VERSION_PATCH 0)
' CMakeLists.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ gsed -i '/project(print)/a\
set(PRINT_VERSION_MINOR 1)
' CMakeLists.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ gsed -i '/project(print)/a\
set(PRINT_VERSION_MAJOR 0)
' CMakeLists.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ git diff
diff --git a/CMakeLists.txt b/CMakeLists.txt
index 97f051c..39c06f3 100644
--- a/CMakeLists.txt
+++ b/CMakeLists.txt
@@ -7,6 +7,13 @@ option(BUILD_EXAMPLES "Build examples" OFF)
 option(BUILD_TESTS "Build tests" OFF)
 
 project(print)
+set(PRINT_VERSION_MAJOR 0)
+set(PRINT_VERSION_MINOR 1)
+set(PRINT_VERSION_PATCH 0)
+set(PRINT_VERSION_TWEAK 0)
+set(PRINT_VERSION
+  ${PRINT_VERSION_MAJOR}.${PRINT_VERSION_MINOR}.${PRINT_VERSION_PATCH}.${PRINT_VERSION_TWEAK})
+set(PRINT_VERSION_STRING "v${PRINT_VERSION}")
 
 add_library(print STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
 
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ touch DESCRIPTION && edit DESCRIPTION
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ touch ChangeLog.md
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ export DATE="`LANG=en_US date +'%a %b %d %Y'`"
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ cat > ChangeLog.md <<EOF
> * ${DATE} ${GITHUB_USERNAME} <${GITHUB_EMAIL}> 0.1.0.0
- Initial RPM release
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$  cat > CPackConfig.cmake <<EOF
include(InstallRequiredSystemLibraries)
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ cat >> CPackConfig.cmake <<EOF
set(CPACK_PACKAGE_CONTACT ${GITHUB_EMAIL})
set(CPACK_PACKAGE_VERSION_MAJOR \${PRINT_VERSION_MAJOR})
set(CPACK_PACKAGE_VERSION_MINOR \${PRINT_VERSION_MINOR})
set(CPACK_PACKAGE_VERSION_PATCH \${PRINT_VERSION_PATCH})
set(CPACK_PACKAGE_VERSION_TWEAK \${PRINT_VERSION_TWEAK})
set(CPACK_PACKAGE_VERSION \${PRINT_VERSION})
set(CPACK_PACKAGE_DESCRIPTION_FILE \${CMAKE_CURRENT_SOURCE_DIR}/DESCRIPTION)
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "static C++ library for printing")
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ cat >> CPackConfig.cmake <<EOF

set(CPACK_RESOURCE_FILE_LICENSE \${CMAKE_CURRENT_SOURCE_DIR}/LICENSE)
set(CPACK_RESOURCE_FILE_README \${CMAKE_CURRENT_SOURCE_DIR}/README.md)
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ cat >> CPackConfig.cmake <<EOF

set(CPACK_RPM_PACKAGE_NAME "print-devel")
set(CPACK_RPM_PACKAGE_LICENSE "MIT")
set(CPACK_RPM_PACKAGE_GROUP "print")
set(CPACK_RPM_CHANGELOG_FILE \${CMAKE_CURRENT_SOURCE_DIR}/ChangeLog.md)
set(CPACK_RPM_PACKAGE_RELEASE 1)
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ cat >> CPackConfig.cmake <<EOF

set(CPACK_DEBIAN_PACKAGE_NAME "libprint-dev")
set(CPACK_DEBIAN_PACKAGE_PREDEPENDS "cmake >= 3.0")
set(CPACK_DEBIAN_PACKAGE_RELEASE 1)
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ cat >> CPackConfig.cmake <<EOF

include(CPack)
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ cat >> CMakeLists.txt <<EOF

include(CPackConfig.cmake)
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ gsed -i 's/lab05/lab06/g' README.md
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ git add .
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ git commit -"added cpack config"
error: unknown switch `d'
usage: git commit [-a | --interactive | --patch] [-s] [-v] [-u<mode>] [--amend]
                  [--dry-run] [(-c | -C | --squash) <commit> | --fixup [(amend|reword):]<commit>)]
                  [-F <file> | -m <msg>] [--reset-author] [--allow-empty]
                  [--allow-empty-message] [--no-verify] [-e] [--author=<author>]
                  [--date=<date>] [--cleanup=<mode>] [--[no-]status]
                  [-i | -o] [--pathspec-from-file=<file> [--pathspec-file-nul]]
                  [(--trailer <token>[(=|:)<value>])...] [-S[<keyid>]]
                  [--] [<pathspec>...]

    -q, --[no-]quiet      suppress summary after successful commit
    -v, --[no-]verbose    show diff in commit message template

Commit message options
    -F, --[no-]file <file>
                          read message from file
    --[no-]author <author>
                          override author for commit
    --[no-]date <date>    override date for commit
    -m, --[no-]message <message>
                          commit message
    -c, --[no-]reedit-message <commit>
                          reuse and edit message from specified commit
    -C, --[no-]reuse-message <commit>
                          reuse message from specified commit
    --[no-]fixup [(amend|reword):]commit
                          use autosquash formatted message to fixup or amend/reword specified commit
    --[no-]squash <commit>
                          use autosquash formatted message to squash specified commit
    --[no-]reset-author   the commit is authored by me now (used with -C/-c/--amend)
    --trailer <trailer>   add custom trailer(s)
    -s, --[no-]signoff    add a Signed-off-by trailer
    -t, --[no-]template <file>
                          use specified template file
    -e, --[no-]edit       force edit of commit
    --[no-]cleanup <mode> how to strip spaces and #comments from message
    --[no-]status         include status in commit message template
    -S, --[no-]gpg-sign[=<key-id>]
                          GPG sign commit

Commit contents options
    -a, --[no-]all        commit all changed files
    -i, --[no-]include    add specified files to index for commit
    --[no-]interactive    interactively add files
    -p, --[no-]patch      interactively add changes
    -o, --[no-]only       commit only specified files
    -n, --no-verify       bypass pre-commit and commit-msg hooks
    --verify              opposite of --no-verify
    --[no-]dry-run        show what would be committed
    --[no-]short          show status concisely
    --[no-]branch         show branch information
    --[no-]ahead-behind   compute full ahead/behind values
    --[no-]porcelain      machine-readable output
    --[no-]long           show status in long format (default)
    -z, --[no-]null       terminate entries with NUL
    --[no-]amend          amend previous commit
    --no-post-rewrite     bypass post-rewrite hook
    --post-rewrite        opposite of --no-post-rewrite
    -u, --[no-]untracked-files[=<mode>]
                          show untracked files, optional modes: all, normal, no. (Default: all)
    --[no-]pathspec-from-file <file>
                          read pathspec from file
    --[no-]pathspec-file-nul
                          with --pathspec-from-file, pathspec elements are separated with NUL character

Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ git commit -m"added cpack config"
[main a81a31e] added cpack config
 5 files changed, 145 insertions(+), 110 deletions(-)
 create mode 100644 CPackConfig.cmake
 create mode 100644 ChangeLog.md
 create mode 100644 DESCRIPTION
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ git tag v0.1.0.0
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ git push origin main --tags
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
remote: Repository not found.
fatal: repository 'https://github.com/Ekaterina06-choi/lab06/' not found
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ it push origin main --tags
it: command not found
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ git push origin main --tags
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
Enumerating objects: 268, done.
Counting objects: 100% (268/268), done.
Delta compression using up to 8 threads
Compressing objects: 100% (145/145), done.
Writing objects: 100% (268/268), 1.31 MiB | 18.42 MiB/s, done.
Total 268 (delta 103), reused 258 (delta 100), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (103/103), done.
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
remote:        https://github.com/Ekaterina06-choi/lab06/security/secret-scanning/unblock-secret/2wIyDOmURyI48p7g1RXpOvKclMf
remote:     
remote:     
remote:       —— GitHub Personal Access Token ——————————————————————
remote:        locations:
remote:          - commit: 1be8e0a6ff5d024f282bad2c4677b0cd4ff72915
remote:            path: lab03/README.md:3
remote:     
remote:        (?) To push, remove secret from commit(s) or follow this URL to allow the secret.
remote:        https://github.com/Ekaterina06-choi/lab06/security/secret-scanning/unblock-secret/2wIyDNPjFq6a1PaE5L4rss9oowr
remote:     
remote: 
remote: 
remote: error: GH013: Repository rule violations found for refs/tags/v0.1.0.0.
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
remote:        https://github.com/Ekaterina06-choi/lab06/security/secret-scanning/unblock-secret/2wIyDOmURyI48p7g1RXpOvKclMf
remote:     
remote:     
remote:       —— GitHub Personal Access Token ——————————————————————
remote:        locations:
remote:          - commit: 1be8e0a6ff5d024f282bad2c4677b0cd4ff72915
remote:            path: lab03/README.md:3
remote:     
remote:        (?) To push, remove secret from commit(s) or follow this URL to allow the secret.
remote:        https://github.com/Ekaterina06-choi/lab06/security/secret-scanning/unblock-secret/2wIyDNPjFq6a1PaE5L4rss9oowr
remote:     
remote: 
remote: 
To https://github.com/Ekaterina06-choi/lab06
 ! [remote rejected] main -> main (push declined due to repository rule violations)
 ! [remote rejected] v0.1.0.0 -> v0.1.0.0 (push declined due to repository rule violations)
error: failed to push some refs to 'https://github.com/Ekaterina06-choi/lab06'
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ git push origin master --tags
error: src refspec master does not match any
error: failed to push some refs to 'https://github.com/Ekaterina06-choi/lab06'
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ git push origin main --tags
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
Enumerating objects: 268, done.
Counting objects: 100% (268/268), done.
Delta compression using up to 8 threads
Compressing objects: 100% (145/145), done.
Writing objects: 100% (268/268), 1.31 MiB | 9.08 MiB/s, done.
Total 268 (delta 103), reused 258 (delta 100), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (103/103), done.
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
remote:          - commit: 1be8e0a6ff5d024f282bad2c4677b0cd4ff72915
remote:            path: lab03/README.md:3
remote:     
remote:        (?) To push, remove secret from commit(s) or follow this URL to allow the secret.
remote:        https://github.com/Ekaterina06-choi/lab06/security/secret-scanning/unblock-secret/2wIyDNPjFq6a1PaE5L4rss9oowr
remote:     
remote: 
remote: 
remote: error: GH013: Repository rule violations found for refs/tags/v0.1.0.0.
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
remote:          - commit: 1be8e0a6ff5d024f282bad2c4677b0cd4ff72915
remote:            path: lab03/README.md:3
remote:     
remote:        (?) To push, remove secret from commit(s) or follow this URL to allow the secret.
remote:        https://github.com/Ekaterina06-choi/lab06/security/secret-scanning/unblock-secret/2wIyDNPjFq6a1PaE5L4rss9oowr
remote:     
remote: 
remote: 
To https://github.com/Ekaterina06-choi/lab06
 ! [remote rejected] main -> main (push declined due to repository rule violations)
 ! [remote rejected] v0.1.0.0 -> v0.1.0.0 (push declined due to repository rule violations)
error: failed to push some refs to 'https://github.com/Ekaterina06-choi/lab06'
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ git push origin main --tags
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
Enumerating objects: 268, done.
Counting objects: 100% (268/268), done.
Delta compression using up to 8 threads
Compressing objects: 100% (145/145), done.
Writing objects: 100% (268/268), 1.31 MiB | 7.73 MiB/s, done.
Total 268 (delta 103), reused 258 (delta 100), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (103/103), done.
To https://github.com/Ekaterina06-choi/lab06
 * [new branch]      main -> main
 * [new tag]         v0.1.0.0 -> v0.1.0.0
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ cmake -H. -B_build
CMake Error: The current CMakeCache.txt directory /home/Katya/Ekaterina06-choi/workspace/projects/lab06/_build/CMakeCache.txt is different than the directory /home/Katya/Ekaterina06-choi/workspace/projects/lab05/_build where CMakeCache.txt was created. This may result in binaries being created in the wrong place. If you are not sure, reedit the CMakeCache.txt
CMake Error: The source "/home/Katya/Ekaterina06-choi/workspace/projects/lab06/CMakeLists.txt" does not match the source "/home/Katya/Ekaterina06-choi/workspace/projects/lab05/CMakeLists.txt" used to generate cache.  Re-run cmake with a different source directory.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ rm -rf _build
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ mkdir _build && cd _build
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06/_build$ cmake -H. -B_build
CMake Error: The source directory "/home/Katya/Ekaterina06-choi/workspace/projects/lab06/_build" does not appear to contain CMakeLists.txt.
Specify --help for usage, or press the help button on the CMake GUI.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06/_build$ cd ..
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ cmake -H. -B_build
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- The C compiler identification is GNU 14.2.0
-- The CXX compiler identification is GNU 14.2.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done (2.3s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/Ekaterina06-choi/workspace/projects/lab06/_build
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ cmake --build _build
[ 50%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[100%] Linking CXX static library libprint.a
[100%] Built target print
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ cd _build
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06/_build$ cpack -G "TGZ"
CPack: Create package using TGZ
CPack: Install projects
CPack: - Run preinstall target for: print
CPack: - Install project: print []
CPack: Create package
CPack: - package: /home/Katya/Ekaterina06-choi/workspace/projects/lab06/_build/print-0.1.0.0-Linux.tar.gz generated.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06/_build$ cd ..
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ cmake -H. -B_build -DCPACK_GENERATOR="TGZ"
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/Ekaterina06-choi/workspace/projects/lab06/_build
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ cmake --build _build --target package
[100%] Built target print
Run CPack packaging tool...
CPack: Create package using TGZ
CPack: Install projects
CPack: - Run preinstall target for: print
CPack: - Install project: print []
CPack: Create package
CPack: - package: /home/Katya/Ekaterina06-choi/workspace/projects/lab06/_build/print-0.1.0.0-Linux.tar.gz generated.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ mkdir artifacts
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ mv _build/*.tar.gz artifacts
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab06$ tree artifacts
artifacts
└── print-0.1.0.0-Linux.tar.gz

1 directory, 1 file
