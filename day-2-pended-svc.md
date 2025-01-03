# Day 2: SysTick vs. PendSV
## Introduction
Today I decided to update the LunaRTOS kernel to utilize the Pended SVC (PendSV) feature for context switching. PendSV is provided in ARM Cortex-M processors, and allows software to trigger an exception to perform the context switch from one thread to another. I originally used SysTick for context switching in LunaRTOS, but this can cause issues if SysTick is needed for higher priority interrupts.