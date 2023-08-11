For ubuntu:
1. Install necessary system available dependencies:
```
sudo apt update
sudo apt-get install build-essential libabsl-dev libboost-all-dev libgrpc++-dev libprotobuf-dev libxtensor-dev pkg-config ninja-build protobuf-compiler-grpc libjson-glib-dev libsoup2.4-dev
```
2. Get [cmake](https://cmake.org/) 3.25+
E.g:
```
mkdir ~/bin
cd ~/bin
wget 'https://github.com/Kitware/CMake/releases/download/v3.27.1/cmake-3.27.1-linux-x86_64.tar.gz'
tar -xzf cmake-3.27.1-linux-x86_64.tar.gz
export PATH="$HOME/bin/cmake-3.27.1-linux-x86_64/bin/:$PATH"
```

3. Clone + build the [viam-cpp-sdk](https://github.com/viamrobotics/viam-cpp-sdk)
```
cd ~/
git clone https://github.com/viamrobotics/viam-cpp-sdk.git
mkdir ~/viam-cpp-sdk/build
cd viam-cpp-sdk/build
cmake .. -G Ninja
# -- Could NOT find gRPC (missing: gRPC_DIR)
# CMake Warning at CMakeLists.txt:359 (message):
#   Failed to find gRPC with `find_package`; falling back to
#   `pkg_check_modules`
#
#
# CMake Deprecation Warning at build/_deps/xtensor-src/CMakeLists.txt:10 (cmake_minimum_required):
#   Compatibility with CMake < 3.5 will be removed from a future version of
#   CMake.
#
#   Update the VERSION argument <min> value or use a ...<max> suffix to tell
#   CMake that the project does not need compatibility with older versions.
#
#
# -- Building xtensor v0.24.3
# ERRORMismatch xtl versions. Found '..' but requires: '0.7.0'
# -- Configuring done (1.8s)
# -- Generating done (0.1s)
# -- Build files have been written to: /home/ubuntu/viam-cpp-sdk/build

ninja # -j <compilation threads>
ninja install
```

4. Install gstreamer
```
sudo apt install libgstreamer1.0-dev
```

5. Clone + Build this demo project
```
cd ~/
git clone https://github.com/dgottlieb/viam-gstreamer.git
mkdir viam-gstreamer/build
cd viam-gstreamer/build
cmake -DCMAKE_PREFIX_PATH=~/viam-cpp-sdk/build/install .. -G Ninja
ninja
./gstream-viam-module
```
