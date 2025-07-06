---
author: arul
category:
  - uncategorized
date: "2017-12-30T10:00:09+00:00"
draft: "true"
guid: http://arulselvan.net/?p=356
title: Getting Started with React JS
url: /

---
Before start coding, we need to setup our local development environment, for this. first need any one of the editor, I used [visual studio code](https://code.visualstudio.com/) for my development, you can use any editor you like, for example WebStrom, Sublime,Adam, etc..

Typically in any project, to make clean and easy, you need good architecture , folder structure , supporting build and configuration tools,  but  now you won't worry about all this, because react team officially recommending the utility package called Create React App, this will do all the job for you.

Let Install this package in our machine, this package available in Node package manager, so our machine should have NPM  or install nodejs on your machine, that will install npm for you(but don't think we not going to do any nodejs code in this article).

Open your terminal or command prompt and type below command, this will install the package globally.

```ps
npm install -g create-react-app
```

 [![](/wp-content/uploads/2017/12/install-create-react-app-1024x233.png)](/wp-content/uploads/2017/12/install-create-react-app.png)

Alright! now we can create our react app by single command.

```ps
create-react-app react-wordpress-app

```

Thats it awesome! our app created successfully, I have opened the folder in my VSCode editor.

[![](/wp-content/uploads/2017/12/react-app-folder-structure-1024x719.png)](/wp-content/uploads/2017/12/react-app-folder-structure.png)

The above folder structure and fields are created by create-react-app. In the package.json you could see all the required dependency packages, react, react-dom and react-scripts(contain all the required script for build moden javascrupt etc)
