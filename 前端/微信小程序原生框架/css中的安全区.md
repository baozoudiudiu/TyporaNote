在css中适配顶部和底部安全区

* 底部 `safe-area-inset-bottom`

```css
.className {
  ...
  bottom: calc(40px +  constant(safe-area-inset-bottom));
	bottom: calc(40px +  env(safe-area-inset-bottom));
  ...
}
```

* 顶部`safe-area-inset-top`

```css
.className {
  ...
	top: calc(40px +  constant(safe-area-inset-bottom));
	top: calc(40px +  env(safe-area-inset-bottom));
  ...
}
```

