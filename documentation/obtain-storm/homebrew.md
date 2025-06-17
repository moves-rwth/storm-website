---
title: Install via Homebrew
layout: default
documentation: true
category_weight: 4
categories: [Obtain Storm]
---

# Install Storm via Homebrew

{:.alert .alert-danger}
This installation method is currently not compatible with [Stormpy](https://moves-rwth.github.io/stormpy/){:target="_blank" .alert-link}—the python bindings of Storm.
If you plan to use Stormpy, you should [build Storm from source](build.html){:.alert-link}.

On macOS, you can use [homebrew](https://brew.sh/){:target="_blank"}, the "missing package manager for macOS" to install Storm.
Once you have installed Homebrew, you need to make Homebrew aware of how to install Storm. In brew-speak, you need to *tap* the Storm Homebrew formulas

```console
$ brew tap moves-rwth/storm
```

Then, installing Storm is as easy as

```console
$ brew install stormchecker
```

This will install Storm and all necessary and some recommended dependencies. More options provided by the package can be seen by invoking

```console
$ brew info stormchecker
```

After installing the package, you should directly be able to invoke

```console
$ storm
```

and continue with the guide on how to [run Storm]({{ '/documentation/usage/running-storm.html' | relative_url }}).

