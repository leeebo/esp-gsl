## Overview

The component is a wrapper of GNU Scientific Library (GSL) for ESP32/S3/S3, users can easily use it under ESP-IDF build system.

The GNU Scientific Library (GSL) is a numerical library for C and C++ programmers. It is free software under the GNU General Public License.

The library provides a wide range of mathematical routines such as random number generators, special functions and least-squares fitting. There are over 1000 functions in total with an extensive test suite.

Unlike the licenses of proprietary numerical libraries the license of GSL does not restrict scientific cooperation. It allows you to share your programs freely with others.

## License Warning

**The esp-gsl API implementation is licensed under GPLv3, you can link the lib for personally test, but you Must replace with other implementation (eg. from BSD Math lib) when distribute software binary or products.**

## How to use

### Add component from esp-registry to your project

You can use the component manager command `add-dependency` to add the `esp-gsl` to your project's dependency, during the `CMake` step the component will be downloaded automatically

```
idf.py add-dependency "leeebo/esp-gsl=*"
```

### Add component from git repository to your project

To add esp-gsl to your project from git repository, create an idf_component.yml file with the following contents and place it in the component's folder that depends on esp-gsl (for example, in the main folder of your project, since main is a special component in the esp-idf build system). The component will be downloaded automatically during the CMake processing step.

```
dependencies:
  esp-gsl:
    git: https://github.com/leeebo/esp-gsl.git
    version: "*"
```

> mirror repository: https://gitee.com/qljz/esp-gsl

### Download example from esp-registry

Please use the component manager command `create-project-from-example` to create the project from example template

```
idf.py create-project-from-example "leeebo/esp-gsl=*:test_project"
```

### Download example from git repository

You can also clone the git repository,and run `example/test_project` in the `esp-gsl/example/test_project` directory. Or you can also copy `example/test_project` to anywhere to run.

Then the example will download `esp-dsl` from the github repository automatically during `CMake`.

