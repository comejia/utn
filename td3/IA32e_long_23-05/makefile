.PHONY : clean

KERNEL_MEMORY=0x8000
KERNEL_SIZE_SECTORS=20

BOOTLOADER_DEFINES=-DKERNEL_SIZE_SECTORS=$(KERNEL_SIZE_SECTORS) -DKERNEL_MEMORY=$(KERNEL_MEMORY)

bootdisk: kernel.bin bootld.bin
	dd if=/dev/zero of=mydisk count=$(KERNEL_SIZE_SECTORS)	
	dd if=bootld.bin of=mydisk conv=notrunc
	dd if=kernel.bin of=mydisk seek=1 conv=notrunc

kernel.bin: long.asm
	nasm -f bin  $(BOOTLOADER_DEFINES) long.asm  -l long.lst -o $@

bootld.bin: bootld.asm
	nasm -f bin $(BOOTLOADER_DEFINES) bootld.asm -l bootld.lst -o $@

clean:
	rm -f bootld.bin kernel.bin disk *.lst mydisk bochsout.txt
