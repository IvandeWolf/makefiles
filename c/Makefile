# File names
PROGNAME = main
SRCFILES = main.c

# Argument when running the script
RUNARGS =

# Which compiler to use
CC = gcc

# Flags for the program
WARNFLAGS = -Wpedantic -Wall -Wextra -Wformat=2 -Wsign-conversion \
	-Wswitch-enum -Wno-switch-default -Wunused -Wfloat-equal -Wconversion \
	-Wpointer-arith -Wtype-limits -Wcast-qual -Wenum-compare \
	-Wsizeof-pointer-memaccess -Wstrict-prototypes
CFLAGS = -std=c11 -g3 -O2 $(WARNFLAGS)
LFLAGS = -lm -lrt -fsanitize=address

# Do some substitution to get a list of .o files from the given .c files
OBJFILES = $(patsubst %.c,%.o,$(SRCFILES))

.PHONY: all run clean todo

all: $(PROGNAME)

$(PROGNAME): $(OBJFILES)
	$(CC) $(CFLAGS) -o $@ $^ $(LFLAGS)

%.o: %.c
	$(CC) -c $(CFLAGS) -o $@ $<

# Run the program with the given arguments
run: $(PROGNAME)
	./$(PROGNAME) $(RUNARGS)

# List all the todo's
todo:
	-@for file in *.c *.h; do \
		grep -FHnT -e TODO $$file | \
			sed 's/:[ \t]*\/\//: \/\//' | \
			sed 's/:[ \t]*\/\*/: \/\*/'; \
		done; true

# Clean up the directory
clean:
	rm -fv $(PROGNAME) $(OBJFILES)
