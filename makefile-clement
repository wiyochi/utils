SRCDIR := src
BUILDDIR := build
TARGET := bin/run.out
 
SRCEXT := cpp
SOURCES := $(shell find $(SRCDIR) -type f -name *.$(SRCEXT))
OBJECTS := $(patsubst $(SRCDIR)/%,$(BUILDDIR)/%,$(SOURCES:.$(SRCEXT)=.o))

UNAME_S := $(shell uname)

CFLAGS := -g3 -O0 -Wall -Wextra

ifeq ($(UNAME_S), Linux)
CC := g++ -std=c++17
LIBPATHS := -L./lib/SFML-2.5.1/lib
LIBFLAGS := -lsfml-graphics -lsfml-window -lsfml-system -lsfml-audio
INC := -Iinclude/ -I./lib/SFML-2.5.1/include
endif

ifeq ($(UNAME_S), Darwin)
CC := clang++ -std=c++17
LIBPATHS := -F./lib/SFML-2.5.1-macos/Frameworks
LIBFLAGS := -framework sfml-graphics -framework sfml-window -framework sfml-system -framework sfml-audio -rpath ./lib/SFML-2.5.1-macos/Frameworks
INC := -Iinclude/
endif

$(TARGET): $(OBJECTS)
	@mkdir -p bin
	$(CC) $^ -o $(TARGET) $(LIBPATHS) $(LIBFLAGS)

$(BUILDDIR)/%.o: $(SRCDIR)/%.$(SRCEXT)
	@mkdir -p $(dir $@)
	$(CC) $(CFLAGS) $(INC) -c -o $@ $<

# Cleaning
clean:
	@rm -rf $(BUILDDIR) $(TARGET)

# Running
run:
ifeq ($(UNAME_S), Linux)
	@export LD_LIBRARY_PATH=$$LD_LIBRARY_PATH:./lib/SFML-2.5.1/lib; ./$(TARGET)
endif

ifeq ($(UNAME_S), Darwin)
	@./$(TARGET)
endif

.PHONY: clean