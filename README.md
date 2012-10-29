doxy2man
========

Create man pages from doxygen XML output.

## Rationale

[Doxygen][1] is great for generating HTML based API documentation. But the man
page output mode of doxygen (`GENERATE_MAN = YES`) is not that awesome. Doxygen
generates for a header file a man page with all functions, enums etc. For each
structure it generates a man page listing all its (public) attributes.  For C
based projects this is not very useful, because one usually expects things like one man
page for each function and referenced structs documented where used.
 
Doxy2man takes the XML generated by Doxygen as input and creates several man
pages from that. It creates a summary man page for a header and for each function a detailed
man page. The output is optimized for C projects. It supports the most common
doxygen features, e.g. implicit and explicit see also tags, copyright, author
information, brief and detailed descriptions, etc.


## Compile

Doxy2man is written in C++ and uses the [Qt][2] library (I tested it with version 4.8). You can build it like this:

    $ qmake-qt4
    $ make

## Usage

Create a small Doxygen configuration file. To enable XML output use something like this:

    GENERATE_XML           = YES
    XML_OUTPUT             = xml
    XML_PROGRAMLISTING     = NO

Call doxygen:

    $ doxygen

The `xml` subdirectory should contain some XML files now.

Call doxy2man:

    $ ./doxy2man xml/myheader_8h.xml

View the man pages:

    $ ls out
    ...
    $ man -l out/my_header.h.3
    $ man -l out/my_func_a.3
    $ man -l out/my_func_b.3
    ...

## Options

Doxy2man implements several useful defaults but is also customizable:

    $ ./doxy2man --help
    Generates man pages from doxygen XML output
    
    call: ./doxy2man OPTIONS DOXYGEN_XML_HEADER_FILE
    
    where
    
    -h,     --help           this screen
            --nowarn         suppress warnings
            --nosummary      don't generate summare man page
            --nocopyright    don't generate copyright section
            --nofollow       don't parse referenced xml files
            --novalidate     don't validate xml files against compound.xsd
            --noseealsoall   don't add all functions under see also
            --nosort         don't sort functions under see also
            --nostructs      don't print structs in function man pages
    -o DIR, --out DIR        output directory
    -s STR, --section STR    man page section
            --short-pkg STR  short man page header/footer string, e.g. 'Linux'
            --pkg STR        man page header/footer string, e.g. 'Linux Programmer's Manual'
    -i STR, --include STR    include path prefix

## Contact ##

Georg Sauthoff <mail@georg.so>

Don't hesitate to mail questions, comments or other feedback.

## License ##

GPLv3+



[1]: http://www.stack.nl/~dimitri/doxygen/
[2]: http://qt.digia.com/


