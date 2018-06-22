---
title: Style API
group: Features
order: 6
---

Use q-grid rich css class naming system to apply specific styles. If more dynamic way is required style model can be used.

## CSS

Each cell, no mater if it is located in header, body or footer, has specific set of css class names.

* `q-grid-{column.type}` class name for css selectors which use column types.
* `q-grid-the-{column.key}` class name for css selectors which use column identifiers. Note that `the` article is used to exclude ambiguous names.

## Style Model

Use style callbacks for dynamic class assignments. For the cell style it is possible to pass an object instead of callback. In this case, object keys will play the role of column key filters.

```typescript
@Component({
   selector: 'my-component',
   template: '<q-grid></q-grid>'
})
export class MyComponent {
   ViewChild(GridComponent) myGrid: GridComponent;

   ngAfterViewInit() {
      const { model } = this.myGrid;
      model.style({
         cell: {
            'myColumnKey': (row, column, context) => {
               context.class(`td-${row.name}`, {
                  color: `#${row.color}`,
                  background: '#3f51b5'
               });
            }
         },
         row: (row, context) => {
            if (!row.isActive) {
               context.class('inactive');
            }
         }
      });
   }
}
```

## Grid Component style callbacks

Another way to utilizef style callbacks is appropriate attribute bindings.

```typescript

@Component({
   selector: 'my-component',
   template: `
      <q-grid [styleCell]="styleCell" [styleRow]="styleRow"></q-grid>
   `
})
export class MyComponent {
   styleCell(row, column, context) {
      if (column.key === 'name') {
         context.class(`td-${row.name}`, {
            color: `#${row.color}`,
            background: '#3f51b5'
         });
      }
   }

   styleRow(row, context) {
      if (!row.isActive) {
         context.class('inactive');
      }
   }
}
```

{% docEditor "github/qgrid/ng2-example/tree/style-cell-basic/latest" %}

## How style model works

Every change detection cycle the q-grid traverses through all visible rows and cells to invoke user defined style callbacks. Note that `context.class` method first argument requires to be an unique identifier. Later when callback series is finished style API will produce dynamic stylesheet using pair of context identifier and column key as a css class name. This technique avoids to use inline styles and makes style management easier. Resizing of rows or columns behaves the same way.

Next picture can be found if open element inspector and follow the style section.

<img src="assets/style-api-html.png" type="image/png" />