# HR管理系统前端重构 - macOS 12 风格

## 🎨 设计系统升级

### 核心色彩体系 macOS 12
- **主色调**：从 #409EFF 升级到 #007AFF（Apple 标准蓝）
- **成功色**：#34C759
- **警告色**：#FF9500
- **危险色**：#FF3B30
- **文字**：#1D1D1F (主) / #424245 (常规) / #86868B (次要)

### 设计元素
1. **圆角系统**
   - 小：6px (input, tags)
   - 中：8px (buttons, modals)
   - 大：12px (cards, dialogs)

2. **阴影系统** - 柔和 macOS 风格
   - 浅阴影：0 2px 8px rgba(0,0,0,0.08)
   - 中阴影：0 8px 24px rgba(0,0,0,0.12)
   - 深阴影：0 12px 32px rgba(0,0,0,0.15)

3. **毛玻璃效果**
   - Header：backdrop-filter blur(30px) + 半透明背景
   - Card：受控毛玻璃，增强可读性
   - Modal：30px模糊 + 完全透明背景

4. **间距系统**
   - xs: 4px | sm: 8px | md: 12px | lg: 16px | xl: 20px | 2xl: 24px

## 📁 重构的文件

### 设计系统文件
- **reset.less** - CSS 变量系统升级
- **glassmorphism.less** - 毛玻璃效果库（新增）
- **forms.less** - 表单样式统一（新增）

### 全局样式
- **common.less** - Element UI 组件美化
- **table.less** - 数据表格优化
- **home.less** - 首页卡片布局

### 组件样式
- **Header.vue** - 毛玻璃顶部栏 + 优化头像
- **Aside.vue** - 深色侧边栏 + 更新配色
- **login/index.vue** - 清爽登录界面

## ✨ 主要优化

### Header 组件
- ✅ 毛玻璃模糊背景
- ✅ 柔和阴影
- ✅ 头像圆形设计 + hover 放大
- ✅ 按钮渐变 + 柔和阴影

### Aside 侧边栏
- ✅ 深色毛玻璃背景
- ✅ 新的活跃状态指示器
- ✅ 调整菜单项间距和圆角
- ✅ 更好的悬停反馈

### 卡片系统
- ✅ 12px 圆角
- ✅ 细致边框
- ✅ Hover 时向上浮动
- ✅ 柔和阴影过渡

### 表单样式
- ✅ Input 圆角优化
- ✅ Focus 时蓝色光圈
- ✅ 更好的可访问性
- ✅ 统一 placeholder 颜色

### 表格优化
- ✅ 表头渐变背景
- ✅ 行 hover 效果
- ✅ 分页器美化
- ✅ 更好的行间距

### 登录页面
- ✅ 增大圆角（20px）到 16px
- ✅ 增强毛玻璃效果
- ✅ 优化输入框样式
- ✅ 验证码框美化

## 🔄 后端兼容性

- ✅ **零破坏性变更** - 仅修改样式，不改 Vue 逻辑
- ✅ **API 完全兼容** - 无数据格式改变
- ✅ **组件结构不变** - 可直接替换样式文件

## 📐 CSS 变量使用

所有样式现在使用 CSS 变量管理，支持运行时修改：

```less
// 使用示例
background: var(--card-bg);
border-radius: var(--card-radius);
box-shadow: var(--card-shadow);
color: var(--text-primary);
```

## 🎯 性能优化

- ✅ backdrop-filter 启用硬件加速
- ✅ 过渡效果优化（使用 ease-in-out）
- ✅ 避免过度动画
- ✅ 合理的层级管理

## 🚀 部署建议

1. 编译测试
   ```bash
   npm run build
   ```

2. 本地预览
   ```bash
   npm run serve
   ```

3. 浏览器支持
   - Chrome 90+
   - Firefox 88+
   - Safari 14+
   - Edge 90+

## 📝 注意事项

- 首次加载时毛玻璃效果可能需要 GPU 加速
- 移动设备上建议关闭或弱化毛玻璃效果
- 某些老旧浏览器可能不支持 backdrop-filter

## 🎨 自定义颜色

修改 `reset.less` 中的 CSS 变量即可全局改色：

```less
:root {
  --color-primary: #007AFF;  // 修改主色
  --sidebar-bg-start: #1C1C1E;  // 修改侧边栏色
  // ...其他变量
}
```

---

**重构完成日期**: 2026-06-16
**设计参考**: Apple macOS 12 Human Interface Guidelines
