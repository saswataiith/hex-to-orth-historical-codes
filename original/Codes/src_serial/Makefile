SHELL = /bin/sh

#compops = -g -Wall  
compops =   -O3 -Wall
#compops =  -axT -fast -finline-functions -march=pentium4 -O3 -Ob2 -pc64\
           -funroll-loops -ipo0 -w1 
linkops =  -lfftw3 -lm

# default compiler is gcc

CC = gcc $(compops)

# List of source files

sources = spino5.c get_input_spino2.c init_confv2.c evolve12.c\
        eigen_strain.c calc_bn.c out_conf.c ran1.c gasdev.c nrutil.c 

# List of object files

objects = $(sources:.c=.o) 

# List of header files

headers = binary.h

# 
# c@ current target
# c< source of the current target
all:binorder
binorder: $(objects) $(headers)
	 gcc $(objects) $(linkops) -o binorder 

spino5.o:binary.h
get_input_spino2.o:binary.h
init_confv2.o:binary.h
calc_bn.o:binary.h
eigen_strain.o:binary.h	
evolve11.o:binary.h
out_conf.o:binary.h
ran1.o:binary.h
gasdev.o:binary.h
nrutil.o:binary.h
# To remove the intermediate object files

clean:
	rm -rf *.o 
install:
	cp binorder /home/saswata/bin/
# End of the makefile
