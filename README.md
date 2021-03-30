# combining-static-libraries
In this simple repository multiple static C++ libraries are combined into one big static library file. In this way we can create static libraries which internally use a lot of libraries themselves. The end user won't have to be bothered by a gigantic amount of library files, but can instead just link one! This also hides some unnecessary information from the end-user 

### Motivation
When working with 3rd party C++ libraries, it can get very annoying to work with lots of library files and include directories. In order to reduce this management overhead I investigate a simple method for combining multiple static libraries into one. The end user then only needs to add the include files from one library.

To summarize the major benefits:
- No more complex linking for 3rd party libraries
- 3rd party libraries used can be obfiscated from the exposed headers for security/privacy reasons.

### How do we do this?
Source: [stackoverflow](https://stackoverflow.com/questions/2157629/linking-static-libraries-to-other-static-libraries)

Using the GCC `ar` tool we can obtain all object files from an existing archive, and rebundle all these extracted object files back into a single archive. 

### How to use
This repository aims to show an as simple as possible example to make this work and to help anyone else understand how this process works.

There are 3 main folders:
- `add` - This is the '3rd-party' library, it simply contains a function for adding two integers (`int add(int,int)`). The end-user doesn't need to know about this function.
- `addTwice` - This is the final library which consumes 'add'. It exposes an addTwice functions which adds an integer to another integer twice. (`int addTwice(int,int)`)
- `main` - This is our product code where we use `int addTwice(int, int)`. Here we only have to link 'addTwice' once addTwice is build.

For ease of use the Makefiles inside each folder are structured in such a way that calling `make` from inside 'main' will also create all libraries. To understand more about the steps required in this process investigate the source files and the Makefiles in these 3 folders.

### tldr
`cd ./main && make`
