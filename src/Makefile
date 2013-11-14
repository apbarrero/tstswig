SHELL = /bin/sh
CXX    = g++
FLAGS        = -I. -I/usr/lib/perl5/5.10.0/i586-linux-thread-multi/CORE/
CXXFLAGS       = -D_REENTRANT -D_GNU_SOURCE -DPERL_USE_SAFE_PUTENV -DDEBUGGING -fno-strict-aliasing -pipe -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64 -march=i586 -mtune=i686 -fmessage-length=0 -O2 -Wall -D_FORTIFY_SOURCE=2 -fstack-protector -funwind-tables -fasynchronous-unwind-tables -g -Wall -pipe -fPIC
LDFLAGS     = -shared
DEBUGFLAGS   = -O0 -D _DEBUG
RELEASEFLAGS = -O2 -D NDEBUG -combine -fwhole-program

SWIG = swig
SWIGFLAGS = -c++ -perl5
SWIG_SOURCES = perlcpp.i
SWIG_CXX_OUTPUT = $(SWIG_SOURCES:.i=_wrap.cxx)
SWIG_OUTPUT = $(SWIG_CXX_OUTPUT) $(SWIG_SOURCES:.i=.pm)

TARGET  = libperlcpp.so
SOURCES = perlcpp.cxx $(SWIG_CXX_OUTPUT)
HEADERS = perlcpp.h
OBJECTS = $(SOURCES:.cxx=.o)

PREFIX = $(shell pwd)
BINDIR = $(PREFIX)/../bin

all: $(TARGET)

debug:
	@echo "SWIG_OUTPUT: $(SWIG_OUTPUT)"
	@echo "SOURCES: $(SOURCES)"
	@echo "OBJECTS: $(OBJECTS)"

%_wrap.cxx: %.i
	$(SWIG) $(SWIGFLAGS) $<

%.o: %.cxx
	$(CXX) $(FLAGS) $(CXXFLAGS) $(DEBUGFLAGS) -c $<

$(TARGET): $(OBJECTS) $(HEADERS)
	$(CXX) $(FLAGS) $(CXXFLAGS) $(LDFLAGS) $(DEBUGFLAGS) -o $(TARGET) $(OBJECTS)

.PHONY: clean
clean:
	rm -f $(TARGET) $(OBJECTS) $(SWIG_OUTPUT)
