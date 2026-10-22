# 精灵立绘放这里

命名用 `SPIRITS` 里的 `id`，例如 `phoenix.webp`、`golem.webp`。

然后在 `index.html` 的 `SPIRITS` 条目里加一行：

```js
art: 'assets/spirits/phoenix.webp',
```

没加 `art` 的精灵继续用 emoji，所以可以逐只替换。
建议 256×256、透明底、webp（png 也行）。
加载失败会自动退回 emoji。
