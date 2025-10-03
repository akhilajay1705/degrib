SHELL = /bin/sh

top_srcdir = ..

CC = gcc
STRIP = /bin/strip
STRIP_FLAGS = -s
STD_FLAGS = -O3 -Wall -fsigned-char -pedantic
DWML_FLAGS = -O3 -Wall -fsigned-char -pedantic
EXEEXT = 
LD_FLAGS = 


STD_DEF = -DSIZEOF_LONG_INT=8    -D_LINUX_ 
STD_INC =  -I../emapf-c -I../degrib-core -I../degrib-core/degrib-lib -I../gd -I../zlib/contrib/minizip -I../zlib

CLOCK_LIB =  -L/usr/lib -lm

DP_LIB =  -L../emapf-c/ -lemapf -L../zlib/contrib/minizip -lminizip -L../zlib -lz -L/usr/lib -lm

DRAWSHP_LIB =  -L../gd/ -lgd -L../libpng -lpng -L../zlib -lz \
          -L../emapf-c/ -lemapf -L/usr/lib -lm
# XML_LIB has to come before zlib.
# Found that gd has to come before tk (on some linux machines)
STD_LIB1 = -L../degrib-core -ldegrib-core -L../emapf-c/ -lemapf \
          -L../jpeg2000/src/libjasper/jpc/.libs/ -ljpc \
          -L../jpeg2000/src/libjasper/base/.libs/ -lbase \
          -L../libpng -lpng -L../zlib/contrib/minizip -lminizip -L../zlib -lz \
           \
          -L/usr/lib -lm
STD_LIB = -L../gd -lgd $(STD_LIB1)

X_LIB = 
DYNAMIC_LIB = -ldl

PRJ_DLL = libdegrib$(TCL_VERSION).so
STUB_LIB = -L../gd -lgd $(X_LIB) $(DYNAMIC_LIB) $(STD_LIB1)

CLOCK_NAME = clock
DP_NAME = degrib_DP
DRAWSHP_NAME = drawshp
PRJ_NAME = degrib
PRJ_A = libdegrib$(TCL_VERSION).a

CFLAGS = $(STD_FLAGS) $(STD_DEF) $(STD_INC)
DWMLFLAGS = $(DWML_FLAGS) $(STD_DEF) $(STD_INC)

############################
# FILES
############################
C_OBJECTS = myutil.o \
            clock.o \
            mymapf.o \
            myerror.o \
            myassert.o \
            tendian.o \
            metaname.o \
            metaparse.o \
            hazard.o \
            weather.o \
            grib1tab.o \
            metaprint.o \
            writeflt.o \
            chain.o \
            writecsv.o \
            writeshp.o \
            writegra.o \
            interp.o \
            inventory.o \
            probe.o \
            userparse.o \
            tdlpack.o \
            degrib1.o \
            degrib2.o \
            pack.o \
            cube.o \
            drawgrib.o \
            commands.o \
            database.o \
            mapini.o \
            drawlib.o \
            genprobe.o \
            solar.o \
            grpprobe.o \
            sector.o \
            writekml.o \
            split.o \
            myzip.o

H_SOURCES = type.h \
            myutil.h \
            clock.h \
            myerror.h \
            myassert.h \
            mymapf.h \
            tendian.h \
            meta.h \
            metaname.h \
            hazard.h \
            weather.h \
            chain.h \
            write.h \
            interp.h \
            inventory.h \
            probe.h \
            userparse.h \
            tdlpack.h \
            degrib1.h \
            degrib2.h \
            pack.h \
            drawgrib.h \
            commands.h \
            database.h \
            mapini.h \
            drawlib.h \
            genprobe.h \
            solar.h \
            grpprobe.h \
            sector.h \
            split.h \
            myzip.h  

CLOCK_OBJECTS = myassert.o \
            myutil.o \
            myerror.o \
            clock.o

DP_OBJECTS = myutil.o \
            clock.o \
            mymapf.o \
            myerror.o \
            myassert.o \
            tendian.o \
            hazard.o \
            weather.o \
            interp.o \
            userparse.o \
            database.o \
            solar.o \
            grpprobe.o \
            sector.o \
            dpgenprobe.o

DRAWSHP_OBJECTS = myassert.o \
            myutil.o \
            tendian.o \
            mapini.o \
            drawlib.o


STUB_OBJECTS = $(C_OBJECTS) \

C_MAIN = cstart.c


CLOCK_MAIN = clockstart.c

DP_MAIN = dpstart.c

DRAWSHP_MAIN = drawshp.c

LIB_DEPENDS = ../emapf-c/libemapf.a ../degrib-core/libdegrib-core.a \
            ../libpng/libpng.a ../zlib/libz.a ../zlib/contrib/minizip/libminizip.a \
            ../jpeg2000/src/libjasper/jpc/.libs/libjpc.a \
            ../jpeg2000/src/libjasper/base/.libs/libbase.a \
            ../gd/libgd.a 

############################
# TARGETS
############################
#all: $(PRJ_NAME) $(CLOCK_NAME) $(DP_NAME) $(DRAWSHP_NAME) $(PRJ_DLL)
all: $(PRJ_NAME) $(CLOCK_NAME) $(DP_NAME) $(DRAWSHP_NAME) 

# In order for PRJ_DLL to work we need to compile with STUB_LIB / STUB_DEF
$(PRJ_DLL): $(STUB_OBJECTS) $(LIB_DEPENDS) $(H_SOURCES)
#	$(CC) -shared $(STUB_OBJECTS) $(STUB_LIB) -o $(PRJ_DLL) \
#         -Wl,--output-def,$(PRJ_NAME).def,--out-implib,$(PRJ_A)
#	$(CC) -shared $(STUB_OBJECTS) $(STUB_LIB) -o $(PRJ_DLL)
	$(CC) -shared $(STUB_OBJECTS) $(STUB_LIB) -o $(PRJ_DLL)
	$(STRIP) $(STRIP_FLAGS) $(PRJ_DLL)

$(PRJ_NAME): $(C_OBJECTS) $(C_MAIN) $(LIB_DEPENDS) $(H_SOURCES)
	$(CC) $(C_MAIN) $(CFLAGS) $(LD_FLAGS) $(C_OBJECTS) $(STD_LIB) -o $(PRJ_NAME)
	$(STRIP) $(STRIP_FLAGS) $(PRJ_NAME)$(EXEEXT)

$(CLOCK_NAME): $(CLOCK_MAIN) $(CLOCK_OBJECTS) $(H_SOURCES)
	$(CC) $(CLOCK_MAIN) $(CFLAGS) $(CLOCK_OBJECTS) $(CLOCK_LIB) -o $(CLOCK_NAME)
	$(STRIP) $(STRIP_FLAGS) $(CLOCK_NAME)$(EXEEXT)

$(DP_NAME): $(DP_OBJECTS) $(DP_MAIN) $(LIB_DEPENDS) $(H_SOURCES)
	$(CC) $(DP_MAIN) $(CFLAGS) $(LD_FLAGS) $(DP_OBJECTS) $(DP_LIB) -o $(DP_NAME)
	$(STRIP) $(STRIP_FLAGS) $(DP_NAME)$(EXEEXT)

$(DRAWSHP_NAME): $(DRAWSHP_MAIN) $(DRAWSHP_OBJECTS) $(H_SOURCES)
	$(CC) $(DRAWSHP_MAIN) $(CFLAGS) $(DRAWSHP_OBJECTS) $(DRAWSHP_LIB) -o $(DRAWSHP_NAME)
	$(STRIP) $(STRIP_FLAGS) $(DRAWSHP_NAME)$(EXEEXT)


# Note: Absence of TCL_NAME and TK_NAME intentional (so degrib can be built
# and installed without Tcl/Tk).
install: $(PRJ_NAME) $(CLOCK_NAME) $(DP_NAME) $(DRAWSHP_NAME)
	cp $(PRJ_NAME)$(EXEEXT) ../../bin
	cp $(CLOCK_NAME)$(EXEEXT) ../../bin
	cp $(DP_NAME)$(EXEEXT) ../../bin
	cp $(DRAWSHP_NAME)$(EXEEXT) ../../bin

clean:
	rm -f *.o *.bak *.BAK *.obj
	rm -f $(PRJ_NAME)$(EXEEXT)
	rm -f $(CLOCK_NAME)$(EXEEXT)
	rm -f $(DP_NAME)$(EXEEXT)
	rm -f $(DRAWSHP_NAME)$(EXEEXT)

distclean: clean
	rm -r -f Makefile

../dwmllib/libdwml.a:
	@echo "-----------------------------"
	@echo "Attempting to compile dwmllib..."
	(cd ../dwmllib && export CC='$(CC)' && export CFLAGS='$(DWMLFLAGS)' && make -f makefile ARFLAGS=' -ruv')
	@echo "Finished with dwmllib..."
	@echo "-----------------------------"

############################
# SUFFIXES
############################

dpgenprobe.o : $(H_SOURCES) genprobe.c
	$(CC) -c $(CFLAGS) -DDP_ONLY genprobe.c -o dpgenprobe.o

.c.o : $(H_SOURCES)
	$(CC) -c $(CFLAGS) $<

