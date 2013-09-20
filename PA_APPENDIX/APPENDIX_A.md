# Pedal to the Metal: 
# Accelerating Python 
__ Make it work, make it right, make it fast. __
    __ ¡ªKent Beck __
	
This appendix is a tiny peek at some of the options for tweaking the constant factors of your 
implementations. Although this kind of optimization in many cases won¡¯t take the place of proper 
algorithm design¡ªespecially if your problems can grow large¡ªmaking your program run ten times as 
fast can indeed be very useful. 
Before calling for external help, you should make sure you¡¯re using Python¡¯s built-in tools to their 
full potential. I¡¯ve given you some pointers throughout the book, including the proper uses of list
versus deque, and how bisect and heapq can give you a great performance boost under the right 
circumstances. As a Python programmer, you¡¯re also lucky enough to have easy access to one of the 
most advanced and efficient (and efficiently implemented) sorting algorithms out there (list.sort), as 
well as a really versatile and fast hash table (dict). You might even find that itertools and functools
(especially the function cache decorators) can give your code a performance boost. 
Also, when choosing your technology, make sure you optimize only what you must. Optimizations 
do tend to make either your code or your tool setup more complicated, so make sure it¡¯s worth it. If your 
algorithm scales ¡°well enough¡± and your code is ¡°fast enough,¡± introducing the extension modules in 
another language such as C might very well not be worth it. What is enough is, of course, up to you to 
determine. (For some hints on timing and profiling your code, see Chapter 2.) 
Note that the packages and extensions discussed in this appendix are mainly about optimizing 
single-processor code, either by providing efficiently implemented functionality, by letting you create or 
wrap extension modules, or by simply speeding up your Python interpreter. Distributing your 
processing to multiple cores and processors can certainly also be a big help. The multiprocessing
module can be a place to start. If you want to explore this approach, you should be able to find a lot of 
third-party tools for distributed computing as well. 
In the following pages, I describe a selection of acceleration tools. There are several efforts in this 
area, and the landscape is of course a changing one: new projects appear from time to time, and some 
old ones fade and die. If you think one of these solutions sounds interesting, you should check out its 
web site, and consider the size and activity of its community¡ªas well, of course, as your own needs. For 
web site URLs, see Table A-1 later in the appendix. 
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
Unladen Swallow is also a JIT compiler for Python, in a way. More precisely, it¡¯s a version of the 
Python interpreter that uses the so-called Lowe Level Virtual Machine (LLVM). The goal of the project 
has been a speedup factor of 5 compared to the standard interpreter. This target has not yet been 
reached, though, and the activity of the project has been waning. 
GPULib and PyStream. These two packages let you use graphics processing units (GPUs) to accelerate 
your code. They don¡¯t provide the kind of drop-in acceleration that a JIT compiler such as Psyco would, 
but if you have a powerful GPU, why not use it? Of the two projects, PyStream is older, and the efforts of 
Tech-X Corporation have shifted to the newer GPULib project. It gives you a high-level interface for 
various forms of numeric computation using GPUs. 
Pyrex, Cython, and Shedskin. These three projects let you translate Python code into C or C++. Shedskin 
compiles plain Python code into C++, while Pyrex and Cython (which is a fork of Pyrex) primarily target 
C. In Cython (and Pyrex), you can add optional type declarations to your code, stating that a variable is 
(and will always be) an integer, for example. In Cython, there is also interoperability support for NumPy 
arrays, letting you write low-level code that accesses the array contents very efficiently. I have used this 
in my own code, achieving speedup factors of up to 300¨C400 for suitable code. The code that is generated 
by Pyrex and Cython can be compiled directly to an extension module that can be imported into Python. 
SWIG, F2PY and Boost.Python. These tools let you wrap C/C++, Fortran, and C++ code, respectively. 
Although you could write your own wrapper code for accessing your extension modules, using a tool like 
one of these takes a lot of the tedium out of the job¡ªand makes it more likely that the result will be 
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