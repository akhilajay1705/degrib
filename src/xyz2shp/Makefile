SHELL = /bin/sh

top_srcdir = ..

CC = gcc
STRIP = /bin/strip
STRIP_FLAGS = -s
STD_FLAGS = -O3 -Wall -fsigned-char -pedantic
EXEEXT = 

STD_DEF = -DSIZEOF_LONG_INT=8   
STD_INC = 

STD_LIB =  -L/usr/lib/ -lm

PRJ_NAME = xyz2shp

CFLAGS = $(STD_FLAGS) $(STD_DEF) $(STD_INC)
MAINFLAGS = $(CFLAGS) -DPKGVERS=\"2.25\" -DPKGDATE=\"20200921\" -DPKGNAME=\"xyz2shp\"

############################
# FILES
############################
SOURCE = myassert.c \
         allocSprintf.c \
         mywarn.c \
         myopt.c \
			tendian.c \
			myutil.c \
         dbffile.c \
			shpfile.c \
         xyzuser.c

OBJECTS = $(SOURCE:.c=.o)

HEADERS = myassert.h \
          allocSprintf.h \
          mywarn.h \
          myopt.h \
			 tendian.h \
			 myutil.h \
          dbffile.h \
			 shpfile.h \
			 xyzuser.h 

MAIN = xyz2shp.c

LIB_DEPENDS = 

############################
# TARGETS
############################
all: $(PRJ_NAME)

$(PRJ_NAME): $(OBJECTS) $(MAIN) $(LIB_DEPENDS) $(HEADERS)
	$(CC) $(MAIN) $(MAINFLAGS) $(LD_FLAGS) $(OBJECTS) $(STD_LIB) -o $(PRJ_NAME)
	$(STRIP) $(STRIP_FLAGS) $(PRJ_NAME)$(EXEEXT)

install: $(PRJ_NAME)
	cp $(PRJ_NAME)$(EXEEXT) ../../bin

clean:
	rm -f *.o *.bak *.BAK *.obj
	rm -f $(PRJ_NAME)$(EXEEXT)

distclean: clean
	rm -r -f Makefile

# DIST_DIR is usually set by the calling Makefile... Set a default here.
package = degrib-2.25
DIST_DIR = ./$(package)
DISTRIB = $(SOURCE) $(HEADERS) $(MAIN) Makefile.in
dist:
	@if [ ! -d $(DIST_DIR) ]; then mkdir $(DIST_DIR); fi
	@for file in $(DISTRIB); do cp $$file $(DIST_DIR); done

############################
# SUFFIXES
############################
.c.o : $(HEADERS)
	$(CC) -c $(CFLAGS) $<
