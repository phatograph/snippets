### Writing CSS

We favour `grid` over `flex`. If it's a layout, go for `grid`,
and if the layout is horizontally dynamic (i.e. you aren't sure how many elements there are,
something like taglist, and vertically dynamic plays well with `grid`), go for `flex`.

We're using an extended [BEM](https://en.bem.info/methodology/css/) methodology. By extended it means
the idea is the same, but for naming you may nest Elements
and have their depth as deep as you like.

Try not to use native-nest (e.g. `.Block { p { … } }`) as much as you can.
Only do it when you really need to override something (e.g. check out `.BuyerAdminOrdersIndex .Placeholder`).

As for an example, here goes;

```scss
// Blocks are PascalCase.
.Block {
  &__element-level-1 {
    …

    // Elements and Modifiers are kebab-case.
    &--modifier-1 {
      …
    }

    &__element-level-2 {
      …

      &--modifier-1 {
        …
      }
    }
  }
}
```

This would suffice;

```html
<div class="Block">
  <div class="Block__element-level-1">
    <div class="Block__element-level-1__element__level-2" />
    <div class="Block__element-level-1__element__level-2 Block__element-level-1__element__level-2--modifier-1" />
  </div>

  <div class="Block__element-level-1 Block__element-level-1--modifier-1" />
</div>
```
