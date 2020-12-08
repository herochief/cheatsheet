# HOW TO USE MARKDOWN SYNTAX

## Introduction

This is a cheatsheet to use some Markdown syntax. It comes with a simple description and syntax from using it. \ 
If you did not know already, its entire tutorial is written in Markdown. \
In gitHub, if you create a "readme.md" file and it contents as Markdown syntax, the repository page will load the file upon loading the page as seen here.
I hope you find it useful and enjoy.


-----------------------------------------------

## CONTENTS

Contents | Contents | Contents
:---------:|:----------:|:----------:
[Headers](#head "How to make Headings")                 | [Blockquote](#blockquote "How to create blockquote") | [Table](#table "Create Table")
[Separation link](#separation "Separating segments")    | [List](#list "How to Create list")                   | [Links](#links "Create Links")
[Commenting](#comment "How to comment")                 | [Code](#code "How to codeblocks")                    | [Bookmarks](#book "Create Bookmarks")
[Emphasis](#emphasis "How to empemphasise words")       | [Images](#img "Putting Images")                      | [Task List](#task "Create Task List")

--------------------------------------------------

## <a name="head"> Headers </a>

You create a header to use hash symbol ( # )

> syntax: `# heading` 

**Note**: Take note of the space between the heading and the #

There are several layers importance to the headings. Single # is huge and increasing the number of # will decrease the size

1.  `# heading 1`
2.  `## heading 2`
3.  `### heading 3`
4.  `#### heading 4`
5.  `##### heading 5`

-------------------------------------------------------------

<!-- ## Separation line or break line -->
## <a name="separation"> Separation line or break line </a>

If you wish to create a line to partition the page. Spam ( --- ) or ( *** ) or ( ___ ) 


> syntax: `------------------------------------`

------------------------------------------------------------

<!-- ## Paragraph and down one line------------------------- -->
## <a name="paragraph"> Paragraph and down one line </a>

### Paragraphing
To create a new paragraph for typing, have a line gap between sentences or double enter button

### Down one line
The Issue with just `enter` once is that the sentance is still taken to be the same sentance as the one directly above. \
Another way to break a sentence with no gap is to use "` \`"

eg. Without `\` 

I am a boy.
She is a girl.
```
I am a boy.
She is a girl.
```

eg. with `\`

I am a boy. \
She is a girl.
```
I am a boy. \
She is a girl.
```

------------------------------------------------------------

<!-- ## COMMENTING------------------------- -->
## <a name="comment"> Commenting </a>

Although Readme are meant to explain everything, we like to have some comments while creating the readme file or insert some easter eggs.

**First Way**: Using HTML commenting syntax of `<!-- text that will not be loaded or seen -->`

**Second Way**: This is one line only, and must be from the start: ` [//]: <> (text that will not be loaded or seen)`

------------------------------------------------------------

<!-- ## Emphasis------------------------- -->
## <a name="emphasis"> Emphasis </a>

The are 2 ways to emphasise: **BOLD** or _italic_. \
There is ~~strikethrough~~ as well


1. **bold**
	- `**bold**`
	- `__bold__`

2. _italic_
    - `*italic*`
	- `_italic_`

3. ~~strikethrough~~
    - `~~strikethrough~~`

**Note**: another way of going about it is that bold used double */- and italic uses single */-

------------------------------------------------------------

<!-- ## blockquote------------------------- -->
## <a name="blockquote"> Blockquote </a>

> This a blockquote \
> Notice the vertical line on the left. \
> It uses the " > " symbol to create it

syntax `> blockquote thing `

You can add more levels or nested 

> level 1
>> level 2 
>
> level 1

```
> level 1
>> level 2 
>
> level 1
```
-----------------------------------------------------------

<!-- ## list------------------------- -->
## <a name="list"> List </a>

You can create a list with `numbers` ,` * `, `-`

1. This was created with `1. something`
2. second      
3. third   

* This was created with `*`

- This was created with `-`

**NOTE**: The "dot" is the same for both * and -
<!-- <div style="text-align: Center"> your-text-here </div> -->

You can create a second level with indentation

1. Drinks
    1. coffee
    2. Milk 
2. Food
    1. steak
    2. rice

```
1. Drinks
    1. coffee
    2. Milk 
2. Food
    1. steak
    2. rice
```

---------------------------------------------------------

<!-- ## Code------------------------- -->
## <a name="code"> Code </a>

This is to create a container or highlight certain words. Usually it is to differetiate code and words. It can sometimes be used to just differentiate things altogether.

### codetick

` this is a code tick ` notice the sort of highlight and different font.

> Syntax: \` text \`  \# We use the \` symbol

It is not a single quotation mark. It is the . You can find it under the `Esc` button, it shares the button with `~` sybol

### codeblock

Instead of a segment, we can expand it to cover several lines instead

```
first line
second line
third line
```

There are 2 ways to go about it.

**First**: indent with `tab`. You indent several line to create the block

**Second**:use ` ``` ` at the start line and end line of your text to create the block.

----------------------------------------------------------------

<!-- ## Images------------------------- -->
## <a name="img"> Images </a>

We can place images

eg. `![GitHub Logo](/images/logo.png)`
> Syntax:  `![Text here if image doesnt show](Url or path/address to image)`

A link for the image can be placed as well

> Syntax  `[ ![ Description of the image ](image path/address) ] ( link address) `

Basically, extra `[]` bracket and `(link address)`

---------------------------------------------------------------

<!-- ## Table------------------------- -->
## <a name="table"> Table </a>

Column 1| Column 2 | Column 3
--------|--------|--------
Somthing 11| Something 12 | Something 32
Somthing 21| Something 22 | Something 32
Somthing 31| Something 32 | Something 32

```
Column 1| Column 2 | Column 3
--------|--------|--------
Somthing 11| Something 12 | Something 32
Somthing 21| Something 22 | Something 32
Somthing 31| Something 32 | Something 32

OR

|Column 1| Column 2 | Column 3|
|--------|--------|--------|
|Somthing 11| Something 12 | Something 32|
|Somthing 21| Something 22 | Something 32|
|Somthing 31| Something 32 | Something 32|


```

-----------------------------------------------------------

<!-- ## Links------------------------- -->
## <a name="links"> Links </a>

eg. `http://github.com `- This is instantly a link

eg. [Github](http://github.com)

syntax: `[The text to click on](Url)`

----------------------------------------------------------

<!-- ## Bookmark------------------------- -->
## <a name="book"> Bookmark </a>


Say your readme is very long and hence you need a guide to move you to different parts quickly. One way is to create internal links to headers in the file. When someone clicks the link, it will take you to that part of the page with that header.

There are 2 parts to the process.

1.  Header is changed to have an address for others to link to:

> Syntax: `## <a name="A_name_to_ref_later"> The header </a>` : Only the header is shown  like `## The header` \
>  eg. `## <a name="exia"> gundam </a>`

2. The link to the header:

> Syntax: `[The text to click on](#A_name_to_ref_later "title shown when mouse over")` : note the `#` just one is enough, does not need to follow the same number of `#` as the header. \
> eg. `[GUNDAM CONTENTS](#exia "This will take you to the section of GUNDAM")`

Try is link to go to the [HEADER](#head "This will take you to the header section") section 

-------------------------------------------------------------------

<!-- ## Task List------------------------- -->
## <a name="task"> Task List </a>

It is to create a list with check boxes. The boxes does not actually work but to illustrate whether a task is completed.

- [x] this is a complete item
- [ ] this is an incomplete item

```
- [x] this is a complete item
- [ ] this is an incomplete item
```

-------------------------------------------------------------------
