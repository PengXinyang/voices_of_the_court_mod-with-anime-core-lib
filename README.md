## 项目原地址

https://github.com/Lisiyuan233/voices_of_the_court_mod.git

感谢up的付出！

# Anime Core Lib (二向箔) 兼容性说明

## 概述

本项目已添加对Anime Core Lib（二向箔）的兼容性支持，使2D肖像和纸片人种族能够参与对话系统。

## 修改内容

### 1. 动画系统兼容 (`gfx/portraits/portrait_animations/conversation_animations.txt`)

#### 添加2D肖像动画定义

- 为`anime_male`、`anime_female`、`anime_boy`、`anime_girl`添加了默认动画定义
- 2D肖像使用静态显示（dead动画作为占位符，Anime Core Lib会自动阻止动画播放）

#### 阻止3D动画应用到2D肖像

- 在所有场景动画（armycamp、hunt、feast）中添加了`waifu_portrait_trigger = no`条件
- 在所有情绪动画（test、idle、sad、happy、love、pain、worry、speaking）中添加了`waifu_portrait_trigger = no`条件
- 在portrait_modifier中添加了`trigger = { waifu_portrait_trigger = no }`条件，确保道具和修饰只应用到3D肖像

### 2. GUI系统兼容 (`gui/shared/conversation_portraits.gui`)

- 保持使用`Character.GetAnimatedPortrait`，该系统对2D和3D肖像都有效
- Anime Core Lib的动画系统会自动阻止3D动画应用到2D肖像
- 2D肖像会通过Anime Core Lib的系统正常显示

## 工作原理

1. **2D肖像识别**：Anime Core Lib使用`waifu_portrait_trigger`来标识2D肖像
2. **动画阻止**：通过在所有3D动画的weight中添加`waifu_portrait_trigger = no`条件，确保这些动画只应用到3D肖像
3. **默认显示**：2D肖像使用默认的静态显示（dead动画），Anime Core Lib会阻止动画播放，显示静态2D图片

## 使用要求

- 需要安装Anime Core Lib（二向箔）mod
- 2D肖像角色必须使用`anime_ethnicity`种族
- 2D肖像角色必须满足`waifu_portrait_trigger`条件（符合二向箔的mod理论上满足这两条要求）

## 兼容性

- ✅ 兼容Anime Core Lib
- ✅ 不影响原版3D肖像的显示
- ✅ 2D肖像和3D肖像可以在同一对话中正常显示

## 注意事项

1. 如果Anime Core Lib未加载，2D肖像相关代码不会执行，不影响原版功能
2. 2D肖像不会使用场景动画（armycamp、hunt、feast等），只会显示静态图片
3. 2D肖像不会使用情绪动画（sad、happy、love等），只会显示默认静态图片
4. 对话系统的其他功能（背景、对话框等）不受影响

## 未来改进

- 可以考虑为2D肖像添加简单的变化（通过切换不同的2D图片）

