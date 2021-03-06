DEBUG=1
CFLAGS= -Wall -Wextra -pedantic
CFLAGSPEDANTIC= -Wfloat-equal -Wundef -Wshadow -Wpointer-arith -Wwrite-strings -Wunreachable-code -Winit-self -fsanitize=address
COMMONFLAGS= -Os
CC=gcc

ifeq (${DEBUG},1)
	COMPILE=${CC} ${CFLAGS} ${CFLAGSPEDANTIC} ${COMMONFLAGS}
else
	COMPILE=${CC} ${COMMONFLAGS}
endif

gram: main.o bars.o editor.o buffer.o utils.o
	${COMPILE} -o gram main.o bars.o editor.o buffer.o utils.o -lc
main.o: main.c editor.h bars.h buffer.h
	${COMPILE} -c main.c
bars.o: bars.c bars.h editor.h
	${COMPILE} -c bars.c  
editor.o: editor.c editor.h
	${COMPILE} -c editor.c  
buffer.o: buffer.c buffer.h editor.h
	${COMPILE} -c buffer.c
utils.o: utils.c utils.h
	${COMPILE} -c utils.c

.PHONY: clean

clean:
	@rm -f gram *.o

# Flags info - disable them for build?
# -Wfloat-equal: useful because usually testing floating-point numbers for equality is bad.
# -Wundef: warn if an uninitialized identifier is evaluated in an #if directive.
# -Wshadow: warn whenever a local variable shadows another local variable, parameter or global variable or whenever a built-in function is shadowed.
# -Wpointer-arith: warn if anything depends upon the size of a function or of void.
# -Wwrite-strings: give string constants the type const char[length] so that copying the address of one into a non-const char * pointer will get a warning.
# -Wunreachable-code: warn if the compiler detects that code will never be executed*.
# -Winit-self: (C, C++, Objective-C and Objective-C++ only)
# Warn about uninitialized variables that are initialized with themselves.
# -fsanitize=address and so on) can be great debugging tools, but they can have unforeseen consequences when used in production builds for long-term use across multiple operating system versions.