#meta:{
  title: "Condoc Quick User's Guide"
  author: "Robert Jahns"
  date: "January 5, 2020"
}

# condoc {.red}

A converter for markup / markdown like **pandoc**, but using the macro-language **C4** for coding and customize input parser and output renderer. It has template engine comparable features and uses an intermarkup (html) as something like a intermediate representation.

An important representation rule has the markdown plus [.mdp] format.

## General options 

`-f` *FORMAT*, `--from=`*FORMAT*

:   Specify input format.  *FORMAT* can be:

    ::: {#input-formats}
    - `commonmark` ([CommonMark] Markdown)
    - `docbook` ([DocBook])
    - `markdown` ([Pandoc's Markdown])
    - `markdown_github` ([GitHub-Flavored Markdown])
    - `markdown_plus` ([condoc's Markdown])
    :::

`-t` *FORMAT*, `--to=`*FORMAT*

:   Specify output format.  *FORMAT* can be:

    ::: {#output-formats}
    - `commonmark` ([CommonMark] Markdown)
    - `docbook5` (DocBook 5)
    - `html` or `html5` ([HTML], i.e. [HTML5]/XHTML [polyglot markup])
    - `html-files` ([HTML5]/XHTML Multi File)
    - `latex` ([LaTeX])
    - `man` ([roff man])
    - `beamer` ([LaTeX beamer][`beamer`] slide show)
    - `s5` ([S5] HTML and JavaScript slide show)
    :::

`--list-input-formats`

:   List supported input formats, one per line.

`--list-output-formats`

:   List supported output formats, one per line.


## Input options {.options}

`--shift-heading-level-by=`*NUMBER*

:   Shift heading levels by a positive or negative integer.
    For example, with `--shift-heading-level-by=-1`, level 2
    headings become level 1 headings, and level 3 headings
    become level 2 headings.  Headings cannot have a level
    less than 1, so a heading that would be shifted below level 1
    becomes a regular paragraph.  Exception: with a shift of -N,
    a level-N heading at the beginning of the document
    replaces the metadata title. `--shift-heading-level-by=-1`
    is a good choice when converting HTML or Markdown documents that
    use an initial level-1 heading for the document title and
    level-2+ headings for sections. `--shift-heading-level-by=1`
    may be a good choice for converting Markdown documents that
    use level-1 headings for sections to HTML, since pandoc uses
    a level-1 heading to render the document title.


## Output options {.options}

`-b` *TAG*, `--break=`*TAG*

:   Define an Intermarkup / HTML Tag, which points to a tag 
    for breaking/split the input to multiple output files.
    
`-i`, `--index`

:   In combination with `-b` / `--break` generates an index file
    with a linking table of content
    
`-c` *URL*, `--css=`*URL*, `--css=`*URL*,*URL*,*URL*

:   Link to a CSS style sheet. This option can be used repeatedly to
    include multiple files. They will be included in the order specified.
    A stylesheet is required for generating EPUB.  If none is
    provided using this option (or the `css` or `stylesheet`
    metadata fields), pandoc will look for a file `epub.css` in the
    user data directory (see `--data-dir`).  If it is not
    found there, sensible defaults will be used.
    
`-h` *TITLE*, `--header-title=`*TITLE*

:   Produce output with an appropriate header and footer (e.g. a
    standalone HTML, LaTeX, TEI, or RTF file, not a fragment).  This option
    is set automatically for `pdf`, `epub`, `epub3`, `fb2`, `docx`, and `odt`
    output.  For `native` output, this option causes metadata to
    be included; otherwise, metadata is suppressed.

`-s`, `--standalone`

:   Produce output with an appropriate header and footer (e.g. a
    standalone HTML, LaTeX, TEI, or RTF file, not a fragment).  This option
    is set automatically for `pdf`, `epub`, `epub3`, `fb2`, `docx`, and `odt`
    output.  For `native` output, this option causes metadata to
    be included; otherwise, metadata is suppressed.

`--toc-depth=`*NUMBER*

:   Specify the number of section levels to include in the table
    of contents.  The default is 3 (which means that level-1, 2, and 3
    headings will be listed in the contents).

`--no-highlight`

:   Disables syntax highlighting for code blocks and inlines, even when
    a language attribute is given.
    
`--html-q-tags`

:   Use `<q>` tags for quotes in HTML.    

`--ascii`

:   Use only ASCII characters in output. Currently supported for XML
    and HTML formats (which use entities instead of UTF-8 when this
    option is selected), CommonMark, gfm, and Markdown (which use
    entities), roff ms (which use hexadecimal escapes), and to a
    limited degree LaTeX (which uses standard commands for accented
    characters when possible). roff man output uses ASCII by default.

## Examples for converts:

### simple markdown plus to html fragment
```bash
$ cat > file.mdp
# Head 1

## Head 1.1
Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore

## Head 1.2
Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore 
magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd 
gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing
elitr, sed diam

$ condoc -t html file.mdp file.html
$ 
```
This convert the file.mdp to a single html file file.html.

```html
    <h1>Head 1</h1>
    
    <h2>Head 1.1</h2>
    <div>Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore</div>
    
    <h2>Head 1.2</h2>
    <div>
    Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore 
    magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd 
    gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing
    elitr, sed diam
    </div>
```

### simple markdown plus to html 
The following converts the file.mdp sets the html title to HTML-Document and writes the converted to stdout.
```bash
$ condoc -f markplus -t html -sh "HTML-Document" file.mdp -
<html>
  <head>
    <title>HTML-Document</title>
  </head>
  <body>
    <h1>Head 1</h1>
    
    <h2>Head 1.1</h2>
    <div>Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore</div>
    
    <h2>Head 1.2</h2>
    <div>
    Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore 
    magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd 
    gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing
    elitr, sed diam
    </div>
   </body>
 </html>
$
```


### markdown plus to multiple html files
Now see a more complex example for writing multiple files from a single input file:
```bash
$ condoc -t html-files -ib "<h2>" -sh "HTML-Document#ifdef(${head2}){' ~ ${head2}'}" file.mdp files/
$ 
```
This will convert a single markdown plus file, to multiple files inside of the files folder.
Breaking this content down by each "\<h2>" / "## header" into a separated file.

generated files are:

files/index.html
```html
<html>
  <head>
    <title>HTML-Document</title>
  </head>
  <body>
    <h1>Head 1</h1>
    
    <ul>
      <li><a href="head_1_1.html">Head 1.1</a></li>
      <li><a href="head_1_2.html">Head 1.2</a></li>
    </ul>
    
  </body>
</html>
```

files/head_1_1.html
```html
<html>
  <head>
    <title>HTML-Document ~ Head 1.1</title>
  </head>
  <body>
    <h2>Head 1.1</h2>
    <div>Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore</div>
    
    <div><a href="index.html">Home</a></div>
  </body>
</html>
```

files/head_1_2.html
```html
<html>
  <head>
    <title>HTML-Document ~ Head 1.2</title>
  </head>
  <body>
    <h2>Head 1.2</h2>
    <div>
    Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore 
    magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd 
    gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing
    elitr, sed diam
    </div>
    
    <div><a href="index.html">Home</a></div>    
  </body>
</html>
```

### convert markdown to html template layout engine
```bash
$ condoc -f markplus -t html-files -ib "<h2>" -sh "HTML-Doc" -e bootstrap.c4.html -v outputfiles=[part1,part2] file.mdp files/
$ 
```
This convert the file.mdp as markdown plus to html files.
Using the `bootstrap.c4.html` file as template.

_footer.c4.html
```razor
<hr />
<div class="footer">
  &copy; 2012 Me. All rights reserved.
</div>
```

_header.c4.html
```razor

@bundle Sheets += () => "
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css">
"
@bundle Scripts += () => "
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js"></script>    
"
@section Script() => "
    <script type="text/javascript">
      console.log("page layout");
    </script>
"

    <nav class="navbar navbar-expand-sm bg-dark navbar-dark">
      <span class="navbar-brand">@head["title"]</span>
      <ul class="navbar-nav">    
        @outputfiles.each(f){ if(n==__file__) '<li><a class="nav-link active" href="#"   >#{f}</a></li>' else 
                                              '<li><a class="nav-link"        href="#{f}">#{f}</a></li>'; }
      </ul>
    </nav>
```


bootstrap.c4.html
```razor
@bundle Scripts += () => "
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
"

<!DOCTYPE html>
<html>
  <head>
    <title>@head["title"]</title>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    @Bundle(Sheets, bundle.minify)
  </head>
  <body>
    @RenderPage("$/_header.c4.html")
    @RenderBody()

    @RenderPage("$/_footer.c4.html")
    @Bundle(Scripts)
    @RenderSection(Script, required: false)
  </body>
</html>
```

files/part1.html
```html
<!DOCTYPE html>
<html>
  <head>
    <title>HTML-Doc</title>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="be722b64-672b-47c1-8088-f120295dfe19.min.css">
  </head>
  <body>
    <nav class="navbar navbar-expand-sm bg-dark navbar-dark">
      <span class="navbar-brand">HTML-Doc</span>
      <ul class="navbar-nav">    
        <li><a class="nav-link active" href="#"         >part1</a></li>
        <li><a class="nav-link"        href="part2.html">part2</a></li>
      </ul>
    </nav>
    <h2>Head 1.1</h2>
    <div>Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore</div>

    <hr />
    <div class="footer">
      &copy; 2012 Me. All rights reserved.
    </div>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js"></script>    
    <script type="text/javascript">
      console.log("page layout");
    </script>
  </body>
</html>
```


files/part2.html
```html
<!DOCTYPE html>
<html>
  <head>
    <title>HTML-Doc</title>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="be722b64-672b-47c1-8088-f120295dfe19.min.css">
  </head>
  <body>
    <nav class="navbar navbar-expand-sm bg-dark navbar-dark">
      <span class="navbar-brand">HTML-Doc</span>
      <ul class="navbar-nav">    
        <li><a class="nav-link"        href="part1.html">part1</a></li>
        <li><a class="nav-link active" href="#"         >part2</a></li>
      </ul>
    </nav>
    <h2>Head 1.2</h2>
    <div>
    Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore 
    magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd 
    gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing
    elitr, sed diam
    </div>

    <div class="footer">
      &copy; 2012 Me. All rights reserved.
    </div>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js"></script>    
    <script type="text/javascript">
      console.log("page layout");
    </script>
  </body>
</html>
```

### Convert to LaTeX

```bash
$ condoc --t latex file.mdp files.tex
$ 
```


---

## Related ...

`condoc` will be used by *Cex* a static document and site generator and cli program.
The target is to create with `cex` a technicality documentary system TDS like DocBook.
It has to generate complete books, websites and s5 presentations.

See for the *cex project* [cex-cli](../condoc-cex.cli)

For *markdown plus* specification see [markdown+](https://cex.github.io/Index.html)

---

A similar approach has maybe https://github.com/rust-spandex.
