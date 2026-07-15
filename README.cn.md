# Mechanical Stop Watch

一个基于 Vue 3、TypeScript 和 Vite 构建的机械秒表交互组件。项目使用真实图片素材还原机械秒表外观，通过指针旋转、按钮命中检测和机械滴答音效提供接近实体秒表的使用体验。

[English README](./README.md)

## 功能特性

- 机械秒表外观：使用独立的表盘、指针、按钮高亮图层进行组合渲染。
- 精准计时：基于 `performance.now()` 和 `requestAnimationFrame` 更新指针角度。
- 双指针显示：秒针显示 60 秒周期，分针显示 60 分钟周期。
- 表冠交互：点击表冠启动或暂停，双击表冠在停止时归零。
- 精确点击区域：使用按钮遮罩图的 alpha 通道判断点击是否落在表冠区域。
- 音效反馈：运行时播放机械滴答音，停止时自动停止音效。
- 响应式尺寸：秒表组件按原始比例缩放，适配不同屏幕宽度。

## 技术栈

- Vue 3
- TypeScript
- Vite
- HTML Canvas，用于读取按钮遮罩 alpha 通道
- Web Audio / `HTMLAudioElement`，用于播放机械音效

## 快速开始

安装依赖：

```bash
npm install
```

启动开发服务器：

```bash
npm run dev
```

构建生产版本：

```bash
npm run build
```

本地预览生产构建：

```bash
npm run preview
```

## 使用方式

启动项目后，在页面中操作机械秒表：

- 将鼠标移动到表冠区域时，会显示按钮高亮提示。
- 单击表冠：启动或暂停计时。
- 双击表冠：归零计时器。当前实现仅在秒表停止时执行归零。

浏览器可能会要求用户先进行一次页面交互后才允许播放音频，这是现代浏览器的自动播放策略。

## 项目结构

```text
.
├── public/
│   ├── assets/
│   │   ├── MechanicalStopwatch/   # 秒表表盘、按钮、指针等图片素材
│   │   └── audio/                 # 机械滴答音效
│   └── favicon.svg
├── src/
│   ├── common/
│   │   ├── MechanicalStopwatch/
│   │   │   ├── MechanicalStopwatch.vue
│   │   │   └── MechanicalStopwatch.ts
│   │   └── audiotool/
│   │       └── PlayAudio.ts
│   ├── App.vue
│   ├── main.ts
│   └── style.css
├── index.html
├── package.json
└── vite.config.ts
```

## 核心实现

`src/common/MechanicalStopwatch/MechanicalStopwatch.vue` 负责组件模板和图层布局。表盘、按钮提示层、分针和秒针以绝对定位叠放，指针通过动态 `transform` 旋转。

`src/common/MechanicalStopwatch/MechanicalStopwatch.ts` 封装秒表状态和交互逻辑，包括计时、指针角度计算、按钮命中检测、单击/双击处理和音效控制。

`src/common/audiotool/PlayAudio.ts` 封装音频播放与停止逻辑，支持重复播放并在秒表停止时清理当前音频。

## 素材说明

秒表图片素材位于 `public/assets/MechanicalStopwatch/`，音效文件位于 `public/assets/audio/`。这些资源通过 Vite public 目录以根路径访问，例如：

```ts
/assets/MechanicalStopwatch/MechanicalStopwatch.png
/assets/audio/TickdaTickda.wav
```

如果后续替换图片素材，需要同步检查 `MechanicalStopwatch.ts` 中的表盘尺寸、指针旋转中心和按钮遮罩区域配置。
