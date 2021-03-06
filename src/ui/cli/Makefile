# Baby Makefile for Linux
#

SRC         = main.cpp

COREPATH        = ../../core
OSPATH          = ../../os
LIBPATH         = ../../../lib/unicodedebug
OBJPATH         = ../../../obj/unicodedebug/cli
BINPATH         = .

#destination related macros
OBJ	 = $(addprefix $(OBJPATH)/,$(subst .cpp,.o,$(SRC)))
EXE	    = $(BINPATH)/pwsafe

LIBCORE	= $(LIBPATH)/libcore.a
LIBOS  	= $(LIBPATH)/libos.a
LIBS    = $(LIBCORE) $(LIBOS)

export CPPFLAGS += -std=c++11

XERCESCPPFLAGS=-DUSE_XML_LIBRARY=XERCES -DWCHAR_INCOMPATIBLE_XMLCH
CXXFLAGS += $(CPPFLAGS) -Wall -I$(COREPATH) -I../.. $(XERCESCPPFLAGS) -DUNICODE

# rules
.PHONY: all clean deepclean setup

$(OBJPATH)/%.o : %.c
	$(CC) -g  $(CFLAGS)   -c $< -o $@

$(OBJPATH)/%.o : %.cpp
	$(CXX) -g $(CXXFLAGS) -c $< -o $@

all : setup $(EXE)


$(LIBCORE): 
	$(MAKE) -C $(COREPATH)

$(LIBOS): 
	$(MAKE) -C $(OSPATH)/unix

$(EXE): $(LIBS) $(OBJ)
	$(CXX) -g $(CXXFLAGS) $(filter %.o,$^)  -o $@ $(LD_FLAGS) \
	-L$(LIBPATH) -lcore -los -lcore -luuid -lxerces-c

clean:
	rm -f *~ $(OBJ) $(EXE) $(LIBS) $(DEPENDFILE)

deepclean: clean
	$(MAKE) -C $(COREPATH) clean

setup:
	@mkdir -p $(OBJPATH) $(BINPATH)
