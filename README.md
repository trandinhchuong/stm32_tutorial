# stm32_tutorial
link tham khao https://stackoverflow.com/questions/35328536/jumping-to-a-second-firmware-on-stm32f4
## Trong bộ tải khởi động, sau khi vô hiệu hóa tất cả các nguồn ngắt, tôi làm như sau:
bootloader

___________________________________________________________________________________
1 #define APP_LOCATION 0x08006000

typedef void (*pFunction)(void);
pFunction jump;
volatile uint32_t jumpAddress;
register uint32_t regMainStackPointer __ASM("msp");

void Jump( void ) {
    jumpAddress = *( volatile uint32_t* )( APP_LOCATION + 4 );
    jump = ( pFunction )jumpAddress;
    mainStackPointer = *( volatile uint32_t* )APP_LOCATION;
    jump();
}

___________________________________________________________________________________
## trong aplication

SCB->VTOR = 0x0x08006000;

