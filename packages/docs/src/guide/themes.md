# Themes

Themes categorizes the different kinds of popper you want to have in your application. For example, you'll usually need "tooltips", "dropdowns" or "menus".

Each kind of popper look and behave differently. Themes allow you to easily configure your popper components for a specific purpose.

By default, v-tooltip provides three themes:
- `tooltip` (used by the `v-tooltip` directive and the `VTooltip` component)
- `dropdown` (used by the `VDropdown` component)
- `menu` (used by the `VMenu` component)

The theme of a popper directive or component can be changed with the `theme` prop:

```vue
<button v-tooltip="{
  theme: 'dropdown'
}">
```

```vue
<VDropdown
  theme="menu"
>
```

Each theme is described by an object that can contain default values of all [available props](../api/).

For example, this `info-tooltip` theme:

```js
Vue.use(VTooltip, {
  themes: {
    'info-tooltip': {
      offset: [0, 24],
      delay: { show: 1000, hide: 0 },
    },
  },
})
```

See the [global configuration](./config.md#default-values) for the values used in the default themes.

## Custom theme

To customize your tooltips and other popovers, you can create themes:

```js
Vue.use(VTooltip, {
  themes: {
    'info-tooltip': {
      $extend: 'tooltip',
      // Other options (see the 'Global options' section)
    },
  },
})
```

Here, `$extend: 'tooltip'` extends the `tooltip` theme defined by default inside `v-tooltip`, so all its options and CSS classes are inherited.

If you don't want to inherit the CSS classes, use `$resetCss`:

```js
Vue.use(VTooltip, {
  themes: {
    'info-tooltip': {
      $extend: 'tooltip',
      $resetCss: true,
    },
  },
})
```

To use the new theme, specify it on the directive:

```vue
<button v-tooltip="{
  content: 'You have ' + count + ' new messages.',
  theme: 'info-tooltip'
}">
```

Then you can customize the CSS for this theme:

```css
.v-popper--theme-info-tooltip {
  $color: rgba(#004499, .9);
}
```

::: tip
You can use the [Theme Editor](../theme-editor.md) to build your v-tooltip themes!
:::

## Theme component

TODO

```js
Vue.use(VTooltip, {
  themes: {
    'info-dropdown': {
      $extend: 'dropdown',
      // Other options (see the 'Global options' section)
      placement: 'right',
      delay: 300,
    },
  },
})
```

```vue
<script>
import { PopperWrapper } from 'v-tooltip'

export default {
  ...PopperWrapper,
  name: 'VInfoDropdown',
  vPopperTheme: 'info-dropdown',
}
</script>

<style>
.v-popper--theme-info-dropdown .v-popper__inner {
  background: #004499;
}

.v-popper--theme-info-dropdown .v-popper__arrow {
  border-color: #004499;
}
</style>
```

```vue
<VInfoDropdown>
  <button>My customized dropdown</button>

  <template #popper>
    Hello world
  </template>
</VInfoDropdown>
```