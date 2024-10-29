---
title: Clean Code
tags:
  - Code
---

# Introduction

It is the job of the developer, not the manager to defend clean code and insist on writing code that will not require additional maintenance over time. The manager should be focused on meeting deadlines and scheduling while the developer should insist on doing things correctly without taking shortcuts because it is in fact the fastest way to meet a deadline. While it may seem like taking more time to write cleaner code would take longer than writing code quickly, over the long run hastily written code consumes more time and requires more maintenance which will result in a greater number of missed deadlines.

 > 
 > Leave the campground cleaner than you found it. - Boy Scouts

# Meaningful Names

## Use Intention Revealing Names

Names of variables, methods, and classes should avoid being implicit and should have easily identifiable names that explicitly state what the piece of code is doing, why it exists, and how to use it. If all cannot be achieved then a comment may be necessary.

### Implicit Code

````c++
public List<int[]> getThem() {  
	List<int[]> list1 = new ArrayList<int[]>(); 
	for (int[] x : theList)
		if (x[0] == 4) 
			list1.add(x);
	return list1; 
}
````

### Explicit Code

````c++
public List<int[]> getFlaggedCells() {  
	List<int[]> flaggedCells = new ArrayList<int[]>(); 
	for (int[] cell : gameBoard)
		if (cell[STATUS_VALUE] == FLAGGED) 
			flaggedCells.add(cell);
	return flaggedCells;
}
````

### Explicit with Classes

````c++
public List<Cell> getFlaggedCells() {  
	List<Cell> flaggedCells = new ArrayList<Cell>(); 
	for (Cell cell : gameBoard)
		if (cell.isFlagged()) 
			flaggedCells.add(cell);
	return flaggedCells; 
}
````

## Avoid Disinformation

* Never name pieces of code using keywords that are not reflective of what you are describing. i.e do not label a group of accounts `AccountList` unless it is actually a list.
* Avoid similarly shaped names, or names that are too close to one another
* Avoid using lowercase L and capital o, as l looks like 1 and O looks like 0

## Make Meaningful Distinctions (I am guilty...)

It can be tempting to satisfy the compiler at times without considering the long term consequences of your decision. It is bad practice to change only a single letter or number when encountering an error to make compiler errors go away. Avoid meaningless and redundant words like "data" vs "info" which can be indistinct in some contexts. Also avoid naming similar to the example below:

````c++
getActiveAccount();
getActiveAccounts();
getActiveAccountInfo();
````

## Make Searchable Names

Avoid using numbers in names because it can be hard to search for. Also avoid names that are too short and contain commonly used letters like 'e.'
One rule of thumb is:

 > 
 > The length of a name should correspond to the size of its scope

## Prefixes

Because classes are much smaller than they used to be and compilers have become so much smarter, prefixes are not necessary and just cause clutter. Prefer `ShapeFactoryImp` for implementation over `IShapeFactory` or `CShapeFactroy`

## Avoid Mental Mappings
