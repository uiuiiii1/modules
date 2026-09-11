# 模块代码小仓库

STM32 常用功能模块代码集合。每个模块独立成文件，可直接拷入工程使用。

> **致谢**：代码实现参考了**江科大自化协（江科大众志）**的 STM32 入门教程。

---

## 模块目录

| 模块 | 文件 | 库 | 说明 |
|---|---|---|---|
| 高级按键 | `Key.c` / `Key.h` | 标准库 | 7 种事件：按住/按下/释放/单击/双击/长按/重复 |
| OLED 显示屏（HAL 库版） | `OLED/oled.c` / `OLED/oled.h` / `OLED/OLED_Data.c` / `OLED/OLED_Data.h` | HAL 库 | 128×64 IIC 接口 SSD1306 显示屏驱动 |
| OLED 显示屏（标准库版） | `OLED2/OLED.c` / `OLED2/OLED.h` / `OLED2/OLED_Data.c` / `OLED2/OLED_Data.h` | 标准库 | 128×64 IIC 接口 SSD1306 显示屏驱动 |

---

## Key 模块：高级按键

**功能**：基于 GPIO 输入 + 定时器中断扫描的按键事件处理，支持 7 种按键事件：

| 事件 | 标志位 | 触发条件 |
|---|---|---|
| 按住 | `KEY_HOLD` | 持续按下 |
| 按下 | `KEY_DOWN` | 按下瞬间（边沿） |
| 释放 | `KEY_UP` | 松开瞬间（边沿） |
| 单击 | `KEY_SINGLE` | 按下后 200ms 内松开 |
| 双击 | `KEY_DOUBLE` | 单击后 200ms 内再次按下 |
| 长按 | `KEY_LONG` | 持续按下超过 2000ms |
| 重复 | `KEY_REPEAT` | 长按后每 100ms 重复触发一次 |

**参考**：江科大自化协 STM32 教程（基础版只有短按/长按，本模块扩展为 7 种事件）。

**用法**：把对应模块的 `.c/.h` 拷入你的工程，按注释初始化即可。`Key_Tick()` 放到 10ms 定时器中断里调用。

**库**：STM32 标准外设库

---

## OLED 模块：显示屏驱动（HAL 库版）

**功能**：128×64 IIC 接口 SSD1306 OLED 显示屏驱动，支持字符/字符串/数字/浮点数/图片/绘图/格式化输出。

主要函数：

| 类别 | 函数 |
|---|---|
| 初始化 | `OLED_Init` / `OLED_Update` / `OLED_Clear` |
| 字符显示 | `OLED_ShowChar` / `OLED_ShowString` |
| 数字显示 | `OLED_ShowNum` / `OLED_ShowSignedNum` / `OLED_ShowHexNum` / `OLED_ShowBinNum` / `OLED_ShowFloatNum` |
| 格式化输出 | `OLED_Printf`（类似 printf） |
| 图片显示 | `OLED_ShowImage` |
| 绘图 | `OLED_DrawPoint` / `DrawLine` / `DrawRectangle` / `DrawTriangle` / `DrawCircle` / `DrawEllipse` / `DrawArc` |
| 区域操作 | `OLED_UpdateArea` / `OLED_ClearArea` / `OLED_Reverse` / `OLED_ReverseArea` |

**硬件**：SSD1306 OLED 显示屏，128×64 分辨率，IIC 接口。

**字符集**：UTF8 / GB2312 可切换（`OLED_Data.h` 顶部宏定义）。

**参考**：江科大自化协 STM32 教程。

**用法**：把对应模块的 `.c/.h` 拷入你的工程，按注释初始化即可。`OLED_Data.c` 需一并拷入（含字模数据）。

**库**：STM32 HAL 库

---

## OLED2 模块：显示屏驱动（标准库版）

**功能**：128×64 IIC 接口 SSD1306 OLED 显示屏驱动，支持字符/字符串/数字/浮点数/图片/绘图/格式化输出。功能与 HAL 库版一致，仅软件库不同。

主要函数：

| 类别 | 函数 |
|---|---|
| 初始化 | `OLED_Init` / `OLED_Update` / `OLED_Clear` |
| 字符显示 | `OLED_ShowChar` / `OLED_ShowString` |
| 数字显示 | `OLED_ShowNum` / `OLED_ShowSignedNum` / `OLED_ShowHexNum` / `OLED_ShowBinNum` / `OLED_ShowFloatNum` |
| 格式化输出 | `OLED_Printf`（类似 printf） |
| 图片显示 | `OLED_ShowImage` |
| 绘图 | `OLED_DrawPoint` / `DrawLine` / `DrawRectangle` / `DrawTriangle` / `DrawCircle` / `DrawEllipse` / `DrawArc` |
| 区域操作 | `OLED_UpdateArea` / `OLED_ClearArea` / `OLED_Reverse` / `OLED_ReverseArea` |

**硬件**：SSD1306 OLED 显示屏，128×64 分辨率，IIC 接口。

**字符集**：UTF8 / GB2312 可切换（`OLED_Data.h` 顶部宏定义）。

**参考**：江科大自化协 STM32 教程。

**用法**：把对应模块的 `.c/.h` 拷入你的工程，按注释初始化即可。`OLED_Data.c` 需一并拷入（含字模数据）。

**库**：STM32 标准外设库
