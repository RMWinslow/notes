---
title: Typesetting Mathematics
layout: post
has_children: true
has_toc: false
redirect_from:
  - /econ/teaching/typesetting/typesettingSoftware
  - /econ/teaching/typesetting/typesettingSoftware.html
---

### LaTeX

LaTeX *(pronounced lah-tehk)* is a syntax for writing documents, and is the standard for scientific publishing. Many of the textbooks you will use in college were written using this system. LaTeX has a lot of features, but the most useful is LaTeX's mathematical notation, which has has become the standard for writing equations not just in LaTeX itself, but in nearly every computer application.

[Click here for some examples of LaTeX mathematical notation.](latex-math)

Below, I've included several examples of software which can be used to type math on a computer. I'll also give a brief demonstration in class about how to use these tools.

### LyX

[LyX](https://www.lyx.org/Home) is a front-end for LaTeX that gives you access to the features of the language, but hides away the code-like syntax. This is the software I prefer to use; the syllabus, assignments, and other documents for this course are prepared in LyX.

Although LyX is my favorite of these options, and in my opinion, the most enjoyable to use, it is slightly complicated to install.

Because LyX is essentially an interface for LaTeX, you need to first install a LaTeX distribution:
- For Mac OS, I would recommend [MacTeX](https://www.tug.org/mactex/mactex-download.html)
- And for Windows, I would recommend [MiKTeX](https://miktex.org/download)

Once you have that installed (which may take a while for a full installation), then install LyX itself. The download can be found here: [www.lyx.org/Download](https://www.lyx.org/Download)

Once LyX is installed, see [this page](lyx-tutorial) for a basic introduction on how to use it.

(*Edit 2023: If you are using a brand new version of Mac OS, you may also need to [install Python from python.org](https://www.python.org/downloads/). Older versions of MacOS came with Python pre-installed.*)

### Overleaf

[Overleaf](https://www.overleaf.com/) is an online LaTeX editor, designed to make it easy for scientists to collaborate on papers. Because it is entirely online and requires no downloads, this program is the easiest to setup. However, as a "pure LaTeX" experience, it also has a higher learning curve. If you want to use this software, you'll need to learn how to use LaTeX in general, and not just the math notation.

### Microsoft Office

Microsoft Office also has a Math Mode. While your cursor is inside an equation object, math can be entered using buttons at the top of the screen, or by typing LaTeX commands.

It is very likely that you already have MS Office installed on your computer. If you don't, and would like to use the software, [UMN students have access to it](https://it.umn.edu/office-microsoft) as part of their tuition.

I personally don't like to use Office for typsetting math, as I've run into some annoying bugs, and the designers like to move UI elements around in different versions. But there is a professor here who writes all of their papers in Word, so it can definitely be done.

## Google Docs

Google Docs has a Math mode very similar to MS Office's. Just select Insert→Equation in the menu at the top.

---

### Exporting a document as pdf.

Regardless of which software you use, it's best practice to export your completed document as a pdf. If you send a zipped LaTeX project, or a .docx file, then the person you send it to might see the document rendered differently on their machine. The pdf format was designed to make it so that when you print a document or send it to another computer, the pdf will always look the same.

### Other LaTeX-compatible Software.

There are many other programs that enable to use of LaTeX math formatting. There are at least two major javascript libraries which allow LaTeX formulas to be included in webpages like so:

$$f(x)= x^2 + {x \over 3} + 2$$

Even Canvas allows instructors to insert LaTeX equations into course webpages. And I recently found out that the default note-taking app on the iPad supports LaTeX input as well.

However, none of these pieces of software are quite ideal for the purpose of authoring a homework assignment. This is because you don't just want to type a nice-looking equation. You also need to turn it in to your instructor, either via email or as a printed document. Software like LyX and MS Office are designed to create documents for printing.
