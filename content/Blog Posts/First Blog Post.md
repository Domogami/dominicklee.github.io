---
title: My First Blogpost
tags:
  - Blog
---

# My First Blogpost

Hey, my name is Dom and I am a recent Mathematics - Computer Science college graduate from UCSD working as a Software Engineer. Last summer, I had the pleasure of interning at Amazon where I had the opportunity to not only expand my skills but also learn what it is like to be a Software Engineer.

From my experience, Software Engineering is a job centered around constantly learning. As someone who loves going down rabbit-holes and learning about tech in my free time, I have found that I am a perfect fit for this line of work. Although I am sure many people would find this field draining and a constant uphill battle. Acknowledging never ending challenges as one of the key components of being a successful Software Engineer has led me to create this blog which will serve as my own personal knowledge bank as I continue to learn throughout my career.

This first post will center around creating the blog that you are reading this post on right now (if this is still my original blog). It is built using Remix.js which is a new web technology that allows for better routing and faster load times. I chose this technology because it is similar to Next.js but has many added benefits including better form handling with "action loaders" and component error bounds which can display a special UI element for a component that fails to render without crashing the entire page. I first heard about this technology from a coworker on my team at Amazon and decided to give it a shot. What I didn't realize was how many unexpected errors would arise from the decision to build with Remix.js.

## The Easy Part

After completing a wonderful Remix.js tutorial blog and following a tutorial by [Chris Benjamin](https://github.com/cbenjamin2009/remix-blog) I felt confident to create a new Remix project using MongoDB as a backend along with Prisma to interact with the database. This part went surprisingly well and I was able to create not only the routes but also set up SCSS for styling which compiles to CSS in an output directory. As someone who as developed many static sites with no backend, I find frontend development and styling very natural and have memorized nearly all of the SCSS properties necessary to build a webpage that looks decent with a distinct style. I have finally gotten to the point where I can go from idea to implementation with very little friction. The same cannot be said for my backend experience.

## Choosing an Editor

Once I began brainstorming and designing the backend for my blog I began realizing that I want an easy way to edit and type up new blogposts and that I needed an Admin page to do this. I began by looking into live markdown compilers for websites similar to embedding something like Obsidian or markdown into an edit page. After a bit of research I fell in love with [Editor.js](https://editorjs.io/) which is an open source block editor that felt very similar to Notion which is what I used throughout my senior year of college. I decided that this was perfect and decided to embed it into my edit-blog-post page. I would love to say that this was an easy task but unfortunately this is where my decision to develop with Remix began testing my patience. Editor.js does not work well with SSR at the moment and I found many posts with similar [issues](https://github.com/Jungwoo-An/react-editor-js/issues/58) regarding the 'window' being undefined. Sadly, it seemed that Next.js has a larger community than Remix.js and it took me quite some time to find the solution to this problem. To get around the server side rendering issues with Editor.js on Remix I had to do the following

````tsx
import EditorJS from '~/editorjs.client.tsx';
import { ClientOnly } from 'remix-utils';

// Component rendering Editorjs
export default function Editor() {
	return (
		<ClientOnly>
			{() => <EditorJS />}
		</ClientOnly>
	);
}
````

Using the ClientOnly component from remix-utils and naming the editor component file with the extension `.client.tsx` ended up solving the issue for me. Editor.js cannot currently be rendered on the server so it must be rendered on the client side in order to work as expected. With the editor working I thought that finally the rest would be smooth sailing but alas, I had only just begun.

## Images with S3

One of the features that I believed my blog needed to have was the ability to have images embedded within each post. What good is a blog about the things that I learn if I cannot make use of visual aids and images to better convey my messages. I turned to my friend Shravan to ask how best to store images using MongoDB and to my dismay I found that Mongo was not the best way to store images. Instead, it is better to use a middleware tool like Multer in coordination with an S3 storage bucket which is a better way to store files and images. MongoDB then stores the URL to the uploaded photo. Unfortunately this is another pain point for Remix.js that I did not realize before I decided to embark on this painful journey.

## Problems with Multer

Multer is a middleware that allows a file to be downloaded by the server side of an application and stored locally then uploaded to a cloud service like AWS S3. Unfortunately because Remix does not have the request and response objects of Node/Connect/Express there is no way to run Multer and it is very difficult to run middleware or an Express server because Remix itself is an express server. Not being able to use Multer made things quite challenging and I ended up needing to upload everything to S3 directly. Additionally because I was having issues with 64 bit filestreams, I ended up creating a Netlify function (very similar to an AWS Lambda Function) that generates a unique upload link that I can use from the frontend to directly upload the file. This ended up being extremely useful because now with one function I can upload an image and as a response the public URL is returned.

## Editor.js to HTML

Now that I am able to successfully upload images it is time to bring it all together. I stumbled across a library that allows editor.js to be converted to HTML, elegantly named [editors-html](https://www.npmjs.com/package/editorjs-html), which gives me full control to style each component of each blogpost. 

After a bit of front end witchcraft and tedious styling, my blog was finally coming together, but before I could write any blogposts, I decided that there needed to be a color scheme that supports light mode and dark mode. 

## Color scheme

For this site, I wanted to have a light mode and a dark mode for greater flexibility and a more functional UX. I also wanted the theme to span the entire website and be loaded in from the browsers memory to preserve dark mode every time you visit the site.

I ended up wrapping the entire application in a ThemeProvider component that changes the background and color css properties according to the selected theme.

````tsx
const ThemeProvider = (props) => {
	return (
		<ThemeContext.Provider value={{ theme, setTheme }}>
			<div className={`theme--${props.theme}`}>{props.children}</div>
		</ThemeContext.Provider>
	);
};
````

The following scss code creates a mixin that can be used across scss files to add a custom theme-specific style to specified components.

````scss
@mixin themed() {
  @each $theme, $map in $themes {
    .theme--#{$theme} & {
      $theme-map: () !global;
      @each $key, $submap in $map {
        $value: map-get(map-get($themes, $theme), '#{$key}');
        $theme-map: map-merge(
          $theme-map,
          (
            $key: $value,
          )
        ) !global;
      }
      @content;
      $theme-map: null !global;
    }
  }
}

@function t($key) {
  @return map-get($theme-map, $key);
}
````

Next, create the themes

````scss
$themes: (
  Light: (
    bg: $bg--light,
    text: $text--light,
    border: 1px solid $text--light,
    g: $green--light,
    b: #61afef,
    r: #e06c75,
    p: #e5c07b,
    y: #c678dd,
  ),
  Dark: (
    bg: $bg--dark,
    text: $text--dark,
    border: 1px solid $text--dark,
    g: $green--dark,
    b: #61afef,
    r: #e06c75,
    p: #c678dd,
    y: #e5c07b,
  ),
);
````

After adding this piece of code, all that is left is to theme each component according to the `themed()` property as shown below.

````scss
.exampleClass {
	@include themed() {
		background-color: t('g');
	}
}
````

# Conclusion

After all of this work, there is still so much left to do. I have yet to do the following:

### Todo

* [ ] Mobile Support
* [ ] Color Scheme flash bug
* [ ] Better Post Query Support
* [ ] Post Search Function

However, despite this blog not being complete, I have already learned so much about not only Remix but also React in general and SCSS. I also got very distracted by my new obsession with neovim and ricing MacOS. The only thing left is to write some actual blogposts and it seems my first one is just about finished.
