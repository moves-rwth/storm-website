---
layout: post
title:  "Repositories moved to github.com/stormchecker"
date:   2026-03-26 13:00:00 +0200
tags: ['tool']
---

The Storm repositories have a new home on GitHub: the [stormchecker organization](https://github.com/stormchecker/).

<!--more-->
The old location [moves-rwth](https://github.com/moves-rwth) reflected the starting point and initial development of Storm in the [MOVES group](https://moves.rwth-aachen.de/) at RWTH Aachen University.
We now introduce a dedicated organization [stormchecker](https://github.com/stormchecker/) to reflect the extended development scope of Storm and the broadening ecosystem around Storm with libraries such as [stormpy](https://stormchecker.github.io/stormpy/) and [Stormvogel](https://stormchecker.github.io/stormvogel/).

Old references to `moves-rwth` should automatically be redirected to the new `stormchecker` organization.

You can update the link of your local Git repository with `git remote set-url`.
For example, the following command updates the `origin` remote for the Storm repository:
```
git remote set-url origin git@github.com:stormchecker/storm.git
```
Please [let us know](https://www.stormchecker.org/documentation/obtain-storm/troubleshooting.html#file-an-issue) in case you found dead links or encounter any issue.
