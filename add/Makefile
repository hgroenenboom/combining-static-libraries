all: build example

build:
	# Compile all object files
	g++ src/add.cpp -c -I./include

	# Create library file
	ar rvs ./lib/libadd.a ./add.o
	
	rm ./*.o

example: build
	g++ example/exampleAdd.cpp -o add -I./include -L./lib -lAdd
	./add

clean:
	rm ./lib/* -f
	rm ./add* -f
	rm ./*.o -f
