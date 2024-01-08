---
date: 2024-01-05 
categories:
  - Thesis
tags:
  - Thesis
  - Obsidian
  - Notes
---

# Thesis Chapter Tracker

I've recently been writing all my notes in [Obsidian](https://obsidian.md/), which I like for a couple reasons:

<!-- more -->

- My notes are saved as locally stored markdown files so I don't need Obsidian to make sense of them
- It has native apps for Windows, Mac, Linux, and iPhone, all of which I use because something is wrong with me
- It has a lot of plugins so if there's something I want to do with it there's a good chance someone has already made a plugin for it.

The two plugins I currently have installed and recommend are:

- [Dataview](https://github.com/blacksmithgu/obsidian-dataview): Makes tables and stuff based on information stored in notes. This is how I make my thesis progress tracker table!
- [Obsidian Git](https://github.com/denolehov/obsidian-git): Let's me backup my notes to git automatically, which functions as a combined version control and cloud sync for notes. Important since I access my notes on four different operating systems 🤪

Once you've got Dataview installed, make a folder in Obsidian where you want to store your thesis notes, then make a note for each chapter in your thesis (or for whatever you want a single row in your table to be).
At the start of each chapter note, add the following lines to tag the note:
```
---
tags:
  - thesis-chapter
---
```
Next, make a new note (in the same folder as your chapter notes) with the following block of code
````
```dataviewjs
dv.table(
	["Chapter", "Tasks Progress"], 
	dv.pages("#thesis-chapter")
	.sort(c => c.file.name)
	.map(c => [c.file.link, dv.span("![progress](https://progress-bar.dev/" + parseInt((c.file.tasks.where(t => t.completed).length / c.file.tasks.length) * 100) + "/)")])
)
```
````
This will generate a table with a row for each note tagged with `thesis-chapter` and two columns: a link to the note, and a progress bar for the tasks within that note.
A task in this case is any line starting with a checkbox `- [ ]`.

There are some Dataview plugin settings you'll need to change to enable js blocks, so make sure those are turned on. 

You could make the columns any number of things, they're defined in the `.map(c => [...])` line. `dataviewjs` blocks are basically just JavaScript, so steal some code of StackOverflow like I did and try stuff out! 
