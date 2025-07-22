---
title: Installing Dependencies
layout: default
documentation: true
category_weight: 1
categories: [Obtain Storm]
---

<h1>Installing Dependencies</h1>

{% include includes/toc.html %}


Storm depends on [several other libraries]({{ '/documentation/obtain-storm/dependencies.html#list-of-dependencies' | relative_url }}).
Partly, they are packed with Storm.
This page describes dependencies which are assumed to be present on the target system.
We both give a general list, as well as operating system specific hints how to install them.


## Compiler

For the compilation step, a C++20-compliant compiler is required. Storm is known to work with GCC, Clang, and AppleClang.

## General Dependencies

In the following, we provide an overview over the *required* and *recommended* dependencies of Storm.
*Required* dependencies are absolutely essential for Storm to be compiled and must be installed.
*Recommended* dependencies are optional, but not installing them may severely limit the offered functionality.

Required:
- automake
- cmake
- git
- boost
- ginac
- gmp
- hwloc

Recommended:
- glpk (use z3 instead if glpk is not present)
- z3 (not strictly required, but already needed for standard tasks like PRISM/JANI model building)
- xerces (needed for the parsing and export of XML files, in particular for GSPNs)


## OS specific preparations

We collected some platform specific hints to ease the installation of Storm on the supported operating systems.
Since Storm has some optional dependencies that enhance it's functionality, and some dependencies that are strictly required, we show how to install both the *required* and *recommended* dependencies.
The installation instructions of the *recommended* dependencies already include the *required* dependencies.

{:.alert .alert-info}
We strongly suggest to install the *recommended* dependencies to obtain the full functionality of Storm.


### <i class="fa fa-apple" aria-hidden="true"></i> macOS

Make sure that you use a recent macOS version.
You need to download and install Xcode or its command line tools (CLT) to have the suitable tools needed for compilation. For more details, we refer to [this tutorial](https://www.moncefbelyamani.com/how-to-install-xcode-homebrew-git-rvm-ruby-on-mac/){:target="_blank"}.

Furthermore, we recommend the usage of [Homebrew](https://brew.sh){:target="_blank"} to install the missing packages.

{:.alert .alert-danger}
For troubleshooting building on ARM-based <i class="fa fa-apple" aria-hidden="true"></i>  Apple Silicon CPUs and for building using x86 emulations, please refer to [this page](apple-silicon.html){:.alert-link}.

- Required:
``` console
$ brew install automake cmake boost ginac glpk gmp hwloc
```

- Recommended:
``` console
$ brew install automake cmake boost ginac glpk gmp hwloc xerces-c z3
```


### <i class="icon-debian"></i> Debian and <i class="icon-ubuntu"></i> Ubuntu
<!-- If these are changed, also change them in `vm.md` -->

We currently support Debian from version 12 and Ubuntu from version 24.04.

- Required:
``` console
$ sudo apt-get install automake build-essential cmake git libboost-all-dev libginac-dev libglpk-dev libgmp-dev libhwloc-dev
```

- Recommended
``` console
$ sudo apt-get install automake build-essential cmake git libboost-all-dev libginac-dev libglpk-dev libgmp-dev libhwloc-dev libeigen3-dev libxerces-c-dev libz3-dev
```


## List of dependencies
Storm supports a range of additional libraries for specific tasks in the back-end such as solvers.
We provide a list of supported libraries below.
By default, Storm searches for these libraries automatically and uses them if found.
If a system library was not found, you can provide the location of specific library `X` via the additional CMake argument `-DX_ROOT=/path/to/x` during the configuration process.
A library can be explicitly disabled by providing the CMake argument `-DSTORM_DISABLE_X`.

### Carl
[CArL](https://github.com/moves-rwth/carl-storm) is a computer arithmetic and logic library.
It is heavily intertwined with Storm and provides the support for symbolic computations and a wrapper for exact arithmetic.
Carl is automatically downloaded and installed during the Storm build process.
You can configure the repository and git tag where carl is obtained by the CMake arguments `-DSTORM_CARL_GIT_REPO` and `-DSTORM_CARL_GIT_TAG`.
To use an existing local copy of the carl repository, you can provide the location via `-DFETCHCONTENT_SOURCE_DIR_CARL=/path/to/carl/repo` during CMake configuration.
Note that Storm only uses the sources from this directory, but still builds the carl library.
The use of Carl cannot be disabled.

### GLPK
[GLPK](https://www.gnu.org/software/glpk/){:target="_blank"} is a solver for linear programming (LP), mixed integer programming (MIP) and related problems.
The location of GLPK can be given via `-DGLPK_ROOT=/path/to/glpk`.

### GMM
[gmm++](https://getfem.org/gmm.html){:target="_blank"} is a library for sparse linear algebra operations.
Storm automatically ships with gmm++.

### Gurobi
[Gurobi](https://www.gurobi.com/){:target="_blank"} is a commercial high-performance solver for (mixed-integer) linear programming (and similar problems).
A free license can be obtained for academic purposes.
Storm provides an implementation of its (MI)LP solver interface that uses Gurobi (provided Storm has been compiled with support for it).
The location of Gurobi can be given via `-DGUROBI_ROOT=/path/to/gurobi`.

### MathSat
[MathSAT](https://mathsat.fbk.eu/){:target="_blank"} is a high-performance SMT solver that can be used as an alternative to Z3.
In contrast to Z3, it provides native support for AllSat (enumeration of all satisfying models of a formula) and may generate Craig interpolants.
This makes MathSAT particularly useful in the [abstraction-refinement engine]({{ '/documentation/background/engines.html#abstraction-refinement' | relative_url }}).
The location of MathSAT can be given via `-DMATHSAT_ROOT=/path/to/mathsat/root` where MathSAT's root directory is required to contain the `include` and `lib` folders with the appropriate files (if you download and unpack it, its the directory into which you unpacked it).

### Soplex
[SoPlex](https://soplex.zib.de/){:target="_blank"} is a solver for linear programs.
The location of Soplex can be given via `-DSOPLEX_ROOT=/path/to/soplex`.

### Spot
[Spot](https://spot.lre.epita.fr/){:target="_blank"} is a library for LTL.
Storm depends on Spot for model checking LTL queries.
To use a system version of Spot, set the path in `-DSPOT_ROOT=/path/to/spot`.
Alternatively, you can force Storm to automatically download and build Spot by giving the CMake option `-DSTORM_SPOT_FORCE_SHIPPED=ON`.

### Xerces
[Xerces](https://xerces.apache.org/){:target="_blank"} is a library for XML parsing.
It is used in Storm to parse [GSPN models]({{ '/documentation/background/languages.html#gspns' | relative_url }}) in the `storm-gspn` library.
The location of Xerces can be given via `-DXERCES_ROOT=/path/to/xerces`.

### Z3
[Z3](https://github.com/Z3Prover/z3){:target="_blank"} is a SMT solving.
Storm makes heavy use of Z3 for parsing and evaluating expressing.
Without Z3, Storm has very limited functionality.
The location of Z3 can be given via `-DZ3_ROOT=/path/to/z3`.


### Additional libraries
Storms uses the following additional libraries for some of its functionality.
- [Boost](https://www.boost.org){:target="_blank"}: just-in-time compilation, parsing of the PRISM language & properties, various other tasks
- [CLN](https://www.ginac.de/CLN/){:target="_blank"}: exact number representation
- [CMake](https://cmake.org){:target="_blank"}: build system
- [cpphoafparser](https://automata.tools/hoa/cpphoafparser/){:target="_blank"}: parser of ω-automata
- [CUDD](https://github.com/ivmai/cudd){:target="_blank"}: an MTBDD library available in the DD-related engines
- [Eigen](https://eigen.tuxfamily.org){:target="_blank"}: sparse linear algebra
- [ExprTk](https://www.partow.net/programming/exprtk/index.html){:target="_blank"}: parsing of mathematical expressions
- [GTest](https://github.com/google/googletest){:target="_blank"}: testing infrastructure
- [L3pp](https://github.com/hbruintjes/l3pp){:target="_blank"}: logging
- [ModernJSON](https://json.nlohmann.me/){:target="_blank"}: parser for JSON
- [Parallel Hashmap](https://github.com/greg7mdp/parallel-hashmap){:target="_blank"}: hashmap
- [PRISM](https://www.prismmodelchecker.org){:target="_blank"}: source of some CUDD extensions for MTBDD based model checking
- [Sylvan](https://trolando.github.io/sylvan/){:target="_blank"}: an MTBDD library available in the DD-related engines
{:target="_blank"}:

## Acknowledgements
A large number of dependencies contribute to the capabilities of Storm.
We would like to thank the developers of all previously mentioned tools.
