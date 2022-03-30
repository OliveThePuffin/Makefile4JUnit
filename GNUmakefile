# Filepath Variables
SRC := $(wildcard src/*/*.java) $(wildcard src/*.java)
OUT := bin
LIB := lib

# Runtime tests and class to execute
TEST_DIR := tests
MAIN_CLASS := main.Main


# Compiler and Runtime Args
JC_FLAGS = -g -d $(OUT) -cp $(JUNIT):$(OUT)
JC = javac

J_FLAGS = -cp $(OUT)
JUNIT_FLAGS = -n "$(TEST_DIR).*" --scan-classpath
J = java


# JUnit variables (For scraping the library online)
JUnit.ver  := 1.8.2
JUnit.mod  := junit-platform-console-standalone
JUnit.jar  := $(JUnit.mod)-$(JUnit.ver).jar
Maven.http := https://repo1.maven.org/maven2/org/junit/platform/$(JUnit.mod)
JUnit.mvn  := $(Maven.http)/$(JUnit.ver)/$(JUnit.jar)
JUNIT      := $(LIB)/$(JUnit.jar)


# Compiler rules
LIST := $(SRC:src/%.java=$(OUT)/%.class)

.PHONY: all exec test clean cleanall

all: $(JUNIT) $(LIST)

exec: all
	@echo "---------------------- PROGRAM START -----------------------"
	@$J $(J_FLAGS) $(OUT) $(MAIN_CLASS)
	@echo "-------------------- PROGRAM TERMINATED --------------------"

test: all
	@echo "------------------------ TEST START ------------------------"
	$J -jar $(JUNIT) $(J_FLAGS) $(JUNIT_FLAGS)
	@echo "---------------------- TEST TERMINATED ---------------------"

$(JUNIT): | $(LIB)
	curl -s -z $(JUNIT) \
		-o $(JUNIT) \
		$(JUnit.mvn)

$(OUT)/%.class: src/%.java
	$(JC) $(JC_FLAGS) $(SRC)

$(OUT):
	@mkdir $@

$(LIB):
	@mkdir $@

clean:
	$(RM) -r $(OUT)

cleanall: clean
	$(RM) -r $(LIB)
