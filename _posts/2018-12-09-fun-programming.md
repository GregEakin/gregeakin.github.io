---
layout: post
title:  "Fun Programming!"
date:   2018-12-09 11:42:59 -0700
categories: software
---
A [__C#__][csharp] version of the data structures from Chris Okasaki's book [_Purely Functional Data Structures_][cambridge], 
coded as static functions to closely resemble the book's description.
This allows you to work through the examples, and follow the narrative, without having to understand [Standard ML][standard-ml] or [Haskell][haskell].
You can also fire these examples up in the debugger, to see the exactly how they tick.
Or even, check the performance with modern tools, and compare them with other designs.
Head on over to [github.com FunProgramming][source-code] to download the source code.

### From the book:
Okasaki, Chris. _Purely Functional Data Structures_.
Cambridge, U.K.: Cambridge UP, 1998. Print.

### Features:
* Abstract Data Types -> templates
* Immutable data structures -> readonly data members
* Lazy evaluation -> `class Lazy<T>`
* Polymorphic recursion -> Static member functions
* Structure dumping -> Only implemented in test code
* Recursive structures -> Not supported (cut and paste for now)

### Links:
* [Source Code][source-code]
* [Git Extensions][git-extensions]
* [Community Edition of Visual Studio][visual-studio]
* [ReShaper, Extensions for .NET Developers][resharper]
* [A retrospective from Chris Okasaki][retrospective]
* [Amazon.com][amazon]
* [Google Books][google-books]
* [The original PhD dissertation][dissertation]

[csharp]: https://en.wikipedia.org/wiki/C_Sharp_(programming_language)
[standard-ml]: https://en.wikipedia.org/wiki/Standard_ML
[haskell]: https://en.wikipedia.org/wiki/Haskell_(programming_language)
[cambridge]: http://www.cambridge.org/catalogue/catalogue.asp?isbn=0521663504
[source-code]: https://github.com/GregEakin/FunProgramming
[git-extensions]: http://gitextensions.github.io
[visual-studio]: https://visualstudio.microsoft.com/vs/community/
[resharper]: https://www.jetbrains.com/resharper/
[retrospective]: http://okasaki.blogspot.com/2008/02/ten-years-of-purely-functional-data.html
[amazon]: https://www.amazon.com/Purely-Functional-Structures-Chris-Okasaki/dp/0521663504/
[google-books]: https://books.google.com/books?id=SxPzSTcTalAC
[dissertation]: http://www.cs.cmu.edu/~rwh/theses/okasaki.pdf
[leonardoborges]: https://github.com/leonardoborges/purely-functional-data-structures
[vkostyukov]: https://github.com/vkostyukov/scalacaster
[topics]: https://github.com/topics/purely-functional-data-structures