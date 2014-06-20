nuwebtemplate
=============

*This project is still in status nascendi*

Template for new projects involving nuweb.

[Nuweb](http://nuweb.sourceforge.net) is my favorite tool for literate
programming. The main advantages are its simplicity and its
independence of programming language. What I specifically like is the
possibility to include the Makefile in the nuweb source, making the
nuweb source self-contained.

On the other hand, there are shortcomings that I like to overcome:

1. I would like the functionality of a macro pre-processor;
2. To set up a proper Makefile is difficult.
3. The functionality of the comment-string (@%) is different
   in different versions of nuweb. I would prefer that it causes
   the remainder of the line, including the end-of-line characters,
   to be removed, inside as well as outside of code-scraps.

A practical problem is, that a contextr-sensitive editor like Emacs,
treats the '$' character as the boundary of LaTeX mathematics mode
sections. This is annoying when '$' characters occur in code-scraps.

Therefore I have set-up a template nuweb file with the following
features:

1. It generates a Makefile, so that the Nuweb source is nearly
   self-contained (however, you still need at least nuweb, LaTeX, m4 and
   make on your computer).
2. Before Nuweb, it runs [Gnu M4](https://www.gnu.org/software/m4/m4.html) 
   on the source.
3. It translates '\$' characters into '$' characters before running
   nuweb.
4. It writes the target files in proper directories.




