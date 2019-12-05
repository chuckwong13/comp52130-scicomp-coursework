# These flags are for GCC (clang/intel) may need different ones
include cflags.mk

LDFLAGS = -lm
CC = gcc-9

OBJ = optimised-gemm.o

.PHONY: check clean help

all: gemm

help:
	@echo "Available targets are"
	@echo "  clean: Remove all build artifacts"
	@echo "  gemm: Build the gemm binary"
	@echo "  check: Run a simple-minded check of your implementation"

clean:
	-rm -f gemm $(OBJ)

gemm: gemm.c $(OBJ)
	$(CC) $(CFLAGS) -o $@ $< $(OBJ) $(LDFLAGS)

optimised-gemm.o: optimised-gemm.c parameters.h cflags.mk
	$(CC) $(CFLAGS) -c -o $@ $<

check: gemm
	./gemm 10 15 21 CHECK

bench: gemm
	for n in $$(seq $(BENCH_MIN) $(BENCH_STEP) $(BENCH_MAX)); do \
          ./gemm $$n $$n $$n BENCH; \
        done > $(BENCH_OUTPUT)