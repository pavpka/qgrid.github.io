---
title: Style API
group: Reference
order: 8
---

Every change detection cycle q-grid goes through all visible rows and cells to invoke user defined style callbacks. Next when callback calls are complete style API will produce dynamic stylesheet using pair of context identifier and column key as css class name, row and column resize works the same. This approach avoids to use inline styles and makes management simple. 

## The Picture

Next picture can be seen in element inspector.

<img src="assets/style-api-html.png" type="image/png" />