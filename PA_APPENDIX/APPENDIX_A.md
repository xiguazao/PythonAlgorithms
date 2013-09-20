# Pedal to the Metal: 
# Accelerating Python 
__ Make it work, make it right, make it fast. __
    __ —Kent Beck __

# 将油门踩到底:
# 加速掌握Python

__ 使它能够工作，使它正确地工作，使它快速地工作。__
	
This appendix is a tiny peek at some of the options for tweaking the constant factors of your 
implementations. Although this kind of optimization in many cases won’t take the place of proper 
algorithm design—especially if your problems can grow large—making your program run ten times as 
fast can indeed be very useful. 

这篇附录提供了一些工具，借此来优化你的代码，使你的代码更简洁，或者更快速。然而这类优化在大多数情况下
并不能代替算法设计，然后让你的程序速度快上十倍——特别是你所处理的问题规模非常大的情况下。

Before calling for external help, you should make sure you’re using Python’s built-in tools to their 
full potential. I’ve given you some pointers throughout the book, including the proper uses of list
versus deque, and how bisect and heapq can give you a great performance boost under the right 
circumstances. As a Python programmer, you’re also lucky enough to have easy access to one of the 
most advanced and efficient (and efficiently implemented) sorting algorithms out there (list.sort), as 
well as a really versatile and fast hash table (dict). You might even find that itertools and functools
(especially the function cache decorators) can give your code a performance boost.

在我们寻求外部帮助之前，我们首先应该审视，我们是否已将Python的内建工具物尽其用了。在本书中，我给了
你很多相关的例子，例如双链表的使用，以及二分法与堆如何在合适的情况下提供巨大的性能提升。作为一个Python
程序员，幸运的是，Python提供了list和dict这两个非常好用的数据结构。list使得你你在很多情况下并不需要关心排序，
因为Python提供了最先进，最有效的排序算法之一的实现（list.sort），而dict则是一个功能多样而又迅速的哈希表的
实现。甚至你会发现，遍历工具与函数工具（特别是函数缓存装饰器）同样会让你的代码变得更高效。

Also, when choosing your technology, make sure you optimize only what you must. Optimizations 
do tend to make either your code or your tool setup more complicated, so make sure it’s worth it. If your 
algorithm scales “well enough” and your code is “fast enough,” introducing the extension modules in 
another language such as C might very well not be worth it. What is enough is, of course, up to you to 
determine. (For some hints on timing and profiling your code, see Chapter 2.) 

其次，当我们选择外部库来优化我们的代码的时候，应该确保是否必须优化。优化本身经常会让我们的代码变得更复杂，
依赖变得更多，所以优化之前要想一想，优化真的值得吗？如果你的算法已经足够好，你的代码已经足够快，那么通常
就不值得引入用其他语言（例如C语言）撰写的外部模块了。当然，什么是“足够好”和“足够快”，是由你自己来判断的。
（你可以在第二章找到一些代码测速与剖析的例子）。

Note that the packages and extensions discussed in this appendix are mainly about optimizing 
single-processor code, either by providing efficiently implemented functionality, by letting you create or 
wrap extension modules, or by simply speeding up your Python interpreter. Distributing your 
processing to multiple cores and processors can certainly also be a big help. The multiprocessing
module can be a place to start. If you want to explore this approach, you should be able to find a lot of 
third-party tools for distributed computing as well.

请注意，这篇附录中所讨论的包和外部扩展主要用于优化单处理器的代码。这些外部工具会提供高效实现的函数，或者
实现或包装扩展模块，或者提高Python解释器的效率。将代码改为多处理器版本当然会大大提高运行效率，如果你真的
打算这么做的话，multiprocessing模块是一个好的开始。如果你希望深入了解多核编程，你一定会找到非常多的关于
分布式计算的第三方工具。
 
In the following pages, I describe a selection of acceleration tools. There are several efforts in this 
area, and the landscape is of course a changing one: new projects appear from time to time, and some 
old ones fade and die. If you think one of these solutions sounds interesting, you should check out its 
web site, and consider the size and activity of its community—as well, of course, as your own needs. For 
web site URLs, see Table A-1 later in the appendix.

在接下来的几页中，我会介绍几种外部工具。有很多人为各种各样的应用情境编写了扩展，而这些扩展都在不断变化
这：新的项目如雨后春笋般不断涌现，而一些旧的项目则逐渐消失。看完我接下来介绍的几种扩展，如果你觉得其中
几个很有趣，并且打算用到你自己的项目里的话，你可以先浏览一下这些扩展的网站以及社区，本篇最后附有这些
网站的地址。
 
NumPy, SciPy, and Sage. NumPy is a package with a long lineage. It is based on older projects such as 
Numeric and numarray, and at its core implements a multidimensional array of numbers. In addition to 
this data structure, NumPy has several efficiently implemented functions and operators that work on the 
entire array so that when you use them from Python, the number of function calls is minimized, letting 
you write highly efficient numeric computations without compiling any custom extensions. SciPy and 
Sage are much more ambitious projects (although with NumPy as one of their building blocks), 
collecting several tools for scientific, mathematical, and high-performance computing (including some 
of the ones mentioned later in this appendix). 
Psyco, PyPy, and Unladen Swallow. One of the least intrusive approaches to speeding up your code is to 
use a just-in-time (JIT) compiler, such as Psyco. After installing it, you simply need to import the psyco
module and call psyco.full() to get a potentially quite noticeable speedup. Psyco compiles parts of your 
Python program into machine code while your program is running. Because it can watch what happens 
to your program at runtime, it can make optimizations that a static compiler could not. For example, a 
Python list can contain arbitrary values. If, however, Psyco notices that a given list of yours only ever 
seems to contain integers, it can assume that this will be the case also in the future and compile that part 
of the code as if your list were an array of integers. Sadly, like several of the Python acceleration 
solutions, Psyco is relatively dormant. There might not be a lot of future development or support. 
PyPy is a more ambitious project: a reimplementation of Python in Python. This does not, of course, 
give a speedup directly, but the idea behind the platform is to put a lot of infrastructure in place for 
analyzing, optimizing, and translating code. Based on this framework, it is then possible to do JIT 
compilation (techniques used in Psyco are being ported to PyPy), or even translation to some highperformance language such as C. The core subset of Python used in implementing PyPy is called 
RPython (for restricted Python), and there are already tools for statically compiling this language into 
efficient machine code. 
Unladen Swallow is also a JIT compiler for Python, in a way. More precisely, it’s a version of the 
Python interpreter that uses the so-called Lowe Level Virtual Machine (LLVM). The goal of the project 
has been a speedup factor of 5 compared to the standard interpreter. This target has not yet been 
reached, though, and the activity of the project has been waning. 
GPULib and PyStream. These two packages let you use graphics processing units (GPUs) to accelerate 
your code. They don’t provide the kind of drop-in acceleration that a JIT compiler such as Psyco would, 
but if you have a powerful GPU, why not use it? Of the two projects, PyStream is older, and the efforts of 
Tech-X Corporation have shifted to the newer GPULib project. It gives you a high-level interface for 
various forms of numeric computation using GPUs. 
Pyrex, Cython, and Shedskin. These three projects let you translate Python code into C or C++. Shedskin 
compiles plain Python code into C++, while Pyrex and Cython (which is a fork of Pyrex) primarily target 
C. In Cython (and Pyrex), you can add optional type declarations to your code, stating that a variable is 
(and will always be) an integer, for example. In Cython, there is also interoperability support for NumPy 
arrays, letting you write low-level code that accesses the array contents very efficiently. I have used this 
in my own code, achieving speedup factors of up to 300–400 for suitable code. The code that is generated 
by Pyrex and Cython can be compiled directly to an extension module that can be imported into Python. 
SWIG, F2PY and Boost.Python. These tools let you wrap C/C++, Fortran, and C++ code, respectively. 
Although you could write your own wrapper code for accessing your extension modules, using a tool like 
one of these takes a lot of the tedium out of the job—and makes it more likely that the result will be 
correct. For example, when using SWIG, you run a command-line tool on your C (or C++) header files, 
and wrapper code is generated. A bonus to using SWIG is that it can generate wrappers for a lot of other 
languages, beside Python, so your extension could be available for Java or PHP as well, for example. 
ctypes, llvm-py, and CorePy. These are modules that let you manipulate low-level code objects in your 
Python code. The ctypes module lets you build C objects in memory and call C functions in shared 
libraries (such as DLLs) with those objects as parameters. The llvm-py package gives you a Python API to 
the LLVM, mentioned earlier, which lets you build code and then compile it efficiently. If you wanted, 
you could use this to build your own compiler (perhaps for a language of your own?) in Python. CorePy
also lets you manipulate and efficiently run code objects, although it works at the assembly level. (Note 
that ctypes is part of the Python standard library.) 
Weave, Cinpy, and PyInline. These three packages let you use C (or some other languages) directly in 
your Python code. This is done quite cleanly, by keeping the C code in multiline Python strings, which 
are then compiled on the fly. The resulting code object is then available to your Python code, using 
facilities such as ctypes for the interfacing.

Table A-1. URLs for Acceleration Tool Web Sites 
Tool Web Site 
Boost.Python http://boost.org 
Cinpy www.cs.tut.fi/~ask/cinpy 
CorePy http://corepy.org 
ctypes http://docs.python.org/library/ctypes.html 
Cython http://cython.org 
F2PY http://cens.ioc.ee/projects/f2py2e 
GPULib http://txcorp.com/products/GPULib 
llvm-py http://mdevan.org/llvm-py 
NumPy http://numpy.scipy.org 
Psyco http://psycho.sf.net 
PyInline http://pyinline.sf.net 
PyPy http://codespeak.net/pypy 
Pyrex www.cosc.canterbury.ac.nz/greg.ewing/python/Pyrex 
PyStream http://code.google.com/p/pystream 
Sage http://sagemath.org 
SciPy http://scipy.org 
Shedskin http://code.google.com/p/shedskin 
SWIG http://swig.org 
Unladen Swallow http://code.google.com/p/unladen-swallow 
Weave http://scipy.org/Weave 