CC ?= aarch64-linux-gnu-g++
ARCH := arm64

PWD := $(shell pwd)
BASIC_DIR := $(PWD)/../../../basic
FUNC_DIR := $(PWD)/../../

INC_BASIC_PATH := -I$(BASIC_DIR)/inc
INC_FUNC_PATH := -I$(FUNC_DIR)/inc

INC_DIR := $(INC_BASIC_PATH) $(INC_FUNC_PATH) -I$(PWD)/inc
SRC_DIR := $(PWD)/src
LINK_LIB_DIR := -L$(BASIC_DIR) -L$(FUNC_DIR) -L$(PWD)

CXXFLAGS := -g -Wall -Werror -fno-rtti -std=gnu++11 -D_WORDSIZE=64 $(INC_DIR)
LDFLAGS := $(LINK_LIB_DIR) -lstdc++ -lm

SRCS := $(wildcard $(SRC_DIR)/*.cpp)
OBJS := $(patsubst %.cpp, %.o, $(SRCS))
ASMS := $(patsubst %.cpp, %.s, $(SRCS))
PRES := $(patsubst %.cpp, %.i, $(SRCS))

EXTRA_FLAG := -std=c++14 -fsigned-char -Wall -Wextra -Werror -Wformat=2\
              -Wdate-time -Wfloat-equal -Wswitch-default\
              -Wcast-qual -Wvla -Wundef -Wnon-virtual-dtor -Wdelete-non-virtual-dtor\
              -Woverloaded-virtual -fno-common -Wframe-larger-than=8192
TARGET := mymake

all:$(TARGET)

$(TARGET):$(OBJS)
    @$(CXX) ${EXTRA_FLAG} ${LDFLAGS} -o $@ $^
    @echo "Linked: $@"

# Rule to compile .cpp files to .o object files
$(SRC_DIR)/%.o: $(SRC_DIR)/%.cpp
    @$(CXX) ${CXXFLAGS} ${EXTRA_FLAG} -c $^ -o $@

# Rule to compile .cpp files to .s assembly files
$(SRC_DIR)/%.s: $(SRC_DIR)/%.cpp
    @$(CC) ${CXXFLAGS} ${EXTRA_FLAG} -S $< -o $@

# Rule to preprocess .cpp files to .i files
$(SRC_DIR)/%.i: $(SRC_DIR)/%.cpp
    @$(CC) ${CXXFLAGS} ${EXTRA_FLAG} -E $< -o $@

# Clean rule
clean:
    @find . -name '*.o' -exec rm -rf {} \;
    @rm -rf $(TARGET)
