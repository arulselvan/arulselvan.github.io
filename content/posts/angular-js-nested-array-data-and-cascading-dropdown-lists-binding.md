---
author: Arul Selvan
category:
  - software-development
date: "2014-08-12T12:22:10+00:00"
draft: "true"
guid: http://arul.pw/?p=183
tag:
  - angularjs
  - java-script
  - technical
title: Angular JS - Nested array data and cascading dropdown lists binding
url: /angularjs-nested-array-cascading-dropdown/

---
The Requirement is very simple.We have to display data with cascading drop down from the collection.

We have some collection of books. I took a sample of book for initial page mapping.

[![Nested Angular Drop down](/wp-content/uploads/2014/08/NestedAngularDropdownlst-1024x279.png)](http://arul.pw/wp-content/uploads/2014/08/NestedAngularDropdownlst.png)

Each row contains dropdowns for books,chapters and titles. By choosing the drop down under book(specify the name of the book), relevant chapter will be loaded. And based on the selection of the chapter, title information will be loaded for that specific book title.

```xhtml
&nbsp;<div class="col-md-4 col-xs-4 col-sm-4">
 <select required ng-change="onBookChange(b,book)" ng-model="book" ng-options="bb.bookName for bb in books" class="form-control" >
 <option value="">--Select--</option>
 </select>
 </div>
 <div class="col-md-4 col-xs-4 col-sm-4">
 <select required ng-model="chapter" ng-change="onChapterChange(b,chapter)" ng-options="cha.chapterName for cha in b.selectedChapters" class="form-control" >
 <option value="">--Select--</option>
 </select>
 </div>
 <div class="col-md-4 col-xs-4 col-sm-4">
 <select required ng-model="title" ng-change="onTitleChange(b,title)" ng-options="t for t in b.selectedTitles" class="form-control" >
 <option value="">--Select--</option>
 </select>
 </div>

```

```
 $scope.onBookChange=function(b,book){

     b.selectedChapters=book.chapter;
 }
 $scope.onChapterChange=function(b,cha){

     // console.log(cha);
     b.selectedChapter=cha;
     b.selectedTitles=cha.titles;

 }
 $scope.onTitleChange=function(b,t){
     b.selectedTitle=t;
 }

```

From above example each drop down "on change event",we are passing the current book object to our method and creating variable dynamically for the selected subsequent item.

You can write any logic inside this method like ajax call to pull out sub drop down values, here we will take from same instance.

Plunker Demo:  [http://plnkr.co/edit/puDh4B?p=preview](http://plnkr.co/edit/puDh4B?p=preview "Plunker Demo")
