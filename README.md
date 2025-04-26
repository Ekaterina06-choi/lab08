Katya@ubuntu:~$ export GITHUB_USERNAME=Ekaterina06-choi
Katya@ubuntu:~$ alias gsed=sed
Katya@ubuntu:~$ cd ${GITHUB_USERNAME}/workspace
Katya@ubuntu:~/Ekaterina06-choi/workspace$ pushd .
~/Ekaterina06-choi/workspace ~/Ekaterina06-choi/workspace
Katya@ubuntu:~/Ekaterina06-choi/workspace$ source scripts/activate
Katya@ubuntu:~/Ekaterina06-choi/workspace$ git clone https://github.com/${GITHUB_USERNAME}/lab04 projects/lab05
Cloning into 'projects/lab05'...
remote: Enumerating objects: 105, done.
remote: Counting objects: 100% (105/105), done.
remote: Compressing objects: 100% (75/75), done.
remote: Total 105 (delta 24), reused 98 (delta 21), pack-reused 0 (from 0)
Receiving objects: 100% (105/105), 70.82 KiB | 833.00 KiB/s, done.
Resolving deltas: 100% (24/24), done.
Katya@ubuntu:~/Ekaterina06-choi/workspace$ cd projects/lab05
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git remote remove origin
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab05
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ cat > .travis.yml <<EOF
> language: cpp
EOF
marialuneva@1511:~/marlinez/workspace/projects/lab05$ cat >> .travis.yml <<EOF
> script:
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build
- cmake --build _build --target install
EOF
bash: marialuneva@1511:~/marlinez/workspace/projects/lab05$: No such file or directory
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ cat > .travis.yml <<EOF
> language: cpp
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ cat >> .travis.yml <<EOF
> script:
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build
- cmake --build _build --target install
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ cat >> .travis.yml <<EOF
> addons:
  apt:
    sources:
      - george-edison55-precise-backports
    packages:
      - cmake
      - cmake-data
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ mkdir third-party
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git submodule add https://github.com/google/googletest third-party/gtest
Cloning into '/home/Katya/Ekaterina06-choi/workspace/projects/lab05/third-party/gtest'...
remote: Enumerating objects: 28002, done.
remote: Counting objects: 100% (239/239), done.
remote: Compressing objects: 100% (153/153), done.
remote: Total 28002 (delta 149), reused 88 (delta 85), pack-reused 27763 (from 4)
Receiving objects: 100% (28002/28002), 13.51 MiB | 868.00 KiB/s, done.
Resolving deltas: 100% (20752/20752), done.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ cd third-party/gtest && git checkout release-1.12.1 && cd ../..
Note: switching to 'release-1.12.1'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 58d77fa8 Updates the version number in CMakeLists.txt to 1.12.1 (#3919)
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git switch -c new-branch
Switched to a new branch 'new-branch'
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git add third-party/gtest
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git commit -m"added gtest framework"
[new-branch 5488d14] added gtest framework
 2 files changed, 4 insertions(+)
 create mode 100644 .gitmodules
 create mode 160000 third-party/gtest
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ gsed -i '/option(BUILD_EXAMPLES "Build examples" OFF)/a\
option(BUILD_TESTS "Build tests" OFF)
' CMakeLists.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ cat >> CMakeLists.txt <<EOF

if(BUILD_TESTS)
  enable_testing()
  add_subdirectory(third-party/gtest)
  file(GLOB \${PROJECT_NAME}_TEST_SOURCES tests/*.cpp)
  add_executable(check \${\${PROJECT_NAME}_TEST_SOURCES})
  target_link_libraries(check \${PROJECT_NAME} gtest_main)
  add_test(NAME check COMMAND check)
endif()
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ mkdir tests
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ cat > tests/test1.cpp <<EOF
#include <print.hpp>

#include <gtest/gtest.h>

TEST(Print, InFileStream)
{
  std::string filepath = "file.txt";
  std::string text = "hello";
  std::ofstream out{filepath};

  print(text, out);
  out.close();

  std::string result;
  std::ifstream in{filepath};
  in >> result;

  EXPECT_EQ(result, text);
}
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ cmake -H. -B_build -DBUILD_TESTS=ON
CMake Error: The current CMakeCache.txt directory /home/Katya/Ekaterina06-choi/workspace/projects/lab05/_build/CMakeCache.txt is different than the directory /home/Katya/Ekaterina06-choi/workspace/projects/lab03/_build where CMakeCache.txt was created. This may result in binaries being created in the wrong place. If you are not sure, reedit the CMakeCache.txt
CMake Error: The source "/home/Katya/Ekaterina06-choi/workspace/projects/lab05/CMakeLists.txt" does not match the source "/home/Katya/Ekaterina06-choi/workspace/projects/lab03/CMakeLists.txt" used to generate cache.  Re-run cmake with a different source directory.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ rm -rf _build
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ mkdir _build
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ cd _build
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05/_build$ cmake -H. -B_build -DBUILD_TESTS=ON
CMake Error: The source directory "/home/Katya/Ekaterina06-choi/workspace/projects/lab05/_build" does not appear to contain CMakeLists.txt.
Specify --help for usage, or press the help button on the CMake GUI.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05/_build$ cmake .. -DBUILD_TESTS=ON
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
-- Found Python: /usr/bin/python3 (found version "3.12.7") found components: Interpreter
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Configuring done (1.5s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/Ekaterina06-choi/workspace/projects/lab05/_build
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05/_build$ cmake -H. -B_build -DBUILD_TESTS=ON
CMake Error: The source directory "/home/Katya/Ekaterina06-choi/workspace/projects/lab05/_build" does not appear to contain CMakeLists.txt.
Specify --help for usage, or press the help button on the CMake GUI.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05/_build$ find . -name CMakeCache.txt -delete
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05/_build$ find . -name CMakeFiles -exec rm -rf {} +
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05/_build$ cmake -H. -B_build -DBUILD_TESTS=ON
CMake Error: The source directory "/home/Katya/Ekaterina06-choi/workspace/projects/lab05/_build" does not appear to contain CMakeLists.txt.
Specify --help for usage, or press the help button on the CMake GUI.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05/_build$ cd ..
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ cmake -H. -B_build -DBUILD_TESTS=ON
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
-- Found Python: /usr/bin/python3 (found version "3.12.7") found components: Interpreter
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Configuring done (0.9s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/Ekaterina06-choi/workspace/projects/lab05/_build
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ cmake --build _build
[  8%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 16%] Linking CXX static library libprint.a
[ 16%] Built target print
[ 25%] Building CXX object third-party/gtest/googletest/CMakeFiles/gtest.dir/src/gtest-all.cc.o
[ 33%] Linking CXX static library ../../../lib/libgtest.a
[ 33%] Built target gtest
[ 41%] Building CXX object third-party/gtest/googletest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
[ 50%] Linking CXX static library ../../../lib/libgtest_main.a
[ 50%] Built target gtest_main
[ 58%] Building CXX object CMakeFiles/check.dir/tests/test1.cpp.o
[ 66%] Linking CXX executable check
[ 66%] Built target check
[ 75%] Building CXX object third-party/gtest/googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o
[ 83%] Linking CXX static library ../../../lib/libgmock.a
[ 83%] Built target gmock
[ 91%] Building CXX object third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o
[100%] Linking CXX static library ../../../lib/libgmock_main.a
[100%] Built target gmock_main
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ cmake --build _build --target test
Running tests...
Test project /home/Katya/Ekaterina06-choi/workspace/projects/lab05/_build
    Start 1: check
1/1 Test #1: check ............................   Passed    0.01 sec

100% tests passed, 0 tests failed out of 1

Total Test time (real) =   0.02 sec
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ _build/check
Running main() from /home/Katya/Ekaterina06-choi/workspace/projects/lab05/third-party/gtest/googletest/src/gtest_main.cc
[==========] Running 1 test from 1 test suite.
[----------] Global test environment set-up.
[----------] 1 test from Print
[ RUN      ] Print.InFileStream
[       OK ] Print.InFileStream (0 ms)
[----------] 1 test from Print (0 ms total)

[----------] Global test environment tear-down
[==========] 1 test from 1 test suite ran. (0 ms total)
[  PASSED  ] 1 test.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ cmake --build _build --target test -- ARGS=--verbose
Running tests...
UpdateCTestConfiguration  from :/home/Katya/Ekaterina06-choi/workspace/projects/lab05/_build/DartConfiguration.tcl
UpdateCTestConfiguration  from :/home/Katya/Ekaterina06-choi/workspace/projects/lab05/_build/DartConfiguration.tcl
Test project /home/Katya/Ekaterina06-choi/workspace/projects/lab05/_build
Constructing a list of tests
Done constructing a list of tests
Updating test list for fixtures
Added 0 tests to meet fixture requirements
Checking test dependency graph...
Checking test dependency graph end
test 1
    Start 1: check

1: Test command: /home/Katya/Ekaterina06-choi/workspace/projects/lab05/_build/check
1: Working Directory: /home/Katya/Ekaterina06-choi/workspace/projects/lab05/_build
1: Test timeout computed to be: 10000000
1: Running main() from /home/Katya/Ekaterina06-choi/workspace/projects/lab05/third-party/gtest/googletest/src/gtest_main.cc
1: [==========] Running 1 test from 1 test suite.
1: [----------] Global test environment set-up.
1: [----------] 1 test from Print
1: [ RUN      ] Print.InFileStream
1: [       OK ] Print.InFileStream (0 ms)
1: [----------] 1 test from Print (0 ms total)
1: 
1: [----------] Global test environment tear-down
1: [==========] 1 test from 1 test suite ran. (0 ms total)
1: [  PASSED  ] 1 test.
1/1 Test #1: check ............................   Passed    0.00 sec

100% tests passed, 0 tests failed out of 1

Total Test time (real) =   0.01 sec
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ gsed -i 's/lab04/lab05/g' README.md
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ gsed -i 's/\(DCMAKE_INSTALL_PREFIX=_install\)/\1 -DBUILD_TESTS=ON/' .travis.yml
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ gsed -i '/cmake --build _build --target install/a\
- cmake --build _build --target test -- ARGS=--verbose
' .travis.yml
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git add .travis.yml
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git add tests
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git add -p
diff --git a/CMakeLists.txt b/CMakeLists.txt
index 96a361e..97f051c 100644
--- a/CMakeLists.txt
+++ b/CMakeLists.txt
@@ -1,9 +1,10 @@
 cmake_minimum_required(VERSION 3.4)
-
+project(lab05)
 set(CMAKE_CXX_STANDARD 11)
 set(CMAKE_CXX_STANDARD_REQUIRED ON)
 
 option(BUILD_EXAMPLES "Build examples" OFF)
+option(BUILD_TESTS "Build tests" OFF)
 
 project(print)
 
(1/2) Stage this hunk [y,n,q,a,d,j,J,g,/,s,e,p,?]? q

Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git commit -m"added tests"
[new-branch 6df19a7] added tests
 2 files changed, 24 insertions(+), 6 deletions(-)
 create mode 100644 tests/test1.cpp
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git push origin main
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
Enumerating objects: 105, done.
Counting objects: 100% (105/105), done.
Delta compression using up to 8 threads
Compressing objects: 100% (72/72), done.
Writing objects: 100% (105/105), 70.82 KiB | 17.71 MiB/s, done.
Total 105 (delta 24), reused 105 (delta 24), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (24/24), done.
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
remote:        https://github.com/Ekaterina06-choi/lab05/security/secret-scanning/unblock-secret/2wGR6xBjFYwnHOA78Dm0jJa0vAP
remote:     
remote:     
remote:       —— GitHub Personal Access Token ——————————————————————
remote:        locations:
remote:          - commit: 1be8e0a6ff5d024f282bad2c4677b0cd4ff72915
remote:            path: lab03/README.md:3
remote:     
remote:        (?) To push, remove secret from commit(s) or follow this URL to allow the secret.
remote:        https://github.com/Ekaterina06-choi/lab05/security/secret-scanning/unblock-secret/2wGR6xke8r3lTjYsuZCWyYSMHmV
remote:     
remote: 
remote: 
To https://github.com/Ekaterina06-choi/lab05
 ! [remote rejected] main -> main (push declined due to repository rule violations)
error: failed to push some refs to 'https://github.com/Ekaterina06-choi/lab05'
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git push origin main
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
Enumerating objects: 105, done.
Counting objects: 100% (105/105), done.
Delta compression using up to 8 threads
Compressing objects: 100% (72/72), done.
Writing objects: 100% (105/105), 70.82 KiB | 70.82 MiB/s, done.
Total 105 (delta 24), reused 105 (delta 24), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (24/24), done.
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
remote:        https://github.com/Ekaterina06-choi/lab05/security/secret-scanning/unblock-secret/2wGR6xke8r3lTjYsuZCWyYSMHmV
remote:     
remote: 
remote: 
To https://github.com/Ekaterina06-choi/lab05
 ! [remote rejected] main -> main (push declined due to repository rule violations)
error: failed to push some refs to 'https://github.com/Ekaterina06-choi/lab05'
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git push origin main
Username for 'https://github.com': Ekaterina06-choi 
Password for 'https://Ekaterina06-choi@github.com': 
Enumerating objects: 105, done.
Counting objects: 100% (105/105), done.
Delta compression using up to 8 threads
Compressing objects: 100% (72/72), done.
Writing objects: 100% (105/105), 70.82 KiB | 70.82 MiB/s, done.
Total 105 (delta 24), reused 105 (delta 24), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (24/24), done.
To https://github.com/Ekaterina06-choi/lab05
 * [new branch]      main -> main
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ 
