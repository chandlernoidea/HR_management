# 样式重构对比指南

## 🎨 颜色系统变化

### 旧系统 vs 新系统

| 用途 | 旧色值 | 新色值 | 变化 |
|------|--------|--------|------|
| 主色 | #409EFF | #007AFF | 更深、更清爽的蓝 |
| 成功 | #67C23A | #34C759 | Apple 标准绿 |
| 警告 | #E6A23C | #FF9500 | Apple 标准橙 |
| 危险 | #F56C6C | #FF3B30 | Apple 标准红 |
| 侧边栏 | #1a1a2e → #16213e | #1C1C1E → #2C2C2E | 更偏黑色 |
| 背景 | #f0f2f5 | #F5F5F7 | 更浅的灰 |

## 📐 圆角变化

| 组件 | 旧值 | 新值 | 说明 |
|------|------|------|------|
| Input | 4px | 8px | 更大更舒适 |
| Card | 8px | 12px | macOS 标准 |
| Dialog | 12px → 8px | 16px → 12px | 更统一 |
| Button | 4px | 8px-12px | 渐进式变化 |
| Tags | 12px | 12px | 保持不变 |

## 🌟 阴影系统升级

### 卡片阴影对比

**旧**:
```css
box-shadow: 0 2px 12px rgba(0, 0, 0, 0.06);
box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);  /* hover */
```

**新** (macOS 风格):
```css
box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);  /* 柔和 */
box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12); /* hover */
```

## ✨ 毛玻璃效果

### Header 对比

**旧**:
```css
background: #ffffff;
box-shadow: 0 1px 4px rgba(0, 21, 41, 0.08);
```

**新** (macOS 12):
```css
background: rgba(255, 255, 255, 0.95);
backdrop-filter: blur(30px);
border-bottom: 1px solid rgba(0, 0, 0, 0.06);
box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08);
```

## 🎯 按钮样式

### 主色按钮

**旧**:
```less
background: linear-gradient(135deg, #409EFF, #3a8ee6);
&:hover {
  background: linear-gradient(135deg, #66b1ff, #409EFF);
  box-shadow: 0 4px 12px rgba(64, 158, 255, 0.4);
}
```

**新**:
```less
background: #007AFF;
&:hover {
  background: #3C9FFF;
  box-shadow: 0 4px 12px rgba(0, 122, 255, 0.3);
  transform: translateY(-1px);
}
```

## 📊 表格改进

### 表头行

**旧**:
```css
background-color: #f8f9fc;
border-bottom: 2px solid #ebeef5;
```

**新** (macOS):
```css
background: linear-gradient(to bottom, 
  rgba(255, 255, 255, 0.8), 
  rgba(245, 245, 247, 0.8)
);
border-bottom: 1px solid #E5E5EA;
```

### 行悬停

**旧**:
```css
background-color: rgba(64, 158, 255, 0.04);
```

**新**:
```css
background-color: rgba(0, 122, 255, 0.03);
```

## 📝 表单输入框

### Input 焦点态

**旧**:
```css
box-shadow: 0 0 0 3px rgba(64, 158, 255, 0.15);
```

**新**:
```css
border-color: #007AFF;
box-shadow: 0 0 0 3px rgba(0, 122, 255, 0.1);
```

## 🎬 过渡效果

| 变化 | 旧 | 新 | 说明 |
|------|----|----|------|
| 快速过渡 | 0.2s ease | 0.15s ease | 更快速的反馈 |
| 标准过渡 | 0.3s ease | 0.3s ease-in-out | 更平滑 |
| 缓慢过渡 | 0.5s cubic-bezier(0.4, 0, 0.2, 1) | 保持不变 | 保留原有 |

## 🚀 性能对比

### 加载时间估算
- **毛玻璃效果**: GPU 加速 (支持 backdrop-filter 的浏览器)
- **阴影**: 优化为更浅，减少渲染压力
- **过渡**: 保持 60fps，避免卡顿

## 🎨 Sidebar 侧边栏

### 激活状态

**旧**:
```css
background-color: rgba(64, 158, 255, 0.15);
color: #409EFF;
```

**新** (更强对比):
```css
background-color: rgba(0, 122, 255, 0.2);
color: #00D4FF;
```

## 📱 响应式考虑

### 移动设备
- 毛玻璃效果：可选禁用（性能考虑）
- 圆角：保持 12px 不变
- 间距：使用 CSS 变量方便调整

## ♿ 可访问性改进

1. **颜色对比度**
   - 所有文本: WCAG AA 标准以上
   - 交互元素: 高对比度设计

2. **焦点态**
   - 所有交互元素都有明显的焦点光圈
   - 键盘导航友好

3. **动画**
   - 遵守 `prefers-reduced-motion` 偏好设置

## 🔄 迁移检查表

- [ ] 验证颜色应用
- [ ] 检查圆角显示
- [ ] 测试阴影效果
- [ ] 验证悬停状态
- [ ] 检查焦点状态
- [ ] 测试移动设备
- [ ] 验证后端 API 兼容性

---

**更新日期**: 2026-06-16
**版本**: 1.0 macOS 12 主题
