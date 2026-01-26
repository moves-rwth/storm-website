---
title: DFT input format
layout: default
documentation: true
category_weight: 3
categories: [Languages]
---

<h1>DFT Input formats</h1>

{% include includes/toc.html %}


There are two main input formats for DFTs: the [Galileo format](#galileo) and our own [JSON format](#json).


## Galileo
The original description of the Galileo format can be found in the [Galileo manual](https://www.cse.msu.edu/~cse870/Materials/FaultTolerant/manual-galileo.htm#Editing%20in%20the%20Textual%20View).
A good overview is also given on the [FFORT website](https://dftbenchmarks.utwente.nl/ffort/galileo.html).

Elements in the Galileo format are identified by their unique name.
Names cannot contain whitespace characters.

DFT gates are defined per line in the form `"Name" type "Child1" "Child2" .. "ChildN";`.
Basic events are defined by the arguments of their distribution, e.g., `"Name" lambda=x dorm=y;`.

The top-level event of the DFT is given by `toplevel "Name"`.

### DFT gates
Storm has parsing support for all elements of the original Galileo format.
However, some elements and parameters might not be supported in the analysis and will lead to an error message.

In the following, we list all supported DFT elements:
- **AND-gate** with type `and`
- **OR-gate** with type `or`
- **VOTing-gate** with either:
  - `votk` where `k` is a number, or 
  - `kofn` which is the same as `votk`
- **Priority-AND-gate (PAND)** with either:
  - `pand` which is inclusive by default
  - `pand-incl` or `pand<=` for inclusive PAND
  - `pand-excl` or `pand<` for exclusive PAND
- **Priority-OR-gate (POR)** with either:
  - `por` which is inclusive by default
  - `por-incl` or `por<=` for inclusive POR
  - `por-excl` or `por<` for exclusive POR
- **SPARE-gate** with one of:
  - `wsp`, `hsp`, `csp`, `spare`.  All four definitions behave the same as the dormancy factor is defined per BE.
- **SEQence enforcer** with type `seq`
- **Mutual exclusion (MUTEX)** with type`mutex`
- **Functional dependency (FDEP)** with type `fdep`
- **Probabilistic dependency (PDEP)** with type `pdep=p` where `p` is a rational probability.

Note that while parsing is supported for all listed elements, the DFT analysis excludes some element variants.
Most notably, only inclusive variants of PAND and POR are supported.

### Basic events (BE)
Storm has parsing support for all failure distributions specified in the original Galileo format.
However, non-exponential distributions are not supported for Markovian analysis.

In the following, we list all supported BE types. Let `x, y, z` be rational numbers and `k` be a positive integer.
- **Constant failed/failsafe** by using argument `prob=1`/`prob=0`.
- **Constant probability distribution** with probability `prob=x` and dormancy `dorm=z`.
- **Exponential distribution** with rate `lambda=x` and dormancy `dorm=z`.
- **Erlang distribution** with rate `lambda=x`, `phases=k` many phases and dormancy `dorm=z`.
- **Weibull distribution** with shape `shape=x` and rate `rate=y`.
- **Log-normal distribution** with mean value `mean=x` and standard deviation `stddev=y`.



## JSON
Storm also supports a custom JSON format to specify DFT.
The JSON format is extended with additional information such as layouting information.

Elements in the JSON format are identified by their unique id.

The toplevel event of the DFT is given by `"toplevel": id`.

The elements are given as a list in `"nodes": [...]` where each element is defined by
```
{
  "classes": "type",   
  "data": {    
    "id": id,
    "name": "Name",           
    "type": "type",
    ...
  },                 
  "group": "nodes"
}
```
The property `data` contains element-specific information.


### DFT gates
DFT gates give the children as a list of child ids in `data` of the form `"children": [childId1,  childId2, ...]`

In the following, we list all supported DFT types for field `type` and list additional properties.
- **AND-gate** with `"type": "and"`.
- **OR-gate** with `"type": "or"`.
- **VOTing-gate** with `"type": "vot"`. The threshold is given by property `"voting": k`.
- **Priority-AND-gate (PAND)** with `"type": "pand"`. The optional Boolean field `inclusive` distinguishes between inclusive and exclusive (default is True).
- **Priority-OR-gate (POR)** with `"type": "por"`. The optional Boolean field `inclusive` distinguishes between inclusive and exclusive (default is True).
- **SPARE-gate** with `"type": "spare"`.
- **SEQence enforcer** with `"type": "seq"`.
- **Mutual exclusion (MUTEX)** with `"type": "mutex"`.
- **Functional dependency (FDEP)** with `"type": "fdep"`.
- **Probabilistic dependency (PDEP)** with `"type": "pdep"`. The probability is given by property `"probability": p`.

### Basic events (BE)
BEs are given by the type `be`.
We distinguish between different distributions by field `distribution` (default is `exponential`).
We list all supported distributions and their required properties in the following:
- **Constant failed/failsafe** with `"distribution": "const"` and Boolean argument `failed`.
- **Constant probability distribution** with `"distribution": "prob"` and arguments `"probability": x`and `"dorm: z"`.
- **Exponential distribution** with `"distribution": "exponential"` and arguments `"rate": x` and `"dorm: z"`.
- **Erlang distribution** with `"distribution": "erlang"` and arguments `"rate": x`, `"phases": k` and `"dorm: z"`.
- **Weibull distribution** with `"distribution": "weibull"` and arguments `"shape": x` and `"rate: y"`.
- **Log-normal distribution** with `"distribution": "lognormal"` and arguments `"mean": x` and `"stddev: y"`.

