BUILD_DIR = ../build

USER_OPTIONS = -DCLEAR_BSS_SEGMENT -DISR_DEBUGGING_CODE -DSP2_CONFIG -ggdb
INCLUDES = -I. -I../include

CPP = cpp
CPPFLAGS = $(USER_OPTIONS) -nostdinc -iquote $(INCLUDES)

CC = gcc
CFLAGS = -fno-builtin -Wall -Wstrict-prototypes $(CPPFLAGS)

AS = as
ASFLAGS =

all: clock.o klibc.o klibs.o process.o queue.o scheduler.o \
		 stack.o support.o syscall.o system.o isr_stubs.o sio.o

.SUFFIXES:>-.S .b

.c.s:
	$(CC) $(CFLAGS) -S $*.c

.S.s:
	$(CPP) $(CPPFLAGS) -o $*.s $*.S

.S.o:
	$(CPP) $(CPPFLAGS) -o $*.s $*.S
	$(AS) -o $*.o $*.s -a=$*.lst
	$(RM) -f $*.s

.s.b:
	$(AS) -o $*.o $*.s -a=$*.lst
	$(LD) -Ttext 0x0 -s --oformat binary -e begtext -o $*.b $*.o

.c.o:
	$(CC) $(CFLAGS) -c $*.c

clean:
	rm -f *.nl *.lst *.b *.o *.image *.dis BuildImage Offsets
