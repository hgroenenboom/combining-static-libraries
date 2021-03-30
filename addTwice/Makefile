all: build example

buildAdd:
	# Calls the Makefile from the 'add' library to build the libAdd.a file
	cd ../add && mingw32-make.exe 

build: buildAdd
	rm ./lib/* -f

	# Build the object files for this library, using the include files from the 'add' library
	g++ src/addTwice.cpp -c -I./include -I../add/include
	
	# Creating the library: Thin archive (archive pointing to other archives using symlinks)
	# ar rvs ./lib/linked.a ./addTwice.o
	# ar crsT ./lib/libaddTwice.a ./lib/linked.a ../add/lib/libAdd.a
	
	# Creating the library: All object files inside a single archive
	# Extract all object files from libAdd.a
	ar x ../add/lib/libAdd.a
	# Add all object files (from 'add' and 'addTwice') to the new archive, thus eliminating the need for 'add' as a seperate lib!
	ar rvs ./lib/libaddTwice.a *.o 

	rm ./*.o

example: build
	g++ example/exampleAddTwice.cpp -o example -I./include -L./lib -laddTwice 
	./example.exe

clean:
	# Clean the build output from 'add'
	cd ../add && mingw32-make.exe clean

	rm lib/* -rf
	rm *.exe -f
	rm *.o -f
