# emscripten-glfw3-cmake-example
emscripten with glfw3 and cmake

With support for both native (glfw) and web (emscripten) builds.

And an option to switch between Legacy OpenGL (fixed function pipeline) and Modern OpenGL (with shaders) with the same visual result.

## Dependencies
Install cmake via `brew install cmake` (Mac OSX) or `sudo apt install cmake` (Ubuntu Linux).

## Native build
Install glfw via `brew install glfw` (Mac OSX) or `sudo apt install libglfw3-dev` (Ubuntu Linux).

Then build the project:
```sh
mkdir build-native
cd build-native
cmake ../src -DUSE_LEGACY_OPENGL={ON|OFF}
make
./emscripten-glfw3-cmake-example
```


## Web build
[Install emscripten](https://emscripten.org/docs/getting_started/downloads.html#installation-instructions) which already includes glfw: 
```sh
git clone https://github.com/emscripten-core/emsdk.git
cd emsdk
git pull
./emsdk update-tags
./emsdk install latest
./emsdk activate latest
source ./emsdk_env.sh
cd ..
```

Then build the project
```sh
mkdir build-web
cd build-web
cmake ../src -DCMAKE_TOOLCHAIN_FILE=../emsdk/upstream/emscripten/cmake/Modules/Platform/Emscripten.cmake -DUSE_LEGACY_OPENGL={ON|OFF}
make
```

serve the file either using node or python
```
npx http-server
python2 -m SimpleHTTPServer 8080
```
Then open http://localhost:8080/emscripten-glfw3-cmake-example.html

## Legacy OpenGL

For both web and native build, one can further switch to legacy OpenGL, the visual result should be the same rotating triangle.

If `-DUSE_LEGACY_OPENGL=ON` is passed, the code uses legacy OpenGL (fixed function pipeline) functions `glBegin`, `glEnd`, `glColor3fv`, `glVertex2fv`, `glMatrixMode` and `glLoadMatrixf`.

If nothing or `-DUSE_LEGACY_OPENGL=OFF` is passed, the code uses Modern OpenGL (with shaders).


## References
Inspired by
 - https://gist.github.com/ousttrue/0f3a11d5d28e365b129fe08f18f4e141
 - https://github.com/siposcsaba89/emscripten-glfw3-cmake-test
 