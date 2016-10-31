.. ##
.. ## Copyright (c) 2016, Lawrence Livermore National Security, LLC.
.. ##
.. ## Produced at the Lawrence Livermore National Laboratory.
.. ##
.. ## All rights reserved.
.. ##
.. ## For release details and restrictions, please see the RAJA/LICENSE file.
.. ##

*********************************
RAJA Coding Guidelines
*********************************

These guidelines define code style conventions for RAJA. Most of the 
guidelines were taken from the cited references, sometimes with 
modifications and simplifications; see :ref:`codingrefs-label`.

The guidelines emphasize code readability, correctness, portability, and 
interoperability. Agreement on coding style and following common idioms 
and patterns provides many benefits to a project with multiple developers. 
A uniform "look and feel" makes it easier to read and understand source code, 
which increases team productivity and reduces confusion and coding errors 
when developers work with code they did not write. Also, guidelines 
facilitate code reviews by enforcing consistency and focusing developers on 
common concerns. Some of these guidelines are arbitrary, but all are based 
on practical experience and widely accepted sound practices. For brevity, 
most guidelines contain little detailed explanation or justification. 

Each guideline is qualified by one of three auxiliary verbs: 
"must", "should", or "may". 

* A "must" item is an absolute requirement. 
* A "should" item is a strong recommendation. 
* A "may" item is a potentially beneficial stylistic suggestion. 

Whether and how to apply items qualified with "should" or "may" often depends
on the particular code situation. It is best to use them in a manner that
enhances code readability and help to reduce user and developer errors.


==============================================================
1 Modifying Existing Code and Deviating from These Guidelines
==============================================================

1.1 When modifying existing code, the style conventions already in
use in the file **must** be followed. This is not intended to
stifle personal creativity - mixing style is disruptive and 
may cause confusion for users and fellow developers.

1.2 When making stylistic changes to existing code, those changes **should** 
extend to a point where the style is consistent across a reasonable scope. 
This may mean that an entire source or header file is changed to prevent
multiple conflicting styles.

1.3 Significant deviations from these guidelines **must** be discussed and
agreed upon by the development team. If the guidelines need to be changed,
they **should** be.


.. _namesec-label:

========
2 Names
========

Good names are essential to sound software design.
This section contains guidelines for naming files, types. functions, 
class members, variables, etc. The main goal is to use a distinct and 
consistent naming convention for each item so that the role of each entity 
in the code is obvious from the form of its name.

-----------
2.1 General
-----------

2.1.1 Every name **must** be meaningful. In particular, its meaning **must** 
be clear to other code developers and users, not just the author of the name.

      A substantial benefit of good name selection is that it can greatly
      reduce the amount of developer debate to define a concepts. A good name
      also tends to reduce the amount of documentation required for others to
      understand it. For example, when the name of a function clearly indicates
      what it does and the meaning and purpose of each argument is clear from
      its name, then code comments may be unnecessary. Documentation is
      can be a substantial part of software and requires maintenance. 
      Minimizing the amount of documentation required reduces this burden.

2.1.2 Terminology **must** be used consistently; i.e., in documentation and 
for names of directories, types, functions, variables, etc. Multiple terms 
**should** not be used to refer to the same concept and a concept **should** 
not be referred to by multiple terms.

      Using a clear, limited set of terminology in a software project helps
      maintain the consistency and integrity of the software, and it makes
      the code easier to understand for developers and users.

2.1.3 Each name **must** be consistent with other similar names in the code.

      For example, if getter/setter methods follow the convention "getFoo"
      and "setFoo" respectively, then adding a new setter method called
      "putBar" is clearly inconsistent.

2.1.4 Tersely abbreviated or cryptic names **should** be avoided. However, 
common acronyms and jargon that are well understood by team members and
users **may** be used.


--------------------
2.2 Directories
--------------------

2.2.1 Each source directory **must** be named so that the collective purpose 
of the files it contains is clear. Directory names **should** follow
the same style conventions. 

      RAJA directory names use all lower case letters and consist of a single 
      word in most cases. A directory name with more than one word uses 
      a 'hyphen' to separate words.


--------------
2.3 Files
--------------

In this section and throughout the guidelines, we refer to "header" and
"source" files. Header files are those that are included in other files
(either header or source). Source files are not included in other files and
form distinct translation units when a program is compiled.

2.3.1 C++ header and source file extensions **must** be: \*.hxx and \*.cxx, 
respectively.

2.3.4 The name of each file **must** clearly indicate its contents.

      For example, the header and source file containing the definition and
      implementation of a major type, such as a class **must** include the 
      type name of the type in the file name. For example, the header and
      implementation file for a class called "MyClass" should be named 
      "MyClass.hxx" and "MyClass.cxx", respectively.

      Files that are not associated with a single type, but which contain 
      closely related functionality or concepts, **must** be named so that
      the functionality or concepts are clear from the name. For example,
      files that define and implement methods that handle file I/O **should** 
      be named "FileIO.hxx" and "FileUtils.cxx", or similar.

2.3.3 Header and source files that are closely related, such as a header file
containing prototypes for a set of methods and a source file containing
implementations of those methods **must** be named the same (excluding 
file extension, of course) or sufficiently similar so that their 
relationship is clear.

2.3.4 File names that differ only in letter case **must** not be used.

      Since we aim to support Windows platforms, which has limited case
      sensitivity for file names, having files with names "MyClass.hxx" 
      and "myclass.hxx", for example, is not acceptable. 


------------------------
2.4 Types
------------------------

2.4.1 Type names (i.e., classes, structs, typedefs, enums, etc.) **must** be 
nouns and **should** be in mixed case with each word starting with 
an upper case letter and all other letters in lower cases.

      For example, these are preferred type names::

         IndexSet, RangeSegment, PolicyBase

      These type names should not be used::

         indexSet, rangesegment, POLICYBASE

2.4.2 Separating characters, such as underscores, **should** not be used 
between words in a type name.

      For example, these names are not preferred type names::

         Index_set, Range_Segment

      **Exceptions to the guidelines above** include cases where types
      play a similar role to those in common use elsewhere. For example, RAJA 
      has iterator classes, such as "base_iterator" and "numeric_iterator". 
      These names are acceptable since they are consistent with those found 
      in the C++ standard library.

2.4.3 Suffixes that may be used by compilers for name mangling, or 
which are used in the C++ standard library, such as "\_t", **must** not 
be used in RAJA type names.


------------------------
2.5 Functions
------------------------

2.5.1 Each function name **must** indicate clearly indicate what the 
function does. 

      For example::

        calculateDensity() and getDensity()

      are good function names because they distinguish the fact that the
      first performs a computation and the second returns a value. If a
      function were named::

        density()

      what it actually does is murky.

2.5.2 Function names **should** begin with a verb.

2.5.3 Complementary verbs such as  "get/set", "add/remove" and "create/destroy"
**must** be used for routines that perform complementary operations.

      Such symmetry prevents confusion and makes interfaces easier to use.

2.5.4 Verbs such as "is", "has", "can", etc. **should** be used for functions 
with a boolean return type.

      For example, the following names are preferred::

         isInitialized(), isAllocated()

2.5.5 Function names **must** use "camelCase" or "pot_hole" style. camelCase 
is preferred. 

      **camelCase style:** The first word has all lower case letters.
      If multiple words are used, each word after the first starts with
      an upper case letter and all other letters in the word are lower case.
      Underscores must not be used in camelCase names, but numbers may be used.

      For example, these are proper camelCase names::

         getLength(), createView2()

      **pot_hole style:** All letters are lower case. If multiple
      words are used, they are separated by a single underscore. Numbers
      may be used in pothole style names.

      For example, these are acceptable pothole style variable names::

         push_front(), push_back_2()

2.5.6 Names of related functions, such as methods for a class, **should** 
follow the same style.
 
      **Exception:** While consistency is important, name style may be mixed 
      when it makes sense to do so. For example, most methods for a class may 
      follow camelCase style. But, that same class may also contain methods 
      that follow pot_hole style if those methods perform operations that are
      similar to C++ standard library functions.


-----------------------------------
2.6 Data members and variables
-----------------------------------

2.6.1 All variables (class/struct members, function-scoped variables, function
arguments, etc.) **must** use either "camelCase" style or "pot_hole" style. 
Pot_hole style is preferred since it distinguishes variable names from 
method names.

       For example, these are acceptable variable names::

         myAverage, person_name, pressure2

2.6.2 Non-static class and struct data member names **must** have the 
prefix "m\_".

      This convention makes it obvious which variables are class 
      members/struct fields and which are other local variables. For 
      example, the following are acceptable names for class data members using
      camelCase style::

         m_myAverage, m_personName

      and acceptable pothole style::

         m_my_average, m_person_name

2.6.3 Static class and struct data member names and static file scope variables
**must** have the prefixes "s\_".

      Similar to the guideline above, this makes it obvious that the variable
      is static.

2.6.4 Verbs, such as "is", "has", "can", etc., **should** be used for boolean 
variables (i.e., either type bool or integer that indicates true/false).

      For example, these names are preferred::

         m_is_initialized, has_license

      to these names::

         m_initialized, license

2.6.5 A variable that refers to a non-fundamental type **should** give an 
indication of its type.

      For example,::

         Topic* my_topic;

      is clearer than::

         Topic* my_value;


------------------------------------
2.7 Macros and enumeration constants
------------------------------------

2.7.1 Preprocessor macro constants **must** be named using all uppercase 
letters and underscores should be used between words.

      For example, these are acceptable macro names::

         MAX_ITERATIONS, READ_MODE

      These are not acceptable::

         maxiterations, readMode

2.7.2 The name of each enumeration value **should** start with a capital letter
and use an underscore between words when multiple words are used.

       For example,::

          enum Orange
          {
             Navel,
             Valencia,
             Num_Orange_Types
          };


.. _dirorgsec-label:

=====================================
3 Directory and File Organization
=====================================

This section contains basic directory and file organization guidelines.
These guidelines help make it easy to locate a file and
to locate essential information in a file easily and quickly.

----------------
3.1 Directories
----------------

3.1.1 The contents of each directory and file **must** be well-defined and
limited so that it can be named to clearly indicate its contents. 
The goal is to prevent directories and files from becoming bloated with 
too many or diverse concepts.


-------------------------------------
3.2 File location
-------------------------------------

3.2.1 Header files and associated implementation files **should** reside in 
the same directory, which is a common practice for C++ libraries, unless
there is a good reason to do otherwise.

3.2.2 Each file **must** reside in the directory that corresponds to the code 
functionality supported by the contents of the file.


.. _headerguide-label:

---------------------------------------------------------
3.3 General header file guidelines
---------------------------------------------------------

Consistently-applied conventions and header file organization can significantly
improve user understanding and developer productivity. This section provides 
general header file guidelines. In section :ref:`headerorg-label`, we describe 
recommended header file organization.

3.3.1 A header file **may** contain multiple type definitions (e.g., structs, 
classes, enums, etc.). However, type definitions and function declarations in 
a header file **must** be related closely and/or support the primary type for 
which the file is named.

3.3.2 A header file **must** be self-contained and self-sufficient.

      Specifically, each header file

      * **Must** have proper header file include guards 
        (see :ref:`headerorg-label`) to prevent multiple inclusion. The macro 
        symbol name for each guard must be chosen to guarantee uniqueness 
        within a compilation unit.
      * **Must** include all other headers and/or forward declarations it 
        needs to be compiled standalone. In addition, a file **should not** 
        rely on symbols defined in other header files it includes; the 
        other files **should** be included explicitly.
      * **Must** contain implementations of all generic templates and inline
        methods defined in it. A compiler will require the full definitions of
        these constructs to be seen in every source file that uses them.

        **Note:** Function templates or class template members whose 
        implementations are fully specialized with all template arguments 
        **must** be defined in an associated source file to avoid linker 
        errors. Fully specialized templates are not templates and 
        are treated just like regular functions.

3.3.3 Header files **should** use forward declarations instead of header file 
inclusions when possible. This may speed up compilation, especially when 
recompiling after header files change.

      **Exceptions:**

      * Header files that define external APIs for RAJA **must**
        include all header files for all types that appear in the API. This
        makes use of the API much easier.
      * When using a function, such as an inline method or template, that is
        implemented in a header file, the header file containing the
        implementation **must** be included.
      * Similarly, when using C++ standard library types in a header file, it
        **may** be preferable to include the actual headers (rather than 
        forward reference headers (e.g., 'iosfwd') in the header file to 
        make it easier to use. This avoids having explicit
        inclusion of standard headers wherever the header file is used.

3.3.4 A forward type declaration **must** be used in a header file when an 
include statement would result in a circular dependency among header files. 

3.3.5 Extraneous header files or forward declarations (i.e., those not 
required for standalone compilation) **must not** be included in header files.

      Spurious header file inclusions, in particular, introduce spurious file
      dependencies, which can increase compilation time unnecessarily.

3.3.6 Header file include statements **should** use the same ordering pattern 
for all files.

      This improves code readability, helps to avoid misunderstood
      dependencies, and insures successful compilation regardless of
      dependencies in other files. A common, recommended header file 
      inclusion ordering scheme is:

      #. Related header (e.g., class header in class implementation file)
      #. C library headers (if needed)
      #. C++ library headers
      #. Headers from other libraries
      #. Project headers

      Also, code is easier to understand when include files are ordered
      alphabetically within each of these sections and a blank line is
      inserted between sections. Also, adding comments that describe the
      header file categories are sometimes useful.  For example,

.. code-block:: cpp

         // Related header
         #include "MyClass.hpp"

         // C standard library (including non-std unistd.h)
         #include <stdio.h>
         #include <unistd.h>

         // C++ standard library
         #include <unordered_map>
         #include <vector>

         // "base" library headers
         #include "base/Port.hxx"

         // Headers from this project
         #include "MyOtherClass.hpp"

3.3.7 A "typedef" statement, when used, **should** appear in the header file 
where the type is defined. 

      This practice helps ensure that all names associated with a given type
      are available when the appropriate header file is used and eliminates
      potentially inconsistent type names.

3.3.8 Routines **should** be ordered and grouped in a header file so that
code readability and understanding are enhanced.

      For example, all related methods should be grouped together. Also,
      public methods, which are part of an interface, should appear before 
      private methods.

3.3.9 The name of each function argument **must** be specified in a header 
file declaration. Also, names in function declarations and definitions 
**must** match.

       For example, this is not an acceptable function declaration::

          void doSomething(int, int, int);

3.3.10 Each function, type, and variable declaration in a header file **must** 
be documented according to the guidelines in Section 4.

       **Exception:** A set of short, simple functions (e.g., inline functions)
       with related functionality **may** be grouped together and described 
       with a single documentation prologue if the result is clearer and more 
       concise documentation. Good names that are self-explanatory are 
       generally preferable to writing (and maintaining!) documentation.


.. _headerorg-label:

---------------------------------------------------------
3.4 Header file content organization
---------------------------------------------------------

Content **must** be organized consistently in all header files. The file 
layout described here is recommended. The following summary uses numbers 
and text to illustrate the basic structure. Details about individual items 
are contained in the guidelines after the summary.

.. code-block:: cpp

   // (1) Doxygen file prologue

   // (2a) Header file include guard, e.g.,
   #ifndef MYCLASS_HPP
   #define MYCLASS_HPP

   // (3) RAJA copyright and release statement

   // (4) Header file inclusions (when NEEDED in lieu of forward declarations)
   #include "..."

   // (5) Forward declarations NEEDED in header file (outside of RAJA namespace)
   class ...;

   // (6a) RAJA namespace declaration
   namespace RAJA {

   // (7a) RAJA internal namespace (if used); e.g.,
   namespace awesome {

   // (8) Forward declarations NEEDED in header file (in RAJA namespace(s))
   class ...;

   // (9) Type definitions (class, enum, etc.) with Doxygen comments e.g.,
   /*!
    * \brief Brief ...summary comment text...
    *
    * ...detailed comment text...
    */
   Class MyClass {
      ...
   };

   // (7b) RAJA internal namespace closing brace (if needed)
   } // awesome namespace closing brace

   // (6b) RAJA namespace closing brace
   } // RAJA namespace closing brace

   // (2b) Header file include guard closing endif */
   #endif // closing endif for header file include guard


3.4.1 Each header file **must** begin with a Doxygen file prologue (item 1).

      See Section 4 for details.

3.4.2 The contents of each header file **must** be guarded using a 
preprocessor directive that defines a unique "guard name" for the header.

      The guard must appear immediately after the file prologue and use the
      '#ifndef' directive (item 2a); this requires a closing '#endif' 
      statement at the end of the file (item 2b). The preprocessor constant 
      must use the file name followed by "_HPP"; e.g., "MYCLASS_HPP" as above.

3.4.3 Each header file **must** contain a comment section that includes the 
RAJA copyright and release statement (item 3).

      See Section 4 for details.

3.4.4 All necessary header file inclusion statements (item 4) **must** 
appear immediately after copyright and release statement and before any 
forward declarations, type definitions, etc.

3.4.5 Any necessary forward declarations (item 5) for types defined outside 
the RAJA namespace **must** appear after the header include statements
and before the RAJA namespace statement.

3.4.6 All types defined and methods defined in a header file **must** be 
included in a namespace.

      Either the main "RAJA" namespace (item 6) or a namespace
      nested within the RAJA namespace (item 7) may be used, or 
      both may be used. A closing brace ( "}" ) is required to close each
      namespace declaration (items 6b and 7b) before the closing '#endif' 
      for the header file include guard.

3.4.7 Forward declarations needed **must** appear first in the "RAJA" or 
nested namespace before any other statements (item 8).

3.4.8 All class and other type definitions (item 9) **must** appear 
after header file inclusions and forward declarations. A proper class 
prologue **must** appear before the class definition; see Section 4 
for details.


.. _sourceguide-label:

---------------------------------------------------------
3.5 General source file guidelines
---------------------------------------------------------

Consistently-applied conventions and source file organization can help
developer productivity. This section provides general source file 
guidelines. In section :ref:`sourceorg-label`, we describe recommended source
file organization.

3.5.1 Each source file **must** have an associated header file with a matching
name, such as "Foo.hxx" for the source file Foo.cxx".

      **Exceptions:** Test files may not require headers.

3.5.2 Unnecessary header files **should not** be included in source files 
(i.e.,headers not needed to compile the file standalone).

      Such header file inclusions introduce spurious file dependencies, which
      may increases compilation time unnecessarily.

3.5.3 The order of routines implemented in a source file **should** match the 
order in which they appear in the associated header file.

      This makes the methods easier to locate and compare with documentation
      in the header file.

3.5.4 Each function implementation in a source file **should** be documented 
following to the guidelines in Section 4.


.. _sourceorg-label:

---------------------------------------------------------
3.6 Source file content organization
---------------------------------------------------------

Content **must** be organized consistently in all source files. The file 
layout described here is recommended. The following summary uses numbers 
and text to illustrate the basic structure. Details about individual items 
are contained in the guidelines after the summary.

.. code-block:: cpp

   // (1) Doxygen file prologue

   // (2) RAJA copyright and release statement

   // (3) Header file inclusions (only those that are NECESSARY)
   #include "..."

   // (4a) RAJA namespace declaration
   namespace RAJA {

   // (5a) RAJA internal namespace (if used); e.g.,
   namespace awesome {

   // (6) Initialization of static variables and data members, if any; e.g.,
   Foo* MyClass::s_shared_foo = 0;

   // (7) Implementation of static class member functions, if any

   // (8) Implementation of non-static class members and other methods

   // (5b) Internal namespace closing brace (if needed)
   } // awesome namespace closing brace

   // (4b) RAJA namespace closing brace
   } // RAJA namespace closing brace


3.6.1 Each source file **must** begin with a Doxygen file prologue (item 1).

      See Section 4 for details.

3.6.2 Each source file **must** contain a comment section that includes the
      RAJA copyright and release statement (item 3).

      See Section 4 for details.

3.6.3 All necessary header file include statements (item 2) **must**
      appear immediately after the copyright and release statement and 
      before any implementation statements in the file.

3.6.4 All contents in a source file **must** follow the same namespace 
inclusion pattern as its corresponding header file (see item 3.4.6).

      Either the main "RAJA" namespace (item 4a) or internal namespace 
      (item 5a) may be used, or both may be used. A closing brace ( "}" ) 
      is required to close each namespace declaration (items 4b and 5b).

3.6.5 When used, static variables and class data members **must** be 
      initialized explicitly in the class source file before any method
      implementations (item 6).


.. _scopesec-label:

=====================================
4 Scope
=====================================

---------------------------------------------------------
4.1 Namespaces
---------------------------------------------------------

4.1.1 All RAJA code **must** be included in the RAJA namespace.

4.1.2 When appropriate, RAJA code should be included in a nested namespace
with the RAJA namespace.

4.1.3 The 'using directive' **must not** be used in any header file.

      Applying this directive in a header file leverages a bad decision to
      circumvent the namespace across every file that directly or indirectly
      includes that header file. Note that this guideline implies that each
      type name appearing in a header file **must be fully-qualified** (i.e.,
      using the namespace identifier and scope operator) if it resides in a
      different namespace than the contents of the file.

4.1.4 The 'using directive' **may** be used in a source file to avoid using a 
fully-qualified type name at each declaration. Using directives **must** appear
after all "#include" directives in a source file.

4.1.5 When only parts of a namespace are used in an implementation file, only 
those parts **should** be included with a using directive instead of the 
entire namespace contents.

      For example, if you only need the standard library vector container form
      the "std" namespace, it is preferable to use::

         using std::vector;

      rather than::

         using namespace std;

4.1.6 Non-member functions that are meant to be used only internally to a 
single source file **should** be placed in the unnamed namespace to make
them invisible outside the file.

      This guarantees link-time name conflicts will not occur. For example::

         namespace {
            void myInternalFunction();
         }

4.1.7 Local variables **should** be declared in the narrowest scope possible 
and as close to first use as possible.

      Minimizing variable scope makes source code easier to comprehend and
      may have performance and other benefits. For example, declaring a loop 
      index inside a for-loop statement such as::

         for (int ii = 0; ...) {

      is preferable to::

         int ii;
         ...
         for (ii = 0; ...) {

      **Exception:** When a local variable is an object, its constructor and
      destructor may be invoked every time a scope (such as a loop) is entered
      and exited, respectively. Thus, instead of this::

         for (int ii = 0; ii < 1000000; ++ii) {
            Foo f;
            f.doSomethingCool(ii);
         }

      it may be more efficient to do this::

         Foo f;
         for (int ii = 0; ii < 1000000; ++ii) {
            f.doSomethingCool(ii);
         }

4.1.8 A reference to any item in the global namespace (which should be rare 
if needed at all) **should** use the scope operator ("::") to make this clear.

      For example::

         int local_val = ::global_val;


---------------------------------------------------------
4.2 Classes
---------------------------------------------------------

4.2.1 Class members **must** be declared in the following order: 

      # "public"
      # "protected"
      # "private"

      That is, order method and data members in terms of 
      "decreasing scope of audience".

4.2.2 "Friend" declarations **should** be used rarely. When used, they 
**must** appear within the body of a class definition before any class 
member declarations.

      Note that placing "friend" declarations before the "public:" keyword 
      makes them private, which preserves encapsulation.

4.2.3 Static class members (methods or data) **must** be used rarely. In 
every case, their usage **must** be carefully reviewed by the team.

      When it is determined that a static member is needed, it **must** appear 
      first in the appropriate member section. Typically, static member 
      functions **should** be "public" and static data members **should** be 
      "private".

4.2.4 Class data members **should** be "private". If "public" or "protected" 
data members are even considered, this choice **must** be reviewed carefully 
by other team members.

      Information hiding is an essential aspect of good software engineering 
      and private data is the best means for a class to preserve its 
      invariants. Specifically, a class should maintain control of how object 
      state can be modified to minimize side effects. In addition, restricting
      direct access to class data enforces encapsulation and facilitates 
      design changes through refactoring.

4.2.5 Nested classes **should** be private unless they are part of the 
enclosing class interface.

      For example::

         class Outer
         {
            // ...
         private:
            class Inner
            {
               // ...
            };
         };

      When only the enclosing class uses a nested class, making it private
      does not pollute the outer scope needlessly. Furthermore, nested classes
      may be forward declared within the enclosing class definition and then
      defined in the implementation file for the enclosing class. For example::

         class Outer
         {
            class Inner; // forward declaration

            // use name 'Inner' in Outer class definition
         };

         // In Outer.cxx implementation file...
         class Outer::Inner
         {
            // Inner class definition
         }

      This makes it clear that the nested class is only needed in the
      implementation and does not clutter the class definition.


.. _docsec-label: 

========================================
5 Code Documentation
========================================

This section contains content and formatting guidelines for the code
documentation items mentioned in earlier sections. The aims of these 
guidelines are to:

   * Document files, data types, functions, etc. consistently.
   * Promote good documentation practices so that essential information is 
     presented clearly and lucidly, and which do not over-burden developers.
   * Generate source code documentation using the Doxygen system.


-----------------------------------------
5.1 General documentation considerations
-----------------------------------------

5.1.1 Documentation **should** only include what is essential for users and 
other developers to easily understand code. Comments **should** be limited to 
describing constraints, pre- and post-conditions, and other issues that 
are important, but not obvious. Extraneous comments (e.g., documenting 
"the obvious") **should** be avoided.

      Code that uses clear, descriptive names (functions, variables, etc.) and 
      clear logical structure is preferable to code that relies on a lot of 
      comments for understanding. To be useful, comments must be understood by 
      others and kept current with the actual code. Generally, maintenance 
      and understanding are better served by rewriting tricky, unclear code 
      than by adding comments to it.

5.1.2 New source code **must** be documented following the guidelines in this 
section. Documentation of existing code **should** be modified to conform to 
these guidelines when appropriate. 

      Documentation of existing code **should** be changed when significant code
      modifications are made (i.e., beyond bug fixes and small changes) and 
      when existing documentation is inadequate.

5.1.3 End-of-line comments **should** not be used to document code logic, 
since they tend to be less visible than other comment forms and may be 
difficult to format cleanly. 

      Short end-of-line comments **may** be useful for labeling closing braces 
      associated with nested loops, conditionals, for scope in general, and 
      for documenting local variable declarations.

5.1.4 All comments, except end-of-line comments, **should** be indented to 
match the indentation of the code they are documenting. Multiple line comment 
blocks **should** be aligned vertically on the left.

5.1.5 To make comment text clear and reduce confusion, code comments 
**should** be written in grammatically-correct complete sentences or 
easily understood sentence fragments.

5.1.6 Comments **should** be clearly delimited from executable code with blank 
lines and "blocking characters" (see examples below) to make them stand out 
and, thus, improve the chances they will be read.

5.1.7 White space, such as blank lines, indentation, and vertical alignment 
**should** be used in comment blocks to enhance readability, emphasize 
important information, etc.


--------------------------------------------------------------------
5.2 General Doxygen usage guidelines and summary of common commands
--------------------------------------------------------------------

The Doxygen code documentation system uses C or C++ style comment sections 
with special markings and Doxygen-specific commands to extract documentation 
from source and header files. Although Doxygen provides many sophisticated 
documentation capabilities and can generate a source code manual in a variety 
of formats such as LaTeX, PDF, and HTML, these guidelines address only a small 
subset of Doxygen syntax. The goal of adhering to a small, simple set of 
documentation commands is that developers will be encouraged to build useful 
documentation when they are writing code.


The Doxygen system interprets each documentation comment as either "brief" 
or "detailed". 

 - A brief comment is a concise statement of purpose for an item (usually no 
   more than one line) and starts with the Doxygen command "\\brief" 
   (or "@brief"). Brief comments appear in summary sections of the generated 
   documentation. They are typically seen before detailed comments when 
   scanning the documentation; thus good brief comments make it easier to 
   can or navigate a source code manual.

 - A detailed comment is any comment that is not identified as 'brief'.


5.2.1 Doxygen comment blocks **may** use either JavaDoc, Qt style, or one 
of the C++ comment forms described below.

      JavaDoc style comments consist of a C-style comment block starting with
      two \*'s, like this::

         /**
          * ...comment text...
          */

      Qt style comments add an exclamation mark (!) after the opening of a
      C-style comment block,like this::

         /*!
          * ...comment text...
          */

      For JavaDoc or Qt style comments, the asterisk characters ("\*") on
      intermediate lines are optional, but encouraged.

      C++ comment block forms start each line with an additional slash::

         ///
         /// ...comment text...
         ///

      or an exclamation mark::

         //!
         //! ...comment text...
         //!

      For these C++ style comment forms, the comment delimiter is required on
      each line.

5.2.2 Whichever Doxygen comment block style is used, it **must** be the same 
within a file.

5.2.3 When adding documentation to existing code, the new comments **must** 
use the same comment forms as the existing documentation.

5.2.4 Most Doxygen comments **should** appear immediately before the items they describe; i.e., no blank lines between comment and item.

      **Exception:** Inline Doxygen comments for class/struct data members, 
      enum values, function arguments, etc. **must** appear after the item 
      **on the same line** and **must** use the following syntax::

          /*!< ...comment text... */

      Note that the "<" character must appear immediately after the opening of
      the Doxygen comment (with no space before). This tells Doxygen that the
      comment applies to the item immediately preceding the comment. See
      examples in later sections.

5.2.5 When an item is documented using the Doxygen inline form above, the
comment **should** not span multiple lines.

5.2.5 A "brief" description **should** be provided in the Doxygen comment 
section for each of the following items: 

      * A type definition (i.e., class, struct, typedef, enum, etc.) 
      * A macro definition
      * A struct field or class data member
      * A class member function declaration (in the header file class 
        definition) 
      * An unbound function signature (in a header file)
      * A function implementation (when there is no description in the 
        associated header file)

5.2.6 Important information of a more lengthy nature (e.g., usage examples
spanning multiple lines) **should** be provided for files, major data types 
and definitions, functions, etc. when needed. A detailed comment **must** be 
separated from a brief comment in the same comment block with a line containing
no documentation text.

5.2.7 Summary of commonly used Doxygen commands

This Section provides an overview of commonly used Doxygen commands.
Please see the `Doxygen guide <http://www.stack.nl/~dimitri/doxygen/manual/index.html>`_ for more details and information about other commands.

Note that to be processed properly, Doxygen commands **must** be preceded with 
either "\\" or "\@" character. For brevity, we use "\\" for all commands 
described here.

   * **\\brief** The "brief" command is used to begin a brief description of 
     a documented item. The brief description ends at the next blank line.
   * **\\file** The "file" command is used to document a file. Doxygen requires
     that to document any global item (function, typedef, enum, etc.), the file
     in which it is defined must be documents. 
   * **\\if** and **\\endif** The "if" command, followed by a label, defines 
     the start of a conditional documentation section. The section ends with a
     matching "endif" command. Conditionals are typically used to 
     enable/disable documentation sections. For example, this may be useful if
     a project wants to provide documentation of all private class members 
     for developer documentation, but wants to hide private members in 
     documentation for users. Conditional sections are disabled by default 
     and must be explicitly enabled in the Doxygen configuration file. 
     Conditional blocks can be nested; nested sections are only enabled if 
     all enclosing sections are. The "\\elseif" command is also available to 
     provide more sophisticated control of conditional documentation.
   * **\\name** The "name" command, followed by a name containing no blank 
     spaces, is used to define a name that can be referred to elsewhere 
     in the documentation (via a link).
   * **\\param** The "param" command documents a function parameter/argument.
     It is followed by the parameter name and description. The "\\param" 
     command can be given an optional attribute to indicate usage of the 
     function argument; possible values are "[in]", "[out]", and "[in,out]".
   * **\\return** The "return" command is used to describe the return value 
     of a function.
   * **\\sa** The "sa" command (i.e., "see also") is used to refer (and 
     provide a link to) another documented item. It is followed by the target 
     of the reference (e.g., class/struct name, function name, documentation 
     page, etc.).
   * **\@{** and **\@}**  These two-character sequences begin and end a 
     grouping of documented items. Optionally, the group can be given a name 
     using the "name" command. Groups are useful for providing additional 
     organization in the documentation, and also when several items can be 
     documented with a single description (e.g., a set of simple, related 
     functions). 
   * **\\verbatim, \\endverbatim** The "verbatim/endverbatim" commands are 
     used to start/stop a block of text that is to appear exactly as it is 
     typed, without additional formatting, in the generated documentation.
   * **-** and **-#** The "-" and "-#" symbols begin an item in a bulleted 
     list or numbered list, respectively. In either case, the item ends at 
     the next blank line or next item.
   * **\\b** and **\\e** These symbols are used to make the next word bold or 
     emphasized/italicized, respectively, in the generated documentation.
   

--------------------------------------------------------------------
5.3 Copyright and release statement
--------------------------------------------------------------------

5.3.1 Each file **must** contain a comment section that includes the RAJA 
release information (using whichever comment characters are appropriate for the language the file is written in). In the interest of brevity, the complete
release statement is summarized here to show the essential information. It 
can be found in any of the RAJA files.

.. code-block:: cpp

   //~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~//
   // Copyright (c) 2016, Lawrence Livermore National Security, LLC.
   // 
   // Produced at the Lawrence Livermore National Laboratory.
   //
   // LLNL-CODE-689114
   //
   // All rights reserved.
   //
   // This file is part of RAJA.
   //
   // For additional details, please also read RAJA/README-license.txt.
   //
   // ...
   //
   //~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~//


--------------------------------------------------------------------
5.4 File documentation
--------------------------------------------------------------------

5.4.1 Each header file that declares a global type, method, etc. **must** 
have a Doxygen file prologue similar to the following:

.. code-block:: cpp

   /*!
    ***************************************************************************
    *
    * \file ...optional name of file...
    *
    * \brief A brief statement describing the file contents/purpose. (optional)
    *
    * Optional detailed explanatory notes about the file.
    *
    ****************************************************************************
    */

5.4.2 The Doxygen command "\\file" **must** appear first in the file prologue.

      The "\\file" command identifies the comment section as documentation 
      for the file. Doxygen requires that the file itself must be documented 
      for documentation to be generated for any global item (global function, 
      typedef, enum, etc.) defined in the file.

      The file name may include (part of) the path if the file name is not 
      unique. If the file name is omitted on the line after the "\\file" 
      command, then any documentation in the comment block will belong to 
      the file in which it is located instead of the summary documentation 
      in the listing of documented files.

5.4.3 A brief statement of purpose for the file **should** appear as the first 
comment after the file command. If included, the brief statement, **must** be 
preceded by the "\\brief" command.

5.4.4 Any detailed notes about the file **may** be included after the brief 
comment. If this is done, the detailed comments **must** be separated from 
the brief statement by a line containing no documentation text.


--------------------------------------------------------------------
5.5 Type documentation
--------------------------------------------------------------------

5.5.1 Each type and macro definition appearing in a header file **must** have 
a Doxygen type definition comment prologue immediately before it. For example

.. code-block:: cpp

   /*!
    ****************************************************************************
    *
    * \brief A brief statement of purpose of the type or macro.
    *
    * Optional detailed information that is helpful in understanding the
    * purpose, usage, etc. of the type/macro ...
    *
    * \sa optional cross-reference to other types, functions, etc...
    * \sa etc...
    *
    * \warning This class is only partially functional.
    *
    ****************************************************************************
    */

**Note that Doxygen requires that a compound entity, such as a class, struct, 
etc. be documented in order to document any of its members.**

5.5.2 A brief statement describing the type **must** appear as the first text 
comment using the Doxygen command "\\brief".

5.5.3 Important details about the item **should** be included after the brief 
comment and, if included, **must** be separated from the brief comment by a 
blank line.

5.5.4 Cross-references to other items, such as other related types **should** 
be included in the prologue to enhance the navigability of the documentation. 

      The Doxygen command "\\sa" (for "see also") **should** appear before each
      such cross-reference so that links are generated in the documentation.

5.5.5 Caveats or limitations about the documented type **should** be noted 
using the "\\warning" Doxygen command as shown above.


--------------------------------------------------------------------
5.6 Function documentation
--------------------------------------------------------------------

5.6.1 Each unbound function **should** be be documented with a function 
prologue in the header file where its prototype appears or in a source file 
immediately preceding its implementation.

5.6.2 Since C++ class member functions define the class interface, they 
**should** be documented with a function prologue immediately preceding 
their declaration in the class definition.

The following examples show two function prologue variations that may 
be used to document a method in a class definition. The first shows how
to document the function arguments in the function prologue.

.. code-block:: cpp

      /*!
       *************************************************************************
       *
       * \brief Initialize a Foo object with given operation mode.
       *
       * The "read" mode means one thing, while "write" mode means another.
       *
       * \return bool indicating success or failure of initialization.
       *              Success returns true, failure returns false.
       *
       * \param[in] mode OpMode enum value specifying initialization mode.
       *                 ReadMode and WriteMode are valid options.
       *                 Any other value generates a warning message and the
       *                 failure value ("false") is returned.
       *
       *************************************************************************
       */
       bool initMode(OpMode mode);

The second example shows how to document the function argument inline.

.. code-block:: cpp

      /*!
       ************************************************************************
       *
       * @brief Initialize a Foo object to given operation mode.
       *
       * The "read" mode means one thing, while "write" mode means another.
       *
       * @return bool value indicating success or failure of initialization.
       *             Success returns true, failure returns false.
       *
       *************************************************************************
       */
       bool initMode(OpMode mode /*!< [in] ReadMode, WriteMode are valid options */ );

Note that the first example uses the "\\" character to identify Doxygen 
commands; the second uses "@". 

5.6.3 A brief statement of purpose for a function must appear as the first 
text comment after the Doxygen command "\\brief" (or "@brief"). 

5.6.4 Any detailed function description, when included, **must** appear 
after the brief comment and **must** be separated from the brief comment by 
a line containing no text.

5.6.4 If the function has a non-void return type, the return value **should** 
be documented in the prologue using the Doxygen command "\return" 
(or "@return") preceding a description of the return value. 

      Functions with "void" return type and C++ class constructors and 
      destructors **should not** have such documentation.

5.6.5 Function arguments **should** be documented in the function prologue 
or inline (as shown above) when the intent or usage of the arguments is not 
obvious. 

      The inline form of the comment may be preferable when the argument 
      documentation is short. When a longer description is provided (such as 
      when noting the range of valid values, error conditions, etc.) the 
      description **should** be placed within the function prologue for 
      readability. However, the two alternatives for documenting function 
      arguments **must not** be mixed within the documentation of a single 
      function to reduce confusion. 

      In any case, superfluous documentation should be avoided. For example, 
      when there are one or two arguments and their meaning is obvious from 
      their names or the description of the function, providing no comments is 
      better than cluttering the code by documenting the obvious. Comments 
      that impart no useful information are distracting and less helpful than 
      no comment at all.

5.6.6 When a function argument is documented in the prologue comment section, 
the Doxygen command "\param" **should** appear before the comment as in the 
first example above.

5.6.7. The "in/out" status of each function argument **should** be documented.

       The Doxygen "\param" command supports this directly by allowing such an
       attribute to be specified as "\param[in]", "\param[out]", or 
       "\param[in,out]". Although the inline comment form does not support 
       this, such a description **should** be included; e.g., by using "[in]", 
       "[out]", or "[in,out]" in the comment.

5.6.8 Short, simple functions (e.g., inline methods) **may** be grouped 
together and documented with a single descriptive comment when this is 
sufficient.

      An example of Doxygen syntax for such a grouping is::

         //@{
         //! @name Setters for data members

         void setMember1(int arg1) { m_member1 = arg1; }
         void setMember2(int arg2) { m_member2 = arg2; }

         //@}

5.6.9 Important implementation details (vs. usage detailed) about a function 
**should** be documented in the source file where the function is implemented,
rather than the header file where the function is declared.

      Header file documentation **should** include only purpose and usage 
      information germane to an interface. When a function has separate 
      implementation documentation, the comments **must** not contain Doxygen 
      syntax. Using Doxygen syntax to document an item in more than one location 
      (e.g., header file and source file) can cause undesired Doxygen 
      formatting issues and potentially confusing documentation.

      A member of a class may be documented as follows in the source file 
      for the class as follows (i.e., no Doxygen comments)::

        /*
         ***********************************************************************
         *
         * Set operation mode for a Foo object.
         *
         * Important detailed information about what the function does...
         *
         ***********************************************************************
         */
         bool Foo::initMode(OpMode mode)
         {
            ...function body...
         }


--------------------------------------------------------------------
5.7 Data member documentation
--------------------------------------------------------------------

5.7.1 Each struct field or class data member **should** have a descriptive 
comment indicating its purpose. 

     This comment may as appear as a prologue before the item, such as::

        /*!
         * \brief Brief statement describing the input mode...
         *
         * Optional detailed information about the input mode...
         */
        int m_input_mode;

     or, it may appear after the item as an inline comment such as::

        int m_input_mode; /*!< \brief Brief statement describing the input mode.... */

5.7.2 Regardless of which documentation form is used, a brief description 
**must** be included using the Doxygen command "\\brief".

5.7.3 Any detailed description of an item, if included, **must** appear after 
the brief comment and be separated from the brief comment with a line
containing no documentation text.

5.7.4 When a detailed comment is provided, or the brief statement requires 
more than one line, the prologue comment form **should** be used instead 
of the inline form to make the documentation easier to read.

5.7.6 If the names of data members are sufficiently clear that their meaning 
and purpose are obvious to other developers (which should be determined in 
a code review), then the members **may** be grouped together and documented 
with a single descriptive comment.

      An example of Doxygen syntax for such a grouping is::

         //@{
         //!  @name Data member description...

         int m_member1;
         int m_member2;
         ...
         //@}


.. _designsec-label:

=======================================================
6 Design and Implement for Correctness and Robustness
=======================================================

The guidelines in this section describe sound software engineering
practices that help enforce correctness and robustness and help
avoid mis-interpretation or confusion by others.


--------------------------------------------------------------------
6.1 General 
--------------------------------------------------------------------

6.1.1 Simplicity, clarity, ease of modification and extension **should** 
always be a main goal when writing new code or changing existing code. 

6.1.2 Each entity (class, struct, variable, function, etc.) **should** embody 
one clear, well-defined concept. 

      The responsibilities of an entity may increase as it is used in new and 
      different ways. However, changes that divert it from its original intent 
      **should** be avoided. Also, large, monolithic entities that provide too 
      much functionality or which include too many concepts tend to increase 
      code coupling and complexity and introduce undesirable side effects. 
      Smaller, clearly constrained objects are easier to write, test, maintain,
      and use correctly. Also, small, simple objects tend to get used more 
      often and reduce code redundancy. 

6.1.3 Global, complex, or opaque data sharing **should** be avoided. Shared 
data increases coupling and contention between different parts of a code base, 
which makes maintenance and modification difficult.

6.1.4 Static or global variables of class type **must not** be used.

      Due to indeterminate order of construction, their use may cause bugs
      that are very hard to find. Static or global variables that are pointers
      to class types **may** be used and must be initialized properly in a
      single source file.


---------------------------------------------------
6.2 Compiler-generated class methods
---------------------------------------------------

The guidelines in this section apply to class methods that may be 
*automatically generated* by a compiler, including constructors, destructors,
copy, and move methods. Developers should be aware of the conditions under
which compilers will and will not generate these methods. Developers should
also be aware of when compiler-generated methods suffice and when they do not.
After providing some guidelines, we discuss standard C++ rules that compilers
follow for generating class methods when they are not explicitly defined. 
See :ref:`automethods-label`.

The most important cases to pay attention to involve the destructor, copy
constructor, and copy-assignment operator. Classes that provide these methods,
either explicitly or compiler-generated, are referred to as *copyable*. Failing 
to follow the rules for these methods can be damaging due to errors or 
unexpected behavior. Rules involving the move constructor and move-assignment 
operator are less important since they mostly affect efficiency and not 
correctness. Copy operations can be used to accomplish the same end result
as move operations, just less efficiently. Move semantics are an important
optimization feature of C++. The C++11 standard requires compilers to use 
move operations instead of copy operations when certain conditions are 
fulfilled. Classes that provide move operations, either explicitly or 
compiler-generated, are referred to as *movable*.

6.2.1 Each class **must** follow the *Rule of Three* which states: if the 
destructor, copy constructor, or copy-assignment operator is explicitly 
defined, then the others **must** be defined.

      Compiler-generated and explicit versions of these methods **must not**
      be mixed. If a class requires one of these methods to be implemented, 
      it almost certainly requires all three to be implemented. 

      This rule helps guarantee that class resources are managed properly. 
      C++ copies and copy-assigns objects of user-defined types in various 
      situations (e.g., passing/returning by value, container manipulations, 
      etc.). These special member functions will be called, if accessible. 
      If they are not user-defined, they are implicitly-defined by the compiler.

      Compiler-generated special member functions are often incorrect 
      if a class manages a resource whose handle is an object of 
      non-class type. Consider a class data member which is a raw pointer to 
      an object. The compiler-generated class destructor will not free the 
      object. Also, the compiler-generated copy constructor and copy-assignment
      operator will perform a "shallow copy"; i.e., they will copy the value 
      of the pointer without duplicating the underlying resource.

6.2.2 A class that manages non-copyable resources through non-copyable handles, 
such as pointers, **should** declare the copy methods private and and leave 
them unimplemented.

      When the intent is that such methods should never be called, this is a 
      good way to help a compiler to catch unintended usage. For example::

	   class MyClass
	   {
	      // ...

	   private:
	      // The following methods are not implemented
	      MyClass();
	      MyClass(const MyClass&);
	      void operator=(const MyClass&);

	      // ...
	   };

      When code does not have access to the private members of a class tries 
      to use such a method, a compile-time error will result. If a class does 
      have private access and tries to use one of these methods an link-time 
      error will result. 

      This is another application of the "Rule of Three".

      **Exception:** If a class inherits from a base class that declares
      these methods private, the subclass need not declare the methods
      private. Including comments in the derived class header indicating that
      the the parent class enforces the non-copyable properties of the class
      is helpful.

6.2.3 When the compiler-generated versions are appropriate (i.e.,
correct and sufficiently fast), the default constructor, copy constructor, 
destructor, and copy assignment **may** be left undeclared. In this case, 
it is often helpful to add comments to the class header file indicating that 
the compiler-generated versions of these methods will be used.

6.2.4 If a class is default-constructable and has POD or bare pointer data 
members, its default constructor **must** be defined explicitly and the 
data members **must** be initialized explicitly. A compiler-generated version 
of a default constructor will not initialize such members, in general.

6.2.5 By convention, a functor class **should** have a copy constructor and 
copy-assignment operator. 

      Typically, the compiler-generated versions are sufficient when the class 
      has no state or non-POD data members. Since such classes are usually 
      small and simple, the compiler-generated versions of these methods 
      **may** be used without documenting the use of default value semantics 
      in the functor definition.


.. _automethods-label:

--------------------------------------------------------
6.3 Standard rules for compiler-generated class methods
--------------------------------------------------------

This section provides some background information related to the guidelines
in the previous section. There, we provide guidelines that help to decide 
when to define class methods that may be generated automatically by a compiler 
and when relying on compiler-generated versions suffices.  Here, we describe
the conditions under which compilers generate methods automatically.

Consider the following simple class::

   class MyClass
   {
   public:
      int x;
   };

How many methods does it have? None?

Actually, MyClass may have as many as **six** methods depending on how it is 
used: a default constructor, destructor, copy constructor, copy-assignment 
operator, move constructor, and move-assignment operator. Any of these may 
be generated by a compiler.

C++ compiler rules for generating class member functions are:

   * The parameter-less default constructor is generated if a class does
     not define *any* constructor and all base classes and data members
     are default-constructable. This means that once you declare a copy
     constructor (perhaps to disable the automatically provided one),
     the compiler will not supply a default constructor.
   * The destructor is automatically supplied if possible, based on the
     members and the base classes.
   * A copy constructor is generated if all base classes and members are
     copy-constructable. Note that reference members are copy-constructable.
   * The copy-assignment operator is generated if all base classes and members
     are copy-assignable. For this purpose, reference members are not
     considered copy-assignable.
   * A move constructor is supplied unless the class has any of the following: 
     a user-defined copy constructor, copy-assignment operator, 
     move-assignment operator, or destructor. If the move constructor cannot
     be implemented because not all base classes or members are
     move-constructable, the supplied move constructor will be defined
     as deleted.
   * A move-assignment operator is generated under the same conditions as 
     the move constructor.

The importance of understanding these rules and applying the guidelines in 
the previous section is underscored by the fact that compiler-generated 
methods may have different behaviors depending on how they are used. Here 
we provide some examples based on MyClass defined above.

If MyClass has a user-defined constructor, then

.. code-block:: cpp

    MyClass item1;

and

.. code-block:: cpp

    MyClass item2 = MyClass();

will both call the user-defined default constructor "MyClass()" and there is
only one behavior.

However, if MyClass relies on the compiler-generated constructor

.. code-block:: cpp

    MyClass item1;

performs *default initialization*, while

.. code-block:: cpp

    MyClass item2 = MyClass();

performs *value initialization*.

Default initialization calls the constructors of any base classes, and nothing
else. Since constructors for intrinsic types do not do anything, that means
all member variables will have garbage values; specifically, whatever values 
happen to reside in the corresponding addresses.

Value initialization also calls the constructors of any base classes. Then,
one of two things happens:

   * If MyClass is a POD class (all member variables are either intrinsic
     types or classes that only contain intrinsic types and have no
     user-defined constructor/destructor), all data is initialized to 0.
   * If MyClass is not a POD class, the constructor does not touch any data,
     which is the same as default initialization (so member variables have
     garbage values unless explicitly constructed otherwise).

Other points worth noting:

   * Intrinsic types, such as int, float, bool, pointers, etc. have
     constructors that do nothing (not even initialize to zero), destructors
     that do nothing, and copy constructors and copy assignment-ers that
     blindly copy bytes.
   * Comparison operators, such as "==" or "!=" are never automatically
     generated by a compiler, even if all base classes and members are
     comparable.



---------------------------------------------------
6.3 Class member initialization and copying
---------------------------------------------------

6.3.1 Each class data member **must** be initialized (using default values 
when appropriate) in every class constructor. That is, an initializer or
initialization **must** be provided for each class data member so that 
every object is in a well-defined state upon construction. 

      Generally, this requires a user-defined default constructor when a class 
      has POD members. Do not assume that a compiler-generated default 
      constructor will leave any member variable in a well-defined state.

      **Exception:** A class that has no data members, including one that 
      is derived from a base class with a default constructor that provides 
      full member initialization, does not require a user-defined default 
      constructor since the compiler-generated version will suffice.

6.3.2 When using initialization instead of assignment to set data member 
values in a constructor, data members **should** always be initialized 
in the order in which they appear in the class definition. 

      Compilers adhere to this order regardless of the order that members 
      appear in the class initialization list. So you may as well agree with 
      the compiler rules and avoid potential errors that could result when
      one member depends on the state of another.

6.3.3 A constructor **must not** call a virtual function on any data member 
object since an overridden method defined in a subclass cannot be called 
until the object is fully constructed. 

      There is no general guarantee that data members are fully-created 
      before a constructor exits.

6.3.4 All memory allocated in a class constructor **should** be de-allocated 
in the class destructor. 

      Note that the intent of constructors is to acquire resources and the 
      intent of destructors is to free those resources.

6.3.5 A user-supplied implementation of a class copy-assignment operator 
**should** check for assignment to self, **must** copy all data members 
from the object passed to operator, and **must** return a reference to "\*this".

      The *copy-and-swap* idiom **should** be used. 

6.3.6 All constructors and copy operations for a derived class **must** call 
the necessary constructors and copy operations for each of its base classes 
to insure that each object is properly allocated and initialized.


---------------------------------------------------
6.4 Inheritance
---------------------------------------------------

6.4.1 Polymorphism via inheritance and virtual methods **must** be used
judiciously in RAJA, if used at all. In the context of heterogeneous 
hardware environments, runtime polymorphism using virtual methods is
problematic; e.g., when objects are passed between host and device code using
CUDA, virtual methods cannot be called.

If inheritance is deemed a good solution for a particular situation, the 
following guidelines should be observed.

6.4.2 Deep inheritance hierarchies; i.e., more than 2 or 3 levels, **should**
be avoided.

6.4.3 Multiple inheritance **should** be restricted so that only one base 
class contains methods that are not "pure virtual".

6.4.4 One **should not** inherit from a class that was not designed to be a 
base class; e.g., if it does not have a virtual destructor.

      Doing so is bad practice and can cause problems that may not be reported 
      by a compiler; e.g., hiding base class members. To add functionality, 
      one **should** employ class composition rather than by "tweaking" an 
      existing class.

6.4.5 The destructor of a class that is designed to be a base class **must** 
be declared "virtual". 

      However, sometimes a destructor should not be declared virtual, such as 
      when deletion through a pointer to a base class object should be 
      disallowed.

6.4.6 If a virtual function in a base class is not expected to be overridden 
in any derived class, then the method **should not** be declared virtual.

6.4.7 If each derived class has to provide specific behavior for a base class 
virtual function, then it **should** be declared *pure virtual*.

6.4.8 Virtual functions **must not** be called in a class constructor or 
destructor. Doing so is undefined behavior. Even if it seems to work 
correctly, it is fragile and potentially non-portable.


--------------------------------------------------------------------
6.5 Const 
--------------------------------------------------------------------

6.4.1 The "const" qualifier **should** be used for variables and methods 
when appropriate to clearly indicate usage and to take advantage of 
compiler-based error-checking. For example, any class member function 
that does not change the state of the object on which it is called 
**should** be declared "const"

      Constant declarations can make code safer and less error-prone since they 
      enforce intent at compile time. They also improve code understanding
      because a constant declaration clearly indicates that the state
      of a variable or object will not change in the scope in which the 
      declaration appears.

6.5.2 Any class member function that does not change a data member of the 
associated class **must** be declared "const".

      This enables the compiler to detect unintended usage.

6.5.3 Any class member function that returns a class data member that 
should not be changed by the caller **must** be declared "const" and 
**must** return the data member as a "const" reference or pointer.

       Often, both "const" and non-"const" versions of member access functions
       are needed so that callers may declare the variable that holds the
       return value with the appropriate "const-ness".


--------------------------------------------------------------------
6.6 Inline Functions
--------------------------------------------------------------------

Function inlining is a compile time operation and the full definition of an 
inline function must be seen wherever it is called. Thus, the implementation
of every function to be inlined must be provided in a header file. 

Whether or not a function implemented in a header file is explicitly declared
inline using the "inline" keyword, the compiler decides if the function will 
be inlined. A compiler will not inline a function that it considers too 
long or too complex (e.g., if it contains complicated conditional logic). 
When a compiler inlines a function, it replace the function call with the 
body of the function. Most modern compilers do a good job of deciding when 
inlining is a good choice.

It is possible to specify function attributes and compiler flags that can
force a compiler to inline a function. Such options should be applied with 
care to prevent excessive inlining that may cause executable code bloat and/or 
may make debugging difficult.

**When in doubt, don't use the "inline" keyword and let the compiler decide 
whether to inline a function.**

6.6.1 Simple, short frequently called functions, such as accessors, that will
almost certainly be inlined by most compilers **should** be implemented inline 
in header files.

6.6.2 Class constructors **should not** be inlined. 

      A class constructor implicitly calls the constructors for its base 
      classes and initializes some or all of its data members, potentially 
      calling more constructors. If a constructor is inlined, the construction 
      and initialization needed for its members and bases will appear at every 
      object declaration.

      **Exception:** A class/struct that has only POD ("plain old data") 
      members, is not a subclass, and does not explicitly declare a destructor,
      can have its constructor safely inlined in most cases. 

6.6.3 Virtual functions **must not** be inlined due to polymorphism. 

      For example, do not declare a virtual class member function as::

         virtual void foo( ) { }

      In most circumstances, a virtual method cannot be inlined because a
      compiler must do runtime dispatch on a virtual method when it doesn't 
      know the complete type at compile time.

      **Exception:** It is safe to define an empty destructor inline in an
      abstract base class with no data members.


--------------------------------------------------------------------
6.7 Function and Operator Overloading
--------------------------------------------------------------------

6.7.1 Function overloading **must not** be used to define functions that 
do conceptually different things. 

      Someone reading declarations of overloaded functions should be able to 
      assume (and rightfully so!) that functions with the same name do 
      something very similar.

6.7.2 If an overloaded virtual method in a base class is overridden in a 
derived class, all overloaded methods with the same name in the base class 
**must** be overridden in the derived class. 

      This prevents unexpected behavior when calling such member functions. 
      Remember that when a virtual function is overridden, the overloads of 
      that function in the base class **are not visible** to the derived class.

6.7.3 Operator overloading **must not** be used to be clever to the point of 
obfuscation and cause others to think too hard about an operation. 
Specifically, an overloaded operator must preserve "natural" semantics 
by appealing to common conventions and **must** have meaning similar 
to non-overloaded operators of the same name.

      Overloading operators can be beneficial, but **should not** be overused 
      or abused. Operator overloading is essentially "syntactic sugar" and an
      overloaded operator is just a function like any other function. An 
      important benefit of overloading is that it often allows more 
      appropriate syntax that more easily communicates the meaning of an 
      operation. The resulting code can be easier to write, maintain, and 
      understand, and it may be more efficient since it may allow the compiler
      to take advantage of longer expressions than it could otherwise.

6.7.4 Both boolean operators "==" and "!=" **should** be implemented if one 
of them is. 

      For consistency and correctness, the "!=" operator **should** be 
      implemented using the "==" operator implementation. For example::

         bool MyClass::operator!= (const MyClass& rhs)
         {
            return !(this == rhs);
         }

6.7.5 Standard operators, such as "&&", "||", and "," (i.e., comma), 
**must not** be overloaded.

      Built-in versions of these operators are typically treated specially 
      by a compiler. Thus, programmers cannot implement their full semantics. 
      This can cause confusion. For example, the order of operand evaluation 
      cannot be guaranteed when overloading operators "&&" or "||". This may 
      cause problems as someone may write code that assumes that evaluation 
      order is the same as the built-in versions.


--------------------------------------------------------------------
6.8 Casts and Type Conversions
--------------------------------------------------------------------

6.8.1 C-style casts **must not** be used.

      All type conversions **must** be done explicitly using the named C++ 
      casting operators; i.e., "static_cast", "const_cast", "dynamic_cast", 
      "reinterpret_cast".

6.8.2 The "const_cast" operator **should** be avoided. 

       Casting away "const-ness" is usually a poor programming decision and can 
       introduce errors.

       **Exception:** It may be necessary in some circumstances to cast away 
       const-ness, such as when calling const-incorrect APIs.

6.8.3 The "reinterpret_cast" **must not** be used unless absolutely necessary.

       This operator was designed to perform a low-level reinterpretation of 
       the bit pattern of an operand. This is needed only in special 
       circumstances and circumvents type safety.

6.8.4  A class constructor that takes a single *non-default* argument, or a 
single argument with a *default* value, **must** be declared"explicit".

       This prevents compilers from performing unexpected (and, in many
       cases, unwanted!) implicit type conversions. For example::

          class MyClass
          {
          public:
             explicit MyClass(int i, double x = 0.0);
          };

       Note that, without the explicit declaration, an implicit conversion 
       from an integer to an object of type MyClass could be allowed. For 
       example::

          MyClass mc = 2;

       Clearly, this is confusing. The "explicit" keyword forces the 
       following usage pattern::

          MyClass mc(2);

       to get the same result, which is much more clear.


--------------------------------------------------------------------
6.9 Enumerations
--------------------------------------------------------------------

6.9.1 An enumeration type **should** be used instead of macro definitions 
or "int" data for sets of related constant values. 

      Since C++ enums are distinct types with a compile-time specified set of 
      values, there values cannot be implicitly cast to integers or 
      vice versa -- a "static_cast" operator must be used to make the 
      conversion explicit. Thus, enums provide type and value safety and 
      scoping benefits.

      In many cases, the C++11 `enum class` construct **should** be used 
      since it provides stronger type safety and better scoping than regular
      enum types.


=====================================
7 Miscellaneous Code Formatting
=====================================

--------------------------------------------------------------------
7.1 Conditional statements and loops
--------------------------------------------------------------------

7.1.1 Curly braces **should** be used in all conditionals, loops, etc. 
even when the content inside the braces is a "one-liner". 

       This helps prevent coding errors and misinterpretation of intent. 
       For example, this::

          if (done) { ... }

       is preferable to this::

          if (done) ...

7.1.2 One-liners **may** not be used for "if" conditionals with 
"else/else if"  clauses when the resulting code is clear. 

       For example, either of the following styles **may** be used::

          if (done) {
             id = 3;
          } else {
             id = 0;
          }

       or::

          if (done) { id = 3; } else { id = 0; }

7.1.3 Complex "if/else if" conditionals with many "else if" clauses 
**should** be avoided.

      Such statements can always be refactored using local boolean variables 
      or "switch" statements. Doing so often makes code easier to read and 
      understand and may improve performance.

7.1.4 An explicit test for zero/nonzero **must** be used in a conditional 
unless the tested quantity is a boolean or pointer type. 

      For example, a conditional based on an integer value should use::

         if (num_lines != 0) {

      not::

         if (num_lines) {


--------------------------------------------------------------------
7.2 White Space and Code Alignment
--------------------------------------------------------------------

Most conventions for indentation, spacing and code alignment 
preferred by the RAJA team are enforced by using the `clang-format` tool. 
It can be run from the top-level RAJA directory using a python script 
in the scripts directory; i.e.,::

   $ ./scripts/clang-format-all.py

The format options are defined in the file `.clang-format` in the top-level
RAJA directory. 

Not all preferred formatting conventions are supported by the clang format 
tool. The following guidelines provide additional recommendations to make
code easier to read and understand.

7.2.1 Blank lines and indentation **should** be used throughout code to 
enhance readability. 

      Examples of helpful white space include:

         * Between operands and operators in arithmetic expressions.
         * After reserved words, such as "while", "for", "if", "switch", etc. 
           and before the parenthesis or curly brace that follows.
         * After commas separating arguments in functions.
         * After semi-colons in for-loop expressions.
         * Before and after curly braces in almost all cases.

7.2.2 White space **must not** appear between a function name and the opening 
parenthesis to the argument list. In particular, if a function call is broken 
across source lines, the break **must not** come between the function name and 
the opening parenthesis.

7.2.3 Tabs **must not** be used for indentation since this can be problematic 
for developers with different text editor settings.

7.2.4 When function arguments (in either a declaration or implementation)
appear on multiple lines, the arguments **should** be aligned vertically 
for readability.

7.2.5 All statements within a function body **should** be indented within the surrounding curly braces.

7.2.6 All source lines in the same scope **should** be aligned vertically.
Continuation of previous lines **may** be indented if it make the code easier
to read.

7.2.7 When a line is broken at a comma or semi-colon, it **must** be broken 
after the comma or semi-colon, not before. 

7.2.8 When a source line is broken at an arithmetic operator 
(i.e., , -, etc.), it **should** be broken after the operator, not before. 

7.2.9 Parentheses **should** be used in non-trivial mathematical and logical 
expressions to clearly indicate structure and intended order of operations. 

      Do not assume everyone who looks at the code knows all the rules for 
      operator precedence.


.. _portsec-label: 

===================================================
8 Portability, Compilation, and Dependencies
===================================================

--------------------------------------------------------------------
8.1 Portability
--------------------------------------------------------------------

8.1.1 C++ language features beyond standard C++11 **must not** be used unless
reviewed by the team and verified that the features are supported by all 
compilers we need to support.

      Changing this guideline requires full con census of all team members.

8.1.2 Special non-standard language constructs, such as GNU extensions, 
**must not** be used if they hinder portability.


--------------------------------------------------------------------
8.2 Compilation
--------------------------------------------------------------------

8.2.3 Excessive use of the preprocessor for conditional compilation at a 
fine granularity (e.g., selectively including or removing individual source 
lines) **should** be avoided. 

      While it may seem convenient, this practice typically produces confusing 
      and error-prone code. Often, it is better to refactor the code into 
      separate routines or large code blocks subject to conditional compilation
      where it is more clear. 

      Code reviews by team members will dictate what is/is not acceptable.

8.2.4 Developers **should** rely on compile-time and link-time errors to 
check for code correctness and invariants. 

      Errors that occur at run-time and which depend on specific control flow 
      and program state are inconvenient for users and can be difficult to 
      detect and fix.

      Add some specific guidance here on how this should be done...

--------------------------------------------------------------------
8.3 Dependencies
--------------------------------------------------------------------

8.3.1 RAJA **should** only require a C++11 standard-complaint compiler and
the parallel programming model backends it encapsulates. Support for those
models should be provided by compilers, associated libraries, and runtimes.



.. _codingrefs-label:

======================================
References and useful resources
======================================

Most of the guidelines here were gathered from the following list sources. 
The list contains a variety of useful resources for programming in C++
beyond what is presented in these guidelines.

#. *The Chromium Projects: C++ Dos and Don'ts*. https://www.chromium.org/developers/coding-style/cpp-dos-and-donts

#. Dewhurst, S., *C++ Gotchas: Avoiding Common Problems in Coding and Design*, Addison-Wesley, 2003.

#. Dewhurst S., *C++ Common Knowledge: Essential Intermediate Programming*, Addison-Wesley, 2005.

#. *Doxygen manual*, http://www.stack.nl/~dimitri/doxygen/manual/index.html

#. *Google C++ Style Guide*, https://google-styleguide.googlecode.com/svn/trunk/cppguide.html

#. *ISO/IEC 14882:2011 C++ Programming Language Standard*.

#. Josuttis, N., *The C++ Standard Library: A Tutorial and Reference, Second Edition*, Addison-Wesley, 2012.

#. Meyers, S., *More Effective C++: 35 New Ways to Improve Your Programs and Designs*, Addison-Wesley, 1996.

#. Meyers, S., *Effective STL: 50 Specific Ways to Improve Your Use of the Standard Template Library*, Addison-Wesley, 2001.

#. Meyers, S., *Effective C++: 55 Specific Ways to Improve Your Programs and Designs (3rd Edition)*, Addison-Wesley, 2005.

#. Meyers, S., *Effective Modern C++: 42 Specific Ways to Improve Your Use of C++11 and C++14*, O'Reilly.

#. Programming Research Ltd., *High-integrity C++ Coding Standard, Version 4.0*, 2013.

#. Sutter, H. and A. Alexandrescu, *C++ Coding Standards: 101 Rules, Guidelines, and Best Practices*, Addison-Wesley, 2005.
