# Typesetting your thesis in LaTeX using Overleaf
This is a brief & scuffed walkthough to formatting your MSc or PhD thesis using LaTeX and Overleaf. 

If you are thinking of using MS Word to format your PhD thesis, let me tell that it's a *bad idea*. You will certainly have to make changes down the line, and no matter how well you planned out your styles and references you will end up with imperfections and possibly mistakes. Furthermore, the document file will become large pretty quicky, and, especially if you use a reference manager, MS Word will start slowing down and will become unusable. 

LaTeX solves all this problems, and ensures your final document has all the bibliography, table and figure referneces correctly formatted automatically, giving a sleek look to your documents. LaTeX is a fully-fledged typesetting language, and can achieve tasks that MS Word simply cannot, and, among other things, is especially good at handling equations and formulae, as well as handling table and figure positioning within the page. Google and StackExchange are your best friends, and learning how to search and adapt code is key. 

[Overleaf](https://www.overleaf.com) is an online tool that lets you write and compile your own LaTeX code, without the need to install anything on your computer. It has extensive help pages, and is great for newcomers to LaTeX. The free version comes with a few limitations, the most important of which is the 3 minutes compilation time limit. This can be annoying if you have lots of high-resolution figures or many long tables, however you can compile your main document incrementally (i.e. by adding one chapter at a time), and the compiler, even if it crashes, will continue updating the log files until, after sveral tounds of compiling, it will eventually spit out the final PDF file. 

Overleaf and LaTeX produce PDF files, which are non-editable and are a pain to comment and correct. For this reason you might want to have one MS Word document for each of you chapters, and get all your corrections and comments from your supervisor(s) done on those (that way you can take advantage of the track changes feature). When you have a final draft of a chapter, you can typeset it in Overleaf, by means of copy-pasting pieces of the manuscript, adding the necessary code snippets as you go along. I find this to be the best course of action, especially if the person(s) that have to make the corrections are not so code savvy. 

You can find a template 

## Pipeline for transferring from Word to Overleaf: 
1. Change citation style from Mendeley's Word plugin (References tab, works only in Windows), select style "BiBTeX in-line citations".
2. Change italics with TeX-friendly wrappers, use procedure from https://tex.stackexchange.com/a/140202: find-and-replace, with empty string in 'Find' with font: Italic; replace with \emph{^&}, font: Regular; click 'Replace all'. 
3. convert using pandoc command prompt utility. Open a terminal in the Word document's directory and use command: pandoc FILENAME.docx -f docx -t latex -s -o OUTPUT.tex
4. Open OUTPUT.tex in text editor and copy-paste bits of code. Will need extensive check and manual adjustment. 

CAUTION: some citation keys WILL be wrong! Need to manually check consistency using the original Word document as reference. 

## Pipeline for export from Mendeley to BiBTeX
1. For formatting of references in Mendeley see other note Mendeley bibliography formatting pipeline 
2. For export, make sure to be in 'All Documents', ordered by 'Author, ascending' 
3. Select all documents (select one, then Ctrl+A)
4. File > Export... > .bib
5. Navigate to where the exported file is
6. Find-replace all <i> to \emph{ and all </i> to }
7. Find and replace all " & " to " \& ".
8. Find and replace "a̧" to "\c{a}".  
9. Find and replace "Ľ" to "\v{L}". 
10. Save file and load to Overleaf
11. Make sure to reference the correct .bib file in the TeX

## Mendeley bibliography formatting pipeline
1. Check that you are in 'All documents' 
2. Check that they are ordered by 'Author, ascending' 
3. Check Citation Key
	- If it's incorrect, note down the incorrect key on the left-hand side of the table below, and the new, correct one on the right hand side
	- This will need to be found-replaced in the LaTeX document (they are inside \citep{^&} 
4. CAUTION: do not modify other fields before changing Citation Key, otherwise it won't register he changes! 
5. Check for correct formatting
	- TITLE: Species are in italics (use HTML notation, <i>text</i>), spaces before/after punctuation are correct, capitalization is correct, accents are correct
	-  AUTHORS 
	- JOURNAL NAME: check for misspelling and use suggested field as necessary
	- YEAR: check in the PDF that the year is correct
6. If the 'Type' is not 'Journal article', check that it is appropriate
7. Check if there are multiple files attached and eventually remove duplicates
