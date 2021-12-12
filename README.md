# Modern C++ Syntax Diff

Modern C++ - Syntax Difference

<!-- md-cpp-begin -->
# Table of Content
* [SET INSERTION](#std-set)
* [SEE ALSO](#see-also)
  * [Syntax specification](#syntax-specification)
  * [Perl implementations](#perl-implementations)
  * [Some other implementations](#some-other-implementations)
<!-- md-cpp-end -->

# SET INSERTION
## C++11 
<!---code: --->

```
std::set<int> mySet;
set::set<int>::iterator iter;
bool inserted { false };
std::tie(iter, inserted) = mySet.insert(55);
```
## C++17
<!---code: --->

```
std::set<int> mySet;
auto [iter, inserted ] = mySet.insert(55);
```

# SEE ALSO

## Syntax specification

* https://daringfireball.net/projects/markdown

## Perl implementations

* https://metacpan.org/pod/Text::Markdown
* https://metacpan.org/pod/Text::MultiMarkdown
* https://metacpan.org/pod/Markdown::TOC

## Some other implementations

* https://github.com/ekalinin/github-markdown-toc
* https://github.com/ekalinin/github-markdown-toc.go
* https://github.com/frnmst/md-toc
* https://github.com/eGavr/toc-md
