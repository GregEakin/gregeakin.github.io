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
Okasaki, Chris. [_Purely Functional Data Structures_](https://en.wikipedia.org/wiki/Purely_functional_data_structure).
Cambridge, U.K.: Cambridge UP, 1998. Print.

### Features:
* Abstract Data Types -> templates
* Immutable data structures -> readonly data members
* Lazy evaluation -> `class Lazy<T>`
* Polymorphic recursion -> Static member functions
* Structure dumping -> Only implemented in test code
* Recursive structures -> Not supported (cut and paste for now)

## Example -- [Unbalanced Set](https://github.com/GregEakin/FunProgramming/blob/dev/FunProgLib/tree/UnbalancedSet.cs)
```csharp
    public static class UnbalancedSet<T> where T : IComparable<T>
    {
        public sealed class Tree
        {
            public Tree(Tree a, T y, Tree b)
            {
                A = a;
                Y = y;
                B = b;
            }

            public Tree A { get; }
            public T Y { get; }
            public Tree B { get; }
        }

        public static Tree Empty => null;

        public static bool Member(T x, Tree s)
        {
            if (s == Empty) return false;
            if (x.CompareTo(s.Y) < 0) return Member(x, s.A);
            if (s.Y.CompareTo(x) < 0) return Member(x, s.B);
            return true;
        }

        public static Tree Insert(T x, Tree s)
        {
            if (s == Empty) return new Tree(Empty, x, Empty);
            if (x.CompareTo(s.Y) < 0) return new Tree(Insert(x, s.A), s.Y, s.B);
            if (s.Y.CompareTo(x) < 0) return new Tree(s.A, s.Y, Insert(x, s.B));
            return s;
        }
    }
```

First, let's convert the tree into a text string, so we can compare them in the [unit tests](https://github.com/GregEakin/FunProgramming/blob/dev/FunProgTests/tree/UnbalancedSetTests.cs).
```csharp
    private static string DumpTree<T>(UnbalancedSet<T>.Tree tree) where T : IComparable<T>
    {
        if (tree == UnbalancedSet<T>.Empty) return "\u2205";

        var results = new StringBuilder();

        results.Append('[');
        if (tree.A != UnbalancedSet<T>.Empty)
        {
            results.Append(DumpTree(tree.A));
            results.Append(',');
        }

        results.Append(tree.Y);

        if (tree.B != UnbalancedSet<T>.Empty)
        {
            results.Append(',');
            results.Append(DumpTree(tree.B));
        }
        results.Append(']');

        return results.ToString();
    }
```

Next we'll test the empty tree.
```csharp
    [Fact]
    public void EmptyTest()
    {
        var tree = UnbalancedSet<string>.Empty;
        Assert.Equal("\u2205", DumpTree(tree));
    }
```

Then we'll start with an empty tree, and add one element.
```csharp
    [Fact]
    public void SingleElementTest()
    {
        var tree = UnbalancedSet<string>.Empty;
        tree = UnbalancedSet<string>.Insert("a", tree);
        Assert.Equal("[a]", DumpTree(tree));
    }
```

Adding the same element twice results in no change.
```csharp
    [Fact]
    public void DuplicateElementTest()
    {
        var tree = UnbalancedSet<string>.Empty;
        tree = UnbalancedSet<string>.Insert("a", tree);
        tree = UnbalancedSet<string>.Insert("a", tree);
        Assert.Equal("[a]", DumpTree(tree));
    }
```

We'll verify the full layout of a given tree.
```csharp
    [Fact]
    public void DumpTreeTest()
    {
        const string data = "How now, brown cow?";
        var tree = data.Split().Aggregate(UnbalancedSet<string>.Empty, (current, word) => UnbalancedSet<string>.Insert(word, current));
        Assert.Equal("[[brown,[cow?]],How,[now,]]", DumpTree(tree));
    }
```

Searching for elements in the tree, works as expected.
```csharp
    [Fact]
    public void FindMembersTest()
    {
        const string data = "How now, brown cow?";
        var tree = data.Split().Aggregate(UnbalancedSet<string>.Empty, (current, word) => UnbalancedSet<string>.Insert(word, current));
        foreach (var word in data.Split())
            Assert.True(UnbalancedSet<string>.Member(word, tree));
        Assert.False(UnbalancedSet<string>.Member("wow", tree));
    }
```

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
[cambridge]: https://www.cambridge.org/core/books/purely-functional-data-structures/0409255DA1B48FA731859AC72E34D494
[source-code]: https://github.com/GregEakin/FunProgramming
[git-extensions]: https://gitextensions.github.io
[visual-studio]: https://visualstudio.microsoft.com/vs/community/
[resharper]: https://www.jetbrains.com/resharper/
[retrospective]: https://okasaki.blogspot.com/2008/02/ten-years-of-purely-functional-data.html
[amazon]: https://www.amazon.com/Purely-Functional-Structures-Chris-Okasaki/dp/0521663504/
[google-books]: https://books.google.com/books?id=SxPzSTcTalAC
[dissertation]: https://www.cs.cmu.edu/~rwh/theses/okasaki.pdf
[leonardoborges]: https://github.com/leonardoborges/purely-functional-data-structures
[vkostyukov]: https://github.com/vkostyukov/scalacaster
[topics]: https://github.com/topics/purely-functional-data-structures
