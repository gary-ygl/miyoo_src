CHAINPREFIX=/opt/buildroot-bittboy/output/host
CROSS_COMPILE=$(CHAINPREFIX)/bin/arm-miyoo-linux-musleabi-

CC = $(CROSS_COMPILE)gcc
CXX = $(CROSS_COMPILE)g++
SYSROOT     := $(CHAINPREFIX)/arm-miyoo-linux-musleabi/sysroot
SDL_CFLAGS  := $(shell $(SYSROOT)/usr/bin/sdl-config --cflags)

OUTPUTNAME = wolf3d

DEFINES = -DHAVE_STDINT_H -DVERSION_BITTBOY
INCLUDES = -Icommon -Iinclude $(SDL_CFLAGS)
OPT_FLAGS  = -Ofast -fdata-sections -fdata-sections -fno-common -fno-PIC -flto
EXTRA_LDFLAGS = -lasound -lmikmod -lmodplug -Wl,--as-needed -Wl,--gc-sections -flto -s

CFLAGS = $(DEFINES) $(INCLUDES) $(OPT_FLAGS)
CXXFLAGS = $(DEFINES) $(INCLUDES) $(OPT_FLAGS)
LDFLAGS = -Wl,--start-group -lSDL -lSDL_image -lpng -ljpeg -lSDL_mixer -logg -lvorbisidec -lmikmod -lmodplug -lm -pthread -lz -lstdc++ $(EXTRA_LDFLAGS) -Wl,--end-group

# Redream (main engine)
OBJS =  \
	fmopl.cpp \
	id_ca.cpp \
	id_in.cpp \
	id_pm.cpp \
	id_sd.cpp \
	id_us_1.cpp \
	id_vh.cpp \
	id_vl.cpp \
	signon.cpp \
	wl_act1.cpp \
	wl_act2.cpp \
	wl_agent.cpp \
	wl_atmos.cpp \
	wl_cloudsky.cpp \
	wl_debug.cpp \
	wl_draw.cpp \
	wl_floorceiling.cpp \
	wl_game.cpp \
	wl_inter.cpp \
	wl_main.cpp \
	wl_menu.cpp \
	wl_parallax.cpp \
	wl_play.cpp \
	wl_state.cpp \
	wl_text.cpp \
	gp2x.cpp
	
.c.o:
	$(CC) $(CFLAGS) -c -o $@ $< 
	
.cpp.o:
	$(CXX) $(CXXFLAGS) -c -o $@ $< 
	
all: executable

executable : $(OBJS)
	$(CC) -o $(OUTPUTNAME) $(OBJS) $(CFLAGS) $(LDFLAGS)

clean:
	rm $(OBJS) $(OUTPUTNAME)