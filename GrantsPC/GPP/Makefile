#Generic Makefile
#Grant Wagner 20100602
#Derived from http://www.cs.colby.edu/maxwell/courses/tutorials/maketutor/

#All referenced paths
BDIR=$(realpath ./)
SDIR=$(BDIR)/src
ODIR=$(BDIR)/obj
LDIR=$(BDIR)/lib
IDIR=$(BDIR)/include

#Compiler and options
#application name, this is the file name of the generated executable
APP=g
#the compiler to use
CC=g++
#the file extension of the source files.
SRC=cpp
#the file extension of the include files.
INCLUDE=hpp

#General uptions
CFLAGS=-I$(IDIR) -Wall -Werror -std=c++11
LIBS=-lm

#Libraries, comment out to add to current build.
# sdl for windows
#CFLAGS+=-I${prefix}/include/SDL -D_GNU_SOURCE=1 -Dmain=SDL_main
#LIBS+=-lmingw32 -lSDLmain -lSDL  -mwindows
# sdl CFLAGS for linux
#CFLAGS+=`sdl2-config --cflags`
#LIBS+=`sdl2-config --libs`
# ncurses
#LIBS+=-lncurses

#If Debugging
CFLAGS+=-g
#else optimize
#CFLAGS+=-O3

#search for files
INCLUDES = $(shell find $(IDIR) -name '*.$(INCLUDE)')
SRCS = $(shell find $(SDIR) -name '*.$(SRC)')
OBJS = $(patsubst $(SDIR)/%.$(SRC),$(ODIR)/%.o,$(SRCS))

#Building Rules
all: $(APP)

#Generic object from source
$(ODIR)/%.o: $(SDIR)/%.$(SRC)
	@echo Compiling $<
	@mkdir -p $(dir $@)
	@$(CC) -c -o $@ $< $(CFLAGS)

#Application from objects
$(APP): $(OBJS)
	@echo Linking to create application
	@$(CC) -o $@ $^ $(CFLAGS) $(LIBS)


#cleaner
.PHONY: clean format

format:
	uncrustify -c proj/geany/uncrustify.cfg --no-backup ${SRCS} $(INCLUDES)

clean:
	rm -rf $(ODIR) core $(APP)
