
# This is how many seconds of loop memory you want your
# plugin to have available.
SAMPLE_MEMORY = 200

# plugin name
PLUGIN = $(shell basename $(shell pwd) | tr A-Z a-z)
PLUGIN_SO = $(PLUGIN).so

# installation prefix
PREFIX ?= /usr/local

# compiler and linker
CXX ?= g++

# flags
CXXFLAGS += -I. -O3 -Wall -fPIC -DPIC -c -DSAMPLE_MEMORY=$(SAMPLE_MEMORY)
LDFLAGS += -shared -lm
ifneq ($(MACOS),true)
LDFLAGS += -Wl,--no-undefined
endif

# remove command
RM = rm -f

# sources and objects
SRC = $(wildcard src/*.cpp)
OBJ = $(SRC:.cpp=.o)

$(PLUGIN_SO): $(OBJ)
	$(CXX) $(OBJ) $(LDFLAGS) -o $(PLUGIN_SO)

%.o: %.cpp
	$(CXX) $< $(CXXFLAGS) -o $@

clean:
	$(RM) src/*.o $(PLUGIN_SO)

install: $(PLUGIN_SO)
	install -d $(DESTDIR)$(PREFIX)/lib/lv2/$(PLUGIN).lv2/
	install -m 644 $(PLUGIN_SO) src/*.ttl $(DESTDIR)$(PREFIX)/lib/lv2/$(PLUGIN).lv2/
