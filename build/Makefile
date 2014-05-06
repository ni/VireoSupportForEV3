VIREO_BASE = $(HOME)/VireoSDK
EV3SOURCES_BASE = $(HOME)/ev3sources-xtended

LMS2012 = $(EV3SOURCES_BASE)/ev3sources/lms2012
DEVKIT = $(EV3SOURCES_BASE)/ev3sources/extra/linux-devkit/arm-none-linux-gnueabi

TARGET = libvireobridge.so

SOURCES = EV3_Input.cpp EV3_Sound.cpp EV3_Output.cpp EV3_Ui.cpp \
          EV3_Entry.cpp EV3_File.cpp EV3_Com.cpp
OBJS = $(SOURCES:%.cpp=%.o)
DEPS = $(OBJS:%.o=%.d)

VIREO_LIB = libvireo.so
INCLUDES = -I$(VIREO_BASE)/source/include \
           -I$(DEVKIT)/usr/include/dbus-1.0 \
           -I$(DEVKIT)/usr/lib/dbus-1.0/include \
           -I$(DEVKIT)/usr/include \
           -I$(LMS2012)/lms2012/source \
           -I$(LMS2012)/c_com/source \
           -I$(LMS2012)/c_input/source \
           -I$(LMS2012)/c_memory/source \
           -I$(LMS2012)/c_output/source \
           -I$(LMS2012)/c_sound/source \
           -I$(LMS2012)/c_ui/source \
           -I$(LMS2012)/c_vireobridge/source \
           -I$(LMS2012)/c_dynload/source

CXX = arm-none-linux-gnueabi-g++
CFLAGS = -DPCASM $(INCLUDES) -Os -Wall -fPIC
LDFLAGS = -shared -L$(VIREO_BASE)/make-it \
          -lvireo -Wl,-rpath=/home/root/lms2012/3rdparty-vm

.DEFAULT_GOAL := $(TARGET)

%.o: ../source/%.cpp
	$(CXX) $(CFLAGS) -c -MMD -MP -o $@ $<

$(VIREO_LIB): $(VIREO_BASE)
	make -C $(VIREO_BASE)/make-it lARMv5
	cp $(VIREO_BASE)/make-it/$@ .

$(TARGET): $(VIREO_LIB) $(OBJS)
	$(CXX) $(LDFLAGS) -o $@ $(OBJS)

clean:
	rm -f $(OBJS) $(DEPS) $(TARGET) $(VIREO_LIB)

.PHONY: clean

-include $(DEPS)

