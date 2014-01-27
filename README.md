#Why?
Todo lists should not be locked in to a single platform or service; todo lists should be open and editable across all apps, devices and computers. With .todo files, you can have a single list used across various applications on all of your devices. Edit with a text editor, iPhone, PC, Android or Mac app - what you use to edit doesn't matter. .todo files can be stored just like text files.

#What?
.todo files are just like text files; you can edit them in a text editor, web browser, or smartphone app. 

#How
Just create a file called `filename.todo`, format it properly and you have the most basic .todo file. Set your default apps or text editor for editing this file, and off you go. Download apps compatible with .todo files for desktop and smartphone if any are ever made.

#Syntax
.todo files are formatted a lot like Task Lists in Github Flavoured Markdown.

```.todo
- [] a task list item
- [] list _syntax_ required
- [] normal **formatting**
-[x]more relaxed about syntax than GFM
- [x]so inconsistencies should be ok
- [] incomplete
- [x] completed
```

What's important is that the first characters in each line are `-` (list), then an optional space ` `, then `[`, then optionally `x`, then `]`, then the actual todo content.

## Regex
I'm terrible at Regular Expressions (so please submit a pull request), but this is one way of handling the parsing.

```regex
^-(\s|)\[(x|)\](\s|).*$
```

in JavaScript

```regex
/^-(\s|)\[(x|)\](\s|).*$/gi
```

A test case, with this regex

```
- [x] completed           #true
-[] not completed         #true
-[x] another completed    #true
- [] incomplete           #true
- invalid result          #false
not even existing         #false
-[x]condensed             #true
-[]ultra                  #true
```

# Conversion
It's also good to be able to convert a set of todos to a .json object

```.todo
- [] todo item one
- [x] completed item
```

=>

```json
[
  {
    "task": "todo item one",
    "completed": false
  },
  {
    "task": "completed item",
    "completed": true
  }
]
```
