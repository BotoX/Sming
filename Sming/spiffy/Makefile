#
# Makefile for spiffy
#

HOST_CC ?= gcc
HOST_LD ?= gcc

INCDIR := -I../Services/SpifFS -I../third-party/spiffs/src
CFLAGS := -O2 -Wall -Wno-unused-value

ifeq ("$(V)","1")
Q :=
vecho := @true
else
Q := @
vecho := @echo
endif

all: spiffy

%.o: ../Services/SpifFS/%.c
	$(vecho) "CC $<"
	$(Q) $(HOST_CC) $(CFLAGS) $(INCDIR) -c $< -o $@
	
%.o: ../third-party/spiffs/src/%.c
	$(vecho) "CC $<"
	$(Q) $(HOST_CC) $(CFLAGS) $(INCDIR) -c $< -o $@

spiffy.o: spiffy.c
	$(vecho) "CC $<"
	$(Q) $(HOST_CC) $(CFLAGS) $(INCDIR) -c $< -o $@

spiffy: spiffy.o spiffs_cache.o spiffs_nucleus.o spiffs_hydrogen.o spiffs_gc.o spiffs_check.o
	$(vecho) "LD $@"
	$(Q) $(HOST_LD) -o $@ $^

clean:
	$(Q) rm -f *.o
	$(Q) rm -f spiffy spiffy.exe
