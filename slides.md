---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
---

# Aspida
-型安全なREST APIとのやり取りを-

---

# Agenda
- What is "Aspida" ?
- How to use
- openapi2aspida
- Conclusion

---

# What is "Aspida" ?
👨‍💻‍こんな経験はないでしょうか？
(`/articles/:articleId?user={userId}`)

```ts{all|7|11,12|all}
type Article = {
    id: number
    content: string
}

const getArticle = async () => {
    const articleId = 'article'
    const userId = 2
    
    const { data } = await axios<Article>.get(
        `/article/${articleId}`,
        { params: userId }
    )
    return data
}
```

---

# What is "Aspida" ?
オレオレ型定義を作るしかないのか。。
思考停止でコードを書きたい！

<div v-click class="text-xl p-2">

そこで、Aspidaの出番!

<img src="public/aspida.png" />

</div>

---

# What is "Aspida" ?
勝手に型補完をしてくれるように

```ts
const getArticle = async () => {
  await aspida.articles._articleId(articleId).$get({ 
    query: { user: userId } 
  })
}
```

Aspidaでできること
- URL文字列のタイピングミスを防げる
- パラメーターの型のミスを防げる
- オレオレ型定義を作るコストを削減できる

---

# How to use

Aspidaの使い方
インストールもこれだけ
axios, fetchなどに対応

```bash
npm install @aspida/axios axios
```

---

# How to use

型定義ファイルの作成
- ファイル・ディレクトリ名をアンダースコアから始めるとパス変数として解釈
- オプションとして'@'で型を指定できる
- デフォルトの型は'string | number'

```ts
// api/articles/_articleId@number.ts

export type Article = {
    id: number
    content: string
}

export type Methods = {
    get: {
        query: {
            user: number
        }
        resBody: Article
    }
}
```

---

# How to use

Scriptを追加する
'--watch'の監視モード起動オプションもあるらしい

```
{
  "scripts": {
    "dev:aspida": "aspida"
  }
}
```

---

# openapi2aspida

APIドキュメントとの連携
- openapi2aspidaでyamlやjsonファイルからTSのファイルへの変換ができる
- ドキュメントさえあれば、型定義ファイルの作成すら不要に

```ts
// api/articles/_articleId@number.ts

export type Article = {
    id: number
    content: string
}

export type Methods = {
    get: {
        query: {
            user: number
        }
        resBody: Article
    }
}
```

---

# Conclusion
- Aspidaで型安全にREST APIリクエストが可能に
- openapi2aspidaで更なる開発体験の向上も



[//]: # (# Welcome to Slidev)

[//]: # ()
[//]: # (Presentation slides for developers)

[//]: # ()
[//]: # (<div class="pt-12">)

[//]: # (  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">)

[//]: # (    Press Space for next page <carbon:arrow-right class="inline"/>)

[//]: # (  </span>)

[//]: # (</div>)

[//]: # ()
[//]: # (<div class="abs-br m-6 flex gap-2">)

[//]: # (  <button @click="$slidev.nav.openInEditor&#40;&#41;" title="Open in Editor" class="text-xl icon-btn opacity-50 !border-none !hover:text-white">)

[//]: # (    <carbon:edit />)

[//]: # (  </button>)

[//]: # (  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub")

[//]: # (    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">)

[//]: # (    <carbon-logo-github />)

[//]: # (  </a>)

[//]: # (</div>)

[//]: # ()
[//]: # (<!--)

[//]: # (The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs]&#40;https://sli.dev/guide/syntax.html#notes&#41;)

[//]: # (-->)

[//]: # ()
[//]: # (---)

[//]: # ()
[//]: # (# What is Slidev?)

[//]: # ()
[//]: # (Slidev is a slides maker and presenter designed for developers, consist of the following features)

[//]: # ()
[//]: # (- 📝 **Text-based** - focus on the content with Markdown, and then style them later)

[//]: # (- 🎨 **Themable** - theme can be shared and used with npm packages)

[//]: # (- 🧑‍💻 **Developer Friendly** - code highlighting, live coding with autocompletion)

[//]: # (- 🤹 **Interactive** - embedding Vue components to enhance your expressions)

[//]: # (- 🎥 **Recording** - built-in recording and camera view)

[//]: # (- 📤 **Portable** - export into PDF, PNGs, or even a hostable SPA)

[//]: # (- 🛠 **Hackable** - anything possible on a webpage)

[//]: # ()
[//]: # (<br>)

[//]: # (<br>)

[//]: # ()
[//]: # (Read more about [Why Slidev?]&#40;https://sli.dev/guide/why&#41;)

[//]: # ()
[//]: # (<!--)

[//]: # (You can have `style` tag in markdown to override the style for the current page.)

[//]: # (Learn more: https://sli.dev/guide/syntax#embedded-styles)

[//]: # (-->)

[//]: # ()
[//]: # (<style>)

[//]: # (h1 {)

[//]: # (  background-color: #2B90B6;)

[//]: # (  background-image: linear-gradient&#40;45deg, #4EC5D4 10%, #146b8c 20%&#41;;)

[//]: # (  background-size: 100%;)

[//]: # (  -webkit-background-clip: text;)

[//]: # (  -moz-background-clip: text;)

[//]: # (  -webkit-text-fill-color: transparent;)

[//]: # (  -moz-text-fill-color: transparent;)

[//]: # (})

[//]: # (</style>)

[//]: # ()
[//]: # (---)

[//]: # ()
[//]: # (# Navigation)

[//]: # ()
[//]: # (Hover on the bottom-left corner to see the navigation's controls panel, [learn more]&#40;https://sli.dev/guide/navigation.html&#41;)

[//]: # ()
[//]: # (### Keyboard Shortcuts)

[//]: # ()
[//]: # (|     |     |)

[//]: # (| --- | --- |)

[//]: # (| <kbd>right</kbd> / <kbd>space</kbd>| next animation or slide |)

[//]: # (| <kbd>left</kbd>  / <kbd>shift</kbd><kbd>space</kbd> | previous animation or slide |)

[//]: # (| <kbd>up</kbd> | previous slide |)

[//]: # (| <kbd>down</kbd> | next slide |)

[//]: # ()
[//]: # (<!-- https://sli.dev/guide/animations.html#click-animations -->)

[//]: # (<img)

[//]: # (  v-click)

[//]: # (  class="absolute -bottom-9 -left-7 w-80 opacity-50")

[//]: # (  src="https://sli.dev/assets/arrow-bottom-left.svg")

[//]: # (/>)

[//]: # (<p v-after class="absolute bottom-23 left-45 opacity-30 transform -rotate-10">Here!</p>)

[//]: # ()
[//]: # (---)

[//]: # (layout: image-right)

[//]: # (image: https://source.unsplash.com/collection/94734566/1920x1080)

[//]: # (---)

[//]: # ()
[//]: # (# Code)

[//]: # ()
[//]: # (Use code snippets and get the highlighting directly![^1])

[//]: # ()
[//]: # (```ts {all|2|1-6|9|all})

[//]: # (interface User {)

[//]: # (  id: number)

[//]: # (  firstName: string)

[//]: # (  lastName: string)

[//]: # (  role: string)

[//]: # (  text: string)

[//]: # (})

[//]: # ()
[//]: # (function updateUser&#40;id: number, update: User&#41; {)

[//]: # (  const user = getUser&#40;id&#41;)

[//]: # (  const newUser = {...user, ...update}  )

[//]: # (  saveUser&#40;id, newUser&#41;)

[//]: # (})

[//]: # (```)

[//]: # ()
[//]: # (<arrow v-click="3" x1="400" y1="420" x2="230" y2="330" color="#564" width="3" arrowSize="1" />)

[//]: # ()
[//]: # ([^1]: [Learn More]&#40;https://sli.dev/guide/syntax.html#line-highlighting&#41;)

[//]: # ()
[//]: # (<style>)

[//]: # (.footnotes-sep {)

[//]: # (  @apply mt-20 opacity-10;)

[//]: # (})

[//]: # (.footnotes {)

[//]: # (  @apply text-sm opacity-75;)

[//]: # (})

[//]: # (.footnote-backref {)

[//]: # (  display: none;)

[//]: # (})

[//]: # (</style>)

[//]: # ()
[//]: # ()
[//]: # (---)

[//]: # ()
[//]: # (# Components)

[//]: # ()
[//]: # (<div grid="~ cols-2 gap-4">)

[//]: # (<div>)

[//]: # ()
[//]: # (You can use Vue components directly inside your slides.)

[//]: # ()
[//]: # (We have provided a few built-in components like `<Tweet/>` and `<Youtube/>` that you can use directly. And adding your custom components is also super easy.)

[//]: # ()
[//]: # (```html)

[//]: # (<Counter :count="10" />)

[//]: # (```)

[//]: # ()
[//]: # (<!-- ./components/Counter.vue -->)

[//]: # (<Counter :count="10" m="t-4" />)

[//]: # ()
[//]: # (Check out [the guides]&#40;https://sli.dev/builtin/components.html&#41; for more.)

[//]: # ()
[//]: # (</div>)

[//]: # (<div>)

[//]: # ()
[//]: # (```html)

[//]: # (<Tweet id="1390115482657726468" />)

[//]: # (```)

[//]: # ()
[//]: # (<Tweet id="1390115482657726468" scale="0.65" />)

[//]: # ()
[//]: # (</div>)

[//]: # (</div>)

[//]: # ()
[//]: # ()
[//]: # (---)

[//]: # (class: px-20)

[//]: # (---)

[//]: # ()
[//]: # (# Themes)

[//]: # ()
[//]: # (Slidev comes with powerful theming support. Themes can provide styles, layouts, components, or even configurations for tools. Switching between themes by just **one edit** in your frontmatter:)

[//]: # ()
[//]: # (<div grid="~ cols-2 gap-2" m="-t-2">)

[//]: # ()
[//]: # (```yaml)

[//]: # (---)

[//]: # (theme: default)

[//]: # (---)

[//]: # (```)

[//]: # ()
[//]: # (```yaml)

[//]: # (---)

[//]: # (theme: seriph)

[//]: # (---)

[//]: # (```)

[//]: # ()
[//]: # (<img border="rounded" src="https://github.com/slidevjs/themes/blob/main/screenshots/theme-default/01.png?raw=true">)

[//]: # ()
[//]: # (<img border="rounded" src="https://github.com/slidevjs/themes/blob/main/screenshots/theme-seriph/01.png?raw=true">)

[//]: # ()
[//]: # (</div>)

[//]: # ()
[//]: # (Read more about [How to use a theme]&#40;https://sli.dev/themes/use.html&#41; and)

[//]: # (check out the [Awesome Themes Gallery]&#40;https://sli.dev/themes/gallery.html&#41;.)

[//]: # ()
[//]: # (---)

[//]: # (preload: false)

[//]: # (---)

[//]: # ()
[//]: # (# Animations)

[//]: # ()
[//]: # (Animations are powered by [@vueuse/motion]&#40;https://motion.vueuse.org/&#41;.)

[//]: # ()
[//]: # (```html)

[//]: # (<div)

[//]: # (  v-motion)

[//]: # (  :initial="{ x: -80 }")

[//]: # (  :enter="{ x: 0 }">)

[//]: # (  Slidev)

[//]: # (</div>)

[//]: # (```)

[//]: # ()
[//]: # (<div class="w-60 relative mt-6">)

[//]: # (  <div class="relative w-40 h-40">)

[//]: # (    <img)

[//]: # (      v-motion)

[//]: # (      :initial="{ x: 800, y: -100, scale: 1.5, rotate: -50 }")

[//]: # (      :enter="final")

[//]: # (      class="absolute top-0 left-0 right-0 bottom-0")

[//]: # (      src="https://sli.dev/logo-square.png")

[//]: # (    />)

[//]: # (    <img)

[//]: # (      v-motion)

[//]: # (      :initial="{ y: 500, x: -100, scale: 2 }")

[//]: # (      :enter="final")

[//]: # (      class="absolute top-0 left-0 right-0 bottom-0")

[//]: # (      src="https://sli.dev/logo-circle.png")

[//]: # (    />)

[//]: # (    <img)

[//]: # (      v-motion)

[//]: # (      :initial="{ x: 600, y: 400, scale: 2, rotate: 100 }")

[//]: # (      :enter="final")

[//]: # (      class="absolute top-0 left-0 right-0 bottom-0")

[//]: # (      src="https://sli.dev/logo-triangle.png")

[//]: # (    />)

[//]: # (  </div>)

[//]: # ()
[//]: # (  <div)

[//]: # (    class="text-5xl absolute top-14 left-40 text-[#2B90B6] -z-1")

[//]: # (    v-motion)

[//]: # (    :initial="{ x: -80, opacity: 0}")

[//]: # (    :enter="{ x: 0, opacity: 1, transition: { delay: 2000, duration: 1000 } }">)

[//]: # (    Slidev)

[//]: # (  </div>)

[//]: # (</div>)

[//]: # ()
[//]: # (<!-- vue script setup scripts can be directly used in markdown, and will only affects current page -->)

[//]: # (<script setup lang="ts">)

[//]: # (const final = {)

[//]: # (  x: 0,)

[//]: # (  y: 0,)

[//]: # (  rotate: 0,)

[//]: # (  scale: 1,)

[//]: # (  transition: {)

[//]: # (    type: 'spring',)

[//]: # (    damping: 10,)

[//]: # (    stiffness: 20,)

[//]: # (    mass: 2)

[//]: # (  })

[//]: # (})

[//]: # (</script>)

[//]: # ()
[//]: # (<div)

[//]: # (  v-motion)

[//]: # (  :initial="{ x:35, y: 40, opacity: 0}")

[//]: # (  :enter="{ y: 0, opacity: 1, transition: { delay: 3500 } }">)

[//]: # ()
[//]: # ([Learn More]&#40;https://sli.dev/guide/animations.html#motion&#41;)

[//]: # ()
[//]: # (</div>)

[//]: # ()
[//]: # (---)

[//]: # ()
[//]: # (# LaTeX)

[//]: # ()
[//]: # (LaTeX is supported out-of-box powered by [KaTeX]&#40;https://katex.org/&#41;.)

[//]: # ()
[//]: # (<br>)

[//]: # ()
[//]: # (Inline $\sqrt{3x-1}+&#40;1+x&#41;^2$)

[//]: # ()
[//]: # (Block)

[//]: # ($$)

[//]: # (\begin{array}{c})

[//]: # ()
[//]: # (\nabla \times \vec{\mathbf{B}} -\, \frac1c\, \frac{\partial\vec{\mathbf{E}}}{\partial t} &)

[//]: # (= \frac{4\pi}{c}\vec{\mathbf{j}}    \nabla \cdot \vec{\mathbf{E}} & = 4 \pi \rho \\)

[//]: # ()
[//]: # (\nabla \times \vec{\mathbf{E}}\, +\, \frac1c\, \frac{\partial\vec{\mathbf{B}}}{\partial t} & = \vec{\mathbf{0}} \\)

[//]: # ()
[//]: # (\nabla \cdot \vec{\mathbf{B}} & = 0)

[//]: # ()
[//]: # (\end{array})

[//]: # ($$)

[//]: # ()
[//]: # (<br>)

[//]: # ()
[//]: # ([Learn more]&#40;https://sli.dev/guide/syntax#latex&#41;)

[//]: # ()
[//]: # (---)

[//]: # ()
[//]: # (# Diagrams)

[//]: # ()
[//]: # (You can create diagrams / graphs from textual descriptions, directly in your Markdown.)

[//]: # ()
[//]: # (<div class="grid grid-cols-3 gap-10 pt-4 -mb-6">)

[//]: # ()
[//]: # (```mermaid {scale: 0.5})

[//]: # (sequenceDiagram)

[//]: # (    Alice->John: Hello John, how are you?)

[//]: # (    Note over Alice,John: A typical interaction)

[//]: # (```)

[//]: # ()
[//]: # (```mermaid {theme: 'neutral', scale: 0.8})

[//]: # (graph TD)

[//]: # (B[Text] --> C{Decision})

[//]: # (C -->|One| D[Result 1])

[//]: # (C -->|Two| E[Result 2])

[//]: # (```)

[//]: # ()
[//]: # (```plantuml {scale: 0.7})

[//]: # (@startuml)

[//]: # ()
[//]: # (package "Some Group" {)

[//]: # (  HTTP - [First Component])

[//]: # (  [Another Component])

[//]: # (})

[//]: # ()
[//]: # (node "Other Groups" {)

[//]: # (  FTP - [Second Component])

[//]: # (  [First Component] --> FTP)

[//]: # (})

[//]: # ()
[//]: # (cloud {)

[//]: # (  [Example 1])

[//]: # (})

[//]: # ()
[//]: # ()
[//]: # (database "MySql" {)

[//]: # (  folder "This is my folder" {)

[//]: # (    [Folder 3])

[//]: # (  })

[//]: # (  frame "Foo" {)

[//]: # (    [Frame 4])

[//]: # (  })

[//]: # (})

[//]: # ()
[//]: # ()
[//]: # ([Another Component] --> [Example 1])

[//]: # ([Example 1] --> [Folder 3])

[//]: # ([Folder 3] --> [Frame 4])

[//]: # ()
[//]: # (@enduml)

[//]: # (```)

[//]: # ()
[//]: # (</div>)

[//]: # ()
[//]: # ([Learn More]&#40;https://sli.dev/guide/syntax.html#diagrams&#41;)

[//]: # ()
[//]: # ()
[//]: # (---)

[//]: # (layout: center)

[//]: # (class: text-center)

[//]: # (---)

[//]: # ()
[//]: # (# Learn More)

[//]: # ()
[//]: # ([Documentations]&#40;https://sli.dev&#41; · [GitHub]&#40;https://github.com/slidevjs/slidev&#41; · [Showcases]&#40;https://sli.dev/showcases.html&#41;)
