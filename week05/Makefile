TARGET_EXEC := week05
TARGET_TEST_EXEC := test_runner

BUILD_DIR := build
SRC_DIR := src
TEST_SRC_DIR := test

SRCS := $(shell find $(SRC_DIR) -name '*.cpp' -not -path src/combined.cpp)
OBJS := $(SRCS:%=$(BUILD_DIR)/%.o)
SRCS_NO_MAIN := $(shell find $(SRC_DIR) -name '*.cpp' -not -path src/main.cpp -not -path src/combined.cpp)
OBJS_NO_MAIN := $(SRCS_NO_MAIN:%=$(BUILD_DIR)/%.o)
TEST_SRCS := $(shell find $(TEST_SRC_DIR) -name 'test-*.cpp')
TEST_OBJS := $(TEST_SRCS:%=$(BUILD_DIR)/%.o)

INC_DIRS := $(shell find $(SRC_DIR) -type d)
INC_FLAGS := $(addprefix -I,$(INC_DIRS)) -Ilib
CPPFLAGS := $(INC_FLAGS) -std=c++11

$(BUILD_DIR)/$(TARGET_EXEC): $(OBJS)
	$(CXX) -g $(OBJS) -o $@

$(BUILD_DIR)/$(TARGET_TEST_EXEC): $(TEST_OBJS) $(OBJS_NO_MAIN)
	$(CXX) -g $(TEST_OBJS) $(OBJS_NO_MAIN) -o $@

$(BUILD_DIR)/%.cpp.o: %.cpp
	mkdir -p $(dir $@)
	$(CXX) $(CPPFLAGS) -g -c $< -o $@

all : $(BUILD_DIR)/$(TARGET_EXEC)

test: $(BUILD_DIR)/$(TARGET_TEST_EXEC)
	$(BUILD_DIR)/$(TARGET_TEST_EXEC)

.PHONY: clean
clean :
	rm -rf build/*