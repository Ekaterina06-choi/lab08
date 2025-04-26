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
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git init
Reinitialized existing Git repository in /home/Katya/Ekaterina06-choi/workspace/projects/lab05/.git/
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git status
On branch new-branch
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   CMakeLists.txt
	modified:   README.md
	modified:   _build/CMakeCache.txt
	modified:   _build/CMakeFiles/3.30.3/CMakeDetermineCompilerABI_C.bin
	modified:   _build/CMakeFiles/3.30.3/CMakeDetermineCompilerABI_CXX.bin
	modified:   _build/CMakeFiles/3.30.3/CMakeSystem.cmake
	modified:   _build/CMakeFiles/3.30.3/CompilerIdC/a.out
	modified:   _build/CMakeFiles/3.30.3/CompilerIdCXX/a.out
	modified:   _build/CMakeFiles/CMakeConfigureLog.yaml
	modified:   _build/CMakeFiles/CMakeDirectoryInformation.cmake
	modified:   _build/CMakeFiles/Makefile.cmake
	modified:   _build/CMakeFiles/Makefile2
	modified:   _build/CMakeFiles/TargetDirectories.txt
	deleted:    _build/CMakeFiles/example1.dir/DependInfo.cmake
	deleted:    _build/CMakeFiles/example1.dir/build.make
	deleted:    _build/CMakeFiles/example1.dir/cmake_clean.cmake
	deleted:    _build/CMakeFiles/example1.dir/compiler_depend.internal
	deleted:    _build/CMakeFiles/example1.dir/compiler_depend.make
	deleted:    _build/CMakeFiles/example1.dir/compiler_depend.ts
	deleted:    _build/CMakeFiles/example1.dir/depend.make
	deleted:    _build/CMakeFiles/example1.dir/examples/example1.cpp.o
	deleted:    _build/CMakeFiles/example1.dir/examples/example1.cpp.o.d
	deleted:    _build/CMakeFiles/example1.dir/flags.make
	deleted:    _build/CMakeFiles/example1.dir/link.txt
	deleted:    _build/CMakeFiles/example1.dir/progress.make
	deleted:    _build/CMakeFiles/example2.dir/DependInfo.cmake
	deleted:    _build/CMakeFiles/example2.dir/build.make
	deleted:    _build/CMakeFiles/example2.dir/cmake_clean.cmake
	deleted:    _build/CMakeFiles/example2.dir/compiler_depend.internal
	deleted:    _build/CMakeFiles/example2.dir/compiler_depend.make
	deleted:    _build/CMakeFiles/example2.dir/compiler_depend.ts
	deleted:    _build/CMakeFiles/example2.dir/depend.make
	deleted:    _build/CMakeFiles/example2.dir/examples/example2.cpp.o
	deleted:    _build/CMakeFiles/example2.dir/examples/example2.cpp.o.d
	deleted:    _build/CMakeFiles/example2.dir/flags.make
	deleted:    _build/CMakeFiles/example2.dir/link.txt
	deleted:    _build/CMakeFiles/example2.dir/progress.make
	modified:   _build/CMakeFiles/print.dir/DependInfo.cmake
	modified:   _build/CMakeFiles/print.dir/build.make
	deleted:    _build/CMakeFiles/print.dir/compiler_depend.internal
	modified:   _build/CMakeFiles/print.dir/compiler_depend.make
	modified:   _build/CMakeFiles/print.dir/flags.make
	modified:   _build/CMakeFiles/print.dir/progress.make
	modified:   _build/CMakeFiles/print.dir/sources/print.cpp.o.d
	modified:   _build/CMakeFiles/progress.marks
	modified:   _build/Makefile
	modified:   _build/cmake_install.cmake
	deleted:    _build/example1
	deleted:    _build/example2
	deleted:    _build/install_manifest.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	_build/CMakeFiles/check.dir/
	_build/CTestTestfile.cmake
	_build/Testing/
	_build/check
	_build/file.txt
	_build/lib/
	_build/third-party/
	file.txt

no changes added to commit (use "git add" and/or "git commit -a")
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git add third-party
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git add .
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git commit -m"added third-party"
[new-branch 525ea19] added third-party
 132 files changed, 4367 insertions(+), 2820 deletions(-)
 mode change 100644 => 100755 _build/CMakeFiles/3.30.3/CMakeDetermineCompilerABI_C.bin
 mode change 100644 => 100755 _build/CMakeFiles/3.30.3/CMakeDetermineCompilerABI_CXX.bin
 mode change 100644 => 100755 _build/CMakeFiles/3.30.3/CompilerIdC/a.out
 mode change 100644 => 100755 _build/CMakeFiles/3.30.3/CompilerIdCXX/a.out
 rename _build/CMakeFiles/{example1.dir => check.dir}/DependInfo.cmake (75%)
 create mode 100644 _build/CMakeFiles/check.dir/build.make
 create mode 100644 _build/CMakeFiles/check.dir/cmake_clean.cmake
 create mode 100644 _build/CMakeFiles/check.dir/compiler_depend.make
 rename _build/CMakeFiles/{example1.dir => check.dir}/compiler_depend.ts (87%)
 rename _build/CMakeFiles/{example1.dir => check.dir}/depend.make (56%)
 rename _build/CMakeFiles/{example1.dir => check.dir}/flags.make (53%)
 create mode 100644 _build/CMakeFiles/check.dir/link.txt
 rename _build/CMakeFiles/{example1.dir => check.dir}/progress.make (100%)
 create mode 100644 _build/CMakeFiles/check.dir/tests/test1.cpp.o
 rename _build/CMakeFiles/{example2.dir/examples/example2.cpp.o.d => check.dir/tests/test1.cpp.o.d} (50%)
 delete mode 100644 _build/CMakeFiles/example1.dir/build.make
 delete mode 100644 _build/CMakeFiles/example1.dir/cmake_clean.cmake
 delete mode 100644 _build/CMakeFiles/example1.dir/compiler_depend.internal
 delete mode 100644 _build/CMakeFiles/example1.dir/compiler_depend.make
 delete mode 100644 _build/CMakeFiles/example1.dir/examples/example1.cpp.o
 delete mode 100644 _build/CMakeFiles/example1.dir/examples/example1.cpp.o.d
 delete mode 100644 _build/CMakeFiles/example1.dir/link.txt
 delete mode 100644 _build/CMakeFiles/example2.dir/build.make
 delete mode 100644 _build/CMakeFiles/example2.dir/cmake_clean.cmake
 delete mode 100644 _build/CMakeFiles/example2.dir/compiler_depend.internal
 delete mode 100644 _build/CMakeFiles/example2.dir/compiler_depend.make
 delete mode 100644 _build/CMakeFiles/example2.dir/examples/example2.cpp.o
 delete mode 100644 _build/CMakeFiles/example2.dir/flags.make
 delete mode 100644 _build/CMakeFiles/example2.dir/link.txt
 delete mode 100644 _build/CMakeFiles/print.dir/compiler_depend.internal
 create mode 100644 _build/CTestTestfile.cmake
 create mode 100644 _build/Testing/Temporary/CTestCostData.txt
 create mode 100644 _build/Testing/Temporary/LastTest.log
 create mode 100755 _build/check
 delete mode 100644 _build/example1
 delete mode 100644 _build/example2
 create mode 100644 _build/file.txt
 delete mode 100644 _build/install_manifest.txt
 create mode 100644 _build/lib/libgmock.a
 create mode 100644 _build/lib/libgmock_main.a
 create mode 100644 _build/lib/libgtest.a
 create mode 100644 _build/lib/libgtest_main.a
 create mode 100644 _build/third-party/gtest/CMakeFiles/CMakeDirectoryInformation.cmake
 create mode 100644 _build/third-party/gtest/CMakeFiles/progress.marks
 create mode 100644 _build/third-party/gtest/CTestTestfile.cmake
 create mode 100644 _build/third-party/gtest/Makefile
 create mode 100644 _build/third-party/gtest/cmake_install.cmake
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/CMakeDirectoryInformation.cmake
 rename _build/{CMakeFiles/example2.dir => third-party/gtest/googlemock/CMakeFiles/gmock.dir}/DependInfo.cmake (69%)
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock.dir/build.make
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock.dir/cmake_clean.cmake
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock.dir/cmake_clean_target.cmake
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock.dir/compiler_depend.make
 rename _build/{CMakeFiles/example2.dir => third-party/gtest/googlemock/CMakeFiles/gmock.dir}/compiler_depend.ts (87%)
 rename _build/{CMakeFiles/example2.dir => third-party/gtest/googlemock/CMakeFiles/gmock.dir}/depend.make (56%)
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock.dir/flags.make
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock.dir/link.txt
 rename _build/{CMakeFiles/example2.dir => third-party/gtest/googlemock/CMakeFiles/gmock.dir}/progress.make (100%)
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o.d
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/DependInfo.cmake
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/build.make
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/cmake_clean.cmake
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/cmake_clean_target.cmake
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/compiler_depend.make
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/compiler_depend.ts
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/depend.make
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/flags.make
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/link.txt
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/progress.make
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o.d
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/progress.marks
 create mode 100644 _build/third-party/gtest/googlemock/CTestTestfile.cmake
 create mode 100644 _build/third-party/gtest/googlemock/Makefile
 create mode 100644 _build/third-party/gtest/googlemock/cmake_install.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/CMakeDirectoryInformation.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/Export/0c08b8e77dd885bfe55a19a9659d9fc1/GTestTargets-noconfig.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/Export/0c08b8e77dd885bfe55a19a9659d9fc1/GTestTargets.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/DependInfo.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/build.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/cmake_clean.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/cmake_clean_target.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/compiler_depend.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/compiler_depend.ts
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/depend.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/flags.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/link.txt
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/progress.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/src/gtest-all.cc.o
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/src/gtest-all.cc.o.d
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/DependInfo.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/build.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/cmake_clean.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/cmake_clean_target.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/compiler_depend.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/compiler_depend.ts
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/depend.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/flags.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/link.txt
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/progress.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o.d
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/progress.marks
 create mode 100644 _build/third-party/gtest/googletest/CTestTestfile.cmake
 create mode 100644 _build/third-party/gtest/googletest/Makefile
 create mode 100644 _build/third-party/gtest/googletest/cmake_install.cmake
 create mode 100644 _build/third-party/gtest/googletest/generated/GTestConfig.cmake
 create mode 100644 _build/third-party/gtest/googletest/generated/GTestConfigVersion.cmake
 create mode 100644 _build/third-party/gtest/googletest/generated/gmock.pc
 create mode 100644 _build/third-party/gtest/googletest/generated/gmock_main.pc
 create mode 100644 _build/third-party/gtest/googletest/generated/gtest.pc
 create mode 100644 _build/third-party/gtest/googletest/generated/gtest_main.pc
 create mode 100644 file.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git push origin main
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
To https://github.com/Ekaterina06-choi/lab05
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/Ekaterina06-choi/lab05'
hint: Updates were rejected because the remote contains work that you do not
hint: have locally. This is usually caused by another repository pushing to
hint: the same ref. If you want to integrate the remote changes, use
hint: 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git pull origin main
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 7 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (7/7), 6.03 KiB | 3.01 MiB/s, done.
From https://github.com/Ekaterina06-choi/lab05
 * branch            main       -> FETCH_HEAD
   551d65e..8c53e12  main       -> origin/main
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
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git config pull.rebase false
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git push origin main
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
To https://github.com/Ekaterina06-choi/lab05
 ! [rejected]        main -> main (non-fast-forward)
error: failed to push some refs to 'https://github.com/Ekaterina06-choi/lab05'
hint: Updates were rejected because a pushed branch tip is behind its remote
hint: counterpart. If you want to integrate the remote changes, use 'git pull'
hint: before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git pull origin main
From https://github.com/Ekaterina06-choi/lab05
 * branch            main       -> FETCH_HEAD
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ nano README.md
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ nano README.md
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git add README.md
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git commit -m"merge changes in README"
[new-branch 89f6761] merge changes in README
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git push origin main
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
To https://github.com/Ekaterina06-choi/lab05
 ! [rejected]        main -> main (non-fast-forward)
error: failed to push some refs to 'https://github.com/Ekaterina06-choi/lab05'
hint: Updates were rejected because a pushed branch tip is behind its remote
hint: counterpart. If you want to integrate the remote changes, use 'git pull'
hint: before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git pull origin main
From https://github.com/Ekaterina06-choi/lab05
 * branch            main       -> FETCH_HEAD
Already up to date.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git push origin main
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
To https://github.com/Ekaterina06-choi/lab05
 ! [rejected]        main -> main (non-fast-forward)
error: failed to push some refs to 'https://github.com/Ekaterina06-choi/lab05'
hint: Updates were rejected because a pushed branch tip is behind its remote
hint: counterpart. If you want to integrate the remote changes, use 'git pull'
hint: before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git push --help
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git pull --rebase origin main
From https://github.com/Ekaterina06-choi/lab05
 * branch            main       -> FETCH_HEAD
warning: unable to rmdir 'third-party/gtest': Directory not empty
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
error: could not apply 525ea19... added third-party
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
hint: Disable this message with "git config advice.mergeConflict false"
Could not apply 525ea19... added third-party
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git add .
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git rebase --continue
[detached HEAD 21a4240] added third-party
 133 files changed, 6758 insertions(+), 2800 deletions(-)
 create mode 100644 README.md M-A
 mode change 100644 => 100755 _build/CMakeFiles/3.30.3/CMakeDetermineCompilerABI_C.bin
 mode change 100644 => 100755 _build/CMakeFiles/3.30.3/CMakeDetermineCompilerABI_CXX.bin
 mode change 100644 => 100755 _build/CMakeFiles/3.30.3/CompilerIdC/a.out
 mode change 100644 => 100755 _build/CMakeFiles/3.30.3/CompilerIdCXX/a.out
 rename _build/CMakeFiles/{example1.dir => check.dir}/DependInfo.cmake (75%)
 create mode 100644 _build/CMakeFiles/check.dir/build.make
 create mode 100644 _build/CMakeFiles/check.dir/cmake_clean.cmake
 create mode 100644 _build/CMakeFiles/check.dir/compiler_depend.make
 rename _build/CMakeFiles/{example1.dir => check.dir}/compiler_depend.ts (87%)
 rename _build/CMakeFiles/{example1.dir => check.dir}/depend.make (56%)
 rename _build/CMakeFiles/{example1.dir => check.dir}/flags.make (53%)
 create mode 100644 _build/CMakeFiles/check.dir/link.txt
 rename _build/CMakeFiles/{example1.dir => check.dir}/progress.make (100%)
 create mode 100644 _build/CMakeFiles/check.dir/tests/test1.cpp.o
 rename _build/CMakeFiles/{example2.dir/examples/example2.cpp.o.d => check.dir/tests/test1.cpp.o.d} (50%)
 delete mode 100644 _build/CMakeFiles/example1.dir/build.make
 delete mode 100644 _build/CMakeFiles/example1.dir/cmake_clean.cmake
 delete mode 100644 _build/CMakeFiles/example1.dir/compiler_depend.internal
 delete mode 100644 _build/CMakeFiles/example1.dir/compiler_depend.make
 delete mode 100644 _build/CMakeFiles/example1.dir/examples/example1.cpp.o
 delete mode 100644 _build/CMakeFiles/example1.dir/examples/example1.cpp.o.d
 delete mode 100644 _build/CMakeFiles/example1.dir/link.txt
 delete mode 100644 _build/CMakeFiles/example2.dir/build.make
 delete mode 100644 _build/CMakeFiles/example2.dir/cmake_clean.cmake
 delete mode 100644 _build/CMakeFiles/example2.dir/compiler_depend.internal
 delete mode 100644 _build/CMakeFiles/example2.dir/compiler_depend.make
 delete mode 100644 _build/CMakeFiles/example2.dir/examples/example2.cpp.o
 delete mode 100644 _build/CMakeFiles/example2.dir/flags.make
 delete mode 100644 _build/CMakeFiles/example2.dir/link.txt
 delete mode 100644 _build/CMakeFiles/print.dir/compiler_depend.internal
 create mode 100644 _build/CTestTestfile.cmake
 create mode 100644 _build/Testing/Temporary/CTestCostData.txt
 create mode 100644 _build/Testing/Temporary/LastTest.log
 create mode 100755 _build/check
 delete mode 100644 _build/example1
 delete mode 100644 _build/example2
 create mode 100644 _build/file.txt
 delete mode 100644 _build/install_manifest.txt
 create mode 100644 _build/lib/libgmock.a
 create mode 100644 _build/lib/libgmock_main.a
 create mode 100644 _build/lib/libgtest.a
 create mode 100644 _build/lib/libgtest_main.a
 create mode 100644 _build/third-party/gtest/CMakeFiles/CMakeDirectoryInformation.cmake
 create mode 100644 _build/third-party/gtest/CMakeFiles/progress.marks
 create mode 100644 _build/third-party/gtest/CTestTestfile.cmake
 create mode 100644 _build/third-party/gtest/Makefile
 create mode 100644 _build/third-party/gtest/cmake_install.cmake
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/CMakeDirectoryInformation.cmake
 rename _build/{CMakeFiles/example2.dir => third-party/gtest/googlemock/CMakeFiles/gmock.dir}/DependInfo.cmake (69%)
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock.dir/build.make
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock.dir/cmake_clean.cmake
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock.dir/cmake_clean_target.cmake
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock.dir/compiler_depend.make
 rename _build/{CMakeFiles/example2.dir => third-party/gtest/googlemock/CMakeFiles/gmock.dir}/compiler_depend.ts (87%)
 rename _build/{CMakeFiles/example2.dir => third-party/gtest/googlemock/CMakeFiles/gmock.dir}/depend.make (56%)
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock.dir/flags.make
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock.dir/link.txt
 rename _build/{CMakeFiles/example2.dir => third-party/gtest/googlemock/CMakeFiles/gmock.dir}/progress.make (100%)
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o.d
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/DependInfo.cmake
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/build.make
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/cmake_clean.cmake
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/cmake_clean_target.cmake
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/compiler_depend.make
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/compiler_depend.ts
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/depend.make
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/flags.make
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/link.txt
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/progress.make
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o.d
 create mode 100644 _build/third-party/gtest/googlemock/CMakeFiles/progress.marks
 create mode 100644 _build/third-party/gtest/googlemock/CTestTestfile.cmake
 create mode 100644 _build/third-party/gtest/googlemock/Makefile
 create mode 100644 _build/third-party/gtest/googlemock/cmake_install.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/CMakeDirectoryInformation.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/Export/0c08b8e77dd885bfe55a19a9659d9fc1/GTestTargets-noconfig.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/Export/0c08b8e77dd885bfe55a19a9659d9fc1/GTestTargets.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/DependInfo.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/build.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/cmake_clean.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/cmake_clean_target.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/compiler_depend.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/compiler_depend.ts
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/depend.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/flags.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/link.txt
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/progress.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/src/gtest-all.cc.o
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest.dir/src/gtest-all.cc.o.d
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/DependInfo.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/build.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/cmake_clean.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/cmake_clean_target.cmake
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/compiler_depend.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/compiler_depend.ts
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/depend.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/flags.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/link.txt
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/progress.make
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o.d
 create mode 100644 _build/third-party/gtest/googletest/CMakeFiles/progress.marks
 create mode 100644 _build/third-party/gtest/googletest/CTestTestfile.cmake
 create mode 100644 _build/third-party/gtest/googletest/Makefile
 create mode 100644 _build/third-party/gtest/googletest/cmake_install.cmake
 create mode 100644 _build/third-party/gtest/googletest/generated/GTestConfig.cmake
 create mode 100644 _build/third-party/gtest/googletest/generated/GTestConfigVersion.cmake
 create mode 100644 _build/third-party/gtest/googletest/generated/gmock.pc
 create mode 100644 _build/third-party/gtest/googletest/generated/gmock_main.pc
 create mode 100644 _build/third-party/gtest/googletest/generated/gtest.pc
 create mode 100644 _build/third-party/gtest/googletest/generated/gtest_main.pc
 create mode 100644 file.txt
Successfully rebased and updated refs/heads/new-branch.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ git push origin new-branch --force-with-lease
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
Enumerating objects: 167, done.
Counting objects: 100% (167/167), done.
Delta compression using up to 8 threads
Compressing objects: 100% (131/131), done.
Writing objects: 100% (144/144), 1.25 MiB | 5.96 MiB/s, done.
Total 144 (delta 60), reused 1 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (60/60), completed with 11 local objects.
remote: 
remote: Create a pull request for 'new-branch' on GitHub by visiting:
remote:      https://github.com/Ekaterina06-choi/lab05/pull/new/new-branch
remote: 
To https://github.com/Ekaterina06-choi/lab05
 * [new branch]      new-branch -> new-branch
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab05$ 
