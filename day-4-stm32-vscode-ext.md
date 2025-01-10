# Day 4: Setting up STM32 VSCode Extension
#workspace
## 1. Introduction
I've been wanting to move away from the STM32CubeIDE for quite some time now. Since I do most of my (non-embedded) development on VSCode, I decided to give the STM32 VSCode Extension a try. In this post, I walk through my experience with the STM32 VSCode extension.

## 2. Setup
Once I installed the STM32 VSCode Extension, I updated the extension's settings by providing the absolute paths to the STM32CubeMX executable and STM32CubeCLT folder. I skipped the STMCUFinder executable for now.

![[Pasted image 20250105214515.png]]

Next, I use the STM32 VSCode extension to create an empty project for the NUCLEO-F446RE. 
![[Pasted image 20250105214956.png]]

I use the following settings:
![[Pasted image 20250105214932.png]]

Unfortunately, I'm running into issues building the empty project. I walked through their User Guide and am not able to get this tool to work at the moment.

TODO: Will update this post once I'm able to get it running.
## 3. Resources
[How to create projects using the STM32 VS Code Extension](https://www.youtube.com/watch?v=DDVdq47Dd94) 
