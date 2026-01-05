# UI with Solar

UI has **never been easier**!
With Solar you can make UI with a couple of lines! The rest is handled by the interpreter. Sadly in v1.0.1 you can't make advanced UI yet :(.
The code snippets listed below are taken from the example file in the GitHub repository.

Here's how you make simple UI:

## Creating the window loop
```ui window main```

## Changing window title
```ui title main "your title"```
## Changing window size
```ui size main 460 260```
## Changing background color (hex)
```ui bg main "#1e1e1e"```
## Changing foreground color (hex)
```ui fg main "#ffffff"```
(Recommended foreground color if BG color is Black: #ffffff)
## Adding a label with text
```ui label main l1 "Name:" at 20 20```
NOTE: l1 is the label ID this can be anything.
## Adding a textbox
```ui entry main name at 90 20```

## Adding a checkbox
```ui checkbox main agree "any text here lol" at 20 70```

## Adding a button that does nothing
```ui button main b1 "this does nothing lolo" at 20 120 do print ""```
Why ```print ""```? Well it's becuase of an unknown error in the interpreter that I'm working on.
This will be fixed in future versions!
## Adding a button that does something
```ui button main b1 "this does something" at 20 120 do function_name```
NOTE: You actually NEED to define the function using Python's def() function (later on will be Solar's own defining system)
## Main loop (very important for it to work, always add this at the end of ur UI code)
```ui run main```
