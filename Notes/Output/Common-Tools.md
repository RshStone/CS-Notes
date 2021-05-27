# Common Tools

## JavaScript RegExp Reference

Reference: https://www.w3schools.com/jsref/jsref_obj_regexp.asp

Regular expressions are used to perform pattern-matching and "search-and-replace" functions on text.

- Syntax: /pattern/modifiers;

- Modifiers: used to perform case-insensitive and global searches:

  | [g](https://www.w3schools.com/jsref/jsref_regexp_g.asp) | Perform a global match            |

  | ------------------------------------------------------- | --------------------------------- |

  | [i](https://www.w3schools.com/jsref/jsref_regexp_i.asp) | Perform case-insensitive matching |

  | [m](https://www.w3schools.com/jsref/jsref_regexp_m.asp) | Perform multiline matching        |


- Brackets: used to find a range of characters:

  **^n找以n开头的**

  **[^n]除了n以外的**

  | [[abc\]](https://www.w3schools.com/jsref/jsref_regexp_charset.asp) | Find any character between the brackets                     |

  | ------------------------------------------------------------ | ----------------------------------------------------------- |

  | [[^abc\]](https://www.w3schools.com/jsref/jsref_regexp_charset_not.asp) | Find any character NOT between the brackets                 |

  | [[0-9\]](https://www.w3schools.com/jsref/jsref_regexp_0-9.asp) | Find any character between the brackets (any digit)         |

  | [[^0-9\]](https://www.w3schools.com/jsref/jsref_regexp_not_0-9.asp) | Find any character NOT between the brackets (any non-digit) |

  | [(x\|y)](https://www.w3schools.com/jsref/jsref_regexp_xy.asp) | Find any of the alternatives specified                      |


- Metacharacters: special meaning characters

  | [.](https://www.w3schools.com/jsref/jsref_regexp_dot.asp)    | Find a single character, except newline or line terminator   |

  | ------------------------------------------------------------ | ------------------------------------------------------------ |

  | [\w](https://www.w3schools.com/jsref/jsref_regexp_wordchar.asp) | Find a word character                                        |

  | [\W](https://www.w3schools.com/jsref/jsref_regexp_wordchar_non.asp) | Find a non-word character                                    |

  | [\d](https://www.w3schools.com/jsref/jsref_regexp_digit.asp) | Find a digit                                                 |

  | [\D](https://www.w3schools.com/jsref/jsref_regexp_digit_non.asp) | Find a non-digit character                                   |

  | [\s](https://www.w3schools.com/jsref/jsref_regexp_whitespace.asp) | Find a whitespace character                                  |

  | [\S](https://www.w3schools.com/jsref/jsref_regexp_whitespace_non.asp) | Find a non-whitespace character                              |

  | [\b](https://www.w3schools.com/jsref/jsref_regexp_begin.asp) | Find a match at the beginning/end of a word, beginning like this: \bHI, end like this: HI\b |

  | [\B](https://www.w3schools.com/jsref/jsref_regexp_begin_not.asp) | Find a match, but not at the beginning/end of a word         |

  | [\0](https://www.w3schools.com/jsref/jsref_regexp_nul.asp)   | Find a NULL character                                        |

  | [\n](https://www.w3schools.com/jsref/jsref_regexp_newline.asp) | Find a new line character                                    |

  | [\f](https://www.w3schools.com/jsref/jsref_regexp_formfeed.asp) | Find a form feed character                                   |

  | [\r](https://www.w3schools.com/jsref/jsref_regexp_carriagereturn.asp) | Find a carriage return character                             |

  | [\t](https://www.w3schools.com/jsref/jsref_regexp_tab.asp)   | Find a tab character                                         |

  | [\v](https://www.w3schools.com/jsref/jsref_regexp_vtab.asp)  | Find a vertical tab character                                |

  | [\xxx](https://www.w3schools.com/jsref/jsref_regexp_octal.asp) | Find the character specified by an octal number xxx          |

  | [\xdd](https://www.w3schools.com/jsref/jsref_regexp_hex.asp) | Find the character specified by a hexadecimal number dd      |

  | [\udddd](https://www.w3schools.com/jsref/jsref_regexp_unicode_hex.asp) | Find the Unicode character specified by a hexadecimal number dddd |


- Quantifiers

  | Quantifier                                                   | Description                                                  |

    | :----------------------------------------------------------- | :----------------------------------------------------------- |

  | [n+](https://www.w3schools.com/jsref/jsref_regexp_onemore.asp) | Matches any string that contains at least one *
  n*            |

  | [n*](https://www.w3schools.com/jsref/jsref_regexp_zeromore.asp) | Matches any string that contains zero or more occurrences of *
  n* |

  | [n?](https://www.w3schools.com/jsref/jsref_regexp_zeroone.asp) | Matches any string that contains zero or one occurrences of *
  n* |

  | [n{X}](https://www.w3schools.com/jsref/jsref_regexp_nx.asp)  | Matches any string that contains a sequence of *X* *
  n*'s     |

  | [n{X,Y}](https://www.w3schools.com/jsref/jsref_regexp_nxy.asp) | Matches any string that contains a sequence of X to Y *
  n*'s  |

  | [n{X,}](https://www.w3schools.com/jsref/jsref_regexp_nxcomma.asp) | Matches any string that contains a sequence of at least X *
  n*'s |

  | [n$](https://www.w3schools.com/jsref/jsref_regexp_ndollar.asp) | Matches any string with *
  n* at the end of it                 |

  | [^n](https://www.w3schools.com/jsref/jsref_regexp_ncaret.asp) | Matches any string with *
  n* at the beginning of it           |

  | [?=n](https://www.w3schools.com/jsref/jsref_regexp_nfollow.asp) | Matches any string that is followed by a specific string *
  n* |

  | [?!n](https://www.w3schools.com/jsref/jsref_regexp_nfollow_not.asp) | Matches any string that is not followed by a specific string *
  n*s |


- RegExp Object Properties

  | Property                                                     | Description                                                  |

  | :----------------------------------------------------------- | :----------------------------------------------------------- |

  | [constructor](https://www.w3schools.com/jsref/jsref_regexp_constructor.asp) | Returns the function that created the RegExp object's prototype |

  | [global](https://www.w3schools.com/jsref/jsref_regexp_global.asp) | Checks whether the "g" modifier is set                       |

  | [ignoreCase](https://www.w3schools.com/jsref/jsref_regexp_ignorecase.asp) | Checks whether the "i" modifier is set                       |

  | [lastIndex](https://www.w3schools.com/jsref/jsref_regexp_lastindex.asp) | Specifies the index at which to start the next match         |

  | [multiline](https://www.w3schools.com/jsref/jsref_regexp_multiline.asp) | Checks whether the "m" modifier is set                       |

  | [source](https://www.w3schools.com/jsref/jsref_regexp_source.asp) | Returns the text of the RegExp pattern                       |


- RegExp Object Methods

  | [exec()](https://www.w3schools.com/jsref/jsref_regexp_exec.asp) | Tests for a match in a string. Returns the first match |

  | ------------------------------------------------------------ | ------------------------------------------------------ |

  | [test()](https://www.w3schools.com/jsref/jsref_regexp_test.asp) | Tests for a match in a string. Returns true or false   |

  | [toString()](https://www.w3schools.com/jsref/jsref_regexp_tostring.asp) | Returns the string value of the regular expression     |


## Maven

- ​	Apache Maven is a software project management and comprehension tool. Based on the concept of a project object model (POM), Maven can manage a project's build, reporting and documentation from a central piece of information.

- **What is Maven?**

  Maven, a [Yiddish word](https://en.wikipedia.org/wiki/Maven) meaning *accumulator of knowledge*

  began as an attempt to simplify the build processes in the Jakarta Turbine project

  The result is a tool that can now be used for building and managing any Java-based project. 

  **Maven's Objectives**

   Maven deals with several areas of concern:

  - Making the build process easy
  - Providing a uniform build system
  - Providing quality project information
  - Encouraging better development practices

- **Feature Summary**(不懂，实践了再回顾)
  - Simple project setup that follows best practices - get a new project or module started in seconds
  - Consistent usage across all projects - means no ramp up time for new developers coming onto a project
  - Superior dependency management including automatic updating, dependency closures (also known as transitive dependencies)
  - Able to easily work with multiple projects at the same time
  - A [large and growing repository of libraries and metadata](https://maven.apache.org/repository/) to use out of the box, and arrangements in place with the largest Open Source projects for real-time availability of their latest releases
  - Extensible, with the ability to easily [write plugins](https://maven.apache.org/plugin-developers/) in Java or scripting languages
  - Instant access to new features with little or no extra configuration
  - Ant tasks for dependency management and deployment outside of Maven
  - Model based builds: Maven is able to build any number of projects into predefined output types such as a JAR, WAR, or distribution based on metadata about the project, without the need to do any scripting in most cases.
  - Coherent site of project information: Using the same metadata as for the build process, Maven is able to generate a web site or PDF including any documentation you care to add, and adds to that standard reports about the state of development of the project. Examples of this information can be seen at the bottom of the left-hand navigation of this site under the "Project Information" and "Project Reports" submenus.
  - Release management and distribution publication: Without much additional configuration, Maven will integrate with your source control system (such as Subversion or Git) and manage the release of a project based on a certain tag. It can also publish this to a distribution location for use by other projects. Maven is able to publish individual outputs such as a JAR, an archive including other dependencies and documentation, or as a source distribution.
  - Dependency management: Maven encourages the use of a central repository of JARs and other dependencies. Maven comes with a mechanism that your project's clients can use to download any JARs required for building your project from a central JAR repository much like Perl's CPAN. This allows users of Maven to reuse JARs across projects and encourages communication between projects to ensure that backward compatibility issues are dealt with.

- 