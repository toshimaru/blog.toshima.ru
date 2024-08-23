---
layout: post
title: Case Statement in Bash
tags: bash
---

The case statetement in Bash is as follows:

```bash
#!/bin/bash

variable="something"

case $variable in
  pattern1)
    echo "Matched pattern1"
    ;;
  pattern2)
    echo "Matched pattern2"
    ;;
  pattern3|pattern4)
    echo "Matched pattern3 or pattern4"
    ;;
  *)
    echo "No match"
    ;;
esac
```

## Test the script

Let's test the script with some different values of the variable:

```bash
variable="something" #=> No match
```

```bash
variable="pattern2" #=> Matched pattern2
```

```bash
variable="pattern3" #=> Matched pattern3 or pattern4
variable="pattern4" #=> Matched pattern3 or pattern4
```
