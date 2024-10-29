---
title: Editor.js
tags:
  - blog
---

## Editor.js

I was having a very difficult time setting up editor.js with my blog because the framework I am working with is server side rendered and uses typescript. I am getting a strange type error when I render the component (but at least I can render the component)

````ts
Uncaught TypeError: Cannot read properties of null (reading 'dataset')
````

````tsx
<ClientOnly>
	{() => <EditorJsWrapper />}
</ClientOnly>
````

Solution:
I found out that the issue was actually being caused by my `<ThemeProvider/>`
and once I figured out my solution for passing the `className="theme--${theme}"` upwards to the `html` and `body` elements the error resolved itself.

WIP:
Form data to actually update blog posts
Success!
I was actually able to do this somehow! I was very shocked not gonna lie. I found out that I need to render the editorjs instance and the editorjs-html react instance within the `<ClientOnly>` wrapper.
