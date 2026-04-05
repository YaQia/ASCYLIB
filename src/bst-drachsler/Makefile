ROOT = ../..

include $(ROOT)/common/Makefile.common

ifeq ($(RO_FAIL),0)
	CFLAGS += -DRO_FAIL=0
	SUFFIX = _no_ro
else
	CFLAGS += -DRO_FAIL=1
endif

BINS  = $(BINDIR)/lb-bst-drachsler$(SUFFIX)
PROF = $(ROOT)/src

.PHONY:	all clean

all:	main

measurements.o:
	$(CC) $(CFLAGS) -c -o $(BUILDIR)/measurements.o $(PROF)/measurements.c

ssalloc.o:
	$(CC) $(CFLAGS) -c -o $(BUILDIR)/ssalloc.o $(PROF)/ssalloc.c

htlock.o:
	$(CC) $(CFLAGS) -c -o $(BUILDIR)/htlock.o $(PROF)/htlock.c

clh.o:
	$(CC) $(CFLAGS) -c -o $(BUILDIR)/clh.o $(PROF)/clh.c

bst-drachsler.o: 
	$(CC) $(CFLAGS) -c -o $(BUILDIR)/bst-drachsler.o bst-drachsler.c

test.o: bst-drachsler.h
	$(CC) $(CFLAGS) -c -o $(BUILDIR)/test.o $(TEST_FILE)

main: measurements.o ssalloc.o htlock.o clh.o bst-drachsler.o test.o 
	$(CC) $(CFLAGS) $(BUILDIR)/measurements.o $(BUILDIR)/ssalloc.o $(BUILDIR)/htlock.o $(BUILDIR)/clh.o $(BUILDIR)/bst-drachsler.o  $(BUILDIR)/test.o -o $(BINS) $(LDFLAGS)


clean:
	rm -f $(BINS)
