---
title: Troubleshooting
layout: default
documentation: true
category_weight: 7
categories: [Obtain Storm]
---

<h1>Troubleshooting</h1>

{% include includes/toc.html %}

## Dependencies
- In general, if issues occur installing certain dependencies of Storm make sure to also consult the documentation of the corresponding dependency.

### CArL
- When manually installing CArL make sure you are using the [Carl-storm] (https://github.com/moves-rwth/carl-storm) repository which is compatible with the latest Storm versions.

## OS specific issues
We list common issues for specific operating systems.

### <i class="fa fa-apple" aria-hidden="true"></i> macOS

- Make sure to have Xcode and its command line utilities installed:
  ``` console
  $ xcode-select --install
  ```

- Start Xcode at least once such that required components might be installed automatically.

- For macOS 10.14 "Mojave" a common error is the following:
  ``` console
  configure: error: cannot run C compiled programs.
  ```
  This error might be due to missing header files which can be installed by the following tool:
  ``` console
  $ open /Library/Developer/CommandLineTools/Packages/macOS_SDK_headers_for_macOS_10.14.pkg
  ```
  For more infos see this [GitHub issue](https://github.com/neovim/neovim/issues/9050#issuecomment-424417456).
  
- Additional steps and common issues for ARM-based Apple Silicon CPUs are outlined on [this](apple-silicon.html) page.

## File an issue

If you encounter problems when building (or using) Storm, feel free to [contact us]({{ '/about.html#people' | relative_url }}) by writing a mail to
- <i class="fa fa-envelope" aria-hidden="true"></i> support ```at``` stormchecker.org.

You may also open an [issue on GitHub](https://github.com/moves-rwth/storm/issues){:target="_blank"}. In any case, please provide as much information on your problem as you possibly can. For example, when [the build step](build.html#build-step) fails, please provide the output of `cmake` in the configuration step and details about your operating system, your machine and any other information that is potentially relevant.
