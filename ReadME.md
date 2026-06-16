\section{Python Fundamentals}

\subsection{Introduction to Python}

\subsubsection{History and Origins}

Python is a high-level, interpreted programming language whose development began in the late 1980s. The language emerged as a successor to the ABC programming language, which had been designed at Centrum Wiskunde \& Informatica (CWI) in the Netherlands. The first official version, Python 0.9.0, was released in February 1991, introducing core constructs such as exception handling, functions, and the module system. Python 2.0, released in October 2000, introduced list comprehensions and a garbage collection mechanism based on cycle detection. The release of Python 3.0 in December 2008 marked a significant transition, deliberately breaking backward compatibility in order to eliminate redundant constructs and establish a cleaner, more consistent language specification. The Python 3 series has since become the standard, with Python 2 reaching end-of-life status in January 2020.

\subsubsection{Guido van Rossum}

Python was conceived and implemented by Guido van Rossum, a Dutch programmer who began work on the language while employed at CWI. Van Rossum served as the language's Benevolent Dictator for Life (BDFL), a title designating his role as the principal authority on language design decisions. This governance model ensured that Python's development retained a coherent design philosophy throughout its early decades. Van Rossum stepped down from the BDFL role in 2018, after which governance transitioned to the Python Steering Council, a five-member elected body responsible for overseeing the language's evolution through a formalized Python Enhancement Proposal (PEP) process. The PEP mechanism remains the primary channel through which language changes, library additions, and process updates are proposed, debated, and ratified by the community.

\subsubsection{Open Source Nature}

Python is developed and maintained under an open-source license approved by the Open Source Initiative. The Python Software Foundation (PSF), a non-profit organization established in 2001, holds the intellectual property rights for the language and its reference implementation. The PSF License permits free use, distribution, and modification of the Python source code, which is hosted publicly and accepts contributions from developers worldwide. This open governance model has been instrumental in fostering a large and active contributor ecosystem. The Python Package Index (PyPI), the official repository for third-party Python packages, hosts over 400,000 projects as of recent estimates, reflecting the breadth of community-driven development built upon the language.

\subsubsection{Dynamic Typing}

Python employs a dynamic type system, wherein the type of a variable is determined at runtime rather than at compile time. This characteristic distinguishes Python from statically typed languages such as C, C++, and Java, in which variable types must be declared explicitly and are enforced during compilation. In Python, a variable functions as a reference to an object, and its associated type is a property of the object itself rather than the variable. Consequently, the same variable may reference objects of different types at different points during execution. While this increases the flexibility and expressiveness of the language, it also introduces the possibility of type-related errors that manifest only at runtime. To address this, Python 3.5 introduced optional type hints via PEP 484, and tools such as \texttt{mypy} enable static type checking as a complementary mechanism without modifying the language's runtime behaviour.

\subsubsection{Cross-Platform Support}

Python's design affords substantial portability across operating systems. The CPython interpreter, the reference implementation of the language, is available on major platforms including GNU/Linux, macOS, and Windows, and is distributed for architectures such as x86-64, ARM, and RISC-V. Python source code written on one platform generally executes without modification on another, provided that any platform-specific system calls or dependencies are abstracted appropriately. This portability is particularly relevant in research and development contexts, where workflows span desktop environments, remote Linux servers, cloud computing instances, and embedded systems. The availability of containerisation tools such as Docker further facilitates consistent execution environments, and Python's compatibility with these tools reinforces its suitability as a primary language for portable scientific and engineering software.

\subsubsection{Importance in Artificial Intelligence}

Python has established itself as the dominant programming language in the field of artificial intelligence and machine learning. Several factors contribute to this status. The language's concise syntax reduces the cognitive overhead associated with expressing complex algorithmic ideas, enabling researchers to prototype rapidly. Its interactive nature, facilitated by environments such as Jupyter Notebook, supports an iterative experimental workflow well-suited to data analysis and model development. More critically, the Python ecosystem encompasses a comprehensive suite of numerical and machine learning libraries — including NumPy, SciPy, Pandas, scikit-learn, TensorFlow, PyTorch, and Hugging Face Transformers — that collectively provide the infrastructure required for modern AI research and deployment. The widespread adoption of these libraries has created a positive feedback cycle in which new AI research is predominantly implemented in Python, further consolidating the language's position in the field.

\subsection{Python Architecture}

\subsubsection{CPython}

CPython is the reference implementation of the Python programming language and the one most widely deployed in practice. It is written in C and is the interpreter distributed through the official Python website. When a Python source file is executed via CPython, the source code undergoes lexical analysis, parsing into an abstract syntax tree (AST), and subsequent compilation into an intermediate bytecode representation. This bytecode is then executed by the CPython virtual machine. CPython incorporates a mechanism known as the Global Interpreter Lock (GIL), a mutex that prevents multiple native threads from executing Python bytecode simultaneously within a single process. The GIL simplifies memory management by ensuring that reference count operations on Python objects are thread-safe, but it also limits the degree to which CPU-bound tasks can exploit multi-core parallelism within a single Python process. Parallelism in CPU-intensive workloads is typically achieved in CPython through multiprocessing rather than multithreading.

\subsubsection{Bytecode}

Python source code is not interpreted directly from text. Instead, CPython compiles source files into platform-independent bytecode, a lower-level representation of the program that is closer to machine instructions but remains independent of any specific hardware architecture. Bytecode is stored in \texttt{.pyc} files within the \texttt{\_\_pycache\_\_} directory and is reused on subsequent executions if the source file has not been modified, thereby reducing startup latency. Each bytecode instruction corresponds to an operation within the CPython virtual machine's instruction set, such as loading a variable, performing a binary operation, or invoking a function. The \texttt{dis} module in the Python standard library provides facilities for disassembling bytecode, which is useful for understanding the low-level behaviour of Python programs and for performance analysis.

\subsubsection{Python Virtual Machine}

The Python Virtual Machine (PVM) is the runtime engine responsible for executing compiled bytecode. It operates as a stack-based interpreter, maintaining an evaluation stack on which operands are pushed and from which results are popped during the execution of each bytecode instruction. The PVM manages the program's call stack, with each function invocation creating a new frame object that encapsulates the local namespace, the execution context, and a reference to the bytecode being executed. The PVM also interfaces with Python's memory management subsystem, which employs reference counting as its primary mechanism for reclaiming memory, supplemented by a cycle-detecting garbage collector to handle circular references. Understanding the PVM's operation is useful in contexts where performance profiling or low-level optimisation of Python code is required.

\subsubsection{Jython}

Jython is an implementation of the Python programming language that runs on the Java Virtual Machine (JVM). Unlike CPython, which compiles Python source to CPython bytecode, Jython compiles Python source code to Java bytecode, enabling direct interoperability with Java libraries and frameworks. This makes Jython particularly suitable for environments in which integration with existing Java codebases is a requirement. However, Jython has not maintained parity with recent CPython versions and does not support many of the performance-sensitive native extension modules written in C, such as NumPy. As a result, its utility in modern machine learning contexts is limited.

\subsubsection{IronPython}

IronPython is an implementation of Python targeting the .NET Common Language Runtime (CLR). It enables Python code to interoperate with .NET libraries and is primarily used in enterprise environments where .NET-based infrastructure is prevalent. IronPython compiles Python source code to .NET intermediate language (IL) bytecode, which is then executed by the CLR's just-in-time compiler. Similar to Jython, IronPython lacks support for many CPython C extensions, restricting its adoption in data science and AI workflows that depend on such libraries.

\subsubsection{PyPy}

PyPy is an alternative Python implementation focused on performance. It features a just-in-time (JIT) compiler that analyses the execution patterns of running Python code and compiles frequently executed code paths to native machine code at runtime. This approach can yield execution speeds significantly faster than CPython for computationally intensive workloads, with benchmarks often reporting improvements of an order of magnitude or more for pure-Python numerical code. PyPy maintains compatibility with a substantial subset of the Python standard library and supports the C extension API through an emulation layer, though compatibility is not universal. In the context of AI and scientific computing, PyPy's utility is partially offset by the fact that performance-critical operations are typically delegated to native C or CUDA extensions such as NumPy and PyTorch, which already bypass the Python interpreter's overhead.

\subsection{Core Programming Concepts}

\subsubsection{Variables and Assignment}

In Python, a variable is a symbolic name that serves as a reference to an object stored in memory. Assignment in Python does not copy data; rather, it binds a name to an existing object. This distinction has practical implications: when two variables are assigned to the same mutable object, modifications made through one variable are reflected when the object is accessed through the other. Python's scoping rules follow the LEGB model — Local, Enclosing, Global, and Built-in — which defines the order in which the interpreter searches for a name when it is referenced. Variables need not be declared before use; they come into existence upon assignment and are eligible for garbage collection once no remaining references point to the associated object.

\subsubsection{Data Types}

Python provides a set of built-in data types that cover the majority of common programming requirements. Numeric types include \texttt{int}, which supports arbitrary-precision integers without overflow, \texttt{float}, which conforms to IEEE 754 double-precision representation, and \texttt{complex} for complex-number arithmetic. The \texttt{bool} type is a subclass of \texttt{int} with two instances, \texttt{True} and \texttt{False}. The \texttt{str} type represents sequences of Unicode code points and is immutable. The \texttt{bytes} and \texttt{bytearray} types represent sequences of raw bytes, the former being immutable and the latter mutable. The \texttt{NoneType}, with its sole instance \texttt{None}, serves as the idiomatic representation of the absence of a value.

\subsubsection{Functions}

Functions in Python are first-class objects, meaning they can be assigned to variables, passed as arguments to other functions, returned as values from functions, and stored in data structures. A function is defined using the \texttt{def} keyword, followed by a name, a parameter list, and a body. Python supports default parameter values, keyword arguments, variable-length positional argument lists via \texttt{*args}, and variable-length keyword argument dictionaries via \texttt{**kwargs}, providing considerable flexibility in function interfaces. Anonymous functions are expressed using the \texttt{lambda} construct, though they are restricted to a single expression. The concepts of closures and higher-order functions — central to functional programming paradigms — are natively supported and are frequently encountered in AI frameworks, where functions such as activation functions, loss functions, and custom optimisation steps are routinely passed as arguments.

\begin{lstlisting}[language=Python, caption={Illustrating first-class function behaviour and closures.}]
def make_scaler(factor):
    def scale(x):
        return x * factor
    return scale

double = make_scaler(2)
triple = make_scaler(3)
print(double(5))   # Output: 10
print(triple(5))   # Output: 15
\end{lstlisting}

\subsubsection{Classes and Objects}

Python is a multi-paradigm language with comprehensive support for object-oriented programming. Classes are defined using the \texttt{class} keyword and serve as blueprints for creating objects. Each class may define an \texttt{\_\_init\_\_} method, which serves as a constructor and is invoked automatically when a new instance is created. Instance attributes are typically initialised within \texttt{\_\_init\_\_} using the \texttt{self} parameter, which holds a reference to the instance being constructed. Python supports single and multiple inheritance, allowing a class to derive attributes and methods from one or more parent classes. Method resolution in the presence of multiple inheritance follows the C3 linearisation algorithm, which determines a consistent method resolution order (MRO). Python's data model exposes a set of special methods — commonly referred to as dunder methods — that allow classes to define behaviour for built-in operations such as arithmetic, comparison, iteration, and string representation. This mechanism is extensively used in frameworks such as PyTorch, where the \texttt{nn.Module} base class relies on dunder methods to support operator overloading and automatic differentiation.

\subsubsection{Modules and Packages}

A module in Python is any file containing Python definitions and statements, identifiable by the \texttt{.py} extension. Modules enable the logical organisation of code into reusable units and are imported into other modules using the \texttt{import} statement. The interpreter searches for modules according to the paths listed in \texttt{sys.path}, which includes the script's directory, directories specified by the \texttt{PYTHONPATH} environment variable, and installation-dependent default paths. A package is a directory that contains an \texttt{\_\_init\_\_} file, signifying to the interpreter that the directory should be treated as a package namespace. This hierarchical organisation scales to large codebases and is the structural basis for the Python ecosystem's major libraries. The standard library, distributed with CPython, provides modules for file I/O, networking, regular expressions, data serialisation, concurrency, and a wide range of other system-level functions without requiring any external installation.

\subsection{Python Data Structures}

\subsubsection{Lists}

The list is Python's primary ordered, mutable sequence type. A list can hold elements of heterogeneous types, including nested lists, and supports standard sequence operations such as indexing, slicing, concatenation, and membership testing. Elements may be appended, inserted, removed, and reordered in place. Internally, CPython implements lists as dynamic arrays of pointers to Python objects, enabling $O(1)$ indexed access but requiring $O(n)$ time for insertions or deletions at arbitrary positions. List comprehensions provide a concise and idiomatic syntax for constructing lists by applying an expression to each element of an iterable, optionally filtered by a predicate. In the context of machine learning, lists are frequently used to accumulate training metrics, construct batches of data samples, and manage configuration parameters prior to conversion into more performance-oriented array types.

\subsubsection{Tuples}

Tuples are ordered, immutable sequences that share much of the syntactic interface of lists but cannot be modified after creation. Their immutability makes them suitable for representing fixed collections of related values, and Python uses tuples extensively in its own internal mechanisms — for example, as the return type of functions that return multiple values and as keys in dictionaries when a compound key is required. The immutability of tuples confers a minor performance advantage over lists in scenarios involving iteration, as the interpreter can make assumptions about the constancy of tuple contents. Named tuples, available through the \texttt{collections} module and the \texttt{typing.NamedTuple} interface, extend plain tuples with field names, improving code readability while retaining the efficiency characteristics of the base type.

\subsubsection{Sets}

A set is an unordered collection of unique, hashable elements. Python provides two set types: \texttt{set}, which is mutable, and \texttt{frozenset}, which is immutable and therefore hashable, allowing it to be used as a dictionary key or as an element of another set. Sets are implemented using hash tables, yielding average-case $O(1)$ complexity for membership testing, insertion, and deletion operations. The set type supports standard mathematical set operations, including union, intersection, difference, and symmetric difference, both as methods and as operators. In data preprocessing workflows, sets are commonly used for deduplication, vocabulary construction in natural language processing tasks, and the computation of class memberships.

\subsubsection{Dictionaries}

The dictionary is Python's built-in associative array, mapping arbitrary hashable keys to values. As of Python 3.7, dictionaries preserve insertion order as part of the language specification, a guarantee that had previously been an implementation detail of CPython 3.6. Dictionaries are implemented as hash tables with open addressing, providing average-case $O(1)$ performance for key lookup, insertion, and deletion. The \texttt{dict} type supports a range of construction methods, including literal syntax, the \texttt{dict()} constructor, the \texttt{dict.fromkeys()} class method, and dictionary comprehensions. In AI and machine learning contexts, dictionaries serve a wide range of purposes: model hyperparameters are commonly represented as dictionaries, configuration files parsed from JSON or YAML are loaded as nested dictionaries, and tokenisation vocabularies mapping tokens to integer indices are stored as dictionary objects. The \texttt{collections} module extends the base dictionary with specialised variants such as \texttt{defaultdict}, which provides automatic default values for missing keys, and \texttt{Counter}, which supports multiset operations and frequency counting.

\begin{lstlisting}[language=Python, caption={Demonstrating core data structure operations in Python.}]
# List: mutable ordered sequence
tokens = ["the", "model", "trains", "fast"]
tokens.append("efficiently")

# Set: unique elements, O(1) lookup
vocab = set(tokens)

# Dictionary: key-value mapping
token_index = {token: idx for idx, token in enumerate(vocab)}

# Tuple: immutable record
config = ("bert-base", 768, 12)
model_name, hidden_dim, num_layers = config
\end{lstlisting}
