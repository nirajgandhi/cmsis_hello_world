
#export PATH="/opt/NXP/S32DS.3.2/S32DS/build_tools/gcc_b1620/gcc-6.3-arm32-eabi/bin:$PATH"
#TOOLPATH = /home/nirajg/toolchain/gcc-arm-none-eabi-5_4-2016q3/bin
TOOLPATH = /home/nirajg/toolchain/gcc-arm-none-eabi-8-2019-q3-update/bin
WORKAREA=/home/nirajg/cmsis
CMSIS_CORE = $(WORKAREA)/CMSIS_5/CMSIS/Core
CMSIS_DIR=$(WORKAREA)/CMSIS_5/Device/ARM/ARMCM7
LINK_DIR=$(CMSIS_DIR)/Source/GCC
INCLUDE_HEADERS = -I$(CMSIS_DIR)/Include -I$(CMSIS_CORE)/Include

# Specify the compiler to use
CC=$(TOOLPATH)/arm-none-eabi-gcc
#CC=aarch64-none-elf-gcc

# Specify the assembler to use
AS=$(TOOLPATH)/arm-none-eabi-as
#AS=aarch64-none-elf-as

# Specity the linker to use
LD=$(TOOLPATH)/arm-none-eabi-gcc
#LD=aarch64-none-elf-gcc

OPTIMIZATION = 0
DEBUG = -g

CCFLAGS=-mcpu=cortex-m7 -mthumb -DARMCM7 -Wall -fno-common -I./ -O$(OPTIMIZATION) $(DEBUG)
#CCFLAGS=-fno-zero-initialized-in-bss -Wall -Wstrict-prototypes -O1 -mcpu=cortex-m4 -mthumb -c -g -nostdlib -fno-builtin -mlittle-endian -DARMCM7 -lc 
#LDFLAGS =-O$(OPTIMIZATION) -mcpu=cortex-m7 -mthumb 
LDFLAGS =-O$(OPTIMIZATION) -mcpu=cortex-m7
#LDFLAGS =-O$(OPTIMIZATION) -march=armv7e-m -mthumb -mcpu=cortex-m7 
LDFLAGS+=--specs=nosys.specs
#LDFLAGS+=--specs=rdimon.specs
#LDFLAGS += --sysroot= "/opt/NXP/S32DS.3.2/S32DS/build_tools/gcc_b1620/gcc-6.3-arm32-eabi/arm-none-eabi/newlib/lib"
#LDFLAGS +=-L/opt/NXP/S32DS.3.2/S32DS/build_tools/gcc_b1620/gcc-6.3-arm32-eabi/arm-none-eabi/newlib/lib
#LDFLAGS+=-L/home/nirajg/toolchain/gcc-arm-none-eabi-5_4-2016q3/lib/
#LDFLAGS+= --sysroot="C:\NXP\gcc-6.3-arm32-eabi\arm-none-eabi\newlib"      \
#-nostdlib -nostartfiles  
# Tell the linker where to find the libraries -> important: use thumb versions
#LIBSPEC= -L/opt/NXP/S32DS.3.2/S32DS/build_tools/gcc_b1620/gcc-6.3-arm32-eabi/lib 

# List the object files involved in this project
OBJS= hello_world.o  startup_ARMCM7.o system_ARMCM7.o

# The default 'target' (output) is main.elf and it depends on the object files being there.
# These object files are linked together to create hello_world.elf
hello_world.elf : $(OBJS)
	$(LD)  $(LDFLAGS) $(OBJS) -T$(LINK_DIR)/gcc_arm.ld -o hello_world.elf 

# The object file hello_world.o depends on hello_world.c.  hello_world.c is compiled to make hello_world.o
hello_world.o: hello_world.c
	$(CC) -c $(CCFLAGS) hello_world.c -o hello_world.o
startup_ARMCM7.o: $(CMSIS_DIR)/Source/startup_ARMCM7.c
	$(CC) -c $(CCFLAGS) $(INCLUDE_HEADERS) $(CMSIS_DIR)/Source/startup_ARMCM7.c -o startup_ARMCM7.o
system_ARMCM7.o: $(CMSIS_DIR)/Source/system_ARMCM7.c
	$(CC) -c $(CCFLAGS) $(INCLUDE_HEADERS) $(CMSIS_DIR)/Source/system_ARMCM7.c -o system_ARMCM7.o

# if someone types in 'make clean' then remove all object files and executables
# associated wit this project
clean: 
	@rm -rf $(OBJS) 
	@rm -rf hello_world.elf *.map 
