# all-about-compiler
Compilers, phases, details, examples

**[Top C++ compilers for hosted environments]**

**1. Microsoft Visual C++ compiler**

This is the C and C++ compiler that Microsoft bundles with [Visual Studio](https://www.incredibuild.com/integrations/visual-studio). The current compiler version, bundled with Visual Studio 2019 version 16.10, is 19.28.29914, which supports both the C++17 core language features as well as C++17 library features completely and the C++20 features [partially](https://docs.microsoft.com/en-us/cpp/overview/visual-cpp-language-conformance?view=msvc-160). It is expected that Visual Studio 2022 – which is currently in the preview version – will include a Visual C++ compiler that will fully support the C++20 features. Although the Visual C++ compiler is primarily used for Windows development, using the windows subsystem for Linux (WSL) integration, it can be used [to develop native Linux applications too](https://devblogs.microsoft.com/cppblog/c-with-visual-studio-2019-and-windows-subsystem-for-linux-wsl). Checkout this nice [video](https://www.youtube.com/watch?v=ijmZKRIfoOI) to learn more on this topic.

**2. The GNU compiler collection**

The GNU compiler collection, GCC, is one of the most famous open-source tools in existence. It is a tool that can be used to compile multiple languages and not just C or C++. The current version of GCC, GCC 11, has full support for C++17 core language features as well as C++17 library features. It also has experimental support for almost all of the C++20 language and library features, except for some minor features in Modules. Notably, GCC 11 also includes some features of the draft C++23 standard which is the next revision of the C++ standard after C++20.*[Learn more about what is GCC](https://www.incredibuild.com/integrations/gcc)

**3. Clang/LLVM**

In one of my recent blog posts, I had compared [GCC vs Clang](https://www.incredibuild.com/blog/gcc-vs-clang-battle-of-the-behemoths). I had detailed the architecture of this compiler and described how the LLVM backend makes it easy to add new optimizations to the compiler. The current version of Clang/LLVM, version 12.0, currently supports C++17 fully and has experimental support for C++20.  As you proceed through this blog post you will understand why a lot of other C++ compilers want to base their code on this open-source platform.

**4. Intel C++ compiler**

I have used the Intel C++ compiler (Intel® one API DPC++/C++ Compiler to be precise) for computationally intensive applications and I have found its performance to be top-notch. Unlike Visual Studio which includes frameworks like MFC (Microsoft foundation classes) for desktop application development and WebView2 support for Web-based applications, Intel’s compiler includes support for Threading Building Blocks (currently open-sourced as one API) and Data Parallel C++ (DPC++) clearly showing the difference in focus. Computationally intensive applications with data parallelism (with parallel STL), Field-programmable gate array (FPGA) support as well as support for Graphics Processing Unit (GPU) is where Intel Compiler shines. The latest version of the Intel C++ compiler supports the C++17 standard.

**5. IBM XLC++**

IBM XLC++ compiler is offered for platforms like z/OS, Linux on Power, AIX, and IBM I (with PASE). This compiler offers advanced optimization technologies thereby generating optimized code for developing complex C++ programs. Recently IBM has contributed code to Clang/LLVM project for Power, AIX, and IBM Z platforms. Last year (2020), IBM announced its [intention to adopt](https://community.ibm.com/community/user/ibmz-and-linuxone/blogs/blog-entry1/2020/02/23/ibm-cc-and-fortran-compilers-to-adopt-llvm-open-source-infrastructure) Clang/LLVM framework for its IBM XLC++ compiler toolchain. This should enable the IBM XLC++ compiler to support the latest C++ standards easily.

**6. MinGW**

It is an open-source program that doesn't need any other components and integrates nicely with Microsoft Windows development. It includes GCC compilers for the programming languages C, C++, and Fortran. The customer prefers this compiler over many others because of the high degree of portability provided by ANSI Compliance in GCC. Using Windows 32 or min32, a customized project may be incorporated, along with other packages, and is licensed for use in a certain version. We have full access to the source code thanks to G++. Its quickness and ease of use, which call for DLL libraries, are major advantages.

Phases in translation

**Lexical Analysis (Scanning)**
In a compiler linear analysis is called lexical analysis or scanning. The lexical analysis
phase reads the characters in the source program and grouped into tokens that are
the sequence of characters having a collective meaning.
EXAMPLE
position : = initial + rate * 60
This can be grouped into the following tokens;

1. The identifier position.
2. The assignment symbol : =
3. The identifier initial
4. The plus sign
5. The identifier rate
6. The multiplication sign

Blanks separating characters of these tokens are normally eliminated during lexical
analysis.

**Syntax Analysis (Parsing)**
Hierarchical Analysis is called parsing or syntax analysis.
It involves grouping the tokens of the source program into grammatical phrases that
are used by the complier to synthesize output. They are represented using a syntax
tree.
A syntax tree is a tree generated as a result of syntax analysis in which the interior
nodes are the operators and the exterior nodes are the operands. This analysis shows
an error when the syntax is incorrect.

**Semantic Analysis**
This phase checks the source program for semantic errors and gathers type
information for subsequent code generation phase.
An important component of semantic analysis is type checking.
Here the compiler checks that each operator has operands that are permitted by the
source language specification.

**[PHASES OF A COMPILER]**
The phases include:

- Lexical Analysis
- Syntax Analysis
- Semantic Analysis
- Intermediate Code Generation
- Code Optimization
- Target Code Generation

**[Lexical Analysis]**

Lexical analysis - converts the source program from a character string to a sequence of semantically-relevant symbols. The symbols and their encoding form the intermediate language output from the lexical analyzer.

- Decomposition of the Grammar - Delimiters (keywords, meaningful special characters, and combinations of special characters), identifiers and constants together are termed basic symbols;
- Lexical Analyzer Interface - is organized as a module with several local state variables and implements
the following elementary operations:
    - initialize_lex ical_analysis - ;
    - next_token - is used by the parser to obtain the next token in the token sequence;
    - wrapup_lexical_analysis - ;

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a56cbdb8-671d-4b40-828d-7df159d2a4b8/Untitled.png)

The lexical analyzer reads the stream of characters making up the source program and
groups the characters into meaningful sequences called *lexemes*.
For each lexeme, the lexical analyzer produces as output a token of the form
*< token- name, attribute-value >*

- the first component token - the name is an abstract symbol that is used during
syntax analysis
- second component attribute - value points to an entry in the
the symbol table for this token.

Information from the symbol-table entry 'is needed for semantic analysis and code
generation.

The characters in this assignment could be grouped into the following lexemes and
mapped into the following tokens passed on to the syntax analyzer:

1. the position is a lexeme that would be mapped into a token <id, 1>, where id is an
abstract symbol standing for identifier and 1 point to the symbol table entry for
position. The symbol-table entry for an identifier holds information about the
identifiers, such as its name and type.
2. The assignment symbol = is a lexeme that is mapped into the token < = >. Since
this token needs no attribute value, we have omitted the second component.
3. initial is a lexeme that is mapped into the token < id, 2> , where 2 points to the
symbol-table entry for initial.
4. is a lexeme that is mapped into the token <+>.
5. rate is a lexeme that is mapped into the token < id, 3 >, where 3 points to the
symbol-table entry for rate.
6. is a lexeme that is mapped into the token <* > .
7. 60 is a lexeme that is mapped into the token <60>

Blanks separating the lexemes would be discarded by the lexical analyzer. The
representation of the assignment statement position = initial + rate * 60 after
lexical analysis as the sequence of tokens as:
< id, l > < = > <id, 2> <+> <id, 3> < * > <60>
`Token` - A token is a sequence of characters that can be treated as a single logical entity.

- Identify;
- keywords;
- operators;
- special symbols;
- constants;

`Pattern` - A set of strings in the input for which the same token is produced as output. This
set of strings is described by a rule called a pattern associated with the token.
`Lexeme` - A lexeme is a sequence of characters in the source program that is matched by the
pattern for a token.

**Reasons why lexical analysis is separated from syntax analysis**

- **Simplicity of design** - The separation of lexical analysis and syntactic analysis often allows us to simplify at least one of these tasks. The syntax analyzer can be smaller and cleaner by removing the low-level details of lexical analysis.
- **Efficiency** - Compiler efficiency is improved. A separate lexical analyzer allows us to apply specialized techniques that serve only the lexical task, not the job of parsing. In addition, specialized
buffering techniques for reading input characters can speed up the compiler significantly.
- **Portability** - Compiler portability is enhanced. Input-device-specific peculiarities can be restricted to the lexical analyzer.

**[Syntax Analysis]**
The second phase of the compiler is syntax analysis or parsing.
The parser uses the first components of the tokens produced by the lexical analyzer to
create a tree-like intermediate representation that depicts the grammatical structure of
the token stream.
A typical representation is a syntax tree in which each interior node represents an
operation and the children of the node represent the arguments of the operation.
The syntax tree for above token stream is:
The tree has an interior node labeled with ( id, 3 ) as its left child and the integer 60 as
its right child.
The node (id, 3) represents the identifier rate.
The node labeled * makes it explicit that we must first multiply the value of rate by 60.
The node labeled + indicates that we must add the result of this multiplication to the
value of initial.
The root of the tree, labeled =, indicates that we must store the result of this addition
into the location for the identifier position.

Reasons why lexical analysis is separated from syntax analysis
• Simplicity of design
The separation of lexical analysis and syntactic analysis often allows us to simplify at least
one of these tasks. The syntax analyzer can be smaller and cleaner by removing the lowlevel
details of lexical analysis.
• Efficiency
Compiler efficiency is improved. A separate lexical analyzer allows us to apply specialized
techniques that serve only the lexical task, not the job of parsing. In addition, specialized
buffering techniques for reading input characters can speed up the compiler significantly.
• Portability
Compiler portability is enhanced. Input-device-specific peculiarities can be restricted to the
lexical analyzer.

**[Semantic Analysis]**
The semantic analyzer uses the syntax tree and the information in the symbol table to
check the source program for semantic consistency with the language definition.
It also gathers type information and saves it in either the syntax tree or the symbol
table, for subsequent use during intermediate-code generation.
An important part of semantic analysis is type checking, where the compiler checks
that each operator has matching operands.
For example, many programming language definitions require an array index to be an
integer; the compiler must report an error if a floating-point number is used to index
an array.
Some sort of type conversion is also done by the semantic analyzer.
For example, if the operator is applied to a floating point number and an integer, the
compiler may convert the integer into a floating point number.
In our example, suppose that position, initial, and rate have been declared to be
floating- point numbers, and that the lexeme 60 by itself forms an integer.
The semantic analyzer discovers that the operator * is applied to a floating-point
number rate and an integer 60.
In this case, the integer may be converted into a floating-point number.
In the following figure, notice that the output of the semantic analyzer has an extra
node for the operator inttofloat, which explicitly converts its integer argument into a
floating-point number.

**[Intermediate Code Generation]**
In the process of translating a source program into target code, a compiler may
construct one or more intermediate representations, which can have a variety of forms.
Syntax trees are a form of intermediate representation; they are commonly used
during syntax and semantic analysis.
After syntax and semantic analysis of the source program, many compilers generate
an explicit low-level or machine-like intermediate representation, which we can think
of as a program for an abstract machine.

This intermediate representation should have two important properties:

- It should be simple and easy to produce
- It should be easy to translate into the target machine.

In our example, the intermediate representation used is a three-address code, which
consists of a sequence of assembly-like instructions with three operands per
instruction.

**[Code Optimization]**
The machine-independent code-optimization phase attempts to improve the
intermediate code so that better target code will result.
The objectives for performing optimization are: faster execution, shorter code, or target
code that consumes less power.
In our example, the optimized code is:
t1 = id3 * 60.0
id1 = id2 + t1

CODE OPTIMIZER: This phase is optional in some Compilers, but so useful and beneficial
in terms of saving development time, effort, and cost. This phase performs the following
specific functions:

- Attempts to improve the IC so as to have a faster machine code. Typical functions
include –Loop Optimization, Removal of redundant computations, Strength
reduction, Frequency reductions etc.
- Sometimes the data structures used in representing the intermediate forms may
also be changed.

**[Code Generator]**
The code generator takes as input an intermediate representation of the source
program and maps it into the target language.
If the target language is machine code, registers or memory locations are selected for
each of the variables used by the program.
Then, the intermediate instructions are translated into sequences of machine
instructions that perform the same task.
A crucial aspect of code generation is the judicious assignment of registers to hold
variables.
If the target language is assembly language, this phase generates the assembly code as
its output.
In our example, the code generated is:

```nasm
LDF R2, id3
MULF R2, #60.0
LDF R1, id2
ADDF R1, R2
STF id1, R1
```

The first operand of each instruction specifies a destination.
The F in each instruction tells us that it deals with floating-point numbers.
The above code loads the contents of address id3 into register R2, then multiplies it
with floating-point constant 60.0.
The # signifies that 60.0 is to be treated as an immediate constant.
The third instruction moves id2 into register Rl and the fourth adds to it the value
previously computed in register R2.
Finally, the value in register Rl is stored into the address of idl , so the code correctly
implements the assignment statement position = initial + rate * 60.

**[Symbol Table]**
The symbol table is a data structure containing a record for each variable name, with
fields for the attributes of the name.
These attributes may provide information about the storage allocated for a name, its
type, its scope (where in the program its value may be used), and in the case of
procedure names, such things as the number and types of its arguments, the method
of passing each argument (for example, by value or by reference), and the type
returned.
The data structure should be designed to allow the compiler to find the record for each
name quickly and to store or retrieve data from that record quickly.

**[Error Detection And Reporting]**
Each phase can encounter errors.
However, after detecting an error, a phase must somehow deal with that error, so that
compilation can proceed, allowing further errors in the source program to be detected.

**`[NFA] Nondeterministic FA`**- an FA that allows transitions on the empty string, and states that have multiple transitions on the same character

**`[DFA] Deterministic FA`** - A DFA is an FA where the transition function is single-valued. DFAs do not allow -transitions.

**[Abstract Program Representation]**

**[Global Tables]**

- Symbol Table - The purpose of the symbol table is to provide a unique, fixed-length encoding for the identifiers (and possibly the keywords) occurring in a program;
- Constant Table - integer operations must conform to the range of the target machine's integer arithmetic, and floating point operations must conform to its radix, range, precision, and rounding characteristics;
- Definition Table - Types, variables, procedures, and parameters are examples of entities: components of the
a program whose attributes are established by declaration;

**[Parser Construction]**

- LL(1) Parsers - are top-down pushdown automata that can be obtained by construction;
- LR Parsers - scans the input from left to right to build a rightmost derivation in reverse;
- SLR(1) - is the following algorithm leads to a deterministic pushdown automaton; cover many practically important language constructs not expressible by LR(0) grammars. Compared to the LR(1) construction, the given algorithm leads to substantially fewer states in the automaton.
- LALR(1) - state set of the pushdown automaton formed by construction G. Instead of obtaining the LALR(1) parser from the LR(1) parser by merging states, one could begin with the SLR(1) parser and determine the exact right context only for those states in which the transition function is ambiguous.
