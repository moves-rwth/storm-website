---
title: Manual Configuration
layout: default
documentation: true
category_weight: 3
categories: [Obtain Storm]
---

<h1>Manual Configuration</h1>

{% include includes/toc.html %}

This guide is designed for users that need particular features and people developing under Storm.
We will detail how to perform a manual configuration of the build process.

There are a number of CMake options that modify how Storm is built.
All of them can be set in the [configuration step]({{ '/documentation/obtain-storm/build.html#configuration-step' | relative_url }}) by providing them to `cmake`.
To modify the options after the configuration step, you may run `ccmake ..` (assuming that you currently are in `STORM_DIR/build`). After changing these options you need to rebuild Storm using `make`.

We don't detail all options here, but only selected ones.
For a full list of options, we refer to `ccmake ..` and all options with prefix `STORM_X`.

## Build configurations

By default, Storm is compiled in release mode which enables various compiler optimization.
For debugging purposes, Storm can also be compiled in debug mode by providing the CMake argument `-DCMAKE_BUILD_TYPE=DEBUG`.

The flag `-DSTORM_BUILD_EXECUTABLES` enables/disables the building of the executables, the flag `-DSTORM_BUILD_TESTS` enables/disables the building of the tests.

## Developer

For developers, we offer the option `-DSTORM_DEVELOPER=ON`. This enables

- more CMake output
- more warnings
- debug and trace log levels (they are not always printed and need to be explicitly enabled through the CLI arguments `--debug` or `--trace`)

## Libraries

Additional libraries can be configured during the configuration step.
We refer to the [documentation on dependencies]({{ '/documentation/obtain-storm/dependencies.html#list-of-dependencies' | relative_url }}) for detailed instructions.

## Link-time optimization

By default, Storm uses link-time optimization (LTO) to enable even more optimizations that are done at link time. This, however, comes at a penalty for building in terms of both time and memory, as the linking step becomes very resource-intensive. Disabling LTO via `-DSTORM_USE_LTO=OFF` avoids this at the price of producing slower binaries.

## Portability

By default, the binaries will be built specifically for your machine, because this enables a wider range of optimizations to be enabled. If you need your binaries to be portable (in the sense that they could run on another machine that has all required dependencies in their right version or in a Docker container), you can set `-DSTORM_PORTABLE=ON` at the cost of producing slower binaries.

