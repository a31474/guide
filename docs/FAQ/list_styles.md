---
tags: [code]
---

# 如何为列表的每个层级指定不同的样式？

群友的魔法

```typst no-render
#let fn-sequence = [ a].func()
#let styled-list(..funcs, body, applied: x => x) = {
  let funcs = funcs.pos()
  body.children.map(x => {
    if x.func() != list.item {
      applied(x)
    } else {
      let body = if x.body.func() == fn-sequence {
        styled-list(
          ..funcs.slice(1),
          funcs.at(0), 
          x.body,
          applied: funcs.at(0)
        )
      } else {
        funcs.at(0)(x.body)
      }
      list.item(body)
    }
  }).sum()
}
```