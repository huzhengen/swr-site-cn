# 预请求数据

有很多方法可以为 SWR 预请求数据。对于顶级请求，强烈推荐 [`rel="preload"`](https://developer.mozilla.org/en-US/docs/Web/HTML/Preloading_content)：

```html
<link rel="preload" href="/api/data" as="fetch" crossorigin="anonymous">
```

这将在 JavaScript 开始下载之前预请求数据。而且你传入的 fetch 请求将重用结果(当然包括 SWR)。

另一个选择是有条件地预请求数据。你可以通过 [mutate](/docs/mutation) 来重新请求以及设置缓存：

```js
function prefetch () {
  mutate('/api/data', fetch('/api/data').then(res => res.json()))
  // 第二个参数是个 Promise
  // SWR 将在解析时使用结果
}
```

然后在需要预加载**资源**时使用它（比如当 [hovering](https://github.com/GoogleChromeLabs/quicklink) [a](https://github.com/guess-js/guess) [link](https://instant.page) 时）。  

配合 Next.js 的 [page prefetching](https://nextjs.org/docs#prefetching-pages)，你将能立即加载下一页和数据。
