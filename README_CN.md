# Marzipan

![sample](assets\sample.jpg)

<div style="text-align: center">[![CC BY-SA 4.0][cc-by-sa-image]][cc-by-sa]</div>

<div style="text-align: center"><a href="./README.md">English</a> | 简体中文</div>

一款简单焊接的，小巧的模块化 Smol Slimes / nRFSlime 方案！尺寸仅为 40\*28\*17mm。

[!CAUTION]
目前的版本存在以下问题：
- 使用 LWKJ 的 ICM-45686 模块情况下，打开开关启动时无法识别传感器，需要再点击一下按钮才能正常启动。
- 按钮工作情况与预期不符。
欢迎提出 PR 进行修复！

如果想要了解更多关于 Smol Slimes / nRFSlime 的事情，欢迎阅读 [Smol Slime - SlimeVR Docs](https://docs.slimevr.dev/diy/smol-slime.html)。

## 文件说明

### PCB

PCB 使用立创 EDA Pro 版本绘制，在仓库中提供了源文件，欢迎进行修改。

针对不同的成品传感器模块，我创建了以下适配不同类型的 PCB，但是由于时间问题仅验证了 `VGGALXI` 版本，其他版本理论上是没问题的。

- `VGGALXI`: 孔位顺序从下到上为 `VCC GND GND SDA SCL X INT`（已验证）
- `VGLAXXI`: 孔位顺序从下到上为 `VCC GND SCL SDA X X INT`（未验证）
- `KOUNO'S_ICM45`: 为 KOUNO 的模块而设计。（未验证）

### 外壳

外壳方面，提供了需要 M2 热熔螺母的版本 `Case_v5.stl` 以及可以直接将螺丝拧到外壳里的版本 `Case_v5_No_Heat_Insert_Nut.stl`。热熔螺母的版本会更加耐用一些。

**对于拓竹打印机，则可以在这里获取预设好的打印配置：**

**https://makerworld.com/zh/models/966982**

仓库中提供的外壳文件适配 25mm 宽度的绑带，~~同时也适配 ReboCap 的快拆（逃~~。

如果想要更宽的绑带可以自行修改 `.step` 格式的源文件。

### 固件

本 PCB 的孔位与原项目中默认孔位相符（`SDA-006`, `SCL-008`, `INT-017`），因此可以直接使用 [Smol Slime](https://docs.slimevr.dev/diy/smol-slime.html) 网站中所提供的固件进行刷写，无需额外更改。

## BOM

### PCB 和组装

这里的是完成一个追踪器所需要的数量。注意，除了所需要的追踪器之外还需要购买一个 nRF52840 SuperMini / Dongle 作为接收器，具体也请参考 Smol Slime 页面中的内容。根据 Discord，一个接收器可以匹配 20 个左右追踪器（尚未验证，但是至少带 6 个是没问题的）。

|         元件名称          | 价格 | 数量 |                 备注                 |
| :-----------------------: | :--: | :--: | :----------------------------------: |
| nRF52840 SuperMini 开发板 |  15  |  1   |                                      |
|    MSK-12D19 滑动开关     | 0.1  |  1   |      一种祖传开关，其他开关也行      |
|  3\*6\*4.3 轻触开关 侧插  | 0.1  |  1   |      也可以换成其他侧向轻触开关      |
|   401230 / 501230 电池    |  4   |  1   |  推荐使用 501230 电池，更小的也可以  |
|    固定电池用的双面胶     |  2   |  1   |         甚至超市买的都行（？         |
|        传感器模块         |  ?   |  1   |                                      |
|        M2\*14 螺丝        | 0.1  |  2   |             用于固定外壳             |
|    M2\*4.5\*3 热熔螺母    | 0.1  |  2   |  如果使用直接拧的外壳版本，则不需要  |
|        25mm 宽绑带        |  2   |  1   | 当然也可以修改外壳文件来适配不同绑带 |

### 3D 打印

推荐使用 PETG 进行打印，PLA 也没问题。

|    元件名称     | 数量 |            备注            |
| :-------------: | :--: | :------------------------: |
|     Lid_v5         |  1   | 盖子 |
|     Case_v5        | 1 | 需要热熔螺母的盒子本体，如果不需要则使用 Case_v5_No_Heat_Insert_Nut |
|  Button_Cap_v5      | 1 | 按钮帽，用于延长按钮 |
|  Switch_Cap_v5    | 1 | 开关帽，用于延长开关 |
| Screw_Holder_v5   |  2   |    螺丝支撑柱，加上会让结构更牢固，也可以不加    |
## 安装说明

### 焊接并组装

- 使用探针等工具检查 SuperMini，传感器模块等是否工作正常。

- 必须首先焊接传感器模块，注意检查传感器的孔位顺序是否与 PCB 相符。将对应的孔位对齐后，从 PCB 背面融化焊锡，完成固定。完成焊接后可以使用万用表检查电路是否正常接通。
- 焊接开关与按钮。
- 确保开关处于关闭状态，然后焊接电池。
- 最后焊接 SuperMini 模块。
- 检查可以正常工作后，将电池用双面胶黏贴在 PCB 背面对应方框的位置。
- 将热熔螺母嵌入壳体中。
- 将按钮帽和开关帽装入壳体，对准孔位将本体塞进去。
- 放入螺丝支撑柱，装上盖子，拧螺丝即可。

### 刷入固件

- 具体请参考 [Smol Slime - SlimeVR Docs](https://docs.slimevr.dev/diy/smol-slime.html) 中刷入固件的部分。
  - 使用 LWKJ 的 45686 模块 + VGGALXI 布局的情况下，使用 `Tracker SuperMini Disabled Disabled ` 的固件可以正常工作。

## 其他链接

- **SlimeVR nRF Receiver Firmware:** https://github.com/SlimeVR/SlimeVR-Tracker-nRF-Receiver

- **SlimeVR nRF Tracker Firmware:** https://github.com/SlimeVR/SlimeVR-Tracker-nRF

- **Scawanf's PCB R3 on Github:** https://github.com/SlimeVR/SlimeVR-Tracker-nRF-PCB

- **Scawanf's PCB R3 on OSHWLab:** https://oshwlab.com/sctanf/slimenrf3

- **SlimeVR Discord:** https://discord.gg/SlimeVR

- **Smol Slime Docs:** https://docs.slimevr.dev/diy/smol-slime.html
