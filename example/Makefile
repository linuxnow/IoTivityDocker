###########################################################################
# Makefile for Thermostat
###########################################################################

# Used for internal functionality macros. Feel free to rename. Need to
#   replace this with an autoconf script which I haven't yet learned how to
#   write.

OPTIMIZATION       = -O0 -g
C_STANDARD         = gnu99
CPP_STANDARD       = gnu++11


# Environmental awareness...
###########################################################################
SHELL        = /bin/sh
WHERE_I_AM   = $(shell pwd)

export CXX   = $(shell which g++)
export CC    = $(shell which gcc)


###########################################################################
# Source files, includes, and linker directives...
###########################################################################
INCLUDES    = -I$(WHERE_I_AM)/. -I/usr/include/resource/
INCLUDES   += -I/usr/include/service/resource-encapsulation/


# Libraries to link
LIBS  = -lstdc++ -lm -lpthread -ldl
LIBS += -lc_common
#LIBS += -llogger
#LIBS += -lcoap
#LIBS += -locsrm
LIBS += -loctbstack
LIBS += -lrcs_common
#LIBS += -lrcs_container
LIBS += -lrcs_server
#LIBS += -lrcs_client
#LIBS += -ltinydtls
#LIBS += -lresource_hosting -ltimer
#LIBS += -lplugin_interface
LIBS += -lconnectivity_abstraction
#LIBS += -lroutingmanager
#LIBS += -lscene_manager
#LIBS += -lTGMSDKLibrary
#LIBS += -lYamlParser

# These are for shared library builds...
LIBS += -loc_logger
LIBS += -loc


# Wrap the include paths into the flags...
CFLAGS  = $(OPTIMIZATION) -Wall $(INCLUDES) -DSECURED=1 -DTARGET_OS=linux
CFLAGS += -Wdouble-promotion -frtti -fexceptions


###########################################################################
# Source file definitions...
###########################################################################
SRCS   = Thermostat.cpp

export CFLAGS
export CPP_FLAGS = $(CFLAGS)


###########################################################################
# Rules for building the Thermostat follow...
###########################################################################

.PHONY: all


all: clean
	$(CXX) -o Thermostat $(SRCS) $(CFLAGS) -std=$(CPP_STANDARD) $(LIBS) -D_GNU_SOURCE -O2

clean:
	rm -f *.o *.su Thermostat
