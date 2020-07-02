---
title: Pagination
---

# Pagination

> A responsive and flexible pagination

---

## Examples

### Base

::: demo

```html
<template>
  <section>
    <o-field grouped group-multiline>
      <o-field label="Total">
        <o-input type="number" v-model="total"></o-input>
      </o-field>
      <o-field label="Items per page">
        <o-input type="number" v-model="perPage"></o-input>
      </o-field>
    </o-field>
    <o-field grouped group-multiline>
      <o-field label="Show buttons before current">
        <o-input type="number" v-model="rangeBefore" min="0"></o-input>
      </o-field>
      <o-field label="Show buttons after current">
        <o-input type="number" v-model="rangeAfter" min="0"></o-input>
      </o-field>
    </o-field>
    <o-field grouped group-multiline>
      <o-field label="Order">
        <o-select v-model="order">
          <option value="">default</option>
          <option value="centered">centered</option>
          <option value="right">right</option>
        </o-select>
      </o-field>
      <o-field label="Size">
        <o-select v-model="size">
          <option value="">default</option>
          <option value="small">small</option>
          <option value="medium">medium</option>
          <option value="large">large</option>
        </o-select>
      </o-field>
    </o-field>
    <o-field grouped group-multiline>
      <o-field label="Previous icon">
        <o-select v-model="prevIcon">
          <option value="chevron-left">Chevron</option>
          <option value="arrow-left">Arrow</option>
        </o-select>
      </o-field>
      <o-field label="Next icon">
        <o-select v-model="nextIcon">
          <option value="chevron-right">Chevron</option>
          <option value="arrow-right">Arrow</option>
        </o-select>
      </o-field>
    </o-field>
    <div class="block">
      <o-switch v-model="isSimple">Simple</o-switch>
      <o-switch v-model="isRounded">Rounded</o-switch>
    </div>

    <hr />
    <o-pagination
      :total="total"
      :current.sync="current"
      :range-before="rangeBefore"
      :range-after="rangeAfter"
      :order="order"
      :size="size"
      :simple="isSimple"
      :rounded="isRounded"
      :per-page="perPage"
      :icon-prev="prevIcon"
      :icon-next="nextIcon"
      aria-next-label="Next page"
      aria-previous-label="Previous page"
      aria-page-label="Page"
      aria-current-label="Current page"
    >
    </o-pagination>
  </section>
</template>

<script>
  export default {
    data() {
      return {
        total: 200,
        current: 10,
        perPage: 10,
        rangeBefore: 3,
        rangeAfter: 1,
        order: "",
        size: "",
        isSimple: false,
        isRounded: false,
        prevIcon: "chevron-left",
        nextIcon: "chevron-right"
      };
    }
  };
</script>
```

:::

### Slots

::: demo

```html
<template>
  <section>
    <o-pagination :total="200" :current.sync="current" :per-page="10">
      <o-pagination-button
        slot-scope="props"
        :page="props.page"
        :id="`page${props.page.number}`"
        tag="router-link"
        :to="`/documentation/pagination#page${props.page.number}`"
      >
        {{ convertToRoman(props.page.number) }}
      </o-pagination-button>

      <o-pagination-button
        slot="previous"
        slot-scope="props"
        :page="props.page"
        tag="router-link"
        :to="`/documentation/pagination#page${props.page.number}`"
      >
        Previous
      </o-pagination-button>

      <o-pagination-button
        slot="next"
        slot-scope="props"
        :page="props.page"
        tag="router-link"
        :to="`/documentation/pagination#page${props.page.number}`"
      >
        Next
      </o-pagination-button>
    </o-pagination>
  </section>
</template>

<script>
  export default {
    data() {
      return {
        current: 10,
        basicRomanNumeral: [
          "",
          "I",
          "II",
          "III",
          "IV",
          "V",
          "VI",
          "VII",
          "VIII",
          "IX",
          "",
          "X",
          "XX",
          "XXX",
          "XL",
          "L",
          "LX",
          "LXX",
          "LXXX",
          "XC",
          "",
          "C",
          "CC",
          "CCC",
          "CD",
          "D",
          "DC",
          "DCC",
          "DCCC",
          "CM",
          "",
          "M",
          "MM",
          "MMM"
        ]
      };
    },
    methods: {
      convertToRoman(num) {
        const numArray = num.toString().split("");
        const base = numArray.length;
        let count = base - 1;
        const convertedRoman = numArray.reduce((roman, digit) => {
          const digitRoman = this.basicRomanNumeral[+digit + count * 10];
          const result = roman + digitRoman;
          count -= 1;
          return result;
        }, "");
        return convertedRoman;
      }
    },
    watch: {
      $route: {
        immediate: true,
        handler(newVal, oldVal) {
          if (newVal.hash) {
            this.current = parseInt(newVal.hash.replace(/\#page/g, ""));
          }
        }
      }
    }
  };
</script>
```

:::

## Props

| Prop name         | Description | Type           | Values | Default                                                                                                                                                                                                                                 |
| ----------------- | ----------- | -------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| total             |             | number\|string | -      |                                                                                                                                                                                                                                         |
| perPage           |             | number\|string | -      | 20                                                                                                                                                                                                                                      |
| current           |             | number\|string | -      | 1                                                                                                                                                                                                                                       |
| rangeBefore       |             | number\|string | -      | 1                                                                                                                                                                                                                                       |
| rangeAfter        |             | number\|string | -      | 1                                                                                                                                                                                                                                       |
| size              |             | string         | -      |                                                                                                                                                                                                                                         |
| simple            |             | boolean        | -      |                                                                                                                                                                                                                                         |
| rounded           |             | boolean        | -      |                                                                                                                                                                                                                                         |
| order             |             | string         | -      |                                                                                                                                                                                                                                         |
| iconPack          |             | string         | -      |                                                                                                                                                                                                                                         |
| iconPrev          |             | string         | -      | () => getValueByPath(config, 'pagination.iconPrev', 'chevron-left')                                                                                                                                                                     |
| iconNext          |             | string         | -      | () => getValueByPath(config, 'pagination.iconNext', 'chevron-right')                                                                                                                                                                    |
| ariaNextLabel     |             | string         | -      |                                                                                                                                                                                                                                         |
| ariaPreviousLabel |             | string         | -      |                                                                                                                                                                                                                                         |
| ariaPageLabel     |             | string         | -      |                                                                                                                                                                                                                                         |
| ariaCurrentLabel  |             | string         | -      |                                                                                                                                                                                                                                         |
| rootClass         |             | string         | -      | () => {<br> const override = getValueByPath(config, 'pagination.override', false)<br> const clazz = getValueByPath(config, 'pagination.rootClass', '')<br> return getCssClass(clazz, override, 'o-pagination')<br>}                     |
| prevBtnClass      |             | string         | -      | () => {<br> const override = getValueByPath(config, 'pagination.override', false)<br> const clazz = getValueByPath(config, 'pagination.prevBtnClass', '')<br> return getCssClass(clazz, override, 'o-pagination-previous')<br>}         |
| nextBtnClass      |             | string         | -      | () => {<br> const override = getValueByPath(config, 'pagination.override', false)<br> const clazz = getValueByPath(config, 'pagination.nextBtnClass', '')<br> return getCssClass(clazz, override, 'o-pagination-next')<br>}             |
| listClass         |             | string         | -      | () => {<br> const override = getValueByPath(config, 'pagination.override', false)<br> const clazz = getValueByPath(config, 'pagination.listClass', '')<br> return getCssClass(clazz, override, 'o-pagination-list')<br>}                |
| linkClass         |             | string         | -      | () => {<br> const override = getValueByPath(config, 'pagination.override', false)<br> const clazz = getValueByPath(config, 'pagination.linkClass', '')<br> return getCssClass(clazz, override, 'o-pagination-link')<br>}                |
| linkCurrentClass  |             | string         | -      | () => {<br> const override = getValueByPath(config, 'pagination.override', false)<br> const clazz = getValueByPath(config, 'pagination.linkCurrentClass', '')<br> return getCssClass(clazz, override, 'o-pagination-link-current')<br>} |
| ellipsisClass     |             | string         | -      | () => {<br> const override = getValueByPath(config, 'pagination.override', false)<br> const clazz = getValueByPath(config, 'pagination.ellipsisClass', '')<br> return getCssClass(clazz, override, 'o-pagination-ellipsis')<br>}        |
| infoClass         |             | string         | -      | () => {<br> const override = getValueByPath(config, 'pagination.override', false)<br> const clazz = getValueByPath(config, 'pagination.infoClass', '')<br> return getCssClass(clazz, override, 'o-pagination-info')<br>}                |
| simpleClass       |             | string         | -      | () => {<br> const override = getValueByPath(config, 'pagination.override', false)<br> const clazz = getValueByPath(config, 'pagination.simpleClass', '')<br> return getCssClass(clazz, override, 'o-pagination-simple')<br>}            |
| roundedClass      |             | string         | -      | () => {<br> const override = getValueByPath(config, 'pagination.override', false)<br> const clazz = getValueByPath(config, 'pagination.roundedClass', '')<br> return getCssClass(clazz, override, 'o-pagination-rounded')<br>}          |

## Events

| Event name     | Type      | Description |
| -------------- | --------- | ----------- |
| change         | undefined |
| update:current | undefined |

## Slots

| Name     | Description | Bindings                                                                                                               |
| -------- | ----------- | ---------------------------------------------------------------------------------------------------------------------- |
| previous |             | [<br> {<br> "name": "linkClass"<br> },<br> {<br> "name": "linkCurrentClass"<br> },<br> {<br> "name": "page"<br> }<br>] |
| next     |             | [<br> {<br> "name": "linkClass"<br> },<br> {<br> "name": "linkCurrentClass"<br> },<br> {<br> "name": "page"<br> }<br>] |
| default  |             | [<br> {<br> "name": "page"<br> },<br> {<br> "name": "linkClass"<br> },<br> {<br> "name": "linkCurrentClass"<br> }<br>] |

## Style

| CSS Variable                                     | SASS Variable                              | Default                      |
| ------------------------------------------------ | ------------------------------------------ | ---------------------------- |
| --oruga-pagination-disabled-opacity              | \$pagination-disabled-opacity              | \$base-disabled-opacity      |
| --oruga-pagination-ellipsis-color                | \$pagination-ellipsis-color                | #b5b5b5                      |
| --oruga-pagination-font-size                     | \$pagination-font-size                     | 1rem                         |
| --oruga-pagination-link-border-color             | \$pagination-link-border-color             | #dbdbdb                      |
| --oruga-pagination-link-border-radius            | \$pagination-link-border-radius            | \$base-border-radius         |
| --oruga-pagination-link-border                   | \$pagination-link-border                   | 1px solid transparent        |
| --oruga-pagination-link-color                    | \$pagination-link-color                    | #363636                      |
| --oruga-pagination-link-current-background-color | \$pagination-link-current-background-color | \$primary                    |
| --oruga-pagination-link-current-border-color     | \$pagination-link-current-border-color     | \$primary                    |
| --oruga-pagination-link-current-color            | \$pagination-link-current-color            | #fff                         |
| --oruga-pagination-link-height                   | \$pagination-link-height                   | 2.25em                       |
| --oruga-pagination-link-hover-border-color       | \$pagination-link-hover-border-color       | #b5b5b5                      |
| --oruga-pagination-link-hover-color              | \$pagination-link-hover-color              | #363636                      |
| --oruga-pagination-link-line-height              | \$pagination-link-line-height              | \$base-line-height           |
| --oruga-pagination-link-margin                   | \$pagination-link-margin                   | .25rem                       |
| --oruga-pagination-link-min-width                | \$pagination-link-min-width                | 2.25em                       |
| --oruga-pagination-margin                        | \$pagination-margin                        | -.25rem                      |
| --oruga-pagination-mobile-breakpoint             | \$pagination-mobile-breakpoint             | 1024px                       |
| --oruga-pagination-rounded-border-radius         | \$pagination-rounded-border-radius         | \$base-rounded-border-radius |