Objectives: Set up serial communication, understand the AM62x Bootprocess,
compile and install the U-Boot bootloader, use basic U-Boot commands, set
up TFTP communication with the development workstation.

To begin with:
    The bootloader is a small program that starts the device and loads the OS (The starter engine of the system)
    -> Initializes the hardware(CPU, RAM, Storage...)
    -> Loads the OS kernel from the storage into RAM
    -> Starts the kernel so the OS can take over

    It often comes in two stages on resource-limited SOCs:
    -> SPL(Secondary Program Loader) -> Small first stage bootloader that runs from internal SRAM(inside the CPU) (Loaded from a file MLO in a FAT filesystem in the first bootable part    ition), Configures DDR and loads the bigger U-Boot
    -> U-boot proper -> full featured bootloader running from external DDR RAM (Double Data RAM SDRAM)(inside the board)

Beaglebone U-Boot boot flow:
    1. ROM code(in SoC):
        -> Runs immediately on power-up
        -> Minimal code in internal ROM
        -> Responsible for: 
            * Basic HW initialization
            * finding and loading the first-stage bootloader (SPL)
    2. SPL:
        -> Tiny bootloader runs from SRAM
        -> Responsible for:
            * initialize DDR (RAM)
            * Loader U-Boot proper into DDR
    3. U-Boot: 
        -> Full featured bootloader, runs from DDR
        -> Responsible for:
            * Initialize peripherals (USB,network...)
            * Provide Command Line Interface (CLI) for debuigging
            * Load Linux kernel and device tree
    4. Linux Kernel:
        -> Starts the main operating system
        -> Initializes drivers, mounts rootfs, starts user processes   
