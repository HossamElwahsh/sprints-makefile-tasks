RM      :=  rm -rf
CC      :=  gcc
CFLAGS  :=  -O1 -Wall #-Werror
LDFLAGS :=  -lm
DISM     =  objdump -d

TARGET   = $(BINDIR)/$(DIRNAME)
SRCS     = $(shell find . -name "*.c" -type f)
HDRS     = $(shell find . -name "*.h" -type f)
#OBJS     = $(SRCS:.c=.o)
OBJS     = $(shell echo $(SRCS) | tr ' ' '\n' | sed -E "s/.*\/(.*).c/$(BUILDDIR)\/\1\.o/" | tr '\n' ' ')
DIRNAME	 = $(shell pwd | sed -E "s/.*\///")
DIR		 = $(shell pwd)

# HELPING FUNS
COMPILE	 = $(CC) $(CFLAGS) -c $(src) -o $(BUILDDIR)/$(shell echo $(src) | sed -E "s/.*\/(.*)\.c/\1.o/") ${\n} 

#OUTPUT PATHS
BINDIR 	 = bin
BUILDDIR = build
#ASMS     = $(SRCS:.c=.s)

test: prebuild 
#	echo $(DIR)
#	echo $(DIRNAME) > bin/test.txt
	echo $(OBJS)
	echo "========= SRCS ==========\n\n"
	echo $(SRCS)

all: prebuild $(TARGET) #$(ASMS)

prebuild: $(BINDIR) $(BUILDDIR)

# prebuild, make dirs
$(BINDIR):
	mkdir -p $@

$(BUILDDIR):
	mkdir -p $@

i: $(OBJS)

# Compile src to objects (Build)
$(OBJS): $(SRCS)
	$(foreach src, $(SRCS), $(COMPILE) &&) echo '\n\n====Building Objects Done====\n\n'
#	$(CC) $(CFLAGS) -c $(SRCS) -o $@

# Link to executable
$(TARGET): $(OBJS)
	$(CC) $(CFLAGS) $(LDFLAGS) -o $@ $^


# DISASSEMPLE EACH COMPILED SRC FILE (.o)
$(ASMS): $(OBJS)
	$(DISM) $< > $@

# DISASSEMPLE EXECUTABLE

$(TARGET).s: $@
	$(DISM) $< > $@


.PHONY: clean

clean:
	$(RM) $(TARGET)
	$(RM) $(OBJS)
	$(RM) $(ASMS)
	$(RM) $(BUILDDIR)
	$(RM) $(BINDIR)
