# Build and Flash Firmware Image

1. Refer to [klipper's official installation](https://www.klipper3d.org/Installation.html)

2. `Building the micro-controller` with the configuration shown below.
  * [*] Enable extra low-level configuration options
  * Micro-controller Architecture = `STM32F103`
  * IF USE BOOTLOADER ([see klipper docs](https://www.klipper3d.org/Bootloaders.html#stm32f103-micro-controllers-blue-pill-devices))
    * Bootloader offset = `offset of your bootloader`
  * ELSE
    * Bootloader offset = `No bootloader`
  * IF USE USB
     * Communication interface = `USB`
  * ElSE IF USE UART0
     * Communication interface = `Serial (on USART0 PA10/PA9)`
  * GPIO pins to set at micro-controller startup = `!PB8,!PB9`

![image](https://github.com/user-attachments/assets/4c990fba-ea35-4c7b-878f-a1544d48abab)

3. Once the configuration is selected, press `q` to exit,  and "Yes" when  asked to save the configuration.
4. Run the command `make`
5. Flash the MCU
   * IF USE BOOTLOADER
     * Follow the instructions of your bootloader
   * ELSE IF USE NO BOOTLOADER
     * Switch `Boot0` to `1`
     * Run the command `make serialflash FLASH_DEVICE=/dev/serial/by-id/<YOUR USB ID>` for flashing via Serial or
     * Switch `Boot0` back to `0`
   * OR
     * Copy `~/klipper/out/klipper.bin` and flash via STLink / ST32CubeProgrammer

# Basic configuration
1. Refer to [klipper's official installation](https://www.klipper3d.org/Installation.html) to `Configuring Klipper`.
2. Copy the configuration file [mmu.cfg](./mmu.cfg) to your klipper installation and include it in your `printer.cfg` with `[include mmu.cfg]`
3. Refer to [klipper's official Config_Reference](https://www.klipper3d.org/Config_Reference.html) to configure the features you want.
4. Run the `ls /dev/serial/by-id/*` command to get the correct ID number of the STM32, and set the ID in `mmu.cfg`. 
    ```
    [mcu]
    serial: /dev/serial/by-id/usb-1a86_USB_Serial-if00-port0
    restart_method: command
    ```
