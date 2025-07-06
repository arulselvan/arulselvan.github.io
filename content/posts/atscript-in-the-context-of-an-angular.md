---
author: Arul Selvan
category:
  - software-development
cover:
  alt: AtScript-300x167
  image: /wp-content/uploads/2014/10/AtScript-300x167-1.png
date: "2014-10-30T10:35:00+00:00"
guid: http://arul.pw/?p=217
tag:
  - technical
title: AtScript in the context of an Angular 2.0
url: /atscript-context-angular-2-0/

---
**What is AtScript ?**

Google revealed AtScript at ngEurope in Pari. This is a superset of Microsoft TypeScript , ES6 and ES5. TypeScript adds types to JavaScript code and AtScript extends this idea further by adding annotations and introspection.

[![](/wp-content/uploads/2014/10/AtScript-300x167.png)](/wp-content/uploads/2014/10/AtScript.png)

Google team  writing Angular v2 on top of the AtScript syntax

**Is it new language?**

No, Its not a new language just influenced by TypeScript and Dart. Like how typescript is superset of javascript. Atscript also using similar kind of syntax but it's a enhancement with what is lacking in previous. so it's called superset for rest.

**What is lacking in existing TypeScript?**

Types are analyzed only statically, once you build the source it's nothing but a java script you cannot check the types thereafter. Example  in run time you are receiving JSON object from the server end you cannot do the type checking, this is the limitation from typescript.

**Why AtScript use a runtime type system?**

it allows free mixing of existing libraries which don't have type and new code which can take advantage of types in the run time, it overcomes  typescript limitations. So the type errors can be caught and resolved before pushing to the production and all the assertions can be removed from the production builds.

**Who all working  this Concept ?**

Below three top people are working together in this concept, adding type system to javascript to making as standard.

       Google AtScript.

       Microsoft TypeScript

       Facebook Flow

**When will be AtScript release?**

Angular team started working on AtScript over a year,most probably it may come to market 2015 starting.

**Reference:**

Microsoft TypeScript and Its Roadmap :

[http://blogs.msdn.com/b/typescript/archive/2014/10/22/typescript-and-the-road-to-2-0.aspx](http://blogs.msdn.com/b/typescript/archive/2014/10/22/typescript-and-the-road-to-2-0.aspx)

AtScript primer doc :

[https://docs.google.com/document/d/11YUzC-1d0V1-Q3V0fQ7KSit97HnZoKVygDxpWzEYW0U/preview?sle=true&pli=1#](https://docs.google.com/document/d/11YUzC-1d0V1-Q3V0fQ7KSit97HnZoKVygDxpWzEYW0U/preview?sle=true&pli=1#)
