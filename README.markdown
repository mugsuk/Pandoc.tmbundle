# Please note

Since David abandoned TextMate for MacVim, and stopped supporting this bundle, I have modified a few of the conversion commands to work with Pandoc 2.19 and above. Most of the functions that I have not changed work with earlier versions of Pandoc, or I do not use and thus have not fiddled with. If you use Pandoc version prior to 2.19, please continue to use David's bundle. 

# Pandoc TextMate Bundle README

This is a TextMate bundle for use with John MacFarlane's [pandoc][].
It is for use with Pandoc versions 2.19 and above.
Pandoc is a command line tool that converts files from one markup format
to another. It is a powerful tool that can be used in many ways for many
purposes.

I write most documents in Pandoc's extended Markdown syntax. This bundle
was put together to serve the needs of someone doing that. It focuses on
commands for converting existing documents into Pandoc's markdown format
and commands for exporting documents written in Pandoc's markdown format
to HTML, LaTeX, ConTeXt, PDF, and ODT.

## Highlights

### Citations

Pandoc 2.19 continues support for processing citations but no longer needs you to call pandoc-citeproc.
This bundle supports this: most conversion commands have a "(citations)"
variant that will process ciations.

You must set the following variable in Preferences -\> Advanced -\>
Shell Variables:

-   $TM\_PANDOC\_BIB: the path of the bibliography database you want to
    use. (If the bundle were smarter it would fall back to
    $TM\_LATEX\_BIB if this variable was not set. But for now, it
    doesn't.)

### Autocompletion of Citation Keys

If $TM\_PANDOC\_BIB points to a bibtex, ris, citeproc json, or mods xml
file, then you can use TextMate's autocompletion (type part of a word
then hit the ESCAPE key) to complete citation keys. I have no idea how
robust this is: I am just using regexps in ruby to find the citation
keys. It shouldn't be hard to expand support for other bibliography
formats: let me know if there is a format that you are using that is
not supported. (FYI: support for completion from a zotero database is
something I'd like to add once zotero's api allows it.)

### Markdown Tidy

The bundle provides several commands that use pandoc as a kind of pretty
printer for markdown: pushing markdown through pandoc allows for each
conversion between inline and reference links, for example, and soft or
hard-wrapped lines. It also cleans up bullets and lists nicely.

### MultiMarkdown

David included a few commands for quickly converting some aspects of MMD
syntax to Pandoc syntax. There are commands for converting MMD metadata
to and from Pandoc Title Blocks. There is also a command for converting
MMD formatted citations, like `[p. 20][#citekey]` to Pandoc formatted
citations, like `[@citekey, p. 20]`.

### Drag and Drop Conversions

Open a new document in TextMate, set the language to Pandoc, drag a file
onto it, and the bundle will try to convert it to Pandoc Markdown - **this may not work as I have not updated these commands.**

Here are the details:

-   HTML, TeX, LaTeX, and RsT files are converted directly by pandoc.
    Limitations in the conversions are limitations in pandoc. All other
    files are first converted to HTML, then converted from HTML by
    pandoc.
-   ODT, DOC, DOCX, RTF, RTFD, WORDML, and webarchive files are first
    converted to html using apple's textutil command. This typically
    destroys footnotes. YMMV.
-   PDF files are first converted to HTML using [pdftohtml][], which
    you'll have to install.

## Language

For the Language syntax, Fletcher Penney's [MultiMarkdown Bundle][] is used, which is a slightly modified version of the
syntax file from the original Markdown plugin. Since several of the MMD
extensions are the same as the Pandoc extensions, this works okay.

## Scope

As a flavor of markdown: text.html.markdown.pandoc.
So if you have a markdown bundle installed, those commands should also
work in this bundle.

This makes sense for those who use markdown as an easy way to
write HTML, but is more likely to be used as an easy way to write
LaTeX or ConTeXt, which suggests changing the scope to something like
text.tex.markdown.pandoc, so as to inherit commands and syntax from the
LaTeX bundle instead of the HTML bundle. Those with greater TextMate fu
might have a better sense of how to think about this.

## Paths

You may need to set the PATH variable in TextMate's Preferences -\>
Advanced -\> Shell Variables to include the path to pandoc.

## Locale

If you get a "hGetContents: invalid argument (Illegal byte sequence)"
error, you need to set the LANG variable in TextMate's Preferences -\>
Advanced -\> Shell Variables to something like "en\_US.UTF-8". See [this
thread][] for details.

## Converting to ODT

The command that converts documents to ODT also automatically opens the
generated document. On a newer Mac, this should be fine. On an older
Mac, this can take a *long* time. If you are using this on an older Mac,
you might want to delete/comment out the line that says:

    open "$targetname"

  [vim-pandoc]: https://github.com/vim-pandoc/vim-pandoc%20The%20Pandoc.tmbundle%20won't%20be%20getting%20much%20love%20from%20me%20going%20forward.%20Since%20I'm%20not%20using%20it,%20I%20won't%20notice%20bugs%20and%20won't%20think%20of%20ways%20to%20improve%20it.%20I'm%20happy%20to%20pull%20in%20any%20bug%20fixes%20or%20improvements%20you%20might%20make.
  [pandoc]: http://johnmacfarlane.net/pandoc
  [elegant haskell scripts]: http://johnmacfarlane.net/pandoc/scripting.html
  [pdftohtml]: http://pdftohtml.sourceforge.net/
  [MultiMarkdown Bundle]: http://fletcherpenney.net/multimarkdown/multimarkdown_bundle_for_textm/
  [MultiMarkdown Theme]: http://files.fletcherpenney.net/MultiMarkdown.tmTheme.zip
  [this thread]: https://groups.google.com/group/pandoc-discuss/browse_thread/thread/3c5c156ac60a3f5a
  [Mellel2MMD.app]: http://wwwuser.gwdg.de/~mrosena/
