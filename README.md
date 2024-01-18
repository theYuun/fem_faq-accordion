# Frontend Mentor - FAQ accordion solution

This is a solution to the [FAQ accordion challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/faq-accordion-wyfFdeBwBz). Frontend Mentor challenges help you improve your coding skills by building realistic projects. 

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
  - [Useful resources](#useful-resources)
- [Author](#author)
- [Acknowledgments](#acknowledgments)
---
## Overview

### The challenge

Users should be able to:

- Hide/Show the answer to a question when the question is clicked
- Navigate the questions and hide/show answers using keyboard navigation alone
- View the optimal layout for the interface depending on their device's screen size
- See hover and focus states for all interactive elements on the page

### Screenshot

![](./screenshot.jpg)

### Links

- Solution URL: [github repo](https://github.com/theYuun/fem_faq-accordion.git)
- Live Site URL: [github pages](https://theyuun.github.io/fem_faq-accordion/)
---
## My process

### Built with

- Semantic HTML5 markup
- CSS custom properties
- Flexbox
- [Vue.js](https://vuejs.org) - The Progressive JavaScript Framework
- [Vite](https://vitejs.dev/) - Next Generation Frontent Tooling
- [npm](npmjs.com) - The world's largest software registry
- [INKSCAPE](https://inkscape.org/) - Draw Freely

### What I learned

I used Vue3 to create this project. It took me a bit longer than simply using HTML, CSS and Javascript would have taken me, since I'm a bit rusty with Vue.
> Vue is a very cool framework, given you know what you're making and looking for. I highly recommend first building a prefabrication (that is, Javascript creates HTML elements with dynamic data on loading the page) project to help you understand what frameworks like Vue (also React and Angular) do. I'll be using Vue to take on all following projects as well.

I started the project asking 'phind' to rekindle my rusty Vue knowledge and adapted its results to my needs.
> 'phind' also showed me some cool shortening techniques, like:
> - where using the arrow buttons to loop from the bottom faq option back to the top one, using a mod calculation in stead of an if loop to match the array length to the index and setting the index to 0 or length - 1 should one navigate down past the last or up past the first, as I would usually do it. (Ex. 1)
This in combination with youtube vids and the vue website helped get me back up to speed, although the power of Vue is not fully on display here.

With the nature of Vue, I created the base components first to see the basic parts fit into place. I had to reshuffle things a bit when I realised that I need to decentralise some components, given that this is one small part of a theoretically larger project. (Ex. 2)
> This means that I aught to have more carefully planned out how the website should be structured before I started putting things together.
> This further helps with other facets of a project, like unit testing.

With HTML alone, you can add additional classes to the class property, simple enough, but how do you deal with needing to add or remove classes on the fly per user input? normally you'd manipulate the '.classlist' using javascript, but Vue gives you bindings for some properties. In this case you can have a 'class=""' property and a ':class=""' property to add class dynamism (Ex. 3)

CSS you beautiful horror... or horrid beauty. A language that makes the "My code works and I have no idea why" meme all too real.
Too often does one run into a problem like the need to change from using animations to transitions or vice versa, because 'that' property, it turns out, does not animate or stutters. (Ex. 4)

Not being someone who needs assistive technologies, and hopefully never will, building in the aria controls is what I am most fearful of, as I'm not sure if I'm missing something. I pretty much just ran my code through 'phind' and asked that it add aria code to it to see what I should be adding. Down the line, I hope I'll get to understand that complexity and beter my coverage of it. (Ex. 5)

One of the more irritating parts of events is how the bubbling interacts with frameworks like Vue and React (not sure how this shows on Angular)
There are options that are supposed to help mitigate bubbling issues, but the reasons why they do and don't work in its application here is confusing. (Ex. 6)


### Code Examples

#### html
```
// (Ex. 2)
// The template element is what Vue uses to cordon off the HTML formatting in a '.vue' file.
<template>
  <background class="bg" />
  <faqSection class="content faqSection"/>
</template>
```
```
// (Ex. 5)
<div :id="'accodion-content-' + index" class="accordionAnswer" :aria-labelledby="'accordion-content-' + index" :aria-hidden="!toggleAnswerState.condition">
  {{ content }}
</div>
```
#### css
```
// (Ex. 4)
// The normal and open states of the answer object when you click on the question button
.accordionAnswer {
  max-height: 0vh;
  transition: max-height 0.25s ease-out;
}
.accordionAnswer-open {
  max-height: 200px;
  transition: max-height 0.25s ease-out;
}
```
```
// (Ex. 3)
// The two classes required for the accordion object to open and close, based on the necessary boolean
<div class="accordionAnswer" :class="{ 'accordionAnswer-open' : toggleAnswerState.condition }">
  {{ content }}
</div>
```
#### js
```
// (Ex. 1)
// Pressing down will loop the list when on the last entry
const nextIndex = (focusedIndex.value + 1) % faqs.value.length;
// Pressing up will loop the list when on the first entry
const prevIndex = (focusedIndex.value - 1 + faqs.value.length) % faqs.value.length;
```
```
// (Ex. 6)
// When building events into the window or document level, use this on the parent of the component that should use the input to prevent the browser from executing default behaviour at the parent level and anything higher up the heirarchy
const handleKeypress = (event) => {
  if(event.key == "Enter" || event.key == " ") {
    event.preventDefault();
    toggleAnswer();
  }
}
```
```
// The above is what I settled on, since event.stopPropagation(); did not seem to do the trick, no matter where I added it. Whenever I look for what it does, it's supposed to prevent the input from sending the event further up the hierarchy. It is removed from the code, but I thought I'd leave this here in case there are comments that can possibly clear up my confusion.
const handleKeypress = (event) => {
  if(event.key == "Enter" || event.key == " ") {
    event.stopPropagation();
    toggleAnswer();
  }
}
```

### Continued development

This was a great refresher of Vue for me. Should I have need for it, I'll use this in future projects and adapt as needed.
I will be putting greater efforts into understanding the aria controls that are and will become available.
I'll need to also build further understanding of event bubbling.

### Useful resources

- [phind](https://www.phind.com/search?home=true) - phind helped me understand quite a few ideas I used to do this project.
- [vue.js](https://vuejs.org/guide/quick-start.html) - Always have the help guides for the software you're working with ready at hand. The examples in there can sometimes bridge the gaps simply reading cannot do.
- [youtube](https://www.youtube.com) - Hands down, my favourite Vue teaching channel.

## Author

- Frontend Mentor - [@theYuun](https://www.frontendmentor.io/profile/theYuun)
- freecodecamp - [theYuun](https://www.freecodecamp.org/theYuun)

## Acknowledgments

- [MakeAppsWithDanny](https://www.youtube.com/@MakeAppswithDanny) was my goto resource when I learned Vue the first time, especially sorting between the different APIs and syntaxes available to Vue users. Also great to see what I vividly remember about the process.

- [LearnVue](https://www.youtube.com/watch?v=yo2bMGnIKE8) was a very handy resource in getting the live site running on github pages