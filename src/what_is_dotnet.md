# What is .NET?

When you start trying to use C#, F#, or .NET, the first and most confusing hurdle in my experience is understanding what anything means. 

For example, the first time I got exposed to the .NET ecosystem and everything surrounding it was a couple of years ago. I decided that I wanted to make a C# application. Being a developer with some experience, I knew that C# was a compiled language similar to Java in some aspects. So, I expected to find some sort of SDK, maybe something equivalent to the JVM, and a compiler. Imagine my confusion when I found out that I had to install something called .NET, and instead of this ".NET" being some clear analogue to something else I've used, it was called a "...free, open-source, cross-platform framework for building modern apps and powerful cloud services" ([.NET | Build. Test. Deploy](https://dotnet.microsoft.com/en-us/)). I thought I was being re-directed to some paid service or some weighty framework that I didn't want to use, and tried desparately to find the "real" barebones C#.

Eventually, I learned that .NET is a critical piece of the "real" C# for most developers, but, even after I accepted that, there was a barage of different technologies and terms that confused me because they all sounded similar. Why does some documentation reference .NET, while others reference .NET full framework and others still reference .NET Core? What is ADO.NET? What is ASP, and is it the same as ASP.NET? What is ASP.NET Core? Is that the same as ASP.NET? What is Entity Framework Core? Is that the same as Entity Framework? And, what does Dapper have to do with that?

Essentailly, there was a lot of new stuff to take in, and a lot of it didn't make sense to me. And, I think it's reasonable if it doesn't make sense to other newcomers, or even people who have been using .NET related stuff for awhile. So, to make everything easier, I'm going to do my best in this section to clarify the differences between all of these similarly named technologies, what their purpose is and a little bit of the history surrounding them to make the origin of these confusing names a bit more clear.

## C#

So, to begin, C# is a programming language, and, according to Microsoft, is the most popular language to use with .NET ([Overview - A tour of C# | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/tour-of-csharp/overview)). C# is defined in the [C# language specification](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/readme), which is worked on by the [ECMA C# standard committee (TC49-TG2)](https://www.ecma-international.org/task-groups/tc49-tg2/) ([Standard specification - C# | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/specification/overview)). All of that is to say that there is a long, boring document worked on by a group of people that is completely public and free to view that defines how C# works. This, theoretically, means that anyone, if they wanted to, could use that specification to develop a C# compiler. 

However, that specification is way behind where C# actually is. The current version of C# is C#12, and the C#8 specification is still a draft.  [Microsoft specifications](https://github.com/dotnet/csharplang/tree/main/proposals), which are what the committee uses to make the real ECMA specifications, are up to date, but, as noted, are not the real, official specifications. In any case, you can easily read through what new features Microsoft added to C# in their unofficial specifications by checking out their [feature specifications page](https://learn.microsoft.com/en-us/dotnet/csharp/specification/feature-spec-overview).

So, in summary, C# is defined in specifications so anyone can make a compiler. ECMA releases official specifications for C#, but these are far behind the current version of C#. Microsoft also produces specifications for C#, which is what ECMA uses to make the real, official specifications. Finally, Microsoft releases feature specifications to allow a programmer to read through the new features the unofficial specifications bring.

However, there is probably one important question I didn't answer in all this talk of C#. And that's how to compile it. C# is a compiled language, but one of the first hurdles someone will have in using it is figuring out where to install the compiler or SDK for it. As time goes on, there may be more compilers or SDKs produced for C#. As I said, the public specification technically means that everyone with an internet connection has all the information they need to produce a C# compiler. However, at the moment, there are really only 3 places I'm aware of that you can find unique C# compilers. Those are [.NET](https://dotnet.microsoft.com/en-us/learn/dotnet/what-is-dotnet), [Mono](https://www.mono-project.com/) and [NativeAOT](https://github.com/dotnet/runtimelab/tree/feature/NativeAOT). But, if you go to any of those, you may notice that none of them are as simple as a compiler you just install and run. To understand that, it's high time I explain what .NET actually is

## .NET

According to [.NET's documentation](https://learn.microsoft.com/en-us/dotnet/core/introduction), ".NET is a free, cross-platform, [open-source developer platform](https://github.com/dotnet/core) for building [many kinds of applications](https://learn.microsoft.com/en-us/dotnet/core/apps). It can run programs written in [multiple languages](https://learn.microsoft.com/en-us/dotnet/fundamentals/languages), with [C#](https://learn.microsoft.com/en-us/dotnet/csharp/) being the most popular. It relies on a [high-performance](https://devblogs.microsoft.com/dotnet/category/performance/) runtime that is used in production by many [high-scale apps](https://devblogs.microsoft.com/dotnet/category/developer-stories/)". This definition is not bad, especially since Microsoft was trying to define a fairly complicated thing in just a few sentences. However, this definition doesn't really get to the heart of what's going on, and may be a bit dis-satisfying for someone trying to understand what .NET actually is.

A more accurate, but more complicated, definition for .NET may go as follows. .NET is a specification for a fancy virtual machine that is paired with a standard library, and, optionally, includes development tools and application frameworks ([.NET implementations - .NET | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/fundamentals/implementations)). For a program to be considered a ".NET Implementation", it specifically needs to have the following four components:

1. One or more runtimes. These runtimes must implment the [ECMA Common Language Infrastructure](https://www.ecma-international.org/publications-and-standards/standards/ecma-335/) standard. When they do that, these runtimes can be considered analagous to a JVM if you're familiar with Java. They're a virtual machine that runs on your computer and converts their own special assembly into instructions for your specific computer

2. A class library. The API of this class library is defined in the [.NET Standard](https://learn.microsoft.com/en-us/dotnet/standard/net-standard?tabs=net-standard-1-0). It can be considered analagous to `glibc` or `musl` if you're familiar with C. Basically, they're a standard library that any language that runs on the included runtimes can use

3. Optionally, one or more application frameworks, like ASP.NET or Windows Forms

4. Optionally, development tools

As you can see, that definition is more accurate, but it is harder to parse. However, I think it gets a lot more to the heart of what .NET is. In any case, I think there are some interesting things not included in that definition that should be noted.

First, for .NET implementations, it seems there's no specific definition for what "application frameworks" or "development tools" are, but it does seem pretty easy to figure out what Microsoft means when they talk about those.  An application framework is something like ASP.NET. It's just some large set of libraries, maybe even including it's own runtime that gives a developer features beyond the standard class library. And, development tools would be things like the dotnet CLI, which are just nice programs that can help a developer develop apps within that .NET implementation

Second, it may seem pedantic to point out that .NET is more of a specification and that there can be many different implementations of it. But, that is important, because Microsoft supports 4 different .NET implementations ([.NET implementations - .NET | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/fundamentals/implementations)). These are specifically:

- .NET 6 and later versions
- .NET Framework
- Mono
- UWP

Finally, you'll notice that this definition for .NET does not include any mention of C#, F# or Visual Basic. It seems that .NET is mainly a term for describing the virtual machine and helpful libraries that C#, F# and Visual Basic use after being compiled. So, .NET is language agnostic and could technically be used by any language or any syntax as long as someone wrote a compiler that allowed the language or syntax to run on a .NET runtime.

However, while this definition is nice, clean and simple, it doesn't necessarily capture the entire reality of the situation. While .NET generally means the definition I put above, in some contexts .NET can mean something else entirely. Mainly, .NET implementations are often just referred to as .NET. So, there's a bit of a dice roll as to whether someone's talking about the general specification or a specific implementation when they bring up ".NET". Further, even if someone is talking about the specification, they may just be talking about a .NET runtime or a class library implementing the .NET Standard. So, when they say ".NET", they actually mean a library or a fancy virual machine. 

Considering that .NET is an umbrella term for a lot of different things that make up an entire ecosystem, this is not too bad of a definition. However, it probably is still confusing to some degree. So, let's dig a little bit more into what .NET is.

You can think of .NET as being a singular thing that comes with 5 different components:

1. Runtimes - With all three languages associated to .NET - C#, F# and Visual Basic, the compiler compiles the code into a binary that needs to be read by a "runtime". A runtime is analgous to a JVM if you're familiar with Java. It's a mini computer that runs on your computer and executes the commands the binaries running on them want to run. There are many different .NET runtimes. As far as I can tell, the one thing that unifies all .NET runtimes is they all implement the [ECMA Common Language Infrastructure](https://www.ecma-international.org/publications-and-standards/standards/ecma-335/) standard. If this defintion is a bit difficult to parse, you can also check out the [.NET glossary's definition of a runtime](https://learn.microsoft.com/en-us/dotnet/standard/glossary#runtime). But, the upshot is that these runtimes are VMs that run binaries made for it.

2. Libraries - Any implementation of .NET includes an extensive amount of class libraries to use. The API of these class libraries is defined in the [.NET Standard](https://learn.microsoft.com/en-us/dotnet/standard/net-standard?tabs=net-standard-1-0). So, just like .NET runtimes, there can be and are many implementations of the standard library. Usually, different implementations are made for different runtimes. In any case, these included libraries can be thought of as the standard library for all the languages that use the .NET runtime ([Runtime libraries overview - .NET | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/standard/runtime-libraries-overview)). If you're importing something from the `System.*` or `Microsoft.*` namespaces, there is a good chance that you are using something from this standard library. Do note, however, that unlike most standard libraries, the implementation of .NET Standard is not attached to the language but to the runtime. And, as far as I know, as long as a language can compile into something compatible with the .NET runtime, it can use a .NET Standard implementation. It's also important to know that there a number of extensions for this standard library you can install via NuGet. These allow you to add things like Configuration, Dependency Inejction, File Globbing, Logging, etc ([Runtime libraries overview - .NET | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/standard/runtime-libraries-overview)).

3. Compilers - .NET includes compilers for C#, F# and Visual Basic. But, as mentioned before, these compilers are a bit unique. Instead of compiling this code into a binary that can run directly on your computer, these compilers compile your code into a binary that can run on a .NET runtime.

4. SDKs and other tools - The .NET Software Development Kit (SDK), like most SDKs, is an install of the most important tools required

5. App stacks

Each of these

However, the fun doesn't end there! .NET is more of an abstract definition rather than a specific implementation. What I mean by that is that there are many implementations of .NET, and a .NET app is one that developed for one or more implementations of .NET ([.NET implementations - .NET | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/fundamentals/implementations)). A .NET implementation must have one or more runtimes, a class library (like BCL), optionally application frameworks like ASP.NET Core and optionally development tools. According to Microsoft, there are 4 different .NET implementations that it supports:

- .NET 6 and later versions
- .NET Framework
- Mono
- UWP
