# Project : ISBN-parser
Purpose is to provide a parser which reads a list of ISBN and tries to lookup metadata in an online repository.

## origin
When trying to compile a list of books I wanted to automate this. Given what was available at that exact time two options needed to be investigated:

* scan ISBN with mobile phone (Android)
* scan ISBN with webcam in laptop (Linux)

Within these options plenty of apps are available, but how good are they and how easy to use?

## output

The desired output would be a list, or something easily converted into it, so it can be mailed to a friend giving an overview of books.

## implementation

### Linux

#### ZBar bar code reader
[ZBar project homepage](http://zbar.sourceforge.net/) seems a logical option. It is also available in Debian which is a big plus. See: [Debian source package of ZBar](https://packages.debian.org/source/stretch/zbar) in Debian Stretch.

Conclusion: rich and interesting project. Drawback is one has to take the books to the laptop. A more mobile scanner would be more convenient.

### Android
