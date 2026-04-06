# CyberNet 数字安全中枢

## 项目概览

CyberNet 是一个网络安全主题的交互式网站，采用深色科技风格，蓝紫霓虹配色，提供全方位的安全信息服务。

### 技术栈
- **前端**: 原生 HTML5 / CSS3 / JavaScript
- **样式**: 自定义 CSS 变量系统，响应式设计
- **交互**: 原生 JavaScript，Canvas 粒子动画
- **构建**: 无构建依赖，纯静态文件

### 项目结构

```
/workspace/projects/
├── index.html          # 首页 - 粒子背景、视差效果
├── about.html          # 关于平台 - 滚动动画、折叠面板
├── news.html           # 安全资讯 - 卡片列表、筛选标签
├── dashboard.html      # 威胁监控 - 实时数据、图表
├── knowledge.html      # 安全科普 - 手风琴菜单
├── tools.html          # 在线工具 - 密码工具、加解密
├── quiz.html           # 安全测评 - 答题系统
├── resources.html      # 学习资源 - 拖拽卡片、翻转效果
├── contact.html        # 留言反馈 - 表单验证
├── styles/
│   └── main.css        # 全局样式
├── js/
│   └── main.js         # 公共脚本
└── .coze               # 项目配置
```

## 开发指南

### 启动开发服务器

项目使用 Coze CLI 管理：

```bash
# 启动开发服务器（端口 5000）
coze dev

# 或使用 Python 简易服务器
python -m http.server 5000
```

### 样式规范

#### CSS 变量

项目使用 CSS 变量实现主题系统：

```css
:root {
  /* 主题色 */
  --primary: #6366f1;        /* 主色调 */
  --primary-light: #818cf8;  /* 浅主色 */
  --neon-blue: #00d4ff;      /* 霓虹蓝 */
  --neon-purple: #bf00ff;    /* 霓虹紫 */
  
  /* 背景色 */
  --bg-primary: #0a0e1a;     /* 主背景 */
  --bg-secondary: #111827;   /* 次背景 */
  --bg-card: rgba(30, 41, 59, 0.8);  /* 卡片背景 */
  
  /* 文字色 */
  --text-primary: #f1f5f9;   /* 主文字 */
  --text-secondary: #94a3b8; /* 次文字 */
}
```

#### 常用类名

- `.btn-primary` / `.btn-secondary` - 按钮样式
- `.card` / `.card-glow` - 卡片样式
- `.scroll-reveal` - 滚动显示动画
- `.modal` - 模态框
- `.input` - 输入框

### JavaScript 功能

#### 公共函数 (CyberNet 对象)

```javascript
// 数字动画
CyberNet.animateNumber(element, target, duration);

// 模态框控制
CyberNet.openModal(modalId);
CyberNet.closeModal(modalId);

// 复制到剪贴板
CyberNet.copyToClipboard(text, button);

// 工具函数
CyberNet.debounce(func, wait);
CyberNet.throttle(func, limit);
CyberNet.formatDate(date);
```

#### 粒子背景

页面粒子背景通过 `ParticleBackground` 类实现：

```javascript
// 自动初始化
const canvas = document.getElementById('particles-canvas');
new ParticleBackground(canvas);
```

## 页面功能说明

### 1. 首页 (index.html)
- 全屏粒子动态背景
- 鼠标视差效果
- 导航栏滚动变色收缩
- 按钮发光脉冲效果
- 数字统计动画

### 2. 关于平台 (about.html)
- 滚动渐入动画
- 折叠面板展开/收起
- 技术栈悬停提示

### 3. 安全资讯 (news.html)
- 卡片 hover 上浮效果
- 分类筛选标签
- 点击弹窗查看详情

### 4. 威胁监控 (dashboard.html)
- 实时数字跳动
- 环形进度条动画
- Canvas 折线图
- 攻击地域分布展示

### 5. 安全科普 (knowledge.html)
- 手风琴折叠菜单
- 图标悬停发光
- 分类切换功能

### 6. 在线工具 (tools.html)
- 密码强度实时检测
- 随机密码生成器
- Base64 编码/解码
- 复制结果功能

### 7. 安全测评 (quiz.html)
- 单选题交互
- 上一题/下一题导航
- 分数计算与结果展示

### 8. 学习资源 (resources.html)
- 卡片拖拽排序
- 分类筛选
- 悬停翻转效果

### 9. 留言反馈 (contact.html)
- 表单实时验证
- 提交加载动画
- 成功弹窗提示

## 全局交互功能

所有页面统一具备以下功能：

1. **平滑滚动** - CSS `scroll-behavior: smooth`
2. **深色模式切换** - 右上角主题切换按钮
3. **回到顶部按钮** - 滚动超过 300px 显示
4. **页面加载动画** - 首次加载显示 loading
5. **响应式适配** - 支持手机/平板/桌面

## 响应式断点

```css
@media (max-width: 1200px) { /* 大屏 */ }
@media (max-width: 992px)  { /* 中屏 - 移动端菜单 */ }
@media (max-width: 768px)  { /* 平板 */ }
@media (max-width: 480px)  { /* 手机 */ }
```

## 测试与验证

### 服务存活检测
```bash
curl -I http://localhost:5000
```

### 页面状态检测
```bash
curl -s -o /dev/null -w '%{http_code}' http://localhost:5000/index.html
```

## 注意事项

1. 所有页面共享 `styles/main.css` 和 `js/main.js`
2. 导航栏使用固定定位，内容区域需预留 `var(--nav-height)` 高度
3. 粒子背景使用 Canvas，需要 `#particles-canvas` 元素
4. 模态框需要独立的 HTML 结构和 JS 控制逻辑
