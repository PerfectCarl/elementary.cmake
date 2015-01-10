# Introduction
elementary.cmake is a set of predefined [cmake](http://cmake.org/) macros to build vala projects in a simple declarative way using sane defaults.

All is needed in **one only cmake** file for your whole project

```
cmake_minimum_required (VERSION 2.8)
cmake_policy (VERSION 2.8)
list (APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)
include (Elementary)

set (VALA_VERSION_MIN "0.26")

set (BUILD_TYPE "Release")

build_elementary_app (
    BINARY_NAME
        webcontracts
    TITLE
        "Sharing Accounts"
    VERSION
        "0.2"
    SOURCE_PATH
        src
    PACKAGES
        gtk+-3.0
        json-glib-1.0
        granite
        rest-0.7
        webkitgtk-3.0
        libsoup-2.4
)

build_translations()
```

elementary.cmake can create the following binary files: 
   - ui application (executable)
   - cli application (executable)
   - static or shared library
   - elementary plug (linux shared library)
   - simple script

elementary.cmake creates the following make targets
   - `make`: build the binary with support for translations
   - `make install`: install the binary along with provided files (.desktop, icons, contracts)
       - if the binary is a library elementary.cmake generates the `pc` and `deps` file
  - `make uninstall`:
  - `make pot`: create the translations files

elementary.cmake generates a [build file](docs/build.md) that can be called from vala code:  
```java
   void print_info () {
      stout.printf ("Usage: %s flickr /my/path/to/image.png\n", Build.BINARY_NAME);
   }
```

# How to use

Replace the cmake folder in your project by the one provided.

Write a `CMakeLists.txt` file using elementary.cmake macros : 
  - `build_elementary_plug`
  - `build_elementary_app`
  - `build_elementary_cli`
  - `build_elementary_library`
  - `build_translations`

> Note: `CMakeLists.txt` file may contain many build_elementary calls if your project produces many binary files

Run 
```
build && mkdir build && cd build &&  
cmake ../ 
make
```

> Note: elementary.cmake set `CMAKE_INSTALL_PREFIX` to `/usr` and uses the value `BUILD_TYPE` for `CMAKE_BUILD_TYPE`

# Samples

You can find samples for: 
  - a library and a sample cli test program: [vala-stacktrace](https://github.com/PerfectCarl/vala-stacktrace)
  - an elementary gtk app: [eidete](https://code.launchpad.net/~name-is-carl/eidete/use-elementary.cmake)
  - an elementary [switchboard](https://launchpad.net/switchboard) plug: [useraccounts](https://code.launchpad.net/~name-is-carlswitchboard-plug-useraccounts/use-elementary.cmake)
  - an elementary plug and a cli application: [webcontracts](https://code.launchpad.net/~elementary-apps/webcontracts/fix-for-freya)

# Documentation 

# [Changelog](CHANGELOG.md)
