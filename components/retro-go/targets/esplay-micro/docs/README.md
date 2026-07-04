# retro-go for ESPlay Micro

- fork from https://github.com/ducalex/retro-go

This port developed for the Micro V2 listed above. Compatibility with the elusive V1 is unknown.

## 构建
```powershell
. D:\Projects\tools\esp-idf-v5.5.4\export.ps1
python rg_tool.py --target esplay-micro build-img
```

## 刷入
```powershell
python rg_tool.py --target esplay-micro --port COM9 --baud 460800 install
```
需要 esp-idf v5.5+。若刷入失败，降低波特率：`--baud 460800`。

## Button Mapping
| 按钮   | 映射                            | 说明                |
|--------|--------------------------------|---------------------|
| 方向键  | UP / DOWN / LEFT / RIGHT      | I2C PCF8574 @0x20   |
| A      | RG_KEY_A                      | I2C bit 6           |
| B      | RG_KEY_B                      | I2C bit 7           |
| START  | RG_KEY_START                  | I2C bit 0           |
| SELECT | RG_KEY_SELECT                 | I2C bit 1           |
| MENU   | GPIO35                        | 物理按键（独立 GPIO）  |
| L      | GPIO36                        | 物理按键（独立 GPIO）  |
| R      | GPIO34                        | 物理按键（独立 GPIO）  |
| OPTION | SELECT + A                    | 虚拟组合键            |

### 操作说明
- **主界面**: `MENU` → 关于菜单, `SELECT+A` (OPTION) → 设置
- **游戏中**: `MENU` → 游戏内菜单（存档/读档/退出）, `SELECT+A` → 设置
- **退出游戏**: 按 MENU → 选择 Quit

# Hardware info
- ESP32-WROVER-B (SoC 16MB Flash + 8MB PSRAM)
- PCF8574 I2C GPIO (To connect the extra buttons)
- UDA1334A (I2S DAC)
- YT240L010 (ILI9341 LCD)
- TP4054 (Lipo Charger IC)
- CH340C (USB to Serial)
- 3.5mm Headphone jack 0_o

The following snippet was in the `config.h`, might contain still useful information.
````
// Experimental. Caused "Menu" to be mapped to a D-pad direction.
//#define RG_GPIO_GAMEPAD_X           GPIO_NUM_NC
//#define RG_GPIO_GAMEPAD_Y           GPIO_NUM_NC
//#define RG_GPIO_GAMEPAD_SELECT      GPIO_NUM_0
//#define RG_GPIO_GAMEPAD_START       GPIO_NUM_36
//#define RG_GPIO_GAMEPAD_A           GPIO_NUM_32
//#define RG_GPIO_GAMEPAD_B           GPIO_NUM_33
//#define RG_GPIO_GAMEPAD_MENU        GPIO_NUM_35
//#define RG_GPIO_GAMEPAD_OPTION      GPIO_NUM_NC
````

# Images
![device.jpg](device.jpg)
