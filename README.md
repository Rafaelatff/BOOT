# BOOT
This repository was create to follow the content of the course 'STM32Fx Microcontroller Custom Bootloader Development'.

## Memory address

* Internal flash memory - its where the code will be placed - Begins 0x0800 0000, divided in sectors and goes up to 0x0803 FFFF.
* Internal SRAM1 - used for global data, static variables, stack and heap purposes - Begins 0x2000 0000 and goes up to 0x2000 FFFF.
* System Memory (ROM) - Bootloader - Begins 0x1FFF 0000 and goes up to 0x1FFF 77FF.


## Reset sequence

* 1. When you reset the MCU, the PC of the processor is loaded with the value 0x0000 0000. *In STM32 uC, is loaded with the value 0x0800 0000*.
* 2. The processor reads the value at memory location 0x0000 0000 in to MSP (Main Stack Pointer) register. *In STM32 uC, MSP value stored at 0x0800 0000*.
* 3. Then the processor reads the value at 0x0000 0004 (value is the address of the reset handler). *In STM32 uC, processor reads the value of the address of the reset handler found at 0x0800 0004*.
* 4. PC jumps to the reset handler. *In STM32 uC, jumps to the reset handler*.

Both addresses can be linked by doing the "memory aliasing" (address value depends on MCU).

# Hardware/Firmware configuration

The documentation (reference manual) shows the options for Boot modes.

BOOT1 (PB2) and BOOT0 (B) pins.

![image](https://user-images.githubusercontent.com/58916022/215750510-5e7f53b9-b6fa-48eb-8fab-75626859e259.png)

*NOTE: When the device boots from SRAM, in the application initialization code, you have to relocate the vector table in SRAM using the NVIC exception table and the offset register.*

![image](https://user-images.githubusercontent.com/58916022/215751604-6c1ad05a-fc80-4793-9237-13cbf05ef020.png)

As we can see, UART2 isn't connected by PA2 and PA3. We canno't talk to ST's Bootloader over this Virtual COM Port. 
![image](https://user-images.githubusercontent.com/58916022/215752046-67a9fe86-0e1d-4277-a0a2-06d4e1ca1d89.png)

USART2 is pointed as a boot option in user manual, but on AN2606 USART3 appears instead of USART2. 

![image](https://user-images.githubusercontent.com/58916022/215753204-60011869-849e-48f3-bd34-ebdbff31d5a6.png)

PA9 and PA10 from USART1 will be used instead.

![image](https://user-images.githubusercontent.com/58916022/215753774-3c02b32c-5038-46a1-b566-decf679737c4.png)

We need a USB-UART conversor. 

# Software

The [FLASHER-STM32](https://www.st.com/en/development-tools/flasher-stm32.html) is required. ST website says that the FLASHER-STM32 was replaced by STM32CubeProgrammer. So, we also downloaded the [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html) for tests purpose.


