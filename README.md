# STM32 Bare-Metal: UART `printf()` Output using USART2 (PA2)

---

## 📌 Summary

This project demonstrates how to use the standard `printf()` function to transmit formatted strings over UART using **USART2** and **PA2 (TX)** pin on the STM32F4 Discovery board.  
It extends the previous lesson by redirecting `printf()` to USART2 via the `__io_putchar()` function.  
No HAL, no CMSIS — this is a pure **bare-metal** approach using direct register access.

---

## 🔁 Previous Lesson

If you haven’t completed the previous step where we transmitted a single character over UART using manual register setup, check it out first:

👉 [Previous Lesson: UART Transmit using USART2 (PA2)](https://github.com/iek2443/stm32-baremetal-uart-tx)

---

## 🧠 What You Will Learn

- How to redirect `printf()` output to a UART peripheral
- How to override `__io_putchar()` for GCC-based toolchains
- How to configure PA2 for USART2 transmission (AF7)
- The importance of TXE flag and timing when writing to `USART_DR`
- Why register fields must sometimes be written with `=` instead of `|=`

---

## ⚙️ Key Registers Used

- `RCC->AHB1ENR` → Enables clock to GPIOA
- `RCC->APB1ENR` → Enables clock to USART2
- `GPIOA->MODER` → Configures PA2 in Alternate Function mode
- `GPIOA->AFRL`  → Selects AF7 (USART2_TX) for PA2
- `USART2->BRR`  → Baud rate register (calculated manually)
- `USART2->CR1`  → Control register (for enabling TX and USART)
- `USART2->SR`   → Status register (TXE flag check)
- `USART2->DR`   → Data register (to send the character)

---

## 🔧 Requirements

- STM32F4 Discovery Board
- ARM GCC Toolchain
- ST-Link programmer
- STM32CubeProgrammer or OpenOCD
- USB-to-UART converter
- Serial terminal software (e.g., PuTTY, TeraTerm, screen)

---

📁 Project Structure
--------------------

stm32-baremetal-uart-printf/\
├── src/\
│   └── main.c         --> Bare-metal `printf` redirect via USART2\
├── inc/               --> (Optional: header files)\
└── README.md

---

🧭 Pin Mapping

| Function         | Port | Pin | Description         |
|------------------|------|-----|---------------------|
| UART2_TX         | A    |  2  | Serial transmit pin |

---
