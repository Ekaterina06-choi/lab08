Katya@ubuntu:~$ export GITHUB_USERNAME=Ekaterina06-choi
Katya@ubuntu:~$ alias gsed=sed
Katya@ubuntu:~$ cd ${GITHUB_USERNAME}/workspace
Katya@ubuntu:~/Ekaterina06-choi/workspace$ pushd .
~/Ekaterina06-choi/workspace ~/Ekaterina06-choi/workspace
Katya@ubuntu:~/Ekaterina06-choi/workspace$ source scripts/activate
Katya@ubuntu:~/Ekaterina06-choi/workspace$ git clone https://github.com/${GITHUB_USERNAME}/lab06 projects/lab07
Cloning into 'projects/lab07'...
remote: Enumerating objects: 271, done.
remote: Counting objects: 100% (271/271), done.
remote: Compressing objects: 100% (145/145), done.
remote: Total 271 (delta 105), reused 267 (delta 103), pack-reused 0 (from 0)
Receiving objects: 100% (271/271), 1.32 MiB | 973.00 KiB/s, done.
Resolving deltas: 100% (105/105), done.
Katya@ubuntu:~/Ekaterina06-choi/workspace$ cd projects/lab07
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ git remote remove origin
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab07
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ mkdir -p cmake
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ wget https://raw.githubusercontent.com/cpp-pm/gate/master/cmake/HunterGate.cmake -O cmake/HunterGate.cmake
--2025-04-27 13:22:47--  https://raw.githubusercontent.com/cpp-pm/gate/master/cmake/HunterGate.cmake
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.110.133, 185.199.111.133, 185.199.108.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.110.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 17231 (17K) [text/plain]
Saving to: ‘cmake/HunterGate.cmake’

cmake/HunterGate.cm 100%[===================>]  16.83K  54.6KB/s    in 0.3s    

2025-04-27 13:22:48 (54.6 KB/s) - ‘cmake/HunterGate.cmake’ saved [17231/17231]

Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ gsed -i '/cmake_minimum_required(VERSION 3.4)/a\
\
include("cmake/HunterGate.cmake")\
HunterGate(\
    URL "https://github.com/cpp-pm/hunter/archive/v0.23.251.tar.gz"\
    SHA1 "5659b15dc0884d4b03dbd95710e6a1fa0fc3258d"\
)' CMakeLists.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ git rm -rf third-party/gtest
rm 'third-party/gtest'
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ gsed -i '/set(PRINT_VERSION_STRING "v${PRINT_VERSION}")/a\
\
hunter_add_package(GTest)\
find_package(GTest CONFIG REQUIRED)\
' CMakeLists.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ gsed -i '/add_subdirectory(third-party\/gtest)/d' CMakeLists.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ gsed -i 's/gtest_main/GTest::main/g' CMakeLists.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ cmake -H. -B_builds -DBUILD_TESTS=ON
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_set_config_location.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:13 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_private_data.cmake:12 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:35 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_initialize.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:36 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


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
-- [hunter] Calculating Toolchain-SHA1
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- [hunter] Calculating Config-SHA1
-- [hunter] HUNTER_ROOT: /home/Katya/.hunter
-- [hunter] [ Hunter-ID: 5659b15 | Toolchain-ID: 29081be | Config-ID: 8a1641b ]
CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_set_config_location.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:13 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_set_config_location.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:13 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


-- [hunter] GTEST_ROOT: /home/Katya/.hunter/_Base/5659b15/29081be/8a1641b/Install (ver.: 1.10.0)
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Configuring done (1.6s)
CMake Error at CMakeLists.txt:60 (target_link_libraries):
  Target "check" links to:

    GTest::main

  but the target was not found.  Possible reasons include:

    * There is a typo in the target name.
    * A find_package call is missing for an IMPORTED target.
    * An ALIAS target is missing.



-- Generating done (0.0s)
CMake Generate step failed.  Build files cannot be regenerated correctly.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ sudo apt-get install libgtest-dev
[sudo] password for Katya: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  googletest
The following NEW packages will be installed:
  googletest libgtest-dev
0 upgraded, 2 newly installed, 0 to remove and 4 not upgraded.
Need to get 799 kB of archives.
After this operation, 5,200 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://ru.archive.ubuntu.com/ubuntu oracular/universe amd64 googletest all 1.15.2-1 [523 kB]
Get:2 http://ru.archive.ubuntu.com/ubuntu oracular/universe amd64 libgtest-dev amd64 1.15.2-1 [276 kB]
Fetched 799 kB in 1s (775 kB/s)        
Selecting previously unselected package googletest.
(Reading database ... 199019 files and directories currently installed.)
Preparing to unpack .../googletest_1.15.2-1_all.deb ...
Unpacking googletest (1.15.2-1) ...
Selecting previously unselected package libgtest-dev:amd64.
Preparing to unpack .../libgtest-dev_1.15.2-1_amd64.deb ...
Unpacking libgtest-dev:amd64 (1.15.2-1) ...
Setting up googletest (1.15.2-1) ...
Setting up libgtest-dev:amd64 (1.15.2-1) ...
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ cmake -S . -B _build
CMake Error: The current CMakeCache.txt directory /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_build/CMakeCache.txt is different than the directory /home/Katya/Ekaterina06-choi/workspace/projects/lab05/_build where CMakeCache.txt was created. This may result in binaries being created in the wrong place. If you are not sure, reedit the CMakeCache.txt
CMake Error: The source "/home/Katya/Ekaterina06-choi/workspace/projects/lab07/CMakeLists.txt" does not match the source "/home/Katya/Ekaterina06-choi/workspace/projects/lab05/CMakeLists.txt" used to generate cache.  Re-run cmake with a different source directory.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ rm -rf /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_build
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ mkdir -p /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_build
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ cd /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_build
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07/_build$ cmake /home/Katya/Ekaterina06-choi/workspace/projects/lab07
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_set_config_location.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:13 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_private_data.cmake:12 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:35 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_initialize.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:36 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


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
-- [hunter] Calculating Toolchain-SHA1
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- [hunter] Calculating Config-SHA1
-- [hunter] HUNTER_ROOT: /home/Katya/.hunter
-- [hunter] [ Hunter-ID: 5659b15 | Toolchain-ID: 29081be | Config-ID: 8a1641b ]
CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_set_config_location.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:13 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_set_config_location.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:13 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


-- [hunter] GTEST_ROOT: /home/Katya/.hunter/_Base/5659b15/29081be/8a1641b/Install (ver.: 1.10.0)
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Configuring done (1.8s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_build
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07/_build$ cmake -H. -B_builds -DBUILD_TESTS=ON
CMake Error: The source directory "/home/Katya/Ekaterina06-choi/workspace/projects/lab07/_build" does not appear to contain CMakeLists.txt.
Specify --help for usage, or press the help button on the CMake GUI.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07/_build$ cd ..
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ cmake -H. -B_builds -DBUILD_TESTS=ON
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_set_config_location.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:13 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_private_data.cmake:12 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:35 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_initialize.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:36 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


-- [hunter] Calculating Toolchain-SHA1
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- [hunter] Calculating Config-SHA1
-- [hunter] HUNTER_ROOT: /home/Katya/.hunter
-- [hunter] [ Hunter-ID: 5659b15 | Toolchain-ID: 29081be | Config-ID: 8a1641b ]
CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_set_config_location.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:13 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_set_config_location.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:13 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


-- [hunter] GTEST_ROOT: /home/Katya/.hunter/_Base/5659b15/29081be/8a1641b/Install (ver.: 1.10.0)
-- Configuring done (1.0s)
CMake Error at CMakeLists.txt:61 (target_link_libraries):
  Target "check" links to:

    GTest::main

  but the target was not found.  Possible reasons include:

    * There is a typo in the target name.
    * A find_package call is missing for an IMPORTED target.
    * An ALIAS target is missing.



-- Generating done (0.0s)
CMake Generate step failed.  Build files cannot be regenerated correctly.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ rm -rf _build/
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ mkdir _build && cd _build
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07/_build$ cmake ..
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_set_config_location.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:13 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_private_data.cmake:12 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:35 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_initialize.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:36 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


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
-- [hunter] Calculating Toolchain-SHA1
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- [hunter] Calculating Config-SHA1
-- [hunter] HUNTER_ROOT: /home/Katya/.hunter
-- [hunter] [ Hunter-ID: 5659b15 | Toolchain-ID: 29081be | Config-ID: 8a1641b ]
CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_set_config_location.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:13 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_set_config_location.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:13 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


-- [hunter] GTEST_ROOT: /home/Katya/.hunter/_Base/5659b15/29081be/8a1641b/Install (ver.: 1.10.0)
-- Found GTest: /home/Katya/.hunter/_Base/5659b15/29081be/8a1641b/Install/lib/cmake/GTest/GTestConfig.cmake (found version "1.10.0")
-- Configuring done (1.7s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_build
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07/_build$ cmake -H. -B_builds -DBUILD_TESTS=ON
CMake Error: The source directory "/home/Katya/Ekaterina06-choi/workspace/projects/lab07/_build" does not appear to contain CMakeLists.txt.
Specify --help for usage, or press the help button on the CMake GUI.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07/_build$ cd ..
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ cmake -H. -B_builds -DBUILD_TESTS=ON
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_set_config_location.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:13 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:34 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_private_data.cmake:12 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:35 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_initialize.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/Hunter:36 (include)
  cmake/HunterGate.cmake:540 (include)
  CMakeLists.txt:4 (HunterGate)


-- [hunter] Calculating Toolchain-SHA1
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- [hunter] Calculating Config-SHA1
-- [hunter] HUNTER_ROOT: /home/Katya/.hunter
-- [hunter] [ Hunter-ID: 5659b15 | Toolchain-ID: 29081be | Config-ID: 8a1641b ]
CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_set_config_location.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:13 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_config_sha1.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:9 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_toolchain_sha1.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:10 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_set_config_location.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_apply_gate_settings.cmake:13 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_calculate_self.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_finalize.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_cache_run.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_load_from_cache.cmake:6 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:22 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_create_cache_meta_directory.cmake:5 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:4 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


CMake Deprecation Warning at /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_lock_directory.cmake:4 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.
Call Stack (most recent call first):
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_make_directory.cmake:7 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_save_to_cache.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_download.cmake:26 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/projects/GTest/hunter.cmake:8 (include)
  /home/Katya/.hunter/_Base/Download/Hunter/0.23.251/5659b15/Unpacked/cmake/modules/hunter_add_package.cmake:62 (include)
  CMakeLists.txt:24 (hunter_add_package)


-- [hunter] GTEST_ROOT: /home/Katya/.hunter/_Base/5659b15/29081be/8a1641b/Install (ver.: 1.10.0)
-- Found GTest: /home/Katya/.hunter/_Base/5659b15/29081be/8a1641b/Install/lib/cmake/GTest/GTestConfig.cmake (found version "1.10.0")
-- Configuring done (1.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ cmake --build _builds
[ 25%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 50%] Linking CXX static library libprint.a
[ 50%] Built target print
[ 75%] Building CXX object CMakeFiles/check.dir/tests/test1.cpp.o
[100%] Linking CXX executable check
[100%] Built target check
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ cmake --build _builds --target test
Running tests...
Test project /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds
    Start 1: check
1/1 Test #1: check ............................   Passed    0.01 sec

100% tests passed, 0 tests failed out of 1

Total Test time (real) =   0.02 sec
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ ls -la $HOME/.hunter
total 12
drwxrwxr-x  3 Katya Katya 4096 Apr 27 11:16 .
drwxr-x--- 19 Katya Katya 4096 Apr 27 11:16 ..
drwxrwxr-x  6 Katya Katya 4096 Apr 27 11:16 _Base
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ git clone https://github.com/cpp-pm/hunter $HOME/projects/hunter
Cloning into '/home/Katya/projects/hunter'...
remote: Enumerating objects: 53004, done.
remote: Counting objects: 100% (857/857), done.
remote: Compressing objects: 100% (230/230), done.
remote: Total 53004 (delta 679), reused 627 (delta 627), pack-reused 52147 (from 3)
Receiving objects: 100% (53004/53004), 13.80 MiB | 217.00 KiB/s, done.
Resolving deltas: 100% (33126/33126), done.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ export HUNTER_ROOT=$HOME/projects/hunter
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ rm -rf _builds
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ cmake -H. -B_builds -DBUILD_TESTS=ON
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
-- [hunter] Calculating Toolchain-SHA1
-- [hunter] Calculating Config-SHA1
-- [hunter] HUNTER_ROOT: /home/Katya/projects/hunter
-- [hunter] [ Hunter-ID: xxxxxxx | Toolchain-ID: 29081be | Config-ID: d14f46d ]
-- [hunter] GTEST_ROOT: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Install (ver.: 1.15.2)
-- [hunter] Building GTest
loading initial cache file /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/cache.cmake
loading initial cache file /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/args.cmake
-- The C compiler identification is GNU 14.2.0
-- The CXX compiler identification is GNU 14.2.0
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done (0.3s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Build
[  6%] Creating directories for 'GTest-Release'
[ 12%] Performing download step (download, verify and extract) for 'GTest-Release'
-- Downloading...
   dst='/home/Katya/projects/hunter/_Base/Download/GTest/1.15.2/568d58e/v1.15.2.tar.gz'
   timeout='none'
   inactivity timeout='none'
-- Using src='https://github.com/google/googletest/archive/v1.15.2.tar.gz'
-- [download 0% complete]
-- [download 1% complete]
-- [download 2% complete]
-- [download 4% complete]
-- [download 5% complete]
-- [download 6% complete]
-- [download 7% complete]
-- [download 8% complete]
-- [download 9% complete]
-- [download 11% complete]
-- [download 13% complete]
-- [download 15% complete]
-- [download 16% complete]
-- [download 18% complete]
-- [download 19% complete]
-- [download 20% complete]
-- [download 21% complete]
-- [download 22% complete]
-- [download 24% complete]
-- [download 26% complete]
-- [download 28% complete]
-- [download 29% complete]
-- [download 31% complete]
-- [download 33% complete]
-- [download 35% complete]
-- [download 36% complete]
-- [download 37% complete]
-- [download 39% complete]
-- [download 41% complete]
-- [download 43% complete]
-- [download 44% complete]
-- [download 46% complete]
-- [download 47% complete]
-- [download 48% complete]
-- [download 50% complete]
-- [download 52% complete]
-- [download 54% complete]
-- [download 56% complete]
-- [download 58% complete]
-- [download 59% complete]
-- [download 60% complete]
-- [download 62% complete]
-- [download 63% complete]
-- [download 65% complete]
-- [download 67% complete]
-- [download 68% complete]
-- [download 70% complete]
-- [download 72% complete]
-- [download 74% complete]
-- [download 76% complete]
-- [download 77% complete]
-- [download 78% complete]
-- [download 79% complete]
-- [download 81% complete]
-- [download 83% complete]
-- [download 84% complete]
-- [download 85% complete]
-- [download 87% complete]
-- [download 88% complete]
-- [download 89% complete]
-- [download 90% complete]
-- [download 91% complete]
-- [download 93% complete]
-- [download 94% complete]
-- [download 95% complete]
-- [download 96% complete]
-- [download 97% complete]
-- [download 98% complete]
-- [download 99% complete]
-- [download 100% complete]
-- verifying file...
       file='/home/Katya/projects/hunter/_Base/Download/GTest/1.15.2/568d58e/v1.15.2.tar.gz'
-- Downloading... done
-- extracting...
     src='/home/Katya/projects/hunter/_Base/Download/GTest/1.15.2/568d58e/v1.15.2.tar.gz'
     dst='/home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Source'
-- extracting... [tar xfz]
-- extracting... [analysis]
-- extracting... [rename]
-- extracting... [clean up]
-- extracting... done
[ 18%] No update step for 'GTest-Release'
[ 25%] No patch step for 'GTest-Release'
[ 31%] Performing configure step for 'GTest-Release'
loading initial cache file /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/cache.cmake
loading initial cache file /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/args.cmake
-- The C compiler identification is GNU 14.2.0
-- The CXX compiler identification is GNU 14.2.0
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Configuring done (0.3s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Build/GTest-Release-prefix/src/GTest-Release-build
[ 37%] Performing build step for 'GTest-Release'
[ 12%] Building CXX object googletest/CMakeFiles/gtest.dir/src/gtest-all.cc.o
[ 25%] Linking CXX static library ../lib/libgtest.a
[ 25%] Built target gtest
[ 50%] Building CXX object googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o
[ 50%] Building CXX object googletest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
[ 62%] Linking CXX static library ../lib/libgtest_main.a
[ 62%] Built target gtest_main
[ 75%] Linking CXX static library ../lib/libgmock.a
[ 75%] Built target gmock
[ 87%] Building CXX object googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o
[100%] Linking CXX static library ../lib/libgmock_main.a
[100%] Built target gmock_main
[ 43%] Performing install step for 'GTest-Release'
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/internal
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/internal/gmock-port.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/internal/gmock-internal-utils.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/internal/gmock-pp.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/internal/custom
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/internal/custom/gmock-port.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/internal/custom/gmock-generated-actions.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/internal/custom/README.md
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/internal/custom/gmock-matchers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/gmock-more-actions.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/gmock-nice-strict.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/gmock-actions.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/gmock-function-mocker.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/gmock-matchers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/gmock-cardinalities.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/gmock.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/gmock-spec-builders.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/gmock-more-matchers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/libgmock.a
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/libgmock_main.a
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/pkgconfig/gmock.pc
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/pkgconfig/gmock_main.pc
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/cmake/GTest/GTestTargets.cmake
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/cmake/GTest/GTestTargets-release.cmake
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/cmake/GTest/GTestConfigVersion.cmake
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/cmake/GTest/GTestConfig.cmake
-- Up-to-date: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest-test-part.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest_prod.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest-typed-test.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest_pred_impl.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest-assertion-result.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-port.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-param-util.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-port-arch.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/custom
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/custom/gtest-port.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/custom/gtest.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/custom/README.md
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/custom/gtest-printers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-internal.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-type-util.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-string.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-filepath.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-death-test-internal.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest-death-test.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest-param-test.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest-matchers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest-spi.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest-printers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest-message.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/libgtest.a
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/libgtest_main.a
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/pkgconfig/gtest.pc
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/pkgconfig/gtest_main.pc
loading initial cache file /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/args.cmake
[ 50%] Completed 'GTest-Release'
[ 50%] Built target GTest-Release
[ 56%] Creating directories for 'GTest-Debug'
[ 62%] Performing download step (download, verify and extract) for 'GTest-Debug'
-- verifying file...
       file='/home/Katya/projects/hunter/_Base/Download/GTest/1.15.2/568d58e/v1.15.2.tar.gz'
-- File already exists and hash match (skip download):
  file='/home/Katya/projects/hunter/_Base/Download/GTest/1.15.2/568d58e/v1.15.2.tar.gz'
  SHA1='568d58e26bd4e838449ca7ab8ebc152b3cbd210d'
-- extracting...
     src='/home/Katya/projects/hunter/_Base/Download/GTest/1.15.2/568d58e/v1.15.2.tar.gz'
     dst='/home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Source'
-- extracting... [tar xfz]
-- extracting... [analysis]
-- extracting... [rename]
-- extracting... [clean up]
-- extracting... done
[ 68%] No update step for 'GTest-Debug'
[ 75%] No patch step for 'GTest-Debug'
[ 81%] Performing configure step for 'GTest-Debug'
loading initial cache file /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/cache.cmake
loading initial cache file /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/args.cmake
-- The C compiler identification is GNU 14.2.0
-- The CXX compiler identification is GNU 14.2.0
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Configuring done (0.3s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Build/GTest-Debug-prefix/src/GTest-Debug-build
[ 87%] Performing build step for 'GTest-Debug'
[ 12%] Building CXX object googletest/CMakeFiles/gtest.dir/src/gtest-all.cc.o
[ 25%] Linking CXX static library ../lib/libgtestd.a
[ 25%] Built target gtest
[ 50%] Building CXX object googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o
[ 50%] Building CXX object googletest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
[ 62%] Linking CXX static library ../lib/libgtest_maind.a
[ 62%] Built target gtest_main
[ 75%] Linking CXX static library ../lib/libgmockd.a
[ 75%] Built target gmock
[ 87%] Building CXX object googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o
[100%] Linking CXX static library ../lib/libgmock_maind.a
[100%] Built target gmock_main
[ 93%] Performing install step for 'GTest-Debug'
-- Up-to-date: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include
-- Up-to-date: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock
-- Up-to-date: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/internal
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/internal/gmock-port.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/internal/gmock-internal-utils.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/internal/gmock-pp.h
-- Up-to-date: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/internal/custom
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/internal/custom/gmock-port.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/internal/custom/gmock-generated-actions.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/internal/custom/README.md
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/internal/custom/gmock-matchers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/gmock-more-actions.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/gmock-nice-strict.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/gmock-actions.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/gmock-function-mocker.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/gmock-matchers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/gmock-cardinalities.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/gmock.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/gmock-spec-builders.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gmock/gmock-more-matchers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/libgmockd.a
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/libgmock_maind.a
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/pkgconfig/gmock.pc
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/pkgconfig/gmock_main.pc
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/cmake/GTest/GTestTargets.cmake
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/cmake/GTest/GTestTargets-debug.cmake
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/cmake/GTest/GTestConfigVersion.cmake
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/cmake/GTest/GTestConfig.cmake
-- Up-to-date: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include
-- Up-to-date: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest-test-part.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest_prod.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest-typed-test.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest_pred_impl.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest-assertion-result.h
-- Up-to-date: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-port.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-param-util.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-port-arch.h
-- Up-to-date: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/custom
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/custom/gtest-port.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/custom/gtest.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/custom/README.md
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/custom/gtest-printers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-internal.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-type-util.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-string.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-filepath.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-death-test-internal.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest-death-test.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest-param-test.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest-matchers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest-spi.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest-printers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/include/gtest/gtest-message.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/libgtestd.a
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/libgtest_maind.a
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/pkgconfig/gtest.pc
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/Install/lib/pkgconfig/gtest_main.pc
loading initial cache file /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest/args.cmake
[100%] Completed 'GTest-Debug'
[100%] Built target GTest-Debug
-- [hunter] Build step successful (dir: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Build/GTest)
-- [hunter] Cache saved: /home/Katya/projects/hunter/_Base/Cache/raw/e6bef9366476f246b70719814daec82b861814ed.tar.bz2
-- Found GTest: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Install/lib/cmake/GTest/GTestConfig.cmake (found version "1.15.2")
-- Configuring done (26.9s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ cmake --build _builds
[ 25%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 50%] Linking CXX static library libprint.a
[ 50%] Built target print
[ 75%] Building CXX object CMakeFiles/check.dir/tests/test1.cpp.o
[100%] Linking CXX executable check
[100%] Built target check
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ cmake --build _builds --target test
Running tests...
Test project /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds
    Start 1: check
1/1 Test #1: check ............................   Passed    0.01 sec

100% tests passed, 0 tests failed out of 1

Total Test time (real) =   0.03 sec
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ cat $HUNTER_ROOT/cmake/configs/default.cmake
# Copyright (c) 2013-2020, Ruslan Baratov, Rahul Sheth
# All rights reserved.

# Do not place header guards here

# Set CMake variables:
#   * HUNTER_${PACKAGE_NAME}_VERSION

# Usage:
#   hunter_default_version(Foo VERSION 1.0.0)
#   hunter_default_version(Boo VERSION 1.2.3z)

include(hunter_default_version)
include(hunter_user_error)

# NOTE: no names with spaces!

hunter_default_version(ARM_NEON_2_x86_SSE VERSION 1.0.0-p0)
hunter_default_version(AllTheFlopsThreads VERSION 0.1-p0)
hunter_default_version(Alut VERSION 1.1.0-469287b-p0)
hunter_default_version(Android-Apk VERSION 1.1.14)
hunter_default_version(Android-Build-Tools VERSION 27.0.3)
hunter_default_version(Android-Google-Repository VERSION 58)
hunter_default_version(Android-Modules VERSION 1.0.0)
hunter_default_version(Android-SDK VERSION 0.0.6)
hunter_default_version(Android-SDK-Platform-tools VERSION r28.0.0)
hunter_default_version(Android-SDK-Tools VERSION 25.2.5)
hunter_default_version(Android-Support-Repository VERSION 47)
hunter_default_version(AngelScript VERSION 2.30-p0)
hunter_default_version(ArrayFire VERSION 3.3.1-p0)
hunter_default_version(Assimp VERSION 5.2.5-9519a62)
hunter_default_version(Async++ VERSION 0.0.3-hunter)
hunter_default_version(Avahi VERSION 0.6.31)
hunter_default_version(BZip2 VERSION 1.0.8-p0)
hunter_default_version(Beast VERSION 1.0.0-b84-hunter-0)

if(MINGW)
  # https://github.com/boostorg/build/issues/301
  hunter_default_version(Boost VERSION 1.64.0)
else()
  hunter_default_version(Boost VERSION 1.83.0)
endif()

hunter_default_version(BoostCompute VERSION 0.5-p0)
hunter_default_version(BoostProcess VERSION 0.5)
hunter_default_version(BoringSSL VERSION 0.0.0-0f5ecd3a8-p0)
hunter_default_version(Box2D VERSION 2.3.1-p0)
hunter_default_version(CLAPACK VERSION 3.2.1)
hunter_default_version(CLI11 VERSION 2.3.2)
hunter_default_version(CURL VERSION 8.5.0-p0)
hunter_default_version(CapnProto VERSION 0.7.0)
hunter_default_version(Catch VERSION 2.13.9)
hunter_default_version(Clang VERSION 6.0.1-p0)
hunter_default_version(ClangToolsExtra VERSION 6.0.1) # Clang
hunter_default_version(Comet VERSION 4.0.2)
hunter_default_version(CppNetlib VERSION 0.10.1-hunter-3)
hunter_default_version(CppNetlibUri VERSION 1.0.5-hunter)
hunter_default_version(CreateLaunchers VERSION 0.2.1)
hunter_default_version(CsvParserCPlusPlus VERSION 1.0.1)
hunter_default_version(EGL-Registry VERSION 0.0.0-dc0b58d-p0)
hunter_default_version(Eigen VERSION 3.4.0)
hunter_default_version(Expat VERSION 2.2.9-p0)
hunter_default_version(FLAC VERSION 1.3.4-p0)
hunter_default_version(FP16 VERSION 0.0.0-febbb1c-p0)
hunter_default_version(FakeIt VERSION 2.0.3)
hunter_default_version(Fruit VERSION 3.1.1-p0)
hunter_default_version(FunctionalPlus VERSION 0.2-p0)
hunter_default_version(GPUImage VERSION 0.1.6-p9)
hunter_default_version(GSL VERSION 2.1.0-p2)

if(MSVC80)
  hunter_default_version(GTest VERSION 1.7.0-hunter-6)
else()
  hunter_default_version(GTest VERSION 1.15.2)
endif()

hunter_default_version(HalideIR VERSION 0.0-32057b5-p0)
hunter_default_version(HastyNoise VERSION 0.8.3)
hunter_default_version(ICU VERSION 63.1-p5)
hunter_default_version(IF97 VERSION 2.1.2)
hunter_default_version(Igloo VERSION 1.1.1-hunter)
hunter_default_version(IlmBase VERSION 2.5.1-p0)
hunter_default_version(Imath VERSION 3.1.5)
hunter_default_version(Immer VERSION 0.6.2-cf44615)
hunter_default_version(Jpeg VERSION 9e-p0)
hunter_default_version(JsonSpirit VERSION 0.0.4-hunter)
hunter_default_version(KTX-Software VERSION 4.0.0-efc9f09-p0)
hunter_default_version(KhronosDataFormat VERSION 1.3.1-1f8c852-p3)
hunter_default_version(LAPACK VERSION 3.7.1)
hunter_default_version(LLVM VERSION 13.0.1) # Clang
hunter_default_version(LLVMCompilerRT VERSION 6.0.1) # Clang
hunter_default_version(Lager VERSION 0.0.0-dbc1fde-p0)
hunter_default_version(Leathers VERSION 0.1.8)
hunter_default_version(Leptonica VERSION 1.74.2-p4)
hunter_default_version(LibCDS VERSION 2.3.1)
hunter_default_version(Libcxx VERSION 3.6.2) # Clang
hunter_default_version(Libcxxabi VERSION 3.6.2) # Clang
hunter_default_version(Libevent VERSION 2.1.8-p4)
hunter_default_version(Libssh2 VERSION 1.9.0-p0)
hunter_default_version(LodePNG VERSION 0.0.0-p1)
hunter_default_version(Lua VERSION 5.3.5)
hunter_default_version(MathFu VERSION 1.1.0-p0)
hunter_default_version(Microsoft.GSL VERSION 2.0.0-p0)
hunter_default_version(MySQL-client VERSION 6.1.9-p1)
hunter_default_version(NASM VERSION 2.15.02)
hunter_default_version(NLopt VERSION 2.5.0-p0)
hunter_default_version(ONNX VERSION 1.4.1-p0)
hunter_default_version(OpenAL VERSION 1.23.1)
hunter_default_version(OpenBLAS VERSION 0.3.27)
hunter_default_version(OpenCL VERSION 2022.01.04-p1)
hunter_default_version(OpenCL-Headers VERSION 2022.01.04)
hunter_default_version(OpenCL-cpp VERSION 2.0.16-61a5c9a-p0)
if(MSVC)
  hunter_default_version(OpenCV VERSION 4.10.0-p0)
  hunter_default_version(OpenCV-Extra VERSION 4.10.0)
else()
  # 4.10.0 has a build problem with TIFF header defines
  hunter_default_version(OpenCV VERSION 4.8.1-p0)
  hunter_default_version(OpenCV-Extra VERSION 4.8.1)
endif()
hunter_default_version(OpenEXR VERSION 3.1.5-p0)
hunter_default_version(OpenGL-Registry VERSION 0.0.0-d15191e-p0)
hunter_default_version(OpenNMTTokenizer VERSION 1.11.0-p1)
hunter_default_version(OpenSSL VERSION 3.0.12)
hunter_default_version(OpenSceneGraph VERSION 3.6.3-p0)
hunter_default_version(Opus VERSION 1.3.1)
hunter_default_version(PNG VERSION 1.6.26-p6)
hunter_default_version(PROJ4 VERSION 5.0.0)
hunter_default_version(PhysUnits VERSION 1.1.0-p0)
hunter_default_version(PocoCpp VERSION 1.10.1-p0)
hunter_default_version(PostgreSQL VERSION 10.0.0)
hunter_default_version(Protobuf VERSION 3.19.4-p0)

string(COMPARE EQUAL "${CMAKE_SYSTEM_NAME}" "Linux" _is_linux)
if(_is_linux OR MINGW)
  # qt-qml example is broken on Linux
  # qt-core example is broken on MinGW
  hunter_default_version(Qt VERSION 5.5.1-cvpixelbuffer-2-p9)
elseif(IOS OR ANDROID)
  hunter_default_version(Qt VERSION 5.9.1-p0)
else()
  hunter_default_version(Qt VERSION 5.11.3)
endif()

hunter_default_version(QtAndroidCMake VERSION 1.0.9)
hunter_default_version(QtCMakeExtra VERSION 1.0.34)
hunter_default_version(QtPropertyEditor VERSION 2.1.3-p0)
hunter_default_version(QtQmlManager VERSION 1.0.0)
hunter_default_version(Qwt VERSION 6.1-p3)
hunter_default_version(RapidJSON VERSION 1.1.0-b557259-p0)
hunter_default_version(RapidXML VERSION 1.13)
hunter_default_version(RedisClient VERSION 0.6.1-p1)
hunter_default_version(SDL2 VERSION 2.30.2)
hunter_default_version(SDL_image VERSION 2.0.5-p0)
hunter_default_version(SDL_mixer VERSION 2.0.4-p0)
hunter_default_version(SDL_net VERSION 2.2.0-p0)
hunter_default_version(SDL_ttf VERSION 2.0.18-p0)
hunter_default_version(SFML VERSION 2.5.1-p0)
hunter_default_version(SPIRV-Headers VERSION 1.5.4.raytracing.fixed)
hunter_default_version(SPIRV-Tools VERSION 2020.4-p0)
hunter_default_version(SimpleSignal VERSION 0.0.0-79c3f68-p1)
hunter_default_version(Snappy VERSION 1.1.7)
hunter_default_version(Sober VERSION 0.1.3)
hunter_default_version(Sqlpp11 VERSION 0.57-p0)
hunter_default_version(SuiteSparse VERSION 7.5.1-1)
hunter_default_version(TCLAP VERSION 1.2.2-p1)
hunter_default_version(TIFF VERSION 4.0.2-p5)
hunter_default_version(Tesseract VERSION 3.05.01-hunter-3)
hunter_default_version(Urho3D VERSION 1.7-p15)
hunter_default_version(Vulkan-Headers VERSION 1.2.182-p0)
hunter_default_version(VulkanMemoryAllocator VERSION 2.3.0-p0)
hunter_default_version(WDC VERSION 1.1.5)
hunter_default_version(WTL VERSION 9.1.5321)
hunter_default_version(Washer VERSION 0.1.2)
hunter_default_version(WebKit VERSION 0.0.2-p0)
hunter_default_version(WebP VERSION 1.2.4-p0)
hunter_default_version(WinSparkle VERSION 0.4.0)
hunter_default_version(YAJL VERSION 2.1.0-p0)
hunter_default_version(ZLIB VERSION 1.3.0-p0)
hunter_default_version(ZMQPP VERSION 4.2.0-p0)
hunter_default_version(ZeroMQ VERSION 4.2.3-p1)
hunter_default_version(Zug VERSION 0.0.1-be20cae)

hunter_default_version(abseil VERSION 20240116.2)
hunter_default_version(acf VERSION 0.1.14)
hunter_default_version(actionlib VERSION 1.11.13-p0)
hunter_default_version(aes VERSION 0.0.1-p1)
hunter_default_version(aglet VERSION 1.2.2)
hunter_default_version(android_arm64_v8a_system_image_packer VERSION 1.0.0)
hunter_default_version(android_arm_eabi_v7a_system_image_packer VERSION 1.0)
hunter_default_version(android_build_tools_packer VERSION 1.0.0)
hunter_default_version(android_google_apis_intel_x86_atom_system_image_packer VERSION 1.0.0)
hunter_default_version(android_google_apis_packer VERSION 1.0.0)
hunter_default_version(android_google_repository_packer VERSION 1.0.0)
hunter_default_version(android_intel_x86_atom_system_image_packer VERSION 1.0.0)
hunter_default_version(android_mips_system_image_packer VERSION 1.0.0)
hunter_default_version(android_sdk_packer VERSION 1.0.0)
hunter_default_version(android_sdk_platform_packer VERSION 1.0.0)
hunter_default_version(android_sdk_platform_tools_packer VERSION 1.0.0)
hunter_default_version(android_sdk_tools_packer VERSION 1.0.3)
hunter_default_version(android_support_repository_packer VERSION 1.0.0)
hunter_default_version(angles VERSION 1.9.11-p0)
hunter_default_version(apg VERSION 0.0.0-b322f7a-p0)
hunter_default_version(arabica VERSION 0.0.0-a202766-p0)
hunter_default_version(asio VERSION 1.22.1-p1)
hunter_default_version(asio-grpc VERSION 2.6.0)
hunter_default_version(astc-encoder VERSION 3.0-7257cbd-p0)
hunter_default_version(autobahn-cpp VERSION 0.2.0)
hunter_default_version(autoutils VERSION 0.3.0)
hunter_default_version(aws-c-common VERSION 0.5.6)
hunter_default_version(aws-sdk-cpp VERSION 1.9.278-p1)
hunter_default_version(aws_lambda_cpp VERSION v0.2.7-p0)
hunter_default_version(basis_universal VERSION 1.16.3-p0)
hunter_default_version(benchmark VERSION 1.8.3)
hunter_default_version(bento4 VERSION 1.6.0-638-p0)
hunter_default_version(binaryen VERSION 1.38.28-p1)
hunter_default_version(bison VERSION 3.0.4-p0)
hunter_default_version(boost-pba VERSION 1.0.0-p0)
hunter_default_version(botan VERSION 2.11.0-110af9494)
hunter_default_version(breakpad VERSION 0.0.0-12ecff3-p4)
hunter_default_version(brotli VERSION 1.0.9-p0)
hunter_default_version(bullet VERSION 2.87-p0)
hunter_default_version(byte-lite VERSION 0.3.0-p0)
hunter_default_version(c-ares VERSION 1.14.0-p0)
hunter_default_version(caffe VERSION rc3-p2)
hunter_default_version(catkin VERSION 0.7.17-p0)
hunter_default_version(cctz VERSION 2.2.0)
hunter_default_version(ccv VERSION 0.7-p6)
hunter_default_version(cereal VERSION 1.2.2-p0)
if(CMAKE_CXX_COMPILER_ID STREQUAL "GNU" AND CMAKE_CXX_COMPILER_VERSION VERSION_LESS "8.0")
  # Ubuntu 18.04 GCC compiler isn't C++17 conformant enough, stay at lower version
  # - Ubuntu 18.04 disablement: https://github.com/ceres-solver/ceres-solver/commit/40c1a7e18ee040261f87b32374c9a46724ca2214
  # - C++17 requirement: https://github.com/ceres-solver/ceres-solver/commit/1274743609bc59621adc9e311cdeeaad7eb65201
  hunter_default_version(ceres-solver VERSION 2.1.0-p1)
else()
  hunter_default_version(ceres-solver VERSION 2.2.0-p2)
endif()
hunter_default_version(cgltf VERSION 1.10-f9a8804-p0)
hunter_default_version(check_ci_tag VERSION 1.0.0)
hunter_default_version(chromium_zlib VERSION 0.0.0-f87c2b10efb4-p0)
hunter_default_version(civetweb VERSION 1.11-p0)
hunter_default_version(clBLAS VERSION 2.10.0-p0)
hunter_default_version(class_loader VERSION 0.4.1-p0)
hunter_default_version(cmcstl2 VERSION 0.0.0-bee0705e99)
hunter_default_version(complex_bessel VERSION 0.5.0-abab4b5)
hunter_default_version(convertutf VERSION 1.0.1)
hunter_default_version(corrade VERSION 2019.10)
hunter_default_version(cpp-statsd-client VERSION 1.0.1-42f02b4-p0)
hunter_default_version(cpp_redis VERSION 3.5.0-h1)
hunter_default_version(cppast VERSION 0.0.0-b155d6a-p0)
hunter_default_version(cppcodec VERSION 0.2-p0)
hunter_default_version(cppfs VERSION 1.3.0)
hunter_default_version(cpr VERSION 1.3.0)
hunter_default_version(cpuinfo VERSION 0.0.0-d5e37ad-p0)
hunter_default_version(crashpad VERSION v0.0.1-p0)
hunter_default_version(crashup VERSION 0.0.2)
hunter_default_version(crc32c VERSION 1.1.1)
hunter_default_version(cryptopp VERSION 8.2.0-p1)
hunter_default_version(ctti VERSION 0.0.2)
hunter_default_version(cub VERSION 1.8.0-p0)
hunter_default_version(cvmatio VERSION 1.0.28)
hunter_default_version(cvsteer VERSION 0.1.2)
hunter_default_version(cxxopts VERSION 2.2.0)
hunter_default_version(czmq VERSION 4.0.2-p1)
hunter_default_version(damageproto VERSION 1.2.1)
hunter_default_version(date VERSION 3.0.1)
hunter_default_version(dbus VERSION 1.10.0-hunter-4)
hunter_default_version(debug_assert VERSION 1.3.2)
hunter_default_version(dest VERSION 0.8.0-p4)
hunter_default_version(dfdutils VERSION 0.0.0-659a739-p1)
hunter_default_version(dlib VERSION 19.17-p0)
hunter_default_version(dlpack VERSION 0.2-0acb731)
hunter_default_version(dmlc-core VERSION 0.3-3943914-p0)
hunter_default_version(doctest VERSION 2.4.9)
hunter_default_version(double-conversion VERSION 3.1.4)
hunter_default_version(draco VERSION 1.4.1-p0)
hunter_default_version(dri2proto VERSION 2.8)
hunter_default_version(dri3proto VERSION 1.0)
hunter_default_version(drishti VERSION 0.8.9)
hunter_default_version(drishti_assets VERSION 1.8)
hunter_default_version(drishti_faces VERSION 1.2)
hunter_default_version(drm VERSION 2.4.94)
hunter_default_version(duktape VERSION 2.2.1-p0)
hunter_default_version(dynalo VERSION 1.0.3)
hunter_default_version(eigen3-nnls VERSION 1.0.1)
hunter_default_version(enet VERSION 1.3.13-p1)
hunter_default_version(entityx VERSION 1.3.0-p1)
hunter_default_version(eos VERSION 0.12.1)
hunter_default_version(etc2comp VERSION 0.0.0-9cd0f9c-p0)
hunter_default_version(ethash VERSION 1.0.0)
hunter_default_version(eventpp VERSION 0.1.2-for-hunter-pm)
hunter_default_version(eyalroz_printf VERSION 6.2.0)
hunter_default_version(farmhash VERSION 1.1)
hunter_default_version(fast_obj VERSION 1.1-9255172-p0)
hunter_default_version(ffmpeg VERSION n4.1-dev-45499e557c-p7)
hunter_default_version(fft2d VERSION 1.0.0-p0)
hunter_default_version(filament VERSION 1.9.8)
hunter_default_version(fixesproto VERSION 5.0)
hunter_default_version(flatbuffers VERSION 2.0.0)
hunter_default_version(flex VERSION 2.6.4)
hunter_default_version(fmt VERSION 10.1.1)
hunter_default_version(folly VERSION 2018.10.22.00-p4)
hunter_default_version(freetype VERSION 2.10.4-p0)
hunter_default_version(freetype-gl VERSION 0.0.0-1a8c007-p0)
hunter_default_version(frugally-deep VERSION 0.2.2-p0)
hunter_default_version(gRPC VERSION 1.44.0-p0)
hunter_default_version(gauze VERSION 0.7.1)
hunter_default_version(gemmlowp VERSION 1.0.0)
hunter_default_version(geos VERSION 3.4.2)
hunter_default_version(getopt VERSION 1.0.0-p0)
hunter_default_version(gflags VERSION 2.2.2)
hunter_default_version(giflib VERSION 5.2.1-p0)
hunter_default_version(gl4es VERSION 1.1.4-p1)
hunter_default_version(glbinding VERSION 3.1.0-p0)
hunter_default_version(glew VERSION 2.0.0-p1)
hunter_default_version(glfw VERSION 3.3.4-p0)
hunter_default_version(glib VERSION 2.54.0)
hunter_default_version(glm VERSION 0.9.9.8)
hunter_default_version(globjects VERSION 1.1.0-p0)
hunter_default_version(glog VERSION 0.6.0)
hunter_default_version(glproto VERSION 1.4.17)
hunter_default_version(glslang VERSION 8.13.3743-9eef54b2-p0)
hunter_default_version(glu VERSION 9.0.1-p1)
hunter_default_version(gsl-lite VERSION 0.40.0-p0)
hunter_default_version(gst_plugins_bad VERSION 1.10.4)
hunter_default_version(gst_plugins_base VERSION 1.10.4)
hunter_default_version(gst_plugins_good VERSION 1.10.4)
hunter_default_version(gst_plugins_ugly VERSION 1.10.4)
hunter_default_version(gstreamer VERSION 1.10.4)
hunter_default_version(gumbo VERSION 0.10.1)
hunter_default_version(h3 VERSION 3.0.7)
hunter_default_version(half VERSION 1.1.0-p1)
hunter_default_version(harfbuzz VERSION 2.9.1-p0)
hunter_default_version(hdf5 VERSION 1.8.15-p1)
hunter_default_version(highwayhash VERSION 0.0.0)
hunter_default_version(http-parser VERSION 2.8.0)
hunter_default_version(hunter_venv VERSION 1.0.2)
hunter_default_version(hypre VERSION 2.22.0)
hunter_default_version(ice VERSION 1.0.9)
hunter_default_version(icu-le-hb VERSION 1.0.3-231788a-p0)
hunter_default_version(icu-lx VERSION 63.1-p1)
hunter_default_version(imagequant VERSION 2.15.1-p0)
hunter_default_version(imgui VERSION 1.70.p0)
hunter_default_version(imshow VERSION 1.0.0-p0)
hunter_default_version(inja VERSION 0.1.1)
hunter_default_version(inputproto VERSION 2.3)
hunter_default_version(intltool VERSION 0.51.0)
hunter_default_version(intsizeof VERSION 2.0.2)
hunter_default_version(intx VERSION 0.9.0)
hunter_default_version(ios_sim VERSION 3.1.1)
if(MSVC)
  hunter_default_version(ippicv VERSION 20240201)
else()
  # see OpenCV for more info
  hunter_default_version(ippicv VERSION 20230330)
endif()
hunter_default_version(iroha-ed25519 VERSION 2.0.0)
hunter_default_version(irrXML VERSION 1.2-p0)
hunter_default_version(ittapi VERSION 3.21.2-p0)
hunter_default_version(jaegertracing VERSION 0.4.1)
hunter_default_version(jansson VERSION 2.11.0)
hunter_default_version(jasper VERSION 2.0.32-p0)
hunter_default_version(jo_jpeg VERSION 0.0.1)
hunter_default_version(jpeg-compressor VERSION 0.0.0-aeb7d3b-p0)
hunter_default_version(jsmn VERSION 1.1.0-053d3cd-p0)

if(MSVC_VERSION LESS 1600)
  # for VS10 - version without support C++11
  hunter_default_version(jsoncpp VERSION 0.7.0)
else()
  hunter_default_version(jsoncpp VERSION 1.9.5-b1)
endif()

hunter_default_version(jwt-cpp VERSION 0.6.0)
hunter_default_version(kNet VERSION 2.7-p1)
hunter_default_version(kbproto VERSION 1.0.7)
hunter_default_version(lcms VERSION 2.13.1-p0)
hunter_default_version(lehrfempp VERSION 0.8.0)
hunter_default_version(leveldb VERSION 1.22-p1)
hunter_default_version(libarchive VERSION 3.4.3)
hunter_default_version(libbacktrace VERSION 1.0.0-ca0de051)
hunter_default_version(libcpuid VERSION 0.4.0)
hunter_default_version(libdaemon VERSION 0.14)
hunter_default_version(libdill VERSION 1.6)
hunter_default_version(libevhtp VERSION 1.2.16-p4)
hunter_default_version(libffi VERSION 3.2.1)
hunter_default_version(libigl VERSION 2.2.0)
hunter_default_version(libjpeg-turbo VERSION 2.1.0)
hunter_default_version(libjson-rpc-cpp VERSION 0.7.0-p3)
hunter_default_version(libmill VERSION 1.18)
hunter_default_version(libogg VERSION 1.3.3-p0)
hunter_default_version(libpcre VERSION 8.41)
hunter_default_version(librtmp VERSION 2.4.0-p0)
hunter_default_version(libscrypt VERSION 1.21-p1)
hunter_default_version(libsodium VERSION 1.0.16-p0)
hunter_default_version(libunibreak VERSION 4.0)
hunter_default_version(libusb VERSION 1.0.23)
hunter_default_version(libuv VERSION 1.42.0-p0)
hunter_default_version(libxdg-basedir VERSION 1.2.3)
hunter_default_version(libxml2 VERSION 2.9.7-p0)
hunter_default_version(libyuv VERSION 1514-p3)
hunter_default_version(libzip VERSION 1.5.2-d68a667-p0)
hunter_default_version(lmdb VERSION 0.9.21-p2)
hunter_default_version(lmdbxx VERSION 0.9.14.0)
hunter_default_version(log4cplus VERSION 1.2.0-p0)
hunter_default_version(lss VERSION 0.0.0-e1e7b0a-p0)
hunter_default_version(lz4 VERSION 1.9.2-p0)
hunter_default_version(lzma VERSION 5.2.3-p4)
hunter_default_version(magnum VERSION 2019.01)
hunter_default_version(md5 VERSION 1.6)
hunter_default_version(meshoptimizer VERSION 0.16-86740c2-p0)
hunter_default_version(mini_chromium VERSION 0.0.1-p2)
hunter_default_version(miniz VERSION 3.0.2)
hunter_default_version(minizip VERSION 1.0.1-p3)
hunter_default_version(mkl VERSION 20190502)
hunter_default_version(mkldnn VERSION 0.19-p0)
hunter_default_version(mng VERSION 2.0.3-p2)
hunter_default_version(mojoshader VERSION 0.0.1)
hunter_default_version(mongoose VERSION 6.10)
hunter_default_version(mpark_variant VERSION 1.0.0)
hunter_default_version(msgpack VERSION 1.4.1-p2)
hunter_default_version(mshadow VERSION 1.1-1d79ecf-p0)
hunter_default_version(mtplz VERSION 0.1-p3)
hunter_default_version(mxnet VERSION 1.5.0.rc1-b64e00a-p0)
hunter_default_version(nanoflann VERSION 1.2.3-p0)
hunter_default_version(nanosvg VERSION 0.0.0-2b08dee-p0)
hunter_default_version(ncnn VERSION 20180314-p2)
hunter_default_version(ncursesw VERSION 6.1)
hunter_default_version(nlohmann_fifo_map VERSION 0.0.0-0dfbf5d-p1)
hunter_default_version(nlohmann_json VERSION 3.11.2)
hunter_default_version(nng VERSION 1.1.1)
hunter_default_version(nsync VERSION 1.14-p1)
hunter_default_version(occt VERSION 7.4.0-p0)
hunter_default_version(odb VERSION 2.4.0)
hunter_default_version(odb-boost VERSION 2.4.0)
hunter_default_version(odb-compiler VERSION 2.4.0)
hunter_default_version(odb-mysql VERSION 2.4.0)
hunter_default_version(odb-pgsql VERSION 2.4.0)
hunter_default_version(odb-sqlite VERSION 2.4.0)
hunter_default_version(ogles_gpgpu VERSION 0.3.6)
hunter_default_version(oneTBB VERSION 2021.5.0)
hunter_default_version(oniguruma VERSION 6.8.1-p0)
hunter_default_version(onmt VERSION 0.4.1-p2)
hunter_default_version(openddlparser VERSION 0.1.0-p2)
hunter_default_version(opentracing-cpp VERSION 1.6.0)
hunter_default_version(opusfile VERSION 0.12-p2)
hunter_default_version(pcg VERSION 0.0.0-p1)
hunter_default_version(pciaccess VERSION 0.13.4)
hunter_default_version(pcre2 VERSION 10.13-p0)
hunter_default_version(pegtl VERSION 2.8.1)

# pip packages
hunter_default_version(pip_GitPython VERSION 2.1.11)
hunter_default_version(pip_astroid VERSION 2.2.5)
hunter_default_version(pip_boto3 VERSION 1.9.130)
hunter_default_version(pip_botocore VERSION 1.12.130)
hunter_default_version(pip_certifi VERSION 2019.3.9)
hunter_default_version(pip_chardet VERSION 3.0.4)
hunter_default_version(pip_cpplint VERSION 1.4.4)
hunter_default_version(pip_decorator VERSION 4.4.0)
hunter_default_version(pip_gitdb VERSION 2.0.5)
hunter_default_version(pip_idna VERSION 2.8)
hunter_default_version(pip_jmespath VERSION 0.9.4)
hunter_default_version(pip_lazy-object-proxy VERSION 1.3.1)
hunter_default_version(pip_nose VERSION 1.3.7)
hunter_default_version(pip_nose-timer VERSION 0.7.5)
hunter_default_version(pip_numpy VERSION 1.17.5)
hunter_default_version(pip_pylint VERSION 2.3.1)
hunter_default_version(pip_python-dateutil VERSION 2.8.0)
hunter_default_version(pip_requests VERSION 2.21.0)
hunter_default_version(pip_six VERSION 1.12.0)
hunter_default_version(pip_smmap VERSION 2.0.5)
hunter_default_version(pip_urllib3 VERSION 1.24.1)
hunter_default_version(pip_wrapt VERSION 1.11.1)

hunter_default_version(pluginlib VERSION 1.12.1-p0)
hunter_default_version(poly2tri VERSION 1.0.0)
hunter_default_version(polyclipping VERSION 4.8.8-p0) # for Assimp
hunter_default_version(presentproto VERSION 1.0)
hunter_default_version(prometheus-cpp VERSION 0.6.0-p2)
hunter_default_version(protobuf-c VERSION 1.3.0-p1)
hunter_default_version(pthread-stubs VERSION 0.4)
hunter_default_version(pthreads-win32 VERSION 2.9.1-7ad2af7-p0)
hunter_default_version(pugixml VERSION 1.10-p0)
hunter_default_version(pybind11 VERSION 2.11.1)
hunter_default_version(qhull VERSION 7.2.0-p1)
hunter_default_version(quickjs VERSION 2020-04-12-p0)
hunter_default_version(rabbitmq-c VERSION 0.10.0)
hunter_default_version(rabit VERSION 0.0.0-p2)
hunter_default_version(randrproto VERSION 1.3.2)
hunter_default_version(rang VERSION 3.1.0-p0)

if(MSVC)
  if(MSVC_VERSION LESS 1916)
    hunter_default_version(range-v3 VERSION vcpkg5-p)
  else()
    hunter_default_version(range-v3 VERSION 0.12.0)
  endif()
else()
  hunter_default_version(range-v3 VERSION 0.12.0)
endif()

hunter_default_version(re2 VERSION 2023.03.01)
hunter_default_version(readline VERSION 6.3)
hunter_default_version(recastnavigation VERSION 1.4-p0)
hunter_default_version(renderproto VERSION 0.11.1)
hunter_default_version(rocksdb VERSION 7.5.3)
hunter_default_version(ros VERSION 1.14.6-p0)
hunter_default_version(ros_comm VERSION 1.14.3-p1)
hunter_default_version(ros_comm_msgs VERSION 1.11.2-p0)
hunter_default_version(ros_common_msgs VERSION 1.12.7-p0)
hunter_default_version(ros_console_bridge VERSION 0.4.3-p0)
hunter_default_version(ros_environment VERSION 1.2.1-p0)
hunter_default_version(ros_gencpp VERSION 0.6.2-p0)
hunter_default_version(ros_geneus VERSION 2.2.6-p0)
hunter_default_version(ros_genlisp VERSION 0.4.16-p0)
hunter_default_version(ros_genmsg VERSION 0.5.12-p0)
hunter_default_version(ros_gennodejs VERSION 2.0.1-p0)
hunter_default_version(ros_genpy VERSION 0.6.8-p0)
hunter_default_version(ros_message_generation VERSION 0.4.0-p0)
hunter_default_version(ros_message_runtime VERSION 0.4.12-p0)
hunter_default_version(ros_std_msgs VERSION 0.5.12-p0)
hunter_default_version(rosconsole VERSION 1.13.10-p0)
hunter_default_version(roscpp_core VERSION 0.6.12-p0)
hunter_default_version(rospack VERSION 2.5.3-p0)
hunter_default_version(s3 VERSION 4.1.0-287e4be-p1)
hunter_default_version(scelta VERSION 0.1.0-a0f4f70-p0)
hunter_default_version(sds VERSION 2.0.0)
hunter_default_version(sentencepiece VERSION 0.1.8-p1)
hunter_default_version(sentry VERSION 0.4.9-p0)
hunter_default_version(shaderc VERSION 2019.0-p1)
hunter_default_version(shaka_player_embedded VERSION 0.1.0-beta-p1)
hunter_default_version(sleef VERSION 3.3.1-p1)
hunter_default_version(sm VERSION 1.2.3)
hunter_default_version(smol-v VERSION 0.0.0-4b52c16-p0)
hunter_default_version(soil VERSION 1.0.4)
hunter_default_version(sources_for_android_sdk_packer VERSION 1.0.0)
hunter_default_version(sparsehash VERSION 2.0.2)

if(MSVC_VERSION LESS 1800)
  # for VS12 - version without support C++11
  hunter_default_version(spdlog VERSION 1.0.0-p0)
else()
  hunter_default_version(spdlog VERSION 1.12.0-p0)
endif()

hunter_default_version(spirv-cross VERSION 20210115)
hunter_default_version(sqlite3 VERSION 3.43.2-p0)
hunter_default_version(sse2neon VERSION 1.0.0-p0)
hunter_default_version(stanhull VERSION 0.0.1)
hunter_default_version(state_machine VERSION 1.1)
hunter_default_version(stb VERSION 0.0.0-80c8f6a-p0)
hunter_default_version(stdext-path VERSION 0.0.1-p0)
hunter_default_version(stormlib VERSION 9.21-p1)
hunter_default_version(sugar VERSION 1.3.0)
hunter_default_version(szip VERSION 2.1.0-p1)
hunter_default_version(tacopie VERSION 3.2.0-h1)
hunter_default_version(taocpp-json VERSION 1.0.0-beta.11-e0895587)
hunter_default_version(taskflow VERSION 3.3.0)
hunter_default_version(tcl VERSION core8.6.8)
hunter_default_version(termcolor VERSION 1.0.1)
hunter_default_version(tf VERSION 1.12.0-p0)
hunter_default_version(tf2 VERSION 0.6.5-p0)
hunter_default_version(theora VERSION 1.1.1-p0)
hunter_default_version(thread-pool-cpp VERSION 1.1.0)
hunter_default_version(thrift VERSION 0.12.0-p0)
hunter_default_version(tiny-process-library VERSION 2.0.2-p0)
hunter_default_version(tinydir VERSION 1.2-p0)
hunter_default_version(tinyexr VERSION 1.0.0-3c33352-p1)
hunter_default_version(tinygltf VERSION 2.5.0-p0)
hunter_default_version(tinyobjloader VERSION 2.0.0-rc6-bec38e3)
hunter_default_version(tinyrefl VERSION 0.4.1-p0)
hunter_default_version(tinyxml2 VERSION 9.0.0)
hunter_default_version(tmxparser VERSION 2.1.0-ab4125b-p1)
hunter_default_version(toluapp VERSION 1.0.93-p1)
hunter_default_version(tomcrypt VERSION 1.18.2-p1)
hunter_default_version(tommath VERSION 1.0.1-p0)
hunter_default_version(tsl_hat_trie VERSION 0.6.0-1739fa1-p0)
hunter_default_version(tsl_robin_map VERSION 0.6.3-dc2023b)
hunter_default_version(tvm VERSION 0.5-a4bc50e-p0)
hunter_default_version(type_safe VERSION 0.2.1-p2)
hunter_default_version(units VERSION 2.3.1)
hunter_default_version(uriparser VERSION 0.9.5)
hunter_default_version(utf8 VERSION 3.1.1)
hunter_default_version(util_linux VERSION 2.30.1)
hunter_default_version(uuid VERSION 1.0.3)
hunter_default_version(v8 VERSION 7.4.98-p3)
hunter_default_version(vectorial VERSION 0.0.0-ae7dc88-p0)
hunter_default_version(vorbis VERSION 1.3.6-p1)
hunter_default_version(vurtun-lib VERSION 0.0.0-f1cda26-p0)
hunter_default_version(websocketpp VERSION 0.8.1-p0)
hunter_default_version(wt VERSION 4.0.4-p0)
hunter_default_version(wxWidgets VERSION 3.0.2)
hunter_default_version(wyrm VERSION 0.1.0)
hunter_default_version(x11 VERSION 1.6.7)
hunter_default_version(x264 VERSION snapshot-20190513-2245)
hunter_default_version(xatlas VERSION 0.0.0-4077f0e-p0)
hunter_default_version(xau VERSION 1.0.9)
hunter_default_version(xcb VERSION 1.13)
hunter_default_version(xcb-proto VERSION 1.13)
hunter_default_version(xcursor VERSION 1.1.13)
hunter_default_version(xdamage VERSION 1.1.4)
hunter_default_version(xext VERSION 1.3.1)
hunter_default_version(xextproto VERSION 7.3.0)
hunter_default_version(xf86vidmodeproto VERSION 2.3.1)
hunter_default_version(xfixes VERSION 5.0.3)
hunter_default_version(xgboost VERSION 0.7.0-p4)
hunter_default_version(xi VERSION 1.6.1)
hunter_default_version(xinerama VERSION 1.1.2)
hunter_default_version(xineramaproto VERSION 1.1.2)
hunter_default_version(xorg-macros VERSION 1.19.2)
hunter_default_version(xproto VERSION 7.0.31)
hunter_default_version(xrandr VERSION 1.3.2)
hunter_default_version(xrender VERSION 0.9.7)
hunter_default_version(xshmfence VERSION 1.3)
hunter_default_version(xtrans VERSION 1.4.0)
hunter_default_version(xxHash VERSION 0.8.2)
hunter_default_version(xxf86vm VERSION 1.1.2)
hunter_default_version(yaml-cpp VERSION 0.6.3)
hunter_default_version(zip VERSION 0.1.15)
hunter_default_version(zlog VERSION 1.2.14)
hunter_default_version(zookeeper VERSION 3.4.9-p2)
hunter_default_version(zstd VERSION 1.5.5)

if(ANDROID)
  string(COMPARE EQUAL "${CMAKE_SYSTEM_VERSION}" "" _is_empty)
  if(_is_empty)
    hunter_user_error("CMAKE_SYSTEM_VERSION is empty")
  endif()

  string(COMPARE EQUAL "${CMAKE_SYSTEM_VERSION}" "24" _is_api_24)
  string(COMPARE EQUAL "${CMAKE_SYSTEM_VERSION}" "22" _is_api_22)
  string(COMPARE EQUAL "${CMAKE_SYSTEM_VERSION}" "21" _is_api_21)
  string(COMPARE EQUAL "${CMAKE_SYSTEM_VERSION}" "19" _is_api_19)
  string(COMPARE EQUAL "${CMAKE_SYSTEM_VERSION}" "16" _is_api_16)

  set(__HUNTER_LAST_DEFAULT_VERSION_NAME "") # Reset alphabetical order checker

  if(_is_api_21)
    hunter_default_version(Android-ARM-EABI-v7a-System-Image VERSION 21_r04)
    hunter_default_version(Android-Google-APIs VERSION 21_r01)
    hunter_default_version(Android-Google-APIs-Intel-x86-Atom-System-Image VERSION 21_r10)
    hunter_default_version(Android-Intel-x86-Atom-System-Image VERSION 21_r05)
    hunter_default_version(Android-SDK-Platform VERSION 21_r02)
    hunter_default_version(Sources-for-Android-SDK VERSION 21)
  elseif(_is_api_19)
    hunter_default_version(Android-ARM-EABI-v7a-System-Image VERSION 19_r05)
    hunter_default_version(Android-Google-APIs VERSION 19_r18)
    hunter_default_version(Android-Intel-x86-Atom-System-Image VERSION 19)
    hunter_default_version(Android-SDK-Platform VERSION 19_r04)
    hunter_default_version(Sources-for-Android-SDK VERSION 19)
  elseif(_is_api_16)
    hunter_default_version(Android-ARM-EABI-v7a-System-Image VERSION 16_r04)
    hunter_default_version(Android-Google-APIs VERSION 16_r04)
    hunter_default_version(Android-Intel-x86-Atom-System-Image VERSION 16)
    hunter_default_version(Android-MIPS-System-Image VERSION 16_r04)
    hunter_default_version(Android-SDK-Platform VERSION 16_r05)
    hunter_default_version(Sources-for-Android-SDK VERSION 16)
  elseif(_is_api_22)
    hunter_default_version(Android-ARM-EABI-v7a-System-Image VERSION 22_r02)
    hunter_default_version(Android-Google-APIs VERSION 22_r01)
    hunter_default_version(Android-Google-APIs-Intel-x86-Atom-System-Image VERSION 22_r21)
    hunter_default_version(Android-Intel-x86-Atom-System-Image VERSION 22_r06)
    hunter_default_version(Android-SDK-Platform VERSION 22_r02)
    hunter_default_version(Sources-for-Android-SDK VERSION 22)
  elseif(_is_api_24)
    hunter_default_version(Android-ARM-EABI-v7a-System-Image VERSION 24_r07)
    hunter_default_version(Android-ARM64-v8a-System-Image VERSION 24_r07)
    hunter_default_version(Android-Google-APIs VERSION 24_r1)
    hunter_default_version(Android-Google-APIs-Intel-x86-Atom-System-Image VERSION 24_r20)
    hunter_default_version(Android-Intel-x86-Atom-System-Image VERSION 24_r08)
    hunter_default_version(Android-SDK-Platform VERSION 24_r02)
    hunter_default_version(Sources-for-Android-SDK VERSION 24)
  else()
    # TODO: Add more versions
  endif()
endif()
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ cat $HUNTER_ROOT/cmake/projects/GTest/hunter.cmake
# Copyright (c) 2013, Ruslan Baratov
# All rights reserved.

# !!! DO NOT PLACE HEADER GUARDS HERE !!!

include(hunter_add_version)
include(hunter_cacheable)
include(hunter_download)
include(hunter_pick_scheme)
include(hunter_cmake_args)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.7.0-hunter"
    URL
    "https://github.com/hunter-packages/gtest/archive/v1.7.0-hunter.tar.gz"
    SHA1
    1ed1c26d11fb592056c1cb912bd3c784afa96eaa
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.7.0-hunter-1"
    URL
    "https://github.com/hunter-packages/gtest/archive/v1.7.0-hunter-1.tar.gz"
    SHA1
    0cb1dcf75e144ad052d3f1e4923a7773bf9b494f
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.7.0-hunter-2"
    URL
    "https://github.com/hunter-packages/gtest/archive/v1.7.0-hunter-2.tar.gz"
    SHA1
    e62b2ef70308f63c32c560f7b6e252442eed4d57
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.7.0-hunter-3"
    URL
    "https://github.com/hunter-packages/gtest/archive/v1.7.0-hunter-3.tar.gz"
    SHA1
    fea7d3020e20f059255484c69755753ccadf6362
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.7.0-hunter-4"
    URL
    "https://github.com/hunter-packages/gtest/archive/v1.7.0-hunter-4.tar.gz"
    SHA1
    9b439c0c25437a083957b197ac6905662a5d901b
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.7.0-hunter-5"
    URL
    "https://github.com/hunter-packages/gtest/archive/v1.7.0-hunter-5.tar.gz"
    SHA1
    796804df3facb074087a4d8ba6f652e5ac69ad7f
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.7.0-hunter-6"
    URL
    "https://github.com/hunter-packages/gtest/archive/v1.7.0-hunter-6.tar.gz"
    SHA1
    64b93147abe287da8fe4e18cfd54ba9297dafb82
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.7.0-hunter-7"
    URL
    "https://github.com/hunter-packages/gtest/archive/v1.7.0-hunter-7.tar.gz"
    SHA1
    19b5c98747768bcd0622714f2ed40f17aee406b2
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.7.0-hunter-8"
    URL
    "https://github.com/hunter-packages/gtest/archive/v1.7.0-hunter-8.tar.gz"
    SHA1
    ac4d2215aa1b1d745a096e5e3b2dbe0c0f229ea5
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.7.0-hunter-9"
    URL
    "https://github.com/hunter-packages/gtest/archive/v1.7.0-hunter-9.tar.gz"
    SHA1
    8a47fe9c4e550f4ed0e2c05388dd291a059223d9
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.7.0-hunter-10"
    URL
    "https://github.com/hunter-packages/gtest/archive/v1.7.0-hunter-10.tar.gz"
    SHA1
    374e6dbe8619ab467c6b1a0b470a598407b172e9
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.7.0-hunter-11"
    URL
    "https://github.com/hunter-packages/gtest/archive/v1.7.0-hunter-11.tar.gz"
    SHA1
    c6ae948ca2bea1d734af01b1069491b00933ed31
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    1.8.0-hunter-p2
    URL
    "https://github.com/hunter-packages/googletest/archive/1.8.0-hunter-p2.tar.gz"
    SHA1
    93148cb8850abe78b76ed87158fdb6b9c48e38c4
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    1.8.0-hunter-p5
    URL https://github.com/hunter-packages/googletest/archive/1.8.0-hunter-p5.tar.gz
    SHA1 3325aa4fc8b30e665c9f73a60f19387b7db36f85
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    1.8.0-hunter-p6
    URL
    "https://github.com/hunter-packages/googletest/archive/1.8.0-hunter-p6.tar.gz"
    SHA1
    f57096bd01c6f8cbef043b312d4d1e82f29648b6
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    1.8.0-hunter-p7
    URL
    "https://github.com/hunter-packages/googletest/archive/1.8.0-hunter-p7.tar.gz"
    SHA1
    4fe083a96d7597f7dce6f453dca01e1d94a1e45b
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    1.8.0-hunter-p8
    URL
    "https://github.com/hunter-packages/googletest/archive/1.8.0-hunter-p8.tar.gz"
    SHA1
    1cdd396b20c8d29f7ea08baaa49673b1c261f545
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    1.8.0-hunter-p9
    URL
    "https://github.com/hunter-packages/googletest/archive/1.8.0-hunter-p9.tar.gz"
    SHA1
    a345f16cb610e0b5dfa7778dc2852b784cfede5b
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    1.8.0-hunter-p10
    URL
    "https://github.com/hunter-packages/googletest/archive/1.8.0-hunter-p10.tar.gz"
    SHA1
    1d92c9f51af756410843b13f8c4e4df09e235394
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.8.0-hunter-p11"
    URL
    "https://github.com/hunter-packages/googletest/archive/1.8.0-hunter-p11.tar.gz"
    SHA1
    76c6aec038f7d7258bf5c4f45c4817b34039d285
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.8.1"
    URL
    "https://github.com/google/googletest/archive/release-1.8.1.tar.gz"
    SHA1
    152b849610d91a9dfa1401293f43230c2e0c33f8
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.10.0"
    URL
    "https://github.com/google/googletest/archive/release-1.10.0.tar.gz"
    SHA1
    9c89be7df9c5e8cb0bc20b3c4b39bf7e82686770
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.10.0-p0"
    URL
    "https://github.com/hunter-packages/googletest/archive/v1.10.0-p0.tar.gz"
    SHA1
    f7c72be12120e018f53cda0e0daa26fab5da7dfc
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.10.0-p1"
    URL
    "https://github.com/hunter-packages/googletest/archive/v1.10.0-p1.tar.gz"
    SHA1
    06a1f667f200ff94d38b608e44c3c8061c7b8f2f
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.11.0"
    URL
    "https://github.com/google/googletest/archive/release-1.11.0.tar.gz"
    SHA1
    7b100bb68db8df1060e178c495f3cbe941c9b058
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.12.1"
    URL
    "https://github.com/google/googletest/archive/release-1.12.1.tar.gz"
    SHA1
    cdddd449d4e3aa7bd421d4519c17139ea1890fe7
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.13.0"
    URL
    "https://github.com/google/googletest/archive/v1.13.0.tar.gz"
    SHA1
    bfa4b5131b6eaac06962c251742c96aab3f7aa78
)

hunter_add_version(
    PACKAGE_NAME
    GTest
    VERSION
    "1.14.0"
    URL
    "https://github.com/google/googletest/archive/v1.14.0.tar.gz"
    SHA1
    2b28c2a3a30d86b1759543ef61fac3c4d69f8c4c
)

hunter_add_version(
        PACKAGE_NAME
        GTest
        VERSION
        "1.15.2"
        URL
        "https://github.com/google/googletest/archive/v1.15.2.tar.gz"
        SHA1
        568d58e26bd4e838449ca7ab8ebc152b3cbd210d
)


if(HUNTER_GTest_VERSION VERSION_LESS 1.8.0 OR HUNTER_GTest_VERSION VERSION_GREATER_EQUAL 1.11.0)
  set(_gtest_license "LICENSE")
else()
  set(_gtest_license "googletest/LICENSE")
endif()

# gtest_force_shared_crt prevents GoogleTest from modifying options
# rather than forcing it to use shared libraries
hunter_cmake_args(
    GTest
    CMAKE_ARGS
    HUNTER_INSTALL_LICENSE_FILES=${_gtest_license}
    gtest_force_shared_crt=TRUE
)

hunter_pick_scheme(DEFAULT url_sha1_cmake)
hunter_cacheable(GTest)
hunter_download(PACKAGE_NAME GTest PACKAGE_INTERNAL_DEPS_ID 1)
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ mkdir cmake/Hunter
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ cat > cmake/Hunter/config.cmake <<EOF
hunter_config(GTest VERSION 1.7.0-hunter-9)
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ mkdir demo
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ cat > demo/main.cpp <<EOF
#include <print.hpp>

#include <cstdlib>

int main(int argc, char* argv[])
{
  const char* log_path = std::getenv("LOG_PATH");
  if (log_path == nullptr)
  {
    std::cerr << "undefined environment variable: LOG_PATH" << std::endl;
    return 1;
  }
  std::string text;
  while (std::cin >> text)
  {
    std::ofstream out{log_path, std::ios_base::app};
    print(text, out);
    out << std::endl;
  }
}
EOF
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ gsed -i '/endif()/a\
\
if(BUILD_EXAMPLES)\
    add_executable(demo ${CMAKE_CURRENT_SOURCE_DIR}/demo/main.cpp)\
    target_link_libraries(demo print)\
    install(TARGETS demo RUNTIME DESTINATION bin)\
endif()\
' CMakeLists.txt
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ mkdir tools
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ git submodule add https://github.com/ruslo/polly tools/polly
Cloning into '/home/Katya/Ekaterina06-choi/workspace/projects/lab07/tools/polly'...
remote: Enumerating objects: 6578, done.
remote: Counting objects: 100% (32/32), done.
remote: Compressing objects: 100% (15/15), done.
remote: Total 6578 (delta 21), reused 20 (delta 17), pack-reused 6546 (from 1)
Receiving objects: 100% (6578/6578), 1.68 MiB | 727.00 KiB/s, done.
Resolving deltas: 100% (4551/4551), done.
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ tools/polly/bin/polly.py --test
Python version: 3.12
Build dir: /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/default
Execute command: [
  `which`
  `cmake`
]

[/home/Katya/Ekaterina06-choi/workspace/projects/lab07]> "which" "cmake"

/usr/bin/cmake
Execute command: [
  `cmake`
  `--version`
]

[/home/Katya/Ekaterina06-choi/workspace/projects/lab07]> "cmake" "--version"

cmake version 3.30.3

CMake suite maintained and supported by Kitware (kitware.com/cmake).
Execute command: [
  `cmake`
  `-H.`
  `-B/home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/default`
  `-DCMAKE_TOOLCHAIN_FILE=/home/Katya/Ekaterina06-choi/workspace/projects/lab07/tools/polly/default.cmake`
]

[/home/Katya/Ekaterina06-choi/workspace/projects/lab07]> "cmake" "-H." "-B/home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/default" "-DCMAKE_TOOLCHAIN_FILE=/home/Katya/Ekaterina06-choi/workspace/projects/lab07/tools/polly/default.cmake"

CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- [polly] Used toolchain: Default
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
-- [hunter] Calculating Toolchain-SHA1
-- [hunter] Calculating Config-SHA1
-- [hunter] HUNTER_ROOT: /home/Katya/projects/hunter
-- [hunter] [ Hunter-ID: xxxxxxx | Toolchain-ID: 29081be | Config-ID: d14f46d ]
-- [hunter] GTEST_ROOT: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Install (ver.: 1.15.2)
-- Found GTest: /home/Katya/projects/hunter/_Base/xxxxxxx/29081be/d14f46d/Install/lib/cmake/GTest/GTestConfig.cmake (found version "1.15.2")
-- Configuring done (2.1s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/default
Execute command: [
  `cmake`
  `--build`
  `/home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/default`
  `--`
]

[/home/Katya/Ekaterina06-choi/workspace/projects/lab07]> "cmake" "--build" "/home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/default" "--"

[ 50%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[100%] Linking CXX static library libprint.a
[100%] Built target print
Run tests
Execute command: [
  `ctest`
]

[/home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/default]> "ctest"

*********************************
No test configuration file found!
*********************************
Usage

  ctest [options]

-
Log saved: /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_logs/polly/default/log.txt
-
Generate: 0:00:03.140442s
Build: 0:00:01.587900s
Test: 0:00:00.020848s
-
Total: 0:00:04.749458s
-
SUCCESS
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ tools/polly/bin/polly.py --install
Python version: 3.12
Build dir: /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/default
Execute command: [
  `which`
  `cmake`
]

[/home/Katya/Ekaterina06-choi/workspace/projects/lab07]> "which" "cmake"

/usr/bin/cmake
Execute command: [
  `cmake`
  `--version`
]

[/home/Katya/Ekaterina06-choi/workspace/projects/lab07]> "cmake" "--version"

cmake version 3.30.3

CMake suite maintained and supported by Kitware (kitware.com/cmake).

== WARNING ==

Looks like cmake arguments changed. You have two options to fix it:
  * Remove build directory completely by adding '--clear' (works 100%)
  * Run configure again by adding '--reconfig' (you must understand how CMake cache variables works/updated)

- "cmake" "-H." "-B/home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/default" "-DCMAKE_TOOLCHAIN_FILE=/home/Katya/Ekaterina06-choi/workspace/projects/lab07/tools/polly/default.cmake"
+ "cmake" "-H." "-B/home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/default" "-DCMAKE_TOOLCHAIN_FILE=/home/Katya/Ekaterina06-choi/workspace/projects/lab07/tools/polly/default.cmake" "-DCMAKE_INSTALL_PREFIX=/home/Katya/Ekaterina06-choi/workspace/projects/lab07/_install/default"
?                                                                                                                                                                                                 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ tools/polly/bin/polly.py --toolchain clang-cxx14
Python version: 3.12
Build dir: /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/clang-cxx14
Execute command: [
  `which`
  `cmake`
]

[/home/Katya/Ekaterina06-choi/workspace/projects/lab07]> "which" "cmake"

/usr/bin/cmake
Execute command: [
  `cmake`
  `--version`
]

[/home/Katya/Ekaterina06-choi/workspace/projects/lab07]> "cmake" "--version"

cmake version 3.30.3

CMake suite maintained and supported by Kitware (kitware.com/cmake).
Execute command: [
  `cmake`
  `-H.`
  `-B/home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/clang-cxx14`
  `-GUnix Makefiles`
  `-DCMAKE_TOOLCHAIN_FILE=/home/Katya/Ekaterina06-choi/workspace/projects/lab07/tools/polly/clang-cxx14.cmake`
]

[/home/Katya/Ekaterina06-choi/workspace/projects/lab07]> "cmake" "-H." "-B/home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/clang-cxx14" "-GUnix Makefiles" "-DCMAKE_TOOLCHAIN_FILE=/home/Katya/Ekaterina06-choi/workspace/projects/lab07/tools/polly/clang-cxx14.cmake"

CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- [polly] Used toolchain: clang / c++14 support

clang not found

CMake Error at tools/polly/utilities/polly_fatal_error.cmake:10 (message):
Call Stack (most recent call first):
  tools/polly/compiler/clang.cmake:23 (polly_fatal_error)
  tools/polly/clang-cxx14.cmake:20 (include)
  /usr/share/cmake-3.30/Modules/CMakeDetermineSystem.cmake:146 (include)
  CMakeLists.txt:14 (project)


CMake Error: CMake was unable to find a build program corresponding to "Unix Makefiles".  CMAKE_MAKE_PROGRAM is not set.  You probably need to select a different build tool.
-- Configuring incomplete, errors occurred!
Command exit with status "1": [/home/Katya/Ekaterina06-choi/workspace/projects/lab07]> "cmake" "-H." "-B/home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/clang-cxx14" "-GUnix Makefiles" "-DCMAKE_TOOLCHAIN_FILE=/home/Katya/Ekaterina06-choi/workspace/projects/lab07/tools/polly/clang-cxx14.cmake"

Log: /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_logs/polly/clang-cxx14/log.txt
*** FAILED ***
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ sudo apt-get install clang make
[sudo] password for Katya: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
make is already the newest version (4.3-4.1build2).
make set to manually installed.
The following additional packages will be installed:
  clang-19 icu-devtools lib32gcc-s1 lib32stdc++6 libc6-i386
  libclang-common-19-dev libclang-cpp19 libclang-rt-19-dev libclang1-19
  libffi-dev libgc1 libicu-dev liblzma-dev libncurses-dev libobjc-14-dev
  libobjc4 libpfm4 libxml2-dev llvm-19 llvm-19-dev llvm-19-linker-tools
  llvm-19-runtime llvm-19-tools zlib1g-dev
Suggested packages:
  clang-19-doc wasi-libc icu-doc liblzma-doc ncurses-doc pkgconf llvm-19-doc
The following NEW packages will be installed:
  clang clang-19 icu-devtools lib32gcc-s1 lib32stdc++6 libc6-i386
  libclang-common-19-dev libclang-cpp19 libclang-rt-19-dev libclang1-19
  libffi-dev libgc1 libicu-dev liblzma-dev libncurses-dev libobjc-14-dev
  libobjc4 libpfm4 libxml2-dev llvm-19 llvm-19-dev llvm-19-linker-tools
  llvm-19-runtime llvm-19-tools zlib1g-dev
0 upgraded, 25 newly installed, 0 to remove and 4 not upgraded.
Need to get 113 MB of archives.
After this operation, 684 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://ru.archive.ubuntu.com/ubuntu oracular/universe amd64 libclang-cpp19 amd64 1:19.1.1-1ubuntu1 [14.2 MB]
Get:2 http://ru.archive.ubuntu.com/ubuntu oracular/main amd64 libgc1 amd64 1:8.2.6-2 [90.6 kB]
Get:3 http://ru.archive.ubuntu.com/ubuntu oracular/universe amd64 libobjc4 amd64 14.2.0-4ubuntu2 [47.0 kB]
Get:4 http://ru.archive.ubuntu.com/ubuntu oracular/universe amd64 libobjc-14-dev amd64 14.2.0-4ubuntu2 [194 kB]
Get:5 http://ru.archive.ubuntu.com/ubuntu oracular/universe amd64 libclang-common-19-dev amd64 1:19.1.1-1ubuntu1 [742 kB]
Get:6 http://ru.archive.ubuntu.com/ubuntu oracular/universe amd64 llvm-19-linker-tools amd64 1:19.1.1-1ubuntu1 [1,312 kB]
Get:7 http://ru.archive.ubuntu.com/ubuntu oracular/universe amd64 libclang1-19 amd64 1:19.1.1-1ubuntu1 [8,246 kB]
Get:8 http://ru.archive.ubuntu.com/ubuntu oracular/universe amd64 clang-19 amd64 1:19.1.1-1ubuntu1 [78.9 kB]
Get:9 http://ru.archive.ubuntu.com/ubuntu oracular/universe amd64 clang amd64 1:19.0-60~exp1 [5,980 B]
Get:10 http://ru.archive.ubuntu.com/ubuntu oracular/main amd64 icu-devtools amd64 74.2-1ubuntu4 [213 kB]
Get:11 http://ru.archive.ubuntu.com/ubuntu oracular-updates/main amd64 libc6-i386 amd64 2.40-1ubuntu3.1 [2,800 kB]
Get:12 http://ru.archive.ubuntu.com/ubuntu oracular/main amd64 lib32gcc-s1 amd64 14.2.0-4ubuntu2 [92.2 kB]
Get:13 http://ru.archive.ubuntu.com/ubuntu oracular/main amd64 lib32stdc++6 amd64 14.2.0-4ubuntu2 [812 kB]
Get:14 http://ru.archive.ubuntu.com/ubuntu oracular/universe amd64 libclang-rt-19-dev amd64 1:19.1.1-1ubuntu1 [3,877 kB]
Get:15 http://ru.archive.ubuntu.com/ubuntu oracular/main amd64 libicu-dev amd64 74.2-1ubuntu4 [11.9 MB]
Get:16 http://ru.archive.ubuntu.com/ubuntu oracular/main amd64 libncurses-dev amd64 6.5-2 [384 kB]
Get:17 http://ru.archive.ubuntu.com/ubuntu oracular-updates/main amd64 liblzma-dev amd64 5.6.2-2ubuntu0.2 [177 kB]
Get:18 http://ru.archive.ubuntu.com/ubuntu oracular/main amd64 zlib1g-dev amd64 1:1.3.dfsg+really1.3.1-1ubuntu1 [895 kB]
Get:19 http://ru.archive.ubuntu.com/ubuntu oracular-updates/main amd64 libxml2-dev amd64 2.12.7+dfsg-3ubuntu0.2 [73.1 kB]
Get:20 http://ru.archive.ubuntu.com/ubuntu oracular/universe amd64 llvm-19-runtime amd64 1:19.1.1-1ubuntu1 [554 kB]
Get:21 http://ru.archive.ubuntu.com/ubuntu oracular/universe amd64 libpfm4 amd64 4.13.0+git32-g0d4ed0e-1 [414 kB]
Get:22 http://ru.archive.ubuntu.com/ubuntu oracular/universe amd64 llvm-19 amd64 1:19.1.1-1ubuntu1 [17.8 MB]
Get:23 http://ru.archive.ubuntu.com/ubuntu oracular/main amd64 libffi-dev amd64 3.4.6-1build1 [62.8 kB]
Get:24 http://ru.archive.ubuntu.com/ubuntu oracular/universe amd64 llvm-19-tools amd64 1:19.1.1-1ubuntu1 [539 kB]
Get:25 http://ru.archive.ubuntu.com/ubuntu oracular/universe amd64 llvm-19-dev amd64 1:19.1.1-1ubuntu1 [47.3 MB]
Fetched 113 MB in 49s (2,294 kB/s)                                             
Selecting previously unselected package libclang-cpp19.
(Reading database ... 199289 files and directories currently installed.)
Preparing to unpack .../00-libclang-cpp19_1%3a19.1.1-1ubuntu1_amd64.deb ...
Unpacking libclang-cpp19 (1:19.1.1-1ubuntu1) ...
Selecting previously unselected package libgc1:amd64.
Preparing to unpack .../01-libgc1_1%3a8.2.6-2_amd64.deb ...
Unpacking libgc1:amd64 (1:8.2.6-2) ...
Selecting previously unselected package libobjc4:amd64.
Preparing to unpack .../02-libobjc4_14.2.0-4ubuntu2_amd64.deb ...
Unpacking libobjc4:amd64 (14.2.0-4ubuntu2) ...
Selecting previously unselected package libobjc-14-dev:amd64.
Preparing to unpack .../03-libobjc-14-dev_14.2.0-4ubuntu2_amd64.deb ...
Unpacking libobjc-14-dev:amd64 (14.2.0-4ubuntu2) ...
Selecting previously unselected package libclang-common-19-dev:amd64.
Preparing to unpack .../04-libclang-common-19-dev_1%3a19.1.1-1ubuntu1_amd64.deb ...
Unpacking libclang-common-19-dev:amd64 (1:19.1.1-1ubuntu1) ...
Selecting previously unselected package llvm-19-linker-tools.
Preparing to unpack .../05-llvm-19-linker-tools_1%3a19.1.1-1ubuntu1_amd64.deb ...
Unpacking llvm-19-linker-tools (1:19.1.1-1ubuntu1) ...
Selecting previously unselected package libclang1-19.
Preparing to unpack .../06-libclang1-19_1%3a19.1.1-1ubuntu1_amd64.deb ...
Unpacking libclang1-19 (1:19.1.1-1ubuntu1) ...
Selecting previously unselected package clang-19.
Preparing to unpack .../07-clang-19_1%3a19.1.1-1ubuntu1_amd64.deb ...
Unpacking clang-19 (1:19.1.1-1ubuntu1) ...
Selecting previously unselected package clang.
Preparing to unpack .../08-clang_1%3a19.0-60~exp1_amd64.deb ...
Unpacking clang (1:19.0-60~exp1) ...
Selecting previously unselected package icu-devtools.
Preparing to unpack .../09-icu-devtools_74.2-1ubuntu4_amd64.deb ...
Unpacking icu-devtools (74.2-1ubuntu4) ...
Selecting previously unselected package libc6-i386.
Preparing to unpack .../10-libc6-i386_2.40-1ubuntu3.1_amd64.deb ...
Unpacking libc6-i386 (2.40-1ubuntu3.1) ...
Selecting previously unselected package lib32gcc-s1.
Preparing to unpack .../11-lib32gcc-s1_14.2.0-4ubuntu2_amd64.deb ...
Unpacking lib32gcc-s1 (14.2.0-4ubuntu2) ...
Selecting previously unselected package lib32stdc++6.
Preparing to unpack .../12-lib32stdc++6_14.2.0-4ubuntu2_amd64.deb ...
Unpacking lib32stdc++6 (14.2.0-4ubuntu2) ...
Selecting previously unselected package libclang-rt-19-dev:amd64.
Preparing to unpack .../13-libclang-rt-19-dev_1%3a19.1.1-1ubuntu1_amd64.deb ...
Unpacking libclang-rt-19-dev:amd64 (1:19.1.1-1ubuntu1) ...
Selecting previously unselected package libicu-dev:amd64.
Preparing to unpack .../14-libicu-dev_74.2-1ubuntu4_amd64.deb ...
Unpacking libicu-dev:amd64 (74.2-1ubuntu4) ...
Selecting previously unselected package libncurses-dev:amd64.
Preparing to unpack .../15-libncurses-dev_6.5-2_amd64.deb ...
Unpacking libncurses-dev:amd64 (6.5-2) ...
Selecting previously unselected package liblzma-dev:amd64.
Preparing to unpack .../16-liblzma-dev_5.6.2-2ubuntu0.2_amd64.deb ...
Unpacking liblzma-dev:amd64 (5.6.2-2ubuntu0.2) ...
Selecting previously unselected package zlib1g-dev:amd64.
Preparing to unpack .../17-zlib1g-dev_1%3a1.3.dfsg+really1.3.1-1ubuntu1_amd64.deb ...
Unpacking zlib1g-dev:amd64 (1:1.3.dfsg+really1.3.1-1ubuntu1) ...
Selecting previously unselected package libxml2-dev:amd64.
Preparing to unpack .../18-libxml2-dev_2.12.7+dfsg-3ubuntu0.2_amd64.deb ...
Unpacking libxml2-dev:amd64 (2.12.7+dfsg-3ubuntu0.2) ...
Selecting previously unselected package llvm-19-runtime.
Preparing to unpack .../19-llvm-19-runtime_1%3a19.1.1-1ubuntu1_amd64.deb ...
Unpacking llvm-19-runtime (1:19.1.1-1ubuntu1) ...
Selecting previously unselected package libpfm4:amd64.
Preparing to unpack .../20-libpfm4_4.13.0+git32-g0d4ed0e-1_amd64.deb ...
Unpacking libpfm4:amd64 (4.13.0+git32-g0d4ed0e-1) ...
Selecting previously unselected package llvm-19.
Preparing to unpack .../21-llvm-19_1%3a19.1.1-1ubuntu1_amd64.deb ...
Unpacking llvm-19 (1:19.1.1-1ubuntu1) ...
Selecting previously unselected package libffi-dev:amd64.
Preparing to unpack .../22-libffi-dev_3.4.6-1build1_amd64.deb ...
Unpacking libffi-dev:amd64 (3.4.6-1build1) ...
Selecting previously unselected package llvm-19-tools.
Preparing to unpack .../23-llvm-19-tools_1%3a19.1.1-1ubuntu1_amd64.deb ...
Unpacking llvm-19-tools (1:19.1.1-1ubuntu1) ...
Selecting previously unselected package llvm-19-dev.
Preparing to unpack .../24-llvm-19-dev_1%3a19.1.1-1ubuntu1_amd64.deb ...
Unpacking llvm-19-dev (1:19.1.1-1ubuntu1) ...
Setting up libncurses-dev:amd64 (6.5-2) ...
Setting up libclang1-19 (1:19.1.1-1ubuntu1) ...
Setting up libclang-common-19-dev:amd64 (1:19.1.1-1ubuntu1) ...
Setting up libffi-dev:amd64 (3.4.6-1build1) ...
Setting up libpfm4:amd64 (4.13.0+git32-g0d4ed0e-1) ...
Setting up icu-devtools (74.2-1ubuntu4) ...
Setting up libgc1:amd64 (1:8.2.6-2) ...
Setting up liblzma-dev:amd64 (5.6.2-2ubuntu0.2) ...
Setting up zlib1g-dev:amd64 (1:1.3.dfsg+really1.3.1-1ubuntu1) ...
Setting up libc6-i386 (2.40-1ubuntu3.1) ...
Setting up llvm-19-linker-tools (1:19.1.1-1ubuntu1) ...
Setting up llvm-19-runtime (1:19.1.1-1ubuntu1) ...
Setting up llvm-19-tools (1:19.1.1-1ubuntu1) ...
Setting up libicu-dev:amd64 (74.2-1ubuntu4) ...
Setting up libclang-cpp19 (1:19.1.1-1ubuntu1) ...
Setting up libobjc4:amd64 (14.2.0-4ubuntu2) ...
Setting up libobjc-14-dev:amd64 (14.2.0-4ubuntu2) ...
Setting up clang-19 (1:19.1.1-1ubuntu1) ...
Setting up libxml2-dev:amd64 (2.12.7+dfsg-3ubuntu0.2) ...
Setting up lib32gcc-s1 (14.2.0-4ubuntu2) ...
Setting up lib32stdc++6 (14.2.0-4ubuntu2) ...
Setting up clang (1:19.0-60~exp1) ...
Setting up libclang-rt-19-dev:amd64 (1:19.1.1-1ubuntu1) ...
Setting up llvm-19 (1:19.1.1-1ubuntu1) ...
Setting up llvm-19-dev (1:19.1.1-1ubuntu1) ...
Processing triggers for base-files (13.3ubuntu6) ...
Processing triggers for libc-bin (2.40-1ubuntu3.1) ...
Processing triggers for systemd (256.5-2ubuntu3.1) ...
Processing triggers for man-db (2.12.1-3) ...
Processing triggers for install-info (7.1-3build2) ...
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ ls -la /home/Katya/Ekaterina06-choi/workspace/projects/lab07/tools/polly/clang-cxx14.cmake
-rw-rw-r-- 1 Katya Katya 510 Apr 27 13:56 /home/Katya/Ekaterina06-choi/workspace/projects/lab07/tools/polly/clang-cxx14.cmake
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ tools/polly/bin/polly.py --toolchain clang-cxx14
Python version: 3.12
Build dir: /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/clang-cxx14
Execute command: [
  `which`
  `cmake`
]

[/home/Katya/Ekaterina06-choi/workspace/projects/lab07]> "which" "cmake"

/usr/bin/cmake
Execute command: [
  `cmake`
  `--version`
]

[/home/Katya/Ekaterina06-choi/workspace/projects/lab07]> "cmake" "--version"

cmake version 3.30.3

CMake suite maintained and supported by Kitware (kitware.com/cmake).
Execute command: [
  `cmake`
  `-H.`
  `-B/home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/clang-cxx14`
  `-GUnix Makefiles`
  `-DCMAKE_TOOLCHAIN_FILE=/home/Katya/Ekaterina06-choi/workspace/projects/lab07/tools/polly/clang-cxx14.cmake`
]

[/home/Katya/Ekaterina06-choi/workspace/projects/lab07]> "cmake" "-H." "-B/home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/clang-cxx14" "-GUnix Makefiles" "-DCMAKE_TOOLCHAIN_FILE=/home/Katya/Ekaterina06-choi/workspace/projects/lab07/tools/polly/clang-cxx14.cmake"

-- [polly] Used toolchain: clang / c++14 support
-- The C compiler identification is Clang 19.1.1
-- The CXX compiler identification is Clang 19.1.1
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/clang - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/clang++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- [hunter] Calculating Toolchain-SHA1
-- [hunter] Calculating Config-SHA1
-- [hunter] HUNTER_ROOT: /home/Katya/projects/hunter
-- [hunter] [ Hunter-ID: xxxxxxx | Toolchain-ID: 476c479 | Config-ID: d14f46d ]
-- [hunter] GTEST_ROOT: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Install (ver.: 1.15.2)
-- [hunter] Building GTest
loading initial cache file /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/cache.cmake
loading initial cache file /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/args.cmake
-- [polly] Used toolchain: clang / c++14 support
-- The C compiler identification is Clang 19.1.1
-- The CXX compiler identification is Clang 19.1.1
-- Check for working C compiler: /usr/bin/clang - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/clang++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done (0.4s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Build
[  6%] Creating directories for 'GTest-Release'
[ 12%] Performing download step (download, verify and extract) for 'GTest-Release'
-- verifying file...
       file='/home/Katya/projects/hunter/_Base/Download/GTest/1.15.2/568d58e/v1.15.2.tar.gz'
-- File already exists and hash match (skip download):
  file='/home/Katya/projects/hunter/_Base/Download/GTest/1.15.2/568d58e/v1.15.2.tar.gz'
  SHA1='568d58e26bd4e838449ca7ab8ebc152b3cbd210d'
-- extracting...
     src='/home/Katya/projects/hunter/_Base/Download/GTest/1.15.2/568d58e/v1.15.2.tar.gz'
     dst='/home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Source'
-- extracting... [tar xfz]
-- extracting... [analysis]
-- extracting... [rename]
-- extracting... [clean up]
-- extracting... done
[ 18%] No update step for 'GTest-Release'
[ 25%] No patch step for 'GTest-Release'
[ 31%] Performing configure step for 'GTest-Release'
loading initial cache file /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/cache.cmake
loading initial cache file /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/args.cmake
-- [polly] Used toolchain: clang / c++14 support
-- The C compiler identification is Clang 19.1.1
-- The CXX compiler identification is Clang 19.1.1
-- Check for working C compiler: /usr/bin/clang - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/clang++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Configuring done (0.5s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Build/GTest-Release-prefix/src/GTest-Release-build
[ 37%] Performing build step for 'GTest-Release'
[ 12%] Building CXX object googletest/CMakeFiles/gtest.dir/src/gtest-all.cc.o
[ 25%] Linking CXX static library ../lib/libgtest.a
[ 25%] Built target gtest
[ 37%] Building CXX object googletest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
[ 50%] Building CXX object googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o
[ 62%] Linking CXX static library ../lib/libgtest_main.a
[ 62%] Built target gtest_main
[ 75%] Linking CXX static library ../lib/libgmock.a
[ 75%] Built target gmock
[ 87%] Building CXX object googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o
[100%] Linking CXX static library ../lib/libgmock_main.a
[100%] Built target gmock_main
[ 43%] Performing install step for 'GTest-Release'
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/internal
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/internal/gmock-port.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/internal/gmock-internal-utils.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/internal/gmock-pp.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/internal/custom
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/internal/custom/gmock-port.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/internal/custom/gmock-generated-actions.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/internal/custom/README.md
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/internal/custom/gmock-matchers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/gmock-more-actions.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/gmock-nice-strict.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/gmock-actions.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/gmock-function-mocker.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/gmock-matchers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/gmock-cardinalities.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/gmock.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/gmock-spec-builders.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/gmock-more-matchers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/libgmock.a
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/libgmock_main.a
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/pkgconfig/gmock.pc
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/pkgconfig/gmock_main.pc
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/cmake/GTest/GTestTargets.cmake
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/cmake/GTest/GTestTargets-release.cmake
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/cmake/GTest/GTestConfigVersion.cmake
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/cmake/GTest/GTestConfig.cmake
-- Up-to-date: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest-test-part.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest_prod.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest-typed-test.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest_pred_impl.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest-assertion-result.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-port.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-param-util.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-port-arch.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/custom
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/custom/gtest-port.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/custom/gtest.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/custom/README.md
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/custom/gtest-printers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-internal.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-type-util.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-string.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-filepath.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-death-test-internal.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest-death-test.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest-param-test.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest-matchers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest-spi.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest-printers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest-message.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/libgtest.a
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/libgtest_main.a
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/pkgconfig/gtest.pc
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/pkgconfig/gtest_main.pc
loading initial cache file /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/args.cmake
[ 50%] Completed 'GTest-Release'
[ 50%] Built target GTest-Release
[ 56%] Creating directories for 'GTest-Debug'
[ 62%] Performing download step (download, verify and extract) for 'GTest-Debug'
-- verifying file...
       file='/home/Katya/projects/hunter/_Base/Download/GTest/1.15.2/568d58e/v1.15.2.tar.gz'
-- File already exists and hash match (skip download):
  file='/home/Katya/projects/hunter/_Base/Download/GTest/1.15.2/568d58e/v1.15.2.tar.gz'
  SHA1='568d58e26bd4e838449ca7ab8ebc152b3cbd210d'
-- extracting...
     src='/home/Katya/projects/hunter/_Base/Download/GTest/1.15.2/568d58e/v1.15.2.tar.gz'
     dst='/home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Source'
-- extracting... [tar xfz]
-- extracting... [analysis]
-- extracting... [rename]
-- extracting... [clean up]
-- extracting... done
[ 68%] No update step for 'GTest-Debug'
[ 75%] No patch step for 'GTest-Debug'
[ 81%] Performing configure step for 'GTest-Debug'
loading initial cache file /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/cache.cmake
loading initial cache file /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/args.cmake
-- [polly] Used toolchain: clang / c++14 support
-- The C compiler identification is Clang 19.1.1
-- The CXX compiler identification is Clang 19.1.1
-- Check for working C compiler: /usr/bin/clang - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/clang++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Configuring done (0.5s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Build/GTest-Debug-prefix/src/GTest-Debug-build
[ 87%] Performing build step for 'GTest-Debug'
[ 12%] Building CXX object googletest/CMakeFiles/gtest.dir/src/gtest-all.cc.o
[ 25%] Linking CXX static library ../lib/libgtestd.a
[ 25%] Built target gtest
[ 50%] Building CXX object googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o
[ 50%] Building CXX object googletest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
[ 62%] Linking CXX static library ../lib/libgtest_maind.a
[ 62%] Built target gtest_main
[ 75%] Linking CXX static library ../lib/libgmockd.a
[ 75%] Built target gmock
[ 87%] Building CXX object googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o
[100%] Linking CXX static library ../lib/libgmock_maind.a
[100%] Built target gmock_main
[ 93%] Performing install step for 'GTest-Debug'
-- Up-to-date: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include
-- Up-to-date: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock
-- Up-to-date: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/internal
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/internal/gmock-port.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/internal/gmock-internal-utils.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/internal/gmock-pp.h
-- Up-to-date: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/internal/custom
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/internal/custom/gmock-port.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/internal/custom/gmock-generated-actions.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/internal/custom/README.md
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/internal/custom/gmock-matchers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/gmock-more-actions.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/gmock-nice-strict.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/gmock-actions.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/gmock-function-mocker.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/gmock-matchers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/gmock-cardinalities.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/gmock.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/gmock-spec-builders.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gmock/gmock-more-matchers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/libgmockd.a
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/libgmock_maind.a
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/pkgconfig/gmock.pc
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/pkgconfig/gmock_main.pc
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/cmake/GTest/GTestTargets.cmake
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/cmake/GTest/GTestTargets-debug.cmake
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/cmake/GTest/GTestConfigVersion.cmake
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/cmake/GTest/GTestConfig.cmake
-- Up-to-date: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include
-- Up-to-date: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest-test-part.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest_prod.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest-typed-test.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest_pred_impl.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest-assertion-result.h
-- Up-to-date: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-port.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-param-util.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-port-arch.h
-- Up-to-date: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/custom
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/custom/gtest-port.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/custom/gtest.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/custom/README.md
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/custom/gtest-printers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-internal.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-type-util.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-string.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-filepath.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/internal/gtest-death-test-internal.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest-death-test.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest-param-test.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest-matchers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest-spi.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest-printers.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/include/gtest/gtest-message.h
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/libgtestd.a
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/libgtest_maind.a
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/pkgconfig/gtest.pc
-- Installing: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/Install/lib/pkgconfig/gtest_main.pc
loading initial cache file /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest/args.cmake
[100%] Completed 'GTest-Debug'
[100%] Built target GTest-Debug
-- [hunter] Build step successful (dir: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Build/GTest)
-- [hunter] Cache saved: /home/Katya/projects/hunter/_Base/Cache/raw/3461ef524267c118316fe229ffbfafe0224ff50b.tar.bz2
-- Found GTest: /home/Katya/projects/hunter/_Base/xxxxxxx/476c479/d14f46d/Install/lib/cmake/GTest/GTestConfig.cmake (found version "1.15.2")
-- Configuring done (20.4s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/clang-cxx14
Execute command: [
  `cmake`
  `--build`
  `/home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/clang-cxx14`
  `--`
]

[/home/Katya/Ekaterina06-choi/workspace/projects/lab07]> "cmake" "--build" "/home/Katya/Ekaterina06-choi/workspace/projects/lab07/_builds/clang-cxx14" "--"

[ 50%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[100%] Linking CXX static library libprint.a
[100%] Built target print
-
Log saved: /home/Katya/Ekaterina06-choi/workspace/projects/lab07/_logs/polly/clang-cxx14/log.txt
-
Generate: 0:00:21.426192s
Build: 0:00:01.420857s
-
Total: 0:00:22.847492s
-
SUCCESS
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ git push origin main
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
Enumerating objects: 271, done.
Counting objects: 100% (271/271), done.
Delta compression using up to 8 threads
Compressing objects: 100% (143/143), done.
Writing objects: 100% (271/271), 1.32 MiB | 24.08 MiB/s, done.
Total 271 (delta 105), reused 271 (delta 105), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (105/105), done.
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
remote:        https://github.com/Ekaterina06-choi/lab07/security/secret-scanning/unblock-secret/2wJblykOwE6JL5L4Ftw29RkN9zH
remote:     
remote:     
remote:       —— GitHub Personal Access Token ——————————————————————
remote:        locations:
remote:          - commit: 1be8e0a6ff5d024f282bad2c4677b0cd4ff72915
remote:            path: lab03/README.md:3
remote:     
remote:        (?) To push, remove secret from commit(s) or follow this URL to allow the secret.
remote:        https://github.com/Ekaterina06-choi/lab07/security/secret-scanning/unblock-secret/2wJbm20LPn41tkfu5uqgzv519TZ
remote:     
remote: 
remote: 
To https://github.com/Ekaterina06-choi/lab07
 ! [remote rejected] main -> main (push declined due to repository rule violations)
error: failed to push some refs to 'https://github.com/Ekaterina06-choi/lab07'
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ git push origin main
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
Enumerating objects: 271, done.
Counting objects: 100% (271/271), done.
Delta compression using up to 8 threads
Compressing objects: 100% (143/143), done.
Writing objects: 100% (271/271), 1.32 MiB | 33.72 MiB/s, done.
Total 271 (delta 105), reused 271 (delta 105), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (105/105), done.
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
remote:        https://github.com/Ekaterina06-choi/lab07/security/secret-scanning/unblock-secret/2wJblykOwE6JL5L4Ftw29RkN9zH
remote:     
remote: 
remote: 
To https://github.com/Ekaterina06-choi/lab07
 ! [remote rejected] main -> main (push declined due to repository rule violations)
error: failed to push some refs to 'https://github.com/Ekaterina06-choi/lab07'
Katya@ubuntu:~/Ekaterina06-choi/workspace/projects/lab07$ git push origin main
Username for 'https://github.com': Ekaterina06-choi
Password for 'https://Ekaterina06-choi@github.com': 
Enumerating objects: 271, done.
Counting objects: 100% (271/271), done.
Delta compression using up to 8 threads
Compressing objects: 100% (143/143), done.
Writing objects: 100% (271/271), 1.32 MiB | 67.43 MiB/s, done.
Total 271 (delta 105), reused 271 (delta 105), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (105/105), done.
To https://github.com/Ekaterina06-choi/lab07
 * [new branch]      main -> main
