### boot IAP
link tham khao
1 https://stackoverflow.com/questions/35328536/jumping-to-a-second-firmware-on-stm32f4
2 https://stm32f4-discovery.net/2017/04/tutorial-jump-system-memory-software-stm32/
3 https://github.com/havenxie/stm32-iap-uart-boot
# Trong bộ tải khởi động, sau khi vô hiệu hóa tất cả các nguồn ngắt, tôi làm như sau:
bootloader

___________________________________________________________________________________
1 #define APP_LOCATION 0x08006000

typedef void (*pFunction)(void);
pFunction jump;
volatile uint32_t jumpAddress;
register uint32_t mainStackPointer __ASM("msp");

void Jump( void ) {
    jumpAddress = *( volatile uint32_t* )( APP_LOCATION + 4 );
    jump = ( pFunction )jumpAddress;
    mainStackPointer = *( volatile uint32_t* )APP_LOCATION;
    jump();
}

___________________________________________________________________________________
## trong aplication

SCB->VTOR = 0x0x08006000;

## Teta term VT send file.bin
