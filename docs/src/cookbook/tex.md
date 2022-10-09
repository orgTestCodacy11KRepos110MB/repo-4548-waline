---
title: 使用自定义 TEX 渲染器
---

本指南将指导你设置自己的 Tex 渲染器。

<!-- more -->

## 一个使用 KaTeX 的案例

有关 KaTeX 选项，请参阅 [KaTeX API](https://katex.org/docs/api.html#server-side-rendering-or-rendering-to-a-string)。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Waline highlighter 案例</title>
    <link
      rel="stylesheet"
      href="https://unpkg.com/@waline/client@v2/dist/waline.css"
    />
    <link
      rel="stylesheet"
      href="https://unpkg.com/katex@v0.16/dist/katex.min.css"
    />
  </head>
  <body>
    <div id="waline" style="max-width: 800px; margin: 0 auto"></div>
    <script type="module">
      import { init } from '"https://unpkg.com/@waline/client@v2/dist/waline.mjs"';
      import katex from 'https://unpkg.com/katex@0.16/dist/katex.mjs';

      init({
        el: '#waline',
        serverURL: 'https://waline.vercel.app',
        path: '/',
        lang: 'en-US',
        texRenderer: (blockmode, tex) =>
          katex.renderToString(tex, {
            displayMode: blockmode,
            throwOnError: false,
          }),
      });
    </script>
  </body>
</html>
```

## 一个使用 MathJax 的案例

有关 MathJax 选项，请参阅 [MathJax API](http://docs.mathjax.org/en/latest/web/typeset.html#converting-a-math-string-to-other-formats)。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Waline highlighter 案例</title>
    <link
      rel="stylesheet"
      href="https://unpkg.com/@waline/client@v2/dist/waline.css"
    />
    <script src="https://unpkg.com/mathjax@v3/es5/tex-svg.js"></script>
  </head>
  <body>
    <div id="waline" style="max-width: 800px; margin: 0 auto"></div>
    <script type="module">
      import { init } from '"https://unpkg.com/@waline/client@v2/dist/waline.mjs"';

      init({
        el: '#waline',
        serverURL: 'https://waline.vercel.app',
        path: '/',
        lang: 'en-US',
        texRenderer: (blockmode, tex) =>
          window.MathJax.startup.adaptor.outerHTML(
            window.MathJax.tex2svg(tex, {
              display: blockmode,
            })
          ),
      });
    </script>
  </body>
</html>
```