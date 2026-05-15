# DESIGN.md

> 新视界 · 视觉传达设计作品集 —— 换个视角，看见新可能

## 1. Visual Theme & Atmosphere

**Brand**: 新视界 (New Vision)
**Style**: 现代东方 · 暖调极简
**Keywords**: 开阔 · 温暖 · 留白 · 克制 · 精致
**Tone**: 干净且有温度 — NOT 沉重·冷感·繁复·工业
**Feel**: 白色画布上，金色线条勾勒出理性的秩序，暖灰与亚麻色铺垫出温润的质感

**Color Source**: `D:\毕业季\毕设\个人资料作品档案库\配色色卡.png`

**Interaction Tier**: L2 流畅交互
**Dependencies**: CSS only + IntersectionObserver（零JS库）

## 2. Color Palette & Roles

```css
:root {
  /* Backgrounds */
  --bg: #FFFFFF;                          /* 纯白基底 */
  --surface: #FAF8F5;                     /* 暖白纸面 */
  --surface-alt: #F4F1EC;                 /* 交替底色 */

  /* Borders */
  --border: #E5DFD6;                      /* 暖灰线 */
  --border-hover: #CCC3B6;                /* 暖灰线显 */

  /* Text */
  --ink: #2F2D2A;                         /* 暖黑（主文字） */
  --ink-secondary: #8C8276;               /* 暖灰（次要文字） */
  --ink-tertiary: #B8AFA2;                /* 浅暖灰（标签/标注） */

  /* Accent */
  --gold: #FFD176;                        /* 暖金（主色调） */
  --gold-hover: #E8B85A;
  --sage: #E2DF8F;                        /* 鼠尾草绿（点缀） */
  --orange: #FFA95C;                      /* 暖橙（少量使用） */
  --taupe: #A6926E;                       /* 灰褐色（中性色） */
}
```

**Color Rules:**
- 暖金为主色调，用于分割线、hover 态、奖项标签、装饰元素
- 鼠尾草绿和暖橙为极少量点缀（≤1处 per page）
- 背景以白色为主，交替 section 使用暖白（#FAF8F5）
- 所有颜色通过 CSS 变量引用，禁止硬编码 hex
- 多色相使用，保持暖调统一

## 3. Typography Rules

**Font Stack （完全离线，无需 Google Fonts）:**

| Role | Font Stack | Size | Weight | Line Ht | Letter Spacing |
|------|-----------|------|--------|---------|----------------|
| Hero H1 | `'STSong','Songti SC','SimSun',serif` | clamp(56px,8vw,96px) | 700 | 1.1 | 0.08em |
| Section H2 | `'STSong','Songti SC','SimSun',serif` | clamp(28px,3.5vw,40px) | 600 | 1.3 | 0.04em |
| H3 | `'STSong','Songti SC','SimSun',serif` | clamp(18px,2vw,22px) | 600 | 1.4 | 0.02em |
| Body CJ | `'PingFang SC','Microsoft YaHei','Heiti SC',sans-serif` | 14px | 400 | 1.9 | 0.02em |
| Body EN | `'Helvetica Neue','Helvetica','Arial',sans-serif` | 15px | 400 | 1.9 | 0.01em |
| Label | `'Helvetica Neue','Helvetica','Arial',sans-serif` | 11px | 400 | 1 | 0.08em |
| Decorative | `'STSong','Songti SC','SimSun',serif` | — | 700 | — | 0.12em |

**Typography Rules:**
- 宋体系列（衬线）做标题，黑体系列（无衬线）做正文
- Hero H1 字距宽松（0.08em），增强大气感
- 正文 14px 略小于常规，配合高行高（1.9）保持阅读舒适
- **NEVER use**: 楷体/KaiTi、书法体、Google Fonts
- 英文和数字用 Helvetica Neue / Arial，与中文宋体形成对比

## 4. Component Stylings

### Buttons
```css
.btn{
  display:inline-flex;align-items:center;gap:8px;
  font-family:'PingFang SC','Microsoft YaHei','Heiti SC',sans-serif;
  font-size:13px;letter-spacing:0.1em;
  padding:12px 32px;text-decoration:none;cursor:pointer;
  transition:all 0.3s;position:relative
}
.btn-primary{background:var(--ink);color:#fff;border:1px solid var(--ink)}
.btn-primary:hover{background:var(--gold);border-color:var(--gold);color:var(--ink)}
.btn-outline{background:transparent;color:var(--ink);border:1px solid var(--border)}
.btn-outline:hover{background:var(--ink);color:#fff}
```

### Navigation
```css
nav{
  position:fixed;top:0;left:0;right:0;z-index:100;height:56px;
  display:flex;align-items:center;
  background:rgba(255,255,255,0.92);
  border-bottom:1px solid var(--border)
}
.nav-brand{font-family:var(--font-song);font-size:16px;letter-spacing:0.12em;display:flex;align-items:center;gap:8px}
.nav-brand .brand-marker{display:inline-block;width:6px;height:6px;background:var(--gold)}
.nav-links a{font-family:'Helvetica Neue',Arial,sans-serif;font-size:11px;letter-spacing:0.08em;text-transform:uppercase;color:var(--ink-secondary);padding:8px 14px;transition:color 0.25s}
.nav-links a:hover{color:var(--ink)}
.nav-links a::after{content:'';display:block;width:0;height:1px;background:var(--gold);margin:2px auto 0;transition:width 0.3s}
.nav-links a:hover::after{width:100%}
```

### Cards (Work/Project Cards)
```css
.work-card{
  position:relative;cursor:pointer;overflow:hidden;
  background:var(--surface);border:1px solid var(--border);
  transition:all 0.4s;aspect-ratio:4/3
}
.work-card:hover{transform:translateY(-3px);border-color:var(--border-hover)}
.work-card img{width:100%;height:100%;object-fit:cover;transition:transform 0.5s}
.work-card:hover img{transform:scale(1.05)}
.work-card .card-overlay{position:absolute;inset:0;background:linear-gradient(to top,rgba(47,45,42,0.75) 0%,transparent 55%);display:flex;flex-direction:column;justify-content:flex-end;padding:20px;opacity:0;transition:opacity 0.35s}
.work-card:hover .card-overlay{opacity:1}
```

## 5. Layout Principles

**Container:**
- Max width: 1120px
- Side padding: 28px (mobile: 16px)

**Spacing Scale:**
- Section padding top/bottom: 120px (mobile: 64px)
- Component gap (grid): 16-28px
- Card internal padding: 20px
- Hero 左侧内容 max-width: 540px（控制阅读宽度）

**Grid:**
```css
.hero-grid{display:grid;grid-template-columns:1fr 1fr;gap:40px;align-items:center}
.work-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:16px}
.manifesto{display:grid;grid-template-columns:1fr 1fr;gap:40px 64px}
.exp-grid{display:grid;grid-template-columns:1fr 1fr;gap:28px}
.awards-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(290px,1fr));gap:12px}
.contact-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:12px}
```

## 6. Visual Hierarchy 设计原则

- **Hero**: H1 字号 clamp(56px,8vw,96px) × 字距 0.08em —— 强调品牌首位
- **Section 标题**: 字号 clamp(28px,3.5vw,40px) × 上方 gold 短线锚定
- **正文**: 14px 紧凑字号 + 1.9 行高 —— 长文不累
- **辅助信息**: 11px 字号 + 大写 + 浅色 —— 明确层级降级
- **装饰元素**: 暖金短线 (`--gold`) 替代之前的朱红，用于分割线、标签、hover 指示

## 7. Depth & Elevation

| Level | Treatment | Use |
|-------|-----------|-----|
| Flat | `none` | 页面背景、section |
| Subtle | `0 4px 12px rgba(47,45,42,0.04)` | 卡片默认 |
| Hover | `0 12px 32px rgba(47,45,42,0.08)` | 卡片悬停 |
| Modal | `0 24px 48px rgba(0,0,0,0.3)` | lightbox |

**Principle**: 极简用阴影，质感来自材质与空间，不依赖光影模拟。

## 8. Animation & Interaction

**Motion Philosophy**: 缓入缓出、克制安静。只用 opacity 和 transform。
**Tier**: L2，零依赖

### Entrance Animation
```css
.reveal{opacity:0;transform:translateY(20px);transition:all 0.7s cubic-bezier(0.22,1,0.36,1)}
.reveal.in-view{opacity:1;transform:translateY(0)}
```

### Reduced Motion
```css
@media (prefers-reduced-motion: reduce) {
  .reveal{opacity:1;transform:none;transition:none}
  *,*::before,*::after{animation-duration:0.01ms!important;animation-iteration-count:1!important;transition-duration:0.01ms!important}
}
```

## 9. Do's and Don'ts

### Do
- 大量留白，大量呼吸空间
- 暖金作为唯一的主色调——用于分割线、hover、装饰
- 宋体标题搭配黑体正文
- 不对称构图
- Hero 右侧留白+极淡网格+金角标——空而不空
- hover 交互克制统一，只用 opacity 和 translateY

### Don't
- ❌ 不使用任何 Google Fonts 或其他在线字体
- ❌ 不加 emoji 作为装饰
- ❌ 不使用阴影体系
- ❌ 不做大面积渐变或鲜艳配色
- ❌ 没有旋转、弹跳、闪烁等花哨动画
- ❌ 不加玻璃拟态、霓虹光效
- ❌ 不加圆角大于 4px 的元素

## 10. Responsive Behavior

**Breakpoints:**
| Name | Width | Key Changes |
|------|-------|-------------|
| Desktop | > 968px | 两列布局、Hero 右侧装饰 |
| Tablet | 768-968px | 合并为单列、隐藏 Hero 右侧 |
| Mobile | < 768px | 全单列、汉堡菜单、section-padding 减至 64px |

```css
@media(max-width:968px){
  .hero-grid{grid-template-columns:1fr}
  .hero-right{display:none}
  .manifesto{grid-template-columns:1fr}
  .exp-grid{grid-template-columns:1fr}
  :root{--section-py:80px}
}
@media(max-width:768px){
  .work-grid{grid-template-columns:1fr}
  .awards-grid{grid-template-columns:1fr}
  .contact-grid{grid-template-columns:1fr}
  :root{--section-py:64px}
}
```
