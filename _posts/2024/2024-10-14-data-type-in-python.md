---
title: 파이썬에서 사용하는 자료형
date: 2024-10-14
categories: Project
tags:
  - python
mermaid: true
---

## 파이썬에서 사용하는 자료형

```mermaid
flowchart TB
    11["list [1,2,3]"]
    12["tuple (1,2,3)"]
    13["dictionary {'a':1, 'b':2}"]
    21["np.array (list)"]
    31["Series (data)"]
    32["DataFrame (data)"]

    subgraph sg1[Python]
    direction LR
    11
    12
    13
    end

    subgraph sg2[Numpy]
    21
    end

    subgraph sg3[Pandas]
    direction LR
    31
    32
    end

sg1 --> sg2 --> sg3
```

_\_EOF\__
