from building import *
import os

# Import environment variables
Import('env')

# Get the current working directory
cwd = GetCurrentDir()

# Initialize include paths and source files list
path = [os.path.join(cwd, 'Include')]
src = [os.path.join(cwd, 'Source', 'Templates', 'system_stm32f3xx.c')]

# Map microcontroller units (MCUs) to their corresponding startup files
mcu_startup_files = {
    'STM32F301x8': 'startup_stm32f301x8.s',
    'STM32F302x8': 'startup_stm32f302x8.s',
    'STM32F302xC': 'startup_stm32f302xc.s',
    'STM32F302xE': 'startup_stm32f302xe.s',
    'STM32F303x8': 'startup_stm32f303x8.s',
    'STM32F303xC': 'startup_stm32f303xc.s',
    'STM32F303xE': 'startup_stm32f303xe.s',
    'STM32F318xx': 'startup_stm32f318xx.s',
    'STM32F328xx': 'startup_stm32f328xx.s',
    'STM32F334x8': 'startup_stm32f334x8.s',
    'STM32F358xx': 'startup_stm32f358xx.s',
    'STM32F373xC': 'startup_stm32f373xc.s',
    'STM32F378xx': 'startup_stm32f378xx.s',
    'STM32F398xx': 'startup_stm32f398xx.s', 
}

# Check each defined MCU, match the platform and append the appropriate startup file
for mcu, startup_file in mcu_startup_files.items():
    if mcu in env.get('CPPDEFINES', []):
        if rtconfig.PLATFORM in ['gcc', 'llvm-arm']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'gcc', startup_file)]
        elif rtconfig.PLATFORM in ['armcc', 'armclang']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'arm', startup_file)]
        elif rtconfig.PLATFORM in ['iccarm']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'iar', startup_file)]
        break

# Define the build group
group = DefineGroup('STM32F3-CMSIS', src, depend=['PKG_USING_STM32F3_CMSIS_DRIVER'], CPPPATH=path)

# Return the build group
Return('group')