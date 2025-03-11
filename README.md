Katya@ubuntu:~$ export GITHUB_USERNAME=Ekaterina06-choi
Katya@ubuntu:~$ cd ${GITHUB_USERNAME}/workspace
Katya@ubuntu:~/Ekaterina06-choi/workspace$ pushd .
~/Ekaterina06-choi/workspace ~/Ekaterina06-choi/workspace
Katya@ubuntu:~/Ekaterina06-choi/workspace$ source scripts/activate
Katya@ubuntu:~/Ekaterina06-choi/workspace$ git clone https://github.com/${GITHUB_USERNAME}/lab02.git projects/lab03
Cloning into 'projects/lab03'...
remote: Enumerating objects: 25, done.
remote: Counting objects: 100% (25/25), done.
remote: Compressing objects: 100% (19/19), done.
remote: Total 25 (delta 5), reused 10 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (25/25), 6.79 KiB | 6.79 MiB/s, done.
Resolving deltas: 100% (5/5), done.
Katya@ubuntu:~/Ekaterina06-choi/workspace$ cd projects/lab03
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ git remote remove origin
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab03.git
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ g++ -std=c++11 -I./include -c sources/print.cpp
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ ls print.o
print.o
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ nm print.o
0000000000000000 T _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSo
000000000000002a T _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSt14basic_ofstreamIcS2_E
                 U _ZSt21ios_base_library_initv
0000000000000000 r _ZStL19piecewise_construct
                 U _ZStlsIcSt11char_traitsIcESaIcEERSt13basic_ostreamIT_T0_ES7_RKNSt7__cxx1112basic_stringIS4_S5_T1_EE
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ ar rvs print.a print.o
ar: creating print.a
a - print.o
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ file print.a
print.a: current ar archive
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ g++ -std=c++11 -I./include -c examples/example1.cpp
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ ls example1.o
example1.o
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ g++ example1.o print.a -o example1
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ ./example1 && echo
hello
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ g++ -std=c++11 -I./include -c examples/example2.cpp
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ nm example2.o
0000000000000000 V DW.ref.__gxx_personality_v0
                 U __gxx_personality_v0
0000000000000000 T main
                 U __stack_chk_fail
                 U _Unwind_Resume
                 U _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSt14basic_ofstreamIcS2_E
                 U _ZNSt14basic_ofstreamIcSt11char_traitsIcEEC1EPKcSt13_Ios_Openmode
                 U _ZNSt14basic_ofstreamIcSt11char_traitsIcEED1Ev
0000000000000000 W _ZNSt15__new_allocatorIcED1Ev
0000000000000000 W _ZNSt15__new_allocatorIcED2Ev
0000000000000000 n _ZNSt15__new_allocatorIcED5Ev
                 U _ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEC1EPKcRKS3_
                 U _ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEED1Ev
                 U _ZSt21ios_base_library_initv
0000000000000000 r _ZStL19piecewise_construct
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ g++ example2.o print.a -o example2
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ ./example2
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ cat log.txt && echo
hello
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ rm -rf example1.o example2.o print.o
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ rm -rf print.a
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ rm -rf example1 example2
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ rm -rf log.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ cat > CMakeLists.txt <<EOF
> cmake_minimum_required(VERSION 3.4)
project(print)
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ cat >> CMakeLists.txt <<EOF
> set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ cat >> CMakeLists.txt <<EOF
> add_library(print STATIC \${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ cat >> CMakeLists.txt <<EOF
> include_directories(\${CMAKE_CURRENT_SOURCE_DIR}/include)
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ cmake -H. -B_build
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
-- Configuring done (1.1s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/Ekaterina06-choi/workspace/projects/lab03/_build
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ cmake --build _build
[ 50%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[100%] Linking CXX static library libprint.a
[100%] Built target print
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ cat >> CMakeLists.txt <<EOF
> add_executable(example1 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example1.cpp)
add_executable(example2 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example2.cpp)
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ cat >> CMakeLists.txt <<EOF
> target_link_libraries(example1 print)
target_link_libraries(example2 print)
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ cmake --build _build
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/Ekaterina06-choi/workspace/projects/lab03/_build
[ 33%] Built target print
[ 50%] Building CXX object CMakeFiles/example1.dir/examples/example1.cpp.o
[ 66%] Linking CXX executable example1
[ 66%] Built target example1
[ 83%] Building CXX object CMakeFiles/example2.dir/examples/example2.cpp.o
[100%] Linking CXX executable example2
[100%] Built target example2
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ cmake --build _build --target print
[100%] Built target print
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ cmake --build _build --target example1
[ 50%] Built target print
[100%] Built target example1
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ cmake --build _build --target example2
[ 50%] Built target print
[100%] Built target example2
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ ls -la _build/libprint.a
-rw-rw-r-- 1 Katya Katya 2238 Mar 11 14:18 _build/libprint.a
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ _build/example1 && echo
hello
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ _build/example2
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ cat log.txt && echo
hello
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ rm -rf log.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ git clone https://github.com/tp-labs/lab03 tmp
Cloning into 'tmp'...
remote: Enumerating objects: 91, done.
remote: Counting objects: 100% (30/30), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 91 (delta 23), reused 21 (delta 21), pack-reused 61 (from 1)
Receiving objects: 100% (91/91), 1.02 MiB | 866.00 KiB/s, done.
Resolving deltas: 100% (41/41), done.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ mv -f tmp/CMakeLists.txt .
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ rm -rf tmp
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ cat CMakeLists.txt
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

option(BUILD_EXAMPLES "Build examples" OFF)

project(print)

add_library(print STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)

target_include_directories(print PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>
)

if(BUILD_EXAMPLES)
  file(GLOB EXAMPLE_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/examples/*.cpp")
  foreach(EXAMPLE_SOURCE ${EXAMPLE_SOURCES})
    get_filename_component(EXAMPLE_NAME ${EXAMPLE_SOURCE} NAME_WE)
    add_executable(${EXAMPLE_NAME} ${EXAMPLE_SOURCE})
    target_link_libraries(${EXAMPLE_NAME} print)
    install(TARGETS ${EXAMPLE_NAME}
      RUNTIME DESTINATION bin
    )
  endforeach(EXAMPLE_SOURCE ${EXAMPLE_SOURCES})
endif()

install(TARGETS print
    EXPORT print-config
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)

install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/ DESTINATION include)
install(EXPORT print-config DESTINATION cmake)
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/Ekaterina06-choi/workspace/projects/lab03/_build
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ cmake --build _build --target install
[100%] Built target print
Install the project...
-- Install configuration: ""
-- Installing: /home/Katya/Ekaterina06-choi/workspace/projects/lab03/_install/lib/libprint.a
-- Installing: /home/Katya/Ekaterina06-choi/workspace/projects/lab03/_install/include
-- Installing: /home/Katya/Ekaterina06-choi/workspace/projects/lab03/_install/include/print.hpp
-- Installing: /home/Katya/Ekaterina06-choi/workspace/projects/lab03/_install/cmake/print-config.cmake
-- Installing: /home/Katya/Ekaterina06-choi/workspace/projects/lab03/_install/cmake/print-config-noconfig.cmake
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ tree _install
_install
├── cmake
│   ├── print-config.cmake
│   └── print-config-noconfig.cmake
├── include
│   └── print.hpp
└── lib
    └── libprint.a

4 directories, 4 files
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ git add CMakeLists.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ git commit -m"added CMakeLists.txt"
[main a85238f] added CMakeLists.txt
 1 file changed, 36 insertions(+)
 create mode 100644 CMakeLists.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ git push origin main
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
To https://github.com/Ekaterina06-choi/lab03.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/Ekaterina06-choi/lab03.git'
hint: Updates were rejected because the remote contains work that you do not
hint: have locally. This is usually caused by another repository pushing to
hint: the same ref. If you want to integrate the remote changes, use
hint: 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ git pull origin main
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 1.45 KiB | 185.00 KiB/s, done.
From https://github.com/Ekaterina06-choi/lab03
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> origin/main
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint:
hint:   git config pull.rebase false  # merge
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint:
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
fatal: Need to specify how to reconcile divergent branches.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ git pull --rebase origin main
From https://github.com/Ekaterina06-choi/lab03
 * branch            main       -> FETCH_HEAD
warning: skipped previously applied commit f2a6ccf
hint: use --reapply-cherry-picks to include skipped commits
hint: Disable this message with "git config advice.skippedCherryPicks false"
Successfully rebased and updated refs/heads/main.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ git rebase --continue
fatal: no rebase in progress
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ git pull origin main
From https://github.com/Ekaterina06-choi/lab03
 * branch            main       -> FETCH_HEAD
Already up to date.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ git push origin main
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
Enumerating objects: 26, done.
Counting objects: 100% (26/26), done.
Delta compression using up to 8 threads
Compressing objects: 100% (15/15), done.
Writing objects: 100% (25/25), 4.17 KiB | 355.00 KiB/s, done.
Total 25 (delta 6), reused 16 (delta 5), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (6/6), done.
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
remote:          - commit: 9e76c07ffecc0131530f82fa7991efd7f7fb3254
remote:            path: README.md:3
remote:     
remote:        (?) To push, remove secret from commit(s) or follow this URL to allow the secret.
remote:        https://github.com/Ekaterina06-choi/lab03/security/secret-scanning/unblock-secret/2uAveXecfaYHRU11rQvbJTWdkK1
remote:     
remote: 
remote: 
To https://github.com/Ekaterina06-choi/lab03.git
 ! [remote rejected] main -> main (push declined due to repository rule violations)
error: failed to push some refs to 'https://github.com/Ekaterina06-choi/lab03.git'
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ git filter-repo --invert-paths --path <file-containing-secret>
bash: syntax error near unexpected token `newline'
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab03$ git push -f origin main
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
Enumerating objects: 26, done.
Counting objects: 100% (26/26), done.
Delta compression using up to 8 threads
Compressing objects: 100% (15/15), done.
Writing objects: 100% (25/25), 4.17 KiB | 1.04 MiB/s, done.
Total 25 (delta 6), reused 16 (delta 5), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (6/6), done.
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
remote:          - commit: 9e76c07ffecc0131530f82fa7991efd7f7fb3254
remote:            path: README.md:3
remote:     
remote:        (?) To push, remove secret from commit(s) or follow this URL to allow the secret.
remote:        https://github.com/Ekaterina06-choi/lab03/security/secret-scanning/unblock-secret/2uAveXecfaYHRU11rQvbJTWdkK1
remote:     
remote: 
remote: 
To https://github.com/Ekaterina06-choi/lab03.git
 ! [remote rejected] main -> main (push declined due to repository rule violations)
error: failed to push some refs to 'https://github.com/Ekaterina06-choi/lab03.git'

