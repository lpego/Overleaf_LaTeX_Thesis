# Typesetting your thesis in LaTeX using Overleaf
This is a brief & scuffed walkthough to formatting your MSc or PhD thesis using LaTeX and Overleaf. 

If you are thinking of using MS Word to format your PhD thesis, let me tell you that it's a *bad idea*. You will certainly have to make changes down the line, and no matter how well you planned out your styles and references you will end up with imperfections and possibly mistakes. Furthermore, the document file will become large pretty quicky, and, especially if you use a reference manager, MS Word will start slowing down and will become unusable. 

LaTeX solves all these problems, and ensures your final document has all the bibliography, table and figure references correctly formatted automagically, as well as giving a sleek look to your documents. LaTeX is a fully-fledged typesetting language, and can achieve tasks that MS Word simply cannot, and, among other things, is especially good at handling equations and formulae, as well as handling table and figure positioning within the page. Google and StackExchange are your best friends, and learning how to search and adapt code snippets is key. 

[Overleaf](https://www.overleaf.com) is an online tool that lets you write and compile your own LaTeX code, without the need to install anything on your computer. It has extensive help pages, and is great for newcomers to LaTeX: see their page on [Learning LaTeX in 30 minutes](https://www.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes). The free version comes with a few limitations, the most important of which is the 3 minutes compilation time limit. This can be annoying if you have lots of high-resolution figures or many long tables, however you can compile your main document incrementally (i.e. by adding one chapter at a time), and the compiler, even if it crashes, will continue updating the log files until, after sveral rounds of compiling, it will eventually spit out the final PDF file. 

Overleaf and LaTeX produce PDF files, which are non-editable and are a pain to comment and correct. For this reason you might want to have one MS Word document for each of you chapters, and get all your corrections and comments from your supervisor(s) done on those (that way you can take advantage of the track changes feature). When you have a final draft of a chapter, you can typeset it in Overleaf, by means of copy-pasting pieces of the manuscript, adding the necessary code snippets as you go along. I find this to be the best course of action, especially if the person(s) that have to make the corrections are not so code savvy. 

--- 

You can find a template to my thesis's Overleaf project here: https://www.overleaf.com/read/vykxxgcxmvmv 
Please note that this is an extract, as I removed most chapters to speed up compiling and keeping it relatively simple. There are many warnings (I get 113), but these are about references to missing files/figures (denoted by **??** in the PDF) that I removed to make the template (i.e. I couldn't be bothered to remove them from the main text). In the template I've left the whole of Chapter 2 with its appendices, so you can get a close idea of what you can expect as a finished product, as well as some useful tricks (e.g. multi-page tables with repeated headers, forcing gifures to float where you want them, etc). 

Hopefully the code is commented enough that you can make sense of it, but note the basic structure: there's a master script, called <code>THESIS.tex</code>, where all the document variables declarations happen, and inside this document I call the separate scripts for each chapter (e.g. <code>Ch2_Apomixis.tex</code>). This way you can comment out (shortcut Ctrl+/ or Cmd+/) the lines chapters that you don't need and only compile what you are working on, significantly improving compilation time. 
Should anything go wrong, you can try and delete the cached files: on the right panel of Overleaf, select the 'Logs and output files' icon, scroll all the way down, and there will be a dustbin icon that allows you to delete cached files. Doing this before recompiling can solve some errors, especially if you move sections around and references get messed up. 

## Pipeline for transferring from MS Word to Overleaf: 
1. Download and install Mendeley's MS Word plugin. 
2. From the MS Word Mendeley plugin, in the 'References' tab, open the 'Style' the drop-down menu and select 'More Styles'. In the new window that opened, go in the 'Get more styles' tab, and paste the link http://csl.mendeley.com/styles/487896501/bibtex into it, then click 'Download'. 
3. Back to MS Word, change citation style from Mendeley's Word plugin ('References' tab), select style "BiBTeX in-line citations".
4. Change italics with TeX-friendly wrappers, use procedure from https://tex.stackexchange.com/a/140202: find-and-replace, with empty string in 'Find' with font: Italic; replace with <code>\emph{^&}</code>, font: Regular; click 'Replace all'. 
5. convert using **Pandoc** command prompt utility (get Pandoc [here](https://pandoc.org/)). Open a terminal in the Word document's directory and use command: <code>pandoc FILENAME.docx -f docx -t latex -s -o OUTPUT.tex</code>. Pandoc is also very handy to convert tables from .xlsx or .csv format to TeX-friendly, just put the correct file format in place of <code>docx</code>. 
6. Open <code>OUTPUT.tex</code> in text editor and copy-paste (piecemeal suggested, easier to debug). Will need extensive check and manual adjustments. 

*CAUTION*: some citation keys *will be* wrong! Need to manually check consistency using the original Word document as reference, particularly for multiple papers per author/year. 

## Reference managers and the bibliography
The way LaTeX manages references is through BiBTeX, technically a separate program but they're almost always used in tandem. BiBTeX understands the <code>.bib</code> format, that uses a number of fields to define a reference. You can read more about that on Overleaf's [help pages](https://www.overleaf.com/learn/latex/bibliography_management_with_bibtex). 

You will most likely already been using a reference manager to keep track of all your bibliograhy. To my knowedge, the most popular are Endnote, Mendeley and Zotero. I used Mendeley, and the procedure below refers to it. You will have to figure a way to have your reference manager of choice export a <code>.bib</code> file with all your references (it does not matter whether you use the in your thesis or not), and upload that to Overleaf. Pay close attention to the first line, immediately following the publication type declaration (e.g. <code>@article{Abbott2003</code>), as these are the keywords that LaTeX will use in the text. Overleaf offers an autocompletion feature for references, that will present you with a choice of matching keywords when you start typing in a reference: be mindful of this, especially if you have multiple papers with the same author(s) and the same year! 

### Using Mendeley to format the references and bibliography

#### Mendeley bibliography formatting pipeline
1. Check that you are in 'All documents' 
2. Check that they are ordered by 'Author, ascending' 
3. Check Citation Key
	- If it's incorrect, note down the incorrect key on the left-hand side of the table below, and the new, correct one on the right hand side
	- This will need to be found-replaced in the LaTeX document (they are inside <code>\citep{^&}</code>) 
4. *CAUTION*: do not modify other fields before changing Citation Key, otherwise it won't register the changes! 
5. Check for correct formatting
	- TITLE: Species are in italics (use HTML notation, <code>\<i\>text\<\/\i></code>), spaces before/after punctuation are correct, capitalization is correct, accents are correct
	- AUTHORS 
	- JOURNAL NAME: check for misspelling and use suggested field as necessary
	- YEAR: check in the PDF that the year is correct
6. If the 'Type' is not 'Journal article', check that it is appropriate
7. Check if there are multiple files attached and eventually remove duplicates

#### Pipeline for export from Mendeley to BiBTeX
1. For formatting of references in Mendeley see other note Mendeley bibliography formatting pipeline 
2. For export, make sure to be in 'All Documents', ordered by 'Author, ascending' 
3. Select all documents (select one, then Ctrl+A or Cmd+A)
4. File > Export... > .bib
5. Navigate to where the exported file is
6. Find-replace all <code>\<i\></code> to <code>\\emph\{</code> and all <code>\<\/i\></code> to <code>\}</code>	
7. Find and replace all <code>" & "</code> to <code>" \\& "</code>.
8. Find and replace <code>"a̧"</code> to <code>"\c{a}</code>".  
9. Find and replace <code>"Ľ"</code> to <code>"\v{L}"</code>. 
10. Save file and load to Overleaf
11. Make sure to reference the correct .bib file in the TeX
