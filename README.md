# Python Markdown Generator

Python library for generating HTML sanitised Markdown documents.

It aims to bring modular approach for dynamically building pure (with some exceptions) Markdown documents with pure Python, with such a way, that they could consist multiple reusable components and with including some automated tasks such as creation  of table of contents.

[![CircleCI](https://img.shields.io/circleci/build/github/Nicceboy/python-markdown-generator?label=CircleCI&logo=circleci)](https://circleci.com/gh/Nicceboy/python-markdown-generator)
[![codecov](https://codecov.io/gh/Nicceboy/python-markdown-generator/branch/master/graph/badge.svg)](https://codecov.io/gh/Nicceboy/python-markdown-generator)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

## But why?

In most cases, Markdown is finally converted into HTML markup language, and there are already multiple existing libraries for generating HTML output dynamically.
Markdown was originally created as a lightweight, user-friendly, user-written text formatting markup language to produce rich text format by using plain text editor, and existence of this kind of library might be against the original purpose of the language.

*However*, there are couple of rare use cases, where you might want machine to generate Markdown *instead* of direct HTML.  
  * Some documents can be ideally generated by machine, but they might be edited by some user later on.
  * There might be need to generate some Markdown templates, which are finally filled by end-user. Still, there might be easier ways to create this kind of templates.
  * Also, there are some external systems, whereof HTML rendering is not supported, but you can input Markdown into them: this allows integration of something automatically into these systems with Markdown
  * Markdown syntax is simple and not fully-featured language, which could result in cleaner and simpler (less buggy!) result. Resulted file itself is a lightweight.

The original need for this kind of library came from the need to generate different kind of reports automatically into Git repositories, with Python. This library was created during [CinCan](https://cincan.io/) project to dynamically make malware analysis reports which are deployed and rendered directly into the Git -repositories.

At the time of starting of making this library, no complete existing similar library was found. If there is some, let's take this as a programming exercise...

> This is **not** yet-another-Markdown-to-HTML conversion tool.


## Quick Install

Python 3.7+ is required.

You can install latest version from the GitHub by using pip:
```shell
pip3 install git+https://github.com/Nicceboy/python-markdown-generator
```

## Quick usage

After installing, library can be just imported and we are ready to rock.
Method names should be self descriptive.

Library is supporting currently all the syntax from the standard Markdown, and some partial functionality of GitHub and GitLab syntax.

:TODO Better example, included in wiki maybe, documentation on the way for methods.

```python
from markdowngenerator import MarkdownGenerator

def main():
    with MarkdownGenerator(
        # By setting enable_write as False, content of the file is written
        # into buffer at first, instead of writing directly into the file
        # This enables for example the generation of table of contents
        filename="example.md", enable_write=False
    ) as doc:
        doc.addHeader(1, "Hello there!")
        doc.writeTextLine(f'{doc.addBoldedText("This is just a test.")}')
        doc.addHeader(2, "Second level header.")
        table = [
            {"Column1": "col1row1 data", "Column2": "col2row1 data"},
            {"Column1": "col1row2 data", "Column2": "col2row2 data"},
        ]

        doc.addTable(dictionary_list=table)
        doc.writeTextLine("Ending the document....")

if __name__ == "__main__":
    main()
```

Which should generate following output:

```
# Hello there!  
**This is just a test.**  
  
### Table of Contents  
  * [Hello there!](#hello-there)
    * [Second level header.](#second-level-header)
  
## Second level header.  
  
| Column1 | Column2 |  
|:---:|:---:|  
| col1row1 data | col2row1 data |  
| col1row2 data | col2row2 data |  

Ending the document....

```




## License

Copyright &#169; 2021 Niklas Saari. All rights reserved.

This work is licensed under the terms of the MIT license.  
For a copy, see <https://opensource.org/licenses/MIT>.


