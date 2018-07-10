# Project : ISBN-parser
Purpose is to provide a parser which reads a list of ISBN and tries to lookup metadata in an online repository.

## Origin
When trying to compile a list of books I wanted to automate this. Given what was available at that exact time two options needed to be investigated:

* scan ISBN with mobile phone (Android)
* scan ISBN with webcam in laptop (Linux)

Within these options plenty of apps are available, but how good are they and how easy to use?

## Output

The desired output would be a list, or something easily converted into it, so it can be mailed to a friend giving an overview of books.

## Scanning implementation

### Linux

#### ZBar bar code reader
[ZBar project homepage](http://zbar.sourceforge.net/) seems a logical option. It is also available in Debian which is a big plus. See: [Debian source package of ZBar](https://packages.debian.org/source/stretch/zbar) in Debian Stretch.

Conclusion: rich and interesting project. Drawback is one has to take the books to the laptop. A more mobile scanner would be more convenient.

### Android

#### LoMag Scanner
Although many apps are available, this one seemed quite friendly given the permissions even though their [Privacy policy](http://www.longint.com/PrivacyPolicy.html) seems inconsistent. 
[LoMag scanner](https://play.google.com/store/apps/details?id=com.longint.lomag.scanner&hl=en)

## Parsing implementation

LoMag seems to works reasonbly well although scanning is not always trivial. Could be the device or the light.
The result can be mailed. The recipient will receive a Microsoft Excel 97-2003 compatible file.

Next this needs to be parsed so the meta data of the ISBN can be looked up by querying one of the online book registries.

### Read XLS file
[Working with Excel Files in Python](http://www.python-excel.org/) lists [XLRD](http://xlrd.readthedocs.io/en/latest/) is an option. As I have been very successful in the past using this, it seemed as a good idea. Again also as it is included in Debian.
So I wrote some code. It is included, for eductional purposes, as.... I found out it fails horribly. "1.0" is not something you want to be found in the xls-file, however every ISBN is read aninterpreted as such.
I am not the only one who stumbled upon this: [1.0 bug xlrd python lib](https://stackoverflow.com/questions/8542274/python-xlrd-receiving-float-from-excel-text-cell?rq=1)
Resulting it uter uselessness with the need to export the data to CSV (Comma Separated Value) file.

### read CVS file
Quite trivial regardless if you are uring Python 2 or Python 3 with [Standard Python CSV library](https://docs.python.org/3.6/library/csv.html)

### ISBNlib
[ISBNlib](https://pypi.org/project/isbnlib/)

ISBNlib allows for various export as can be seen on the [ISBNlib on Github](https://github.com/xlcnd/isbnlib) page:
The output can be formatted as:
* bibtex
* csl (CSL-JSON)
* msword
* endnote,
* refworks,
* opf
* json (BibJSON)
 bibliographic formats with isbnlib.registry.bibformatters. Cache only allows two values: 'Default' or 'None'. You can change the kind of cache by using isbnlib.registry.set_cache (see below). Now, you can extend the functionality of this function by adding pluggins, more metadata providers or new bibliographic formatters (check for available pluggins).

For all(?) output take note of:
* maybe not all items can be resolved
* maybe not all items are fully resolved
* documents are created per item, these should be combined in a properly formatted single document/file.

#### BiBTeX
Based on LaTeX.

* Homepage : https://bibtexparser.readthedocs.io/en/master/index.html
* Links with background info: https://bibtexparser.readthedocs.io/en/master/bibtex_conv.html
* Validate offline: https://code.google.com/archive/p/bibtex-check/
* Validate online: http://truben.no/latex/bibtex/

#### CSL (CSL-JSON)
Citation Styles Language based on JSON
https://citationstyles.org/

#### MS-Word
MSWord 2003 format
https://python-docx.readthedocs.io/en/latest/

#### EndNote
https://endnote.com/

#### RefWorks
https://en.wikipedia.org/wiki/RefWorks

#### Opf
http://idpf.org/

#### JSON (BibJSON)
http://okfnlabs.org/bibjson/

### CSV
I added this feature as this is what it was all about: import ISBN, query to get details and export it all in an easy to be used generic format.


### note to self: biblib
[BibLib](https://pypi.org/project/biblib/)
[Example](http://wgserve.de/biblib/tutorial.html#example)
