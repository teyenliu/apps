#
# Copyright (C) 2013 TeYen Liu
#

TREMA = ../../trema

CC = gcc
AR = ar
RANLIB = ranlib

TREMA_CONFIG = $(shell which trema-config)
ifeq ($(TREMA_CONFIG),)
  TREMA_CONFIG = $(TREMA)/trema-config
endif

CFLAGS = $(shell $(TREMA_CONFIG) --cflags) -std=gnu99 -D_GNU_SOURCE -g -fno-strict-aliasing -Wall -Wextra -Wformat=2 -Wcast-qual -Wcast-align -Wwrite-strings -Wconversion -Wfloat-equal -Wpointer-arith
LDFLAGS = $(shell $(TREMA_CONFIG) --libs)

LIB = libtrema_restapi_manager.a
SRCS = simple_restapi_manager.c librestapi.c mongoose.c
OBJS = $(SRCS:.c=.o)

TARGET = $(LIB)

EXAMPLES = examples

DEPENDS = .depends

.PHONY: all depend clean examples

.SUFFIXES: .c .o

all: depend $(TARGET) examples

$(TARGET): $(OBJS)
	$(AR) -cq $@ $(OBJS)
	$(RANLIB) $@

.c.o:
	$(CC) $(CFLAGS) -c $<

depend:
	$(CC) -MM $(CFLAGS) $(SRCS) > $(DEPENDS)

clean:
	@rm -rf $(DEPENDS) $(OBJS) $(TARGET) *~

examples:
	cd $(EXAMPLES) && $(MAKE)

-include $(DEPENDS)
