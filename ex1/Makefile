# compiler:
CC = g++

# compiler flags:
CFLAGS = -std=c++11 -O3
LIBS = 

# target executable to build:
TARGET = ex1

# data file to read:
DATA = ex1.dat

# path of cppcheck:
CPPCHECKPATH = ./

# flags to use for cppcheck:
CPPCHECKFLAGS = --enable=all --inconclusive --std=posix --check-config

all: $(TARGET)
$(TARGET): $(TARGET).cxx
	$(CC) $(CFLAGS) $(TARGET).cxx -o $(TARGET) $(LIBS)

doc: 
	doxygen -g
	doxygen Doxyfile
	sed -i 's/PROJECT_NAME.*=.*/$/PROJECT_NAME = "Exercise 1"/' Doxyfile
	sed -i 's/EXTRACT_ALL.*=.*/$/EXTRACT_ALL = YES/' Doxyfile
	sed -i 's/EXTRACT_PRIVATE.*=.*/$/EXTRACT_PRIVATE = YES/' Doxyfile
	# if more than one doxygen-readable file is present in directory:
	(cat Doxyfile; echo "INPUT = $(TARGET).cxx") | doxygen - 
	# otherwise:
	# doxygen Doxyfile

coverage:
	$(CC) $(CFLAGS) --coverage $(TARGET).cxx -o $(TARGET) $(LIBS)
	mkdir -p gcov
	./$(TARGET) $(DATA)
	mv $(TARGET).gcno $(TARGET).gcda gcov
	lcov -t "result" -o result.info -c -d gcov
	genhtml -o result result.info

check:
	# if cppcheck binary is in the same folder as source file:
	#./cppcheck $(CPPCHECKFLAGS) $(TARGET).cxx
	# otherwise, if cppcheck is an installed library:
	cppcheck $(CPPCHECKFLAGS) $(TARGET).cxx

clean:
	$(RM) $(TARGET)
	
.PHONY: all doc coverage check clean

