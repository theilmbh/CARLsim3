##----------------------------------------------------------------------------##
##
##   CARLsim3 CARLsim-ECJ PTI interface examples Makefile
##   -------------------------
##
##   Authors:   Eric Scott <escott8@gmu.edu>
##		Michael Beyeler <mbeyeler@uci.edu>
##              Kristofor Carlson <kdcarlso@uci.edu>
##
##   Institute: Cognitive Anteater Robotics Lab (CARL)
##              Department of Cognitive Sciences
##              University of California, Irvine
##              Irvine, CA, 92697-5100, USA
##
##   Version:   03/04/2017
##
##----------------------------------------------------------------------------##

#------------------------------------------------------------------------------
# Include configuration file
#------------------------------------------------------------------------------

# NOTE: If your CARLsim3 installation does not reside in the default path, make
# sure the environment variable CARLSIM3_INSTALL_DIR is set.
ifneq ($(CARLSIM3_INSTALL_DIR),)
	CARLSIM3_INC_DIR  := $(CARLSIM3_INSTALL_DIR)/inc
else
	CARLSIM3_INC_DIR  := /usr/local/include/carlsim
endif

# include compile flags etc.
include $(CARLSIM3_INC_DIR)/configure.mk

pti_lib_path := $(ECJ_PTI_DIR)/lib/
pti_lib := -lCARLsimPTI
pti_inc_path := $(ECJ_PTI_DIR)/inc/

#------------------------------------------------------------------------------
# Build local variables
#------------------------------------------------------------------------------

cpp_files  := $(wildcard *.cpp)
targets := $(patsubst %.cpp, build/%, $(cpp_files))
obj_files    := $(patsubst %.cpp, obj/%.o, $(cpp_files))

# handled by clean
clean_files := $(obj_files) $(targets)

#------------------------------------------------------------------------------
# Project targets and rules
#------------------------------------------------------------------------------

.PHONY: clean distclean help all
default: all

all: $(targets)

$(targets): build/%: obj/%.o
	@test -d build/ || mkdir -p build/
	$(CXX) $(CARLSIM3_FLG) -I$(pti_inc_path) -L$(pti_lib_path) $< -o $@ $(CARLSIM3_LIB) $(pti_lib)

obj/%.o: %.cpp
	@test -d obj/ || mkdir -p obj/
	echo $(pti_inc_path)
	$(CXX) -c $(CARLSIM3_FLG) $(CXXINCFL) $(CXXFL) -I$(pti_inc_path) $< -o $@

clean:
	$(RM) $(clean_files)

help:
	$(info CARLsim-ECJ PTI examples Makefile options:)
	$(info )
	$(info make	       Compiles all examples)
	$(info make clean	 Cleans out all compiled files)
	$(info make help	  Brings up this message)
