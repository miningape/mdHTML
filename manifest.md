# Manifest
Manifest is a programming language to compile several .md files into a "book" website (similar to rust's mdBook), the structure of the table of contents (menu on the left), 
is determined with Manifest, along with what .md file to turn into that particular webpage of the entire website. It also allows for the changing of the book title, 
menu themes, as well as adding custom javascript, css or html code to the header or footer, of either 1 or more webpages.

Manifest is a programming language I created, in overly descriptive terms it is a 'contextual, regular' markup language. What this means is that it is easy to understand and code in.

## Cheatsheet
1. Read the tutorial (it takes 5 mins and you'll know whats happening)
1. Your filename has to be mani.fest (.fest meaning Fast Easy Setup Template)
1. Inline comments work after everything
1. These are the 3 expressions explained
    1. The code to define a chapter block is: `# "Name"(relative/link/to.md)` The number of "#" is the precedence (think subchapters or md headings)
    1. The code to alter the content of the header/footer of a page is: `property> "literal Insert"(relative/link/to.md)`
    1. The code to alter the content of the website (theme, name, etc) is `<property> "literal insert"(relative/link/to.anything)`
1. Caveats
    1. The ordering of ""() doesnt matter (i.e. `js> "hi()"(hi.js)` is equivalent to `js> (hi.js)"hi()"`)
    1. Just dont use `""()""` or `()""()` as its not gonna give you the result you expect
    1. Code inside of `""` is added before the link `()` in the page that is created no matter what
    1. Indentation and Whitespace is allowed anywhere so long as you keep the basic structure the compiler is agnostic
1. You can change from unnumbered to numbered like so: `<numbering> "true"`
1. And the theme like so `<theme> "Dark"`

# Tutorial
The easiest way to think of this language is in terms of the "structure" of the book you are creating.

## Page/Chapter headings
What I mean by this is that the language describes the chapters, and sub-chapters within your book. For example, the code:
```
# "Hello"(hello.md)
```
Defines a chapter with the name "Hello", the page rendered for this chapter is styled/designed by the file "hello.md".

So the structure for defining a page/chapter in your book is:
```
# "name"(relative/path/to/mdfile)
```
The "#" symbol defines the precidence of the chapter, this will be made clear with my next example. So, let's say you wanted to make a book
explaining the life inside a pond (I know very boring). You would want a chapter for the foreword, and maybe every category of life inside the pond (plants, fish, mammals, fungi).
For each of these categories you may want to have a mode detailed breakdown (for plants: aglae, sea weed, linma, etc). TThis process as you can see could continue indefinately,
but for this example the code would look like this:
```
# "Foreword"(foreword.md)

# "Plants"(plants.md)
## "Algae"(algae.md)
## "Sea Weed"(weed.md)
## "Linma"(linma.md)

# "Fish"(fish.md)
## "Carp"(carp_fish.md)

# "Mammals"(mamal.md)
# "Fungi"(fungi.md)
```
This would become a book with a structure like so:
```
1 Foreword

2 Plants
  2.1 Algae
  2.2 Sea Weed
  2.3 Linma
  
3 Fish
  3.1 Carp
  
4 Mammals

5 Fungi
```
And it would also create a webpage with that table of contents structure on the left hand side. Every webpages "body" content is determined by the md file in the perenthesis,
the nice thing about using md, is that it can also be used to add actual html to the webpage, allowing you to add a custom div to the page and then insert some javascript code
to affect that div. This basically allows the creation of a fully functional website, with custom styling, javascript, and body. There are also other nice things, like 
automatically creating next/previous page (in the sequence of chapters) buttons at the bottom of every page.

## Adding Custom CSS and JavaScript to a page
Now that we know how to string md files together into a webpage lets start making those pages yours. After defining a page you can start to edit its content. This looks like this:
```
# "Looking Good"(main.md) // Create page block/anchor
js> "init()"    //Indentation doesnt matter
    css> "h1 {color: red}"
header> "<style> h2 {color: blue} </style>"
footer> "<script type="text/javascript"> let init = () => {console.log("Hello World")}</script>"
```
As you can see the indentation does __NOT__ matter, but the line the tag is on is the line the code has to be on. In other words everything has to be in __ONE LINE__.

You can probably see how this is gonna get inconvinient really quickly (imagine trying to write a full program in one line... shudders). This is probably the number one 
thing I want to change about the language. But as a work around to this you can link another file in your code. This is done like so:
```
# "Looking Good"(main.md) // Create page block/anchor
js> (relative/path/to.js)  
```
So you can see to have a path to a file just put it inside of "()". But what if you wanted to combine these things and have a link as well as a script... well
you can do that!
```
# "Looking Good"(main.md) // Create page block/anchor
js> (relative/path/to.js)"init()"  // () then "" works
css> "h3{}"(path/style.css)        // "" then () also works!
header> "stuff"(path/to_stuff.htm)"more stuff"  // !! "" () "" = Breaken compiler :(
footer> (stuff)"path/to_stuff.htm"(more stuff)  // !! () "" () = Also leads to a broken compiler :,(
```
So basically, just dont have 2 literals or links.

The `"literal text"` is __ALWAYS__ added after the `(link)` in the order of the webpage. So a function defined in a file can be invoked with the literal text.

## So what is the difference between header, js, css and footer?
These tags affect where the code is placed. (no shit but what does that mean?)

* The `header>` and `footer>` tags are literal inserts into the html. They aren't wrapped inside any tags, so you are gonna need to define your own.
    * `header>` is added inside the <head> html tags </head>
    * `footer>` is added after anything else in the page right before </html> (except for the js tag)
* The `js>` and `css>` tags are inserted after the `header` and `footer` tags respectively. But this time
    * `css>` is added inside a <style> block of code </style>
    * `js>` is inserted after `footer>` so literally right before </html>
    
This behaviour lets you add a anything before your actual code. This means that if you depend on a library (for example p5js), you can insert it into the 
page via cdn, or some other code.

## anchor <> Tags 
This part really isnt built yet, but here it is.

Basically tags like this 
```
<footer> "p5 cdn link or something"
```
Affect every webpage rather than the one you are below. So they can be inserted anywhere in the code. This also means the list of tags you can use is more extensive
and it affects the compiling environment rather than an individual page. List of possible tags (these "special" tags can only be used with "" tags):
```
<theme> can be set to "Dark", "Light", "Lol", "Wiki"
<name> affects the main name displayed on the page 
<my nama jeff> is to open a brainfuck environment in the terminal that can be run with
```
