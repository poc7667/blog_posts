---
title: salesforce-trigger
date: 2016-11-23 11:24:42
tags: salesforce
---

Triggers are similar to callbacks in `Ruby on Rails`

Types

- before
- after

## idea: Context variables

`Trigger.New` is a Context variable.
Which contains all the records the were inserted in insert or update triggers.

`Trigger.Old`  provides the old version of `sObjects` before they were updated.

Triggers can fire when insert/update via API or Apex in a bulk or not.
