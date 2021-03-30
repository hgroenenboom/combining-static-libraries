all: run

buildDependencies:
	# Build 'addTwice' using its Makefile. (Also rebuilds 'add' and adds it to its library file)
	cd ../addTwice && $(MAKE)

build: buildDependencies
	# Compile using only the 'addTwice' library, the 'add' library is not necessary anymore
	g++ src/main.cpp -o main.exe -L../addTwice/lib -laddTwice -I../addTwice/include

run: build
	./main.exe

clean:
	# Clean the build output from 'addTwice'. (Also cleans the build output from 'add')
	cd ../addTwice && $(MAKE) clean

	rm ./*.exe -f
