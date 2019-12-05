include ../../../include.mk
include ../vsn.mk

APP_NAME   = ec_map_example
APP_DIR    = $(shell dirname $(PWD))
GENET	   = ../../../../../ec_genet
YANG_DIR   = ../../../yang
YANGS	   = $(filter-out %-ann.yang, $(wildcard $(YANG_DIR)/*.yang))
NS_DIR	   = ../ns
NS_FILES   = $(YANGS:$(YANG_DIR)/%.yang=$(NS_DIR)/%.hrl)
ERL_FILES  = $(wildcard *.erl)
HRL_FILES  = $(wildcard *.hrl) $(NS_FILES)
MODULES    = $(ERL_FILES:%.erl=%)
EBIN_FILES = $(MODULES:%=../ebin/%.beam) ../ebin/$(APP_NAME).app

$(NS_DIR)/%.hrl: $(YANG_DIR)/%.yang
	$(COMPILER) --emit-hrl $@ \
		--yangpath $(SYSTEM_DIR)/src/$(SYSTEM)/yang \
		--fail-on-warnings $<

ERLC       = erlc
ERLC_FLAGS := \
	+debug_info \
	-I $(GENET)/src/erlang-lib/ec_genet/include -I $(NS_DIR) \
	-pa $(SYSTEM_DIR)/erlang/econfd/ebin \
	-pa ../../ec_map_example/ebin

# mvolf: turned off errors for no-logging
#	+warnings_as_errors \

APPSCRIPT = '$$vsn=shift; $$mods=""; while(@ARGV){ $$_=shift; s/^([A-Z].*)$$/\'\''$$1\'\''/; $$mods.=", " if $$mods; $$mods .= $$_; } while(<>) { s/%VSN%/$$vsn/; s/%MODULES%/$$mods/; print; }'

all: $(SYSTEM_DIR)/erlang/econfd/ebin $(NS_FILES) $(EBIN_FILES)

clean:
	rm -f $(EBIN_FILES) $(NS_FILES) erl_crash.dump core* *~

../ebin/%.app: %.app.src ../vsn.mk Makefile
	perl -e $(APPSCRIPT) "$(VSN)" $(MODULES) < $< > $@

../ebin/%.beam: %.erl
	$(ERLC) $(ERLC_FLAGS) -o ../ebin $<

$(EBIN_FILES): $(ERL_FILES) $(HRL_FILES)
