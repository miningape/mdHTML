# mdHTML

## what is this project
this project aims to create "book like" websites based off of md files. For a basic idea of what a "book like" website is check https://book.amethyst.rs/stable/intro.html.

## Reasoning/Motivation
A lot of github projects use md files to help contributors understand what to do, and often use them to also create github wikis. The idea of this project is to create very nice looking wikis for contributors based off the md files already being used. There are a few caveats one of them being if you want a complex (read, headings with subheadings much like the table of contents on wikipedia) they will need to either use json or my own language to affect this.

# Usage
The basic idea is that it generates a table of contents as well as all the webpages, while allowing the user to customize everything, even add for example p5js sketches and other html/js/css extensions/cms to affect the content of the wiki.

This will be done by specifying the file structure as well as the links.

There are 3 things we are hoping to make with this: an executable (and npm module), a webapp, and a wikipedia reader.

* The executable will be able to get downloaded and then run it in the directory you want.
* The npm module will essentially act like the executable but be a bit more flexible, and you can import it into your own project
* The webapp will allow you to build a website without downloading anything. The idea is that you upload your files, edit the manifest (in browser/upload it), and it produces
a download link for you with your html files.
* The wiki reader will scan a wikipedia page and build a book from iy
