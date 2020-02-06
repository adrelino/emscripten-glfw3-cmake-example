# emscripten-glfw3-cmake-example
emscripten with glfw3 and cmake

native build
```sh
mkdir build-native
cd build-native
cmake ../src -DCMAKE_BUILD_TYPE=Release
make
./emscripten-glfw3-cmake-example.html
```


web build
```sh
mkdir build-web
cd build-web
git clone https://github.com/emscripten-core/emsdk.git
cmake ../src -DCMAKE_TOOLCHAIN_FILE=./emsdk/upstream/emscripten/cmake/Modules/Platform/Emscripten.cmake -DCMAKE_BUILD_TYPE=Release
make
npx http-server -o emscripten-glfw3-cmake-example.html
```

Inspired by
 - https://gist.github.com/ousttrue/0f3a11d5d28e365b129fe08f18f4e141
 - https://github.com/siposcsaba89/emscripten-glfw3-cmake-test
 