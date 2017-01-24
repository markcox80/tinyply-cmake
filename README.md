Tinyply CMake
=============

A simple CMake wrapper for [tinyply](https://github.com/ddiakopoulos/tinyply).

Installation
------------

    $ git submodule init
    $ git submodule update
    $ mkdir /tmp/build
    $ cd /tmp/build
    $ cmake ${SOURCE_DIR} \
            -DCMAKE_INSTALL_PREFIX=${PREFIX} \
            -DCMAKE_BUILD_TYPE=Release
    $ make
    $ make tests
    $ sudo make install

How to use it in CMake
----------------------

Put the following in your project's `CMakeLists.txt`.

    find_package(tinyply REQUIRED)

    add_executable(my-app my-app.cpp)
    target_link_libraries(my-app tinyply)

Invoke CMake with `CMAKE_PREFIX_PATH` containing the path to the
tinply-cmake installation prefix.

    $ cmake -DCMAKE_PREFIX_PATH=/path/to/tinply-cmake/prefix ...