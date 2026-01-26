---
title: DRN input format
layout: default
documentation: true
category_weight: 2
categories: [languages]
---

<h1>DRN input format</h1>

{% include includes/toc.html %}


The *DiRect eNcoding format (DRN)* is a Storm-specific explicit format.
It is inspired by existing [explicit formats]({{ '/documentation/background/languages.html#explicit' | relative_url }}) and extends it to all supported model types.
DRN files can be automatically generated for models loaded into Storm via another input language.
A DRN file can then be exported via the flag `-drn <output_file.drn>` or the more general command `--exportbuild <output_file.drn>`.

DRN files are explicit files and are therefore human-readable.
In the following, we describe the file structure.


## File structure
In DRN files, anything after `//` is a **comment**, and will be ignored. Comments should be on their own line.

### Header sections
Generally, files are a list of **sections**, where the first sections provide general information on the model.
Each section starts with an `@` and an identifier describing what kind of section it is. Each section occurs only once.

Section `@type: <model_type>` indicates the **model type**: DTMC, MDP, CTMC, Markov Automaton, POMDP.

Section `@nr_states` provides the total **number of states** in the next line.
Similarly, section `@nr_choices` provides the total **number of choices** (also called actions) of the model in the next line.
For deterministic models, the number of states and the number of actions coincide.

### Optional sections
The following are **optional** sections and can be omitted if not relevant.

Section `@parameters` provides the **parameter names** for parametric models. The following line contains the parameter names separated by a whitespace. An example is `p q` for two parameters.

Section `@placeholders` allows to provide **placeholder names** for common expressions. These placeholders can then later be referenced.
Each following line contains one placeholder described as follows `$placeholdername:expression`.

Section `@reward_models` provides the names of the **reward models**. The following line contains the reward models separated by a whitespace.


### Transition relation
The last section is `@model` which describes the transition relation.
The transition relation lists all states explicitly and has the following form:

```bash
state <state_id> {<observation} [<rewards>] !<exit_rate> <labels>
	action <action_id> [<rewards>] <labels>
		<successor_state_id> : <probability>
		<successor_state_id> : <probability>
		...
	action <action_id> [<rewards>]
...
```

#### States
Each state has a **state id** `<state_id>`, which is generally just a number from 0 to nr_states - 1.

For partially observable models, the **observation class** id can be given in braces `{<observation>}`.

The **state rewards** are optional and can be given in `<rewards>`. The rewards are given as a list of comma-separated values where each value correspond to a reward model previously defined in the reward section. The order of rewards here must match the order given in `@reward_models`.

For continuous-time models, the **exit rate** of each state must be given with an exclamation point `!<exit_rate>`.

**Labels** are used to identify states, the initial state must be labeled with `init`, other labels can be an arbitrary string. Labels are separated by whitespace and can optionally be enclosed in quotation marks `"label_1"`.

#### Actions
For each state, all actions are listed, line by line.
Again actions have an **action id** <action_id>, which is typically just a number. Optionally, **choice rewards** and **choice labels** can be given.

#### Transitions
Then, the successor states for taking this action in this state are listed, as key-value pairs of transitions with the state id of the **successor state** and the **transition probability** to move there.


## Example file
An extract of an example DRN file is provided below:

```bash
// Exported by storm
// Original model type: MDP
@type: MDP
@parameters

@reward_models
coinflips
@nr_states
169
@model
state 0 [0] init
	action 0 [1]
		1 : 0.5
		2 : 0.5
	action 1 [1]
		3 : 0.5
		4 : 0.5
...
```
