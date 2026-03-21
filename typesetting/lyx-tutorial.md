---
title: Using LyX
parent: Typesetting Mathematics
layout: post
toc: true
redirect_from:
  - /econ/teaching/typesetting/lyxTutorial
  - /econ/teaching/typesetting/lyxTutorial.html
---

Below is a brief overview of what I think are the most important things to know about using LyX. A more comprehensive tutorial can be found [here](https://wiki.lyx.org/uploads/LyX/tutorials/essentials/LyX_Essentials.pdf) and the official documentation can be found [here](https://wiki.lyx.org/LyX/Documentation).

### The idea behind LyX

The main difference between LyX and a program like MS Word is that Word has you format the document as you work on it. LyX, on the other hand, is set up so that you worry only about the structure and content of the document, and the details of the formatting are left until you export the document at the end.

### Document Structure

In the top left of the window there is a drop-down menu which allows you to change the layout environment for the current paragraph.

<div style="text-align:center;"><img src="lyxEnvironments.png" alt="LyX Environments Drop-down"></div>

"Standard" just means that you are in a normal paragraph. You can use this drop-down menu to create section and subsection headers, to create lists, and to insert a specially formatted title at the top of your document.

### Inserting Math

If you insert an inline formula, you get something like this: \(U=\sum_t\beta^t u(c_t)\). The shortcut for creating an inline formula is ctrl-m on Windows and command-m on Mac. You can also insert a 'display' formula (shortcut: ctrl-shift-m or cmd-shift-m) which is bigger and occupies its own line:

$$U=\sum_t\beta^t u(c_t)$$

When typing in a formula, there's a bar at the bottom of the window full of common mathematical symbols. You can click on these buttons to add them to your formula. Or if you hover over the button, a tooltip will appear to tell you the LaTeX command for entering that symbol. [This page has some of the most common math commands.](latex-math)

### Inserting an Image

If you click on insert→graphics in the menu at the top, you will be prompted to select an image file. This will insert that image into LyX. You can then click on the image to change its size in your document. Note that LyX only points to that original image file, so if you edit or delete the image, if will change in LyX as well.

### Formatting Options

Optionally, you can change the format of the page by clicking on document→settings at the top. There are lots of options, but the only thing I ever change are the page margins because I like to save paper.

### Finishing and Exporting Your File

If you click on the eye at the top of the page, you can view a preview of how your final document will appear.

To actually generate your final document, once you're done writing, click File→Export→PDF. There are several different backend options (LuaTeX, XeTeX, etc), but for math homework, it doesn't matter which one you click.

The program will generate a pdf in the same folder you saved the .lyx file in. This pdf is what you want to print off or email.
