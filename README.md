## Overview

The component is a wrapper of GNU Scientific Library (GSL) for ESP32/S3/S3, users can easily use it under ESP-IDF build system.

The GNU Scientific Library (GSL) is a numerical library for C and C++ programmers. It is free software under the GNU General Public License.

The library provides a wide range of mathematical routines such as random number generators, special functions and least-squares fitting. There are over 1000 functions in total with an extensive test suite.

Unlike the licenses of proprietary numerical libraries the license of GSL does not restrict scientific cooperation. It allows you to share your programs freely with others.

## How to use

### Add component to your project

Please use the component manager command `add-dependency` to add the `esp-gsl` to your project's dependency, during the `CMake` step the component will be downloaded automatically

```
idf.py add-dependency "leeebo/esp-gsl=*"
```

### Examples

Please use the component manager command `create-project-from-example` to create the project from example template

```
idf.py create-project-from-example "leeebo/esp-gsl=*:test_project"
```

Then the example will be downloaded in current folder, you can check into it for build and flash.
