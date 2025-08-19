# nanarinostyl/vue

[![pnpm v9](https://img.shields.io/badge/maintained%20with-pnpm%209.0-cc00ff.svg?style=for-the-badge&logo=pnpm)](https://pnpm.io/)
[![nodejs v20](https://img.shields.io/badge/Node.js-v20.17.0-026e00.svg?style=for-the-badge&logo=nodedotjs)](https://nodejs.org/)

一个 [nanarinostyl](https://nanarino.github.io/stylus/) 主題的 [vue3](https://vuejs.org/) 元件合集

## 開發

```bash
pnpm i
pnpm dev
```

### 约束

爲了可以源碼引入，不要使用路徑別名如 `@`

爲了可以離線訪問，不要用網路元件如 `<iconify-icon />`

## 利用

元件暫時未計劃發佈到 [npm](https://www.npmjs.com/), 可以按以下方式安裝, 或者直接拷貝到自己的專案

```diff
// package.json
{
  "dependencies": {
+    "@nanarinostyl/vue": "github:nanarino/na-vue",
  }
}
```

```shell
pnpm i nanarinostyl
pnpm update @nanarinostyl/vue
```

樣式套件引入：

```astro
---
import nanarinostyl from "nanarinostyl?url"
---
<html lang="en-HK">
    <head>
        <link rel="stylesheet" href={nanarinostyl} />
    </head>
    <body>
        <slot />
    </body>
</html>
```

若使用 css in js 方式引入，有些打包器（如 vite）在構建后纔會將其置於 `<head />` 中，開發環境出現 [FOUC](https://en.wikipedia.org/wiki/Flash_of_unstyled_content) 問題是正常的

```ts
// css in js
import "nanarinostyl"
```

但是初始化明暗的脚本不應該使用 `import` 引入

```astro
<html lang="en-HK">
    <head>
        <script is:inline>
            document.documentElement.dataset["theme"] =
                localStorage.getItem("theme") ??
                ["dark", "light"][
                    +!window.matchMedia?.("(prefers-color-scheme: dark)")?.matches
                ]
        </script>
    </head>
    <body>
        <slot />
    </body>
</html>
```
