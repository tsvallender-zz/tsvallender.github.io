---
title:  "Single table inheritance in Rails"
date:   2022-01-13 17:12:31 +0000
categories: rails oo db
---

Yesterday I implemented Single Table Inheritance in a Rails app I'm working on. Here, I want to document the process.

Single table inheritance is a method of organising object-oriented data in a relational database. Instead of having individual tables for every class in your application, you store multiple classes of object in one table which has a "type" column to store what class of object that row should create. For example, in my note-taking application, a Todo is a subclass of Note, but both are stored in the notes table.

This is most useful when dealing with very similar classes which only diverge in small ways, otherwise we end up with very large amounts of null data in the table and don't really gain anything. 

Here's how we go about implementing this.

