---
layout: post
title:  "Block Diagrams"
date:   2024-12-12 08:18:59 -0700
categories: software
---

```nomnoml
[example|
  propertyA: Int
  propertyB: string
|
  methodA()
  methodB()
|
  [subA]--[subB]
  [subA]-:>[sub C]
]
```

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```