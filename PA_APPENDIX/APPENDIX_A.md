#Pedal to the Metal: Accelerating Python
#将油门踩到底：加速Python学习进程

__Make it work, make it right, make it fast.__

__首先，我们让程序能够运行。接着，我们设法让它正确工作。最后，我们让它变得越来越快。__

—Kent Beck

——肯特·贝克，美国著名软件工程师与作家

This appendix is a tiny peek at some of the options for tweaking the constant factors of your implementations. Although this kind of optimization in many cases won’t take the place of proper algorithm design—especially if your problems can grow large—making your program run ten times as fast can indeed be very useful.

这篇附录提供了一些工具，借此来优化你的代码，使你的代码更简洁，或者更快速。然而这类优化在大多数情况下 并不能代替算法设计，然后让你的程序速度快上十倍——特别是你所处理的问题规模非常大的情况下。

Before calling for external help, you should make sure you’re using Python’s built-in tools to their full potential. I’ve given you some pointers throughout the book, including the proper uses of list versus deque, and how bisect and heapq can give you a great performance boost under the right circumstances. As a Python programmer, you’re also lucky enough to have easy access to one of the most advanced and efficient (and efficiently implemented) sorting algorithms out there (list.sort), as well as a really versatile and fast hash table (dict). You might even find that itertools and functools (especially the function cache decorators) can give your code a performance boost.

在我们寻求外部帮助之前，我们首先应该审视，我们是否已将Python的内建工具物尽其用了。在本书中，我给了 你很多相关的例子，例如双链表的使用，以及二分法与堆如何在合适的情况下提供巨大的性能提升。作为一个Python 程序员，幸运的是，Python提供了list和dict这两个非常好用的数据结构。list使得你你在很多情况下并不需要关心排序， 因为Python提供了最先进，最有效的排序算法之一的实现（list.sort），而dict则是一个功能多样而又迅速的哈希表的 实现。甚至你会发现，遍历工具与函数工具（特别是函数缓存装饰器）同样会让你的代码变得更高效。

Also, when choosing your technology, make sure you optimize only what you must. Optimizations do tend to make either your code or your tool setup more complicated, so make sure it’s worth it. If your algorithm scales “well enough” and your code is “fast enough,” introducing the extension modules in another language such as C might very well not be worth it. What is enough is, of course, up to you to determine. (For some hints on timing and profiling your code, see Chapter 2.)

其次，当我们选择外部库来优化我们的代码的时候，应该确保是否必须优化。优化本身经常会让我们的代码变得更复杂， 依赖变得更多，所以优化之前要想一想，优化真的值得吗？如果你的算法已经足够好，你的代码已经足够快，那么通常 就不值得引入用其他语言（例如C语言）撰写的外部模块了。当然，什么是“足够好”和“足够快”，是由你自己来判断的。 （你可以在第二章找到一些代码测速与剖析的例子）。

Note that the packages and extensions discussed in this appendix are mainly about optimizing single-processor code, either by providing efficiently implemented functionality, by letting you create or wrap extension modules, or by simply speeding up your Python interpreter. Distributing your processing to multiple cores and processors can certainly also be a big help. The multiprocessing module can be a place to start. If you want to explore this approach, you should be able to find a lot of third-party tools for distributed computing as well.

请注意，这篇附录中所讨论的包和外部扩展主要用于优化单处理器的代码。这些外部工具会提供高效实现的函数，或者 实现或包装扩展模块，或者提高Python解释器的效率。将代码改为多处理器版本当然会大大提高运行效率，如果你真的 打算这么做的话，multiprocessing模块是一个好的开始。如果你希望深入了解多核编程，你一定会找到非常多的关于 分布式计算的第三方工具。

In the following pages, I describe a selection of acceleration tools. There are several efforts in this area, and the landscape is of course a changing one: new projects appear from time to time, and some old ones fade and die. If you think one of these solutions sounds interesting, you should check out its web site, and consider the size and activity of its community—as well, of course, as your own needs. For web site URLs, see Table A-1 later in the appendix.

在接下来的几页中，我会介绍几种外部工具。有很多人为各种各样的应用情境编写了扩展，而这些扩展都在不断变化 这：新的项目如雨后春笋般不断涌现，而一些旧的项目则逐渐消失。看完我接下来介绍的几种扩展，如果你觉得其中 几个很有趣，并且打算用到你自己的项目里的话，你可以先浏览一下这些扩展的网站以及社区，本篇最后附有这些 网站的地址。

__NumPy, SciPy, and Sage.__ NumPy is a package with a long lineage. It is based on older projects such as Numeric and numarray, and at its core implements a multidimensional array of numbers. In addition to this data structure, NumPy has several efficiently implemented functions and operators that work on the entire array so that when you use them from Python, the number of function calls is minimized, letting you write highly efficient numeric computations without compiling any custom extensions. SciPy and Sage are much more ambitious projects (although with NumPy as one of their building blocks), collecting several tools for scientific, mathematical, and high-performance computing (including some of the ones mentioned later in this appendix).

__NumPy, SciPy, 和 Sage.__Numpy是一个历史悠久的包。它起源于更古老的项目，例如Numeric和numaray。Numpy在核心实现了多维数组。除此之外，它还实现了数个函数与运算符，它们能够高效地进行数组运算。Numpy包精简了函数调用次数，所以你可以使用它来进行极其高效的数学运算，而不用编译任何内置的扩展。SciPy和Sage则更为庞大，它们将NumPy内置为一部分，并且还内置了几样其他的工具，从而实现了科学，数学，以及高性能计算。在本附录接下来的篇幅中会详细介绍。

__Psyco, PyPy, and Unladen Swallow.__ One of the least intrusive approaches to speeding up your code is to use a just-in-time (JIT) compiler, such as Psyco. After installing it, you simply need to import the psyco module and call psyco.full() to get a potentially quite noticeable speedup. Psyco compiles parts of your Python program into machine code while your program is running. Because it can watch what happens to your program at runtime, it can make optimizations that a static compiler could not. For example, a Python list can contain arbitrary values. If, however, Psyco notices that a given list of yours only ever seems to contain integers, it can assume that this will be the case also in the future and compile that part of the code as if your list were an array of integers. Sadly, like several of the Python acceleration solutions, Psyco is relatively dormant. There might not be a lot of future development or support.

__Psyco, PyPy, 和 Unladen Swallow.__让代码运行得更快，而尽可能不改变代码本身的方法之一，就是使用实时编译器（just-in-time (JIT) compiler），例如Psyco。在安装完Psyco后，你只需要importpsyco模块，然后调用`psyco.full()`，代码的运行速度就会有明显的提升。在你运行Python程序时，Psyco将一部分代码编译为汇编码。而因为它可以在运行时监控程序，它也就可以做出静态编译器无法做出的优化。例如，一个Python列表可以包含不同数据类型的元素，而当Psyco注意到某个列表其实只包含整型时，它就会假设，可能这个列表在之后的运行时间里也仅会包含整型，从而编译相关代码，将这个列表编译为整型列表。遗憾的是，包括Psyco在内的数个致力于加速Python运行得项目，似乎都停滞不前了，这些库大概不会有新的开发与支持了。

PyPy is a more ambitious project: a reimplementation of Python in Python. This does not, of course, give a speedup directly, but the idea behind the platform is to put a lot of infrastructure in place for analyzing, optimizing, and translating code. Based on this framework, it is then possible to do JIT compilation (techniques used in Psyco are being ported to PyPy), or even translation to some high- performance language such as C. The core subset of Python used in implementing PyPy is called RPython (for restricted Python), and there are already tools for statically compiling this language into efficient machine code.
Unladen Swallow is also a JIT compiler for Python, in a way. More precisely, it’s a version of the Python interpreter that uses the so-called Lowe Level Virtual Machine (LLVM). The goal of the project has been a speedup factor of 5 compared to the standard interpreter. This target has not yet been reached, though, and the activity of the project has been waning.

PyPy则是一个更庞大的项目：使用Python语言将Python本身重新实现。当然，这本身不会直接加快运行速度，这么做的目的，是为代码的分析，优化与翻译提供便捷。基于这个框架，实时编译变为了可能，人们不再需要使用类似于Psyco的外部库，而是在PyPy内部就完成了编译。甚至，在PyPy里，代码能够被翻译为更为高效的语言，例如C语言。实现PyPy的Python语言子集被称为RPython（即restricted Python，有限的Python）。而且已经有工具可以静态地将Python编译为高效的机器码。在某种程度上，Unladen Swallow也是Python的及时编译器。更精确地说，它是Python解释器的一个版本，被称为底层虚拟机（Low Level Virtual Machine，LLVM）。这个项目的目标，是将加速因子相对标准编译器提高5（猜测是提高5%的速度的意思）。然而Unladen Swallow项目还没有达到这个目标，并且它的开发活跃度在不断减小。

__GPULib and PyStream.__ These two packages let you use graphics processing units (GPUs) to accelerate your code. They don’t provide the kind of drop-in acceleration that a JIT compiler such as Psyco would, but if you have a powerful GPU, why not use it? Of the two projects, PyStream is older, and the efforts of Tech-X Corporation have shifted to the newer GPULib project. It gives you a high-level interface for various forms of numeric computation using GPUs.

__GPULib和PyStream__这两个包通过使用图像处理单元（graphics processing units，GPUs）来加快代码执行速度。它们并不会像Psyco这样的JIT编译器一样，通过代码优化来加速程序运行。但如果你的GPU很强大的话，为什么不使用GPU来计算呢？比起GPULib，PyStream更加古老一点，而Tech-X公司已经转向了更为年亲的GPULib项目的开发。它提供了基于GPU的各种形式的数学计算。

__Pyrex, Cython, and Shedskin.__ These three projects let you translate Python code into C or C++. Shedskin compiles plain Python code into C++, while Pyrex and Cython (which is a fork of Pyrex) primarily target C. In Cython (and Pyrex), you can add optional type declarations to your code, stating that a variable is (and will always be) an integer, for example. In Cython, there is also interoperability support for NumPy arrays, letting you write low-level code that accesses the array contents very efficiently. I have used this in my own code, achieving speedup factors of up to 300–400 for suitable code. The code that is generated by Pyrex and Cython can be compiled directly to an extension module that can be imported into Python.

__Pyrex，Cython，和Shedskin。__这三个项目致力于将Python代码翻译为C语言及C++。Shedskin将Python代码编译为C++，而Pyrex和Cython（后者是前者的一个分支）则主要致力于C语言。使用Cython和Pyrex时，可以选择性地在代码中做出声明，例如将某个变量声明为整型。Cython还有NumPy数组的额外支持，使你可以写底层的代码，以高效操作数组内容。我在自己的代码中使用了这个特性，并且对于某些代码，我获得了300-400的加速因子。由Pyrex和Cython生成的代码，可以直接编译为Python扩展，然后在代码中使用。

__SWIG, F2PY and Boost.Python.__ These tools let you wrap C/C++, Fortran, and C++ code, respectively. Although you could write your own wrapper code for accessing your extension modules, using a tool like one of these takes a lot of the tedium out of the job—and makes it more likely that the result will be correct. For example, when using SWIG, you run a command-line tool on your C (or C++) header files, and wrapper code is generated. A bonus to using SWIG is that it can generate wrappers for a lot of other languages, beside Python, so your extension could be available for Java or PHP as well, for example.

__SWIG, F2PY 和 Boost.Python.__这些工具可以帮助你将其他的语言包装为Python的模块，自左到右的包装语言是：C/C++，Fortran，C++。当然，你也可以自己进行包装，但如果使用这些工具可以帮助你省下那些单调乏味的工作，并且如果结果正确的话，为什么不使用它们呢？以SWIG而言，你只需要使用命令行工具，输入C语言或是C++的头文件，包装器代码就自动生成了。SWIG的另一个优点在于，除了Python它可以为很多语言生成包装器，所以，当你用C语言或者C++写完扩展后，你也可以很容易地在Java或者PHP里使用它们。

__ctypes, llvm-py, and CorePy.__ These are modules that let you manipulate low-level code objects in your Python code. The ctypes module lets you build C objects in memory and call C functions in shared libraries (such as DLLs) with those objects as parameters. The llvm-py package gives you a Python API to the LLVM, mentioned earlier, which lets you build code and then compile it efficiently. If you wanted, you could use this to build your own compiler (perhaps for a language of your own?) in Python. CorePy also lets you manipulate and efficiently run code objects, although it works at the assembly level. (Note that ctypes is part of the Python standard library.)

__ctypes, llvm-py,和CorePy.__你可以通过这些模块操纵Python的底层对象。你可以通过ctypes模块，在内存编译C语言写的对象，然后将这些对象作为参数，在共享库（例如DLL）中调用C的函数。llvm-py包，如之前所提到过的，提供了LLVM的Python接口，让你可以构建代码，然后更高效地编译它们。甚至如果你愿意的话，你可以在Python中用它来构建你自己的编译器，例如发明一种你自己的编程语言！CorePy也一样，可以帮助你处理与高效运行代码对象，所不同的是，它运行在汇编级。这三个库中，ctypes已被集成在Python标准库中了。


__Weave, Cinpy, and PyInline.__ These three packages let you use C (or some other languages) directly in your Python code. This is done quite cleanly, by keeping the C code in multiline Python strings, which are then compiled on the fly. The resulting code object is then available to your Python code, using facilities such as ctypes for the interfacing.

__Weave, Cinpy, 和 PyInline.__这三个包使你可以在Python代码中直接使用C语言（或者其他语言）。虽然不同的语言混排了，但代码仍然可以保持干净整洁，因为你可以使用Python的字符串的多行特性，将C语言按照它自己的代码风格来排版。之后，整个字符串会被送进编译器，然后输出代码对象，你就可以使用像ctypes这样的模块来使用它们了。

Table A-1. URLs for Acceleration Tool Web Sites

表A-1 一些加速工具的网站链接

##此处有个表