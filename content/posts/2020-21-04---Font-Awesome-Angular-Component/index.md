---
title: Use Font Awesome Angular Component in 5 simple steps
date: "2020-04-21T23:46:37.121Z"
template: "post"
draft: false
slug: "Font-Awesome-Angular-Component"
category: "Angular"
tags:
  - "Angular FontAwesome Component"
description: "Fontawesome is most popular icon tool kit. It has 1500+ free icons. Most importantly these icons are created using scalable vectors and automatically inherits CSS size and color. This means they blend in with text inline wherever you put them. This makes it high quality icons that works well on any screen size."
socialImage: "/media/title.jpeg"
---

![Font Awesome Angular Component](/media/title.png)

<a href="https://fontawesome.com/" target="_blank">Fontawesome</a> is most popular icon tool kit. It has 1500+ free icons. Most importantly these icons are created using scalable vectors and automatically inherits CSS size and color. This means they blend in with text inline wherever you put them. This makes it high quality icons that works well on any screen size.

Before Angular 5, we had to install font-awesome package and reference its css. Now we have angular component for fontawesome which makes it simple, clean and neat.

Below are the five simple steps to add fontawesome component into your angular application.

You can download the source code from <a href="https://github.com/gunnala-sri/angular9-fontawesom5" target="_blank">here</a>

1. Create new angular app. And remove the whole code in ‘app.component.html’ file. We don’t need this as we just want to see how to use it.

```
ng new angular-fontawesome
```

2. Install fontawesome angular components

```
npm install @fortawesome/fontawesome-svg-core
npm install @fortawesome/free-solid-svg-icons
npm install @fortawesome/angular-fontawesome
```

3. Import FontAwesomeModule into app.module.ts

![Font Awesome Angular Component](/media/1-code-snippet.png)

4. Import the icon you want to use in to component

![Font Awesome Angular Component](/media/2-code-snippet.png)

Identifying font classes is very easy.

class name **‘fa-home’** converts to faHome

class name **‘fa-long-arrow-alt-left‘** converts to faLongArrowAltLeft

5. Add the icon in component html file.

```
<fa-icon [icon]="home"></fa-icon>
```

Compile and run it.

![Font Awesome Angular Component](/media/3-code-snippet.png)