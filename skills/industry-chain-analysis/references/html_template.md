# HTML 输出模板

## 页面结构约定

```
<!DOCTYPE html>
<html lang="zh-CN">
<head>...</head>
<body>
  <h1>XX产业链深度分析</h1>
  <p class="subtitle">日期 | 数据来源</p>

  <div class="note">
    <strong>核心发现：</strong>一句话核心结论
  </div>

  <!-- SVG产业链图（来自show_widget） -->
  <div class="svg-wrap">...</div>

  <h2>一、这个行业在做什么？</h2>
  一句话理解 + 关键分类表格

  <h2>二、产业链分层详解</h2>
  上游 → 中游 → 下游，每个环节独立.card

  <h2>三、产业演进推演</h2>
  历史→现状→未来必然性

  <h2>四、五维⭐️评级</h2>
  第一梯队 → 第二梯队 → 防守型

  <h2>五、核心矛盾与风险</h2>
  风险矩阵（概率×影响）

  <h2>六、总结</h2>
  3-5句话核心结论

  <div class="note">免责声明</div>
</body>
```

## CSS 变量

所有样式内联在 `<style>` 中，使用以下CSS变量：

```css
:root {
  --bg: #f4f7f6;
  --text: #1a1a2e;
  --text-muted: #6b7280;
  --border: #d8e2de;
  --accent: #0f766e;          /* 青绿结构色；上下游用下方 pastel 强区分 */
  --star: #EF9F27;
  --upstream-bg: #EEF3FA; --upstream-border: #B5D4F4;
  --mid-bg: #FAF0EC; --mid-border: #F0997B;
  --down-bg: #E5F7F0; --down-border: #5DCAA5;
}
```

> 硬约束对齐 wb-finance（浅底深字、首屏「核心发现」、ECharts/`node --check`）。**视觉特色**：页头/标题用青绿 `--accent`；**上中下游 pastel 是本报告主角**（分层卡 + SVG 三层分色），勿整页刷成单一 navy。关系拓扑用 SVG，数值趋势用 ECharts。

## 字体

- 正文：15px, line-height: 1.7
- 标题 h1：26px, font-weight: 600
- 标题 h2：20px, font-weight: 600, border-bottom: 2px solid --accent
- 标题 h3：16px, font-weight: 600, color: --accent
- 卡片内文字：13-14px
- max-width: 900px
- 注意框 / `.note`「核心发现」：背景 #fff9e6 / 左边框 #EF9F27（首屏结论先行）
- 上游/中游/下游分层卡：分别用 `--upstream-*` / `--mid-*` / `--down-*`

## 响应式

@media (max-width: 640px) 时缩小字体和边距。

## 公司卡片格式

每个公司使用 `.company` div：

```html
<div class="company">
  <div class="company-header">
    <div>
      <span class="company-name">公司名</span>
      <span class="company-code">代码</span>
    </div>
    <span class="company-marketcap">市值 XXXX亿</span>
    <span class="company-stars">⭐⭐⭐⭐⭐</span>
  </div>
  <p class="company-desc"><strong>做什么的：</strong>一句话定位。补充逻辑说明。</p>
  <div class="dim-row"><span class="dim-label">产业逻辑</span><span class="dim-stars">⭐...</span><span class="dim-note">理由</span></div>
  <div class="dim-row"><span class="dim-label">增量空间</span><span class="dim-stars">⭐...</span><span class="dim-note">理由</span></div>
  <div class="dim-row"><span class="dim-label">不可替代性</span><span class="dim-stars">⭐...</span><span class="dim-note">理由</span></div>
  <div class="dim-row"><span class="dim-label">技术壁垒</span><span class="dim-stars">⭐...</span><span class="dim-note">理由</span></div>
  <div class="dim-row"><span class="dim-label">不可复制性</span><span class="dim-stars">⭐...</span><span class="dim-note">理由</span></div>
</div>
```

## 通俗类比要求

每个关键环节至少用1个通俗类比（如「电子布=混凝土里的钢筋」「TGV=把手术从木头桌换到大理石台面」「HBM=48车道高速路vs DDR4=双车道」）。

## 数量控制

- 第一梯队：3-6家公司（完整五维度详解）
- 第二梯队：5-10家公司（精简五维度，如只列产业逻辑+不可替代性）
- 防守型：表格形式（一句话逻辑）

## SVG图要求

- 浅色主题配色
- viewBox="0 0 680 H"
- 上中下游三层分色背景
- 关键公司名称标注在对应的子层矩形内
- 未上市公司用虚线框
- 箭头连接各层
- 底部标注核心变量/风险点
