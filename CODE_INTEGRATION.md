# CyberNet 数字安全中枢 - 完整代码整合

## 项目结构
```
CyberNet/
├── index.html          # 首页
├── about.html          # 关于平台
├── news.html           # 安全资讯
├── dashboard.html      # 威胁监控
├── knowledge.html      # 安全科普
├── tools.html          # 在线工具
├── quiz.html           # 安全测评
├── resources.html      # 学习资源
├── contact.html        # 留言反馈
├── styles/
│   └── main.css        # 全局样式
├── js/
│   └── main.js         # 公共脚本
├── images/             # 图片资源
│   ├── news-*.jpg      # 资讯图片
│   ├── resource-*.jpg  # 资源图片
│   └── tag-*.jpg       # 标签图片
├── .coze               # 项目配置
└── AGENTS.md           # 项目说明
```

---

## 1. 公共样式文件 (styles/main.css)

```css
/* ========== CSS 变量 ========== */
:root {
  /* 颜色系统 */
  --primary: #6366f1;
  --primary-light: #818cf8;
  --primary-dark: #4f46e5;
  --secondary: #8b5cf6;
  --accent: #06b6d4;
  --success: #10b981;
  --warning: #f59e0b;
  --danger: #ef4444;

  /* 背景颜色 */
  --bg-primary: #0a0e1a;
  --bg-secondary: #0f1423;
  --bg-tertiary: #1a1f35;
  --bg-card: #131829;
  --bg-hover: #1e2540;

  /* 文字颜色 */
  --text-primary: #f0f0f0;
  --text-secondary: #a0a5b9;
  --text-muted: #6b7280;
  --text-inverse: #000000;

  /* 边框颜色 */
  --border-color: rgba(99, 102, 241, 0.2);
  --border-hover: rgba(99, 102, 241, 0.4);

  /* 渐变 */
  --gradient-primary: linear-gradient(135deg, #6366f1, #8b5cf6);
  --gradient-neon: linear-gradient(135deg, #00d4ff, #8b5cf6, #bf00ff);
  --gradient-warm: linear-gradient(135deg, #f97316, #ef4444);
  --gradient-cool: linear-gradient(135deg, #06b6d4, #3b82f6);

  /* 阴影 */
  --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.1);
  --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.3);
  --shadow-lg: 0 10px 20px rgba(0, 0, 0, 0.4);
  --shadow-glow: 0 0 30px rgba(99, 102, 241, 0.3);

  /* 圆角 */
  --radius-sm: 0.25rem;
  --radius-md: 0.5rem;
  --radius-lg: 0.75rem;
  --radius-xl: 1rem;
  --radius-full: 9999px;

  /* 间距 */
  --spacing-xs: 0.5rem;
  --spacing-sm: 0.75rem;
  --spacing-md: 1rem;
  --spacing-lg: 1.5rem;
  --spacing-xl: 2rem;
  --spacing-2xl: 3rem;

  /* 动画 */
  --transition-fast: 0.2s ease;
  --transition-normal: 0.3s ease;
  --transition-slow: 0.5s ease;

  /* 导航栏 */
  --nav-height: 70px;
}

/* ========== 全局样式 ========== */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif;
  background: var(--bg-primary);
  color: var(--text-primary);
  line-height: 1.6;
  overflow-x: hidden;
}

/* ========== 页面加载动画 ========== */
.page-loader {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: var(--bg-primary);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 9999;
  transition: opacity 0.5s ease, visibility 0.5s ease;
}

.page-loader.hidden {
  opacity: 0;
  visibility: hidden;
}

.loader-content {
  text-align: center;
}

.loader-spinner {
  width: 50px;
  height: 50px;
  border: 3px solid var(--bg-tertiary);
  border-top-color: var(--primary);
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin: 0 auto var(--spacing-md);
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

.loader-text {
  font-size: 0.875rem;
  color: var(--text-secondary);
  letter-spacing: 2px;
}

/* ========== 粒子背景 ========== */
.particles-bg {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  pointer-events: none;
}

#particles-canvas {
  width: 100%;
  height: 100%;
}

/* ========== 导航栏 ========== */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: var(--nav-height);
  background: rgba(10, 14, 26, 0.8);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid var(--border-color);
  z-index: 1000;
  transition: all var(--transition-normal);
}

.navbar.scrolled {
  background: rgba(10, 14, 26, 0.95);
  box-shadow: var(--shadow-md);
}

.navbar-container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 var(--spacing-lg);
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 100%;
}

.navbar-logo {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
  text-decoration: none;
  color: var(--text-primary);
  font-size: 1.25rem;
  font-weight: 700;
  transition: all var(--transition-fast);
}

.navbar-logo:hover {
  color: var(--primary-light);
}

.logo-icon {
  font-size: 1.5rem;
}

.navbar-menu {
  display: flex;
  list-style: none;
  gap: var(--spacing-md);
}

.navbar-menu a {
  color: var(--text-secondary);
  text-decoration: none;
  font-size: 0.95rem;
  font-weight: 500;
  padding: var(--spacing-xs) var(--spacing-md);
  border-radius: var(--radius-full);
  transition: all var(--transition-fast);
}

.navbar-menu a:hover {
  color: var(--text-primary);
  background: var(--bg-tertiary);
}

.navbar-menu a.active {
  color: var(--primary-light);
  background: rgba(99, 102, 241, 0.1);
}

.navbar-actions {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
}

.theme-toggle {
  width: 40px;
  height: 40px;
  border: 1px solid var(--border-color);
  background: var(--bg-tertiary);
  border-radius: var(--radius-md);
  cursor: pointer;
  font-size: 1.25rem;
  transition: all var(--transition-fast);
  display: flex;
  align-items: center;
  justify-content: center;
}

.theme-toggle:hover {
  border-color: var(--primary);
  transform: scale(1.05);
}

.menu-toggle {
  width: 40px;
  height: 40px;
  background: transparent;
  border: none;
  cursor: pointer;
  display: none;
  flex-direction: column;
  gap: 5px;
}

.menu-toggle span {
  width: 25px;
  height: 2px;
  background: var(--text-primary);
  transition: all var(--transition-fast);
}

.menu-toggle.active span:nth-child(1) {
  transform: rotate(45deg) translate(5px, 5px);
}

.menu-toggle.active span:nth-child(2) {
  opacity: 0;
}

.menu-toggle.active span:nth-child(3) {
  transform: rotate(-45deg) translate(5px, -5px);
}

/* ========== 主内容 ========== */
.main-content {
  position: relative;
  z-index: 1;
  min-height: calc(100vh - var(--nav-height));
  padding-top: var(--nav-height);
}

.container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 var(--spacing-lg);
}

.section {
  padding: var(--spacing-2xl) 0;
}

.section-title {
  font-size: 2rem;
  font-weight: 700;
  text-align: center;
  margin-bottom: var(--spacing-sm);
  background: var(--gradient-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.section-subtitle {
  text-align: center;
  color: var(--text-secondary);
  margin-bottom: var(--spacing-xl);
  font-size: 1rem;
}

/* ========== 网格系统 ========== */
.grid {
  display: grid;
  gap: var(--spacing-lg);
}

.grid-2 {
  grid-template-columns: repeat(2, 1fr);
}

.grid-3 {
  grid-template-columns: repeat(3, 1fr);
}

.grid-4 {
  grid-template-columns: repeat(4, 1fr);
}

/* ========== 按钮 ========== */
.btn {
  display: inline-flex;
  align-items: center;
  gap: var(--spacing-sm);
  padding: var(--spacing-sm) var(--spacing-xl);
  border: none;
  border-radius: var(--radius-lg);
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  text-decoration: none;
  transition: all var(--transition-fast);
  color: white;
}

.btn-primary {
  background: var(--gradient-primary);
  box-shadow: var(--shadow-md);
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-lg);
}

.btn-secondary {
  background: var(--bg-tertiary);
  border: 1px solid var(--border-color);
}

.btn-secondary:hover {
  background: var(--bg-hover);
  border-color: var(--primary);
}

.btn-glow {
  animation: glow 2s ease-in-out infinite;
}

@keyframes glow {
  0%, 100% {
    box-shadow: 0 0 5px rgba(99, 102, 241, 0.5);
  }
  50% {
    box-shadow: 0 0 20px rgba(99, 102, 241, 0.8);
  }
}

/* ========== 滚动显示动画 ========== */
.scroll-reveal {
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}

.scroll-reveal.revealed {
  opacity: 1;
  transform: translateY(0);
}

.delay-1 { transition-delay: 0.1s; }
.delay-2 { transition-delay: 0.2s; }
.delay-3 { transition-delay: 0.3s; }
.delay-4 { transition-delay: 0.4s; }

/* ========== 页脚 ========== */
.footer {
  background: var(--bg-secondary);
  border-top: 1px solid var(--border-color);
  padding: var(--spacing-2xl) 0 var(--spacing-lg);
}

.footer-content {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: var(--spacing-xl);
  margin-bottom: var(--spacing-xl);
}

.footer-section h4 {
  color: var(--text-primary);
  margin-bottom: var(--spacing-md);
  font-size: 1.1rem;
}

.footer-section ul {
  list-style: none;
}

.footer-section ul li {
  margin-bottom: var(--spacing-xs);
}

.footer-section a {
  color: var(--text-secondary);
  text-decoration: none;
  transition: color var(--transition-fast);
}

.footer-section a:hover {
  color: var(--primary-light);
}

.footer-bottom {
  text-align: center;
  padding-top: var(--spacing-lg);
  border-top: 1px solid var(--border-color);
  color: var(--text-muted);
  font-size: 0.875rem;
}

/* ========== 回到顶部按钮 ========== */
.back-to-top {
  position: fixed;
  bottom: var(--spacing-xl);
  right: var(--spacing-xl);
  width: 50px;
  height: 50px;
  background: var(--gradient-primary);
  border: none;
  border-radius: var(--radius-full);
  color: white;
  font-size: 1.5rem;
  cursor: pointer;
  opacity: 0;
  visibility: hidden;
  transition: all var(--transition-normal);
  box-shadow: var(--shadow-lg);
  z-index: 900;
}

.back-to-top.visible {
  opacity: 1;
  visibility: visible;
}

.back-to-top:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-glow);
}

/* ========== 响应式设计 ========== */
@media (max-width: 1200px) {
  .footer-content {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 992px) {
  .grid-4,
  .grid-3 {
    grid-template-columns: repeat(2, 1fr);
  }

  .menu-toggle {
    display: flex;
  }

  .navbar-menu {
    position: fixed;
    top: var(--nav-height);
    left: 0;
    width: 100%;
    background: var(--bg-secondary);
    flex-direction: column;
    padding: var(--spacing-lg);
    transform: translateY(-100%);
    opacity: 0;
    visibility: hidden;
    transition: all var(--transition-normal);
  }

  .navbar-menu.active {
    transform: translateY(0);
    opacity: 1;
    visibility: visible;
  }

  .navbar-menu a {
    width: 100%;
    text-align: center;
    padding: var(--spacing-md);
  }
}

@media (max-width: 768px) {
  .grid-4,
  .grid-3,
  .grid-2 {
    grid-template-columns: 1fr;
  }

  .footer-content {
    grid-template-columns: 1fr;
  }

  .back-to-top {
    bottom: var(--spacing-md);
    right: var(--spacing-md);
  }
}

/* ========== 标签样式 ========== */
.tag {
  display: inline-block;
  padding: var(--spacing-xs) var(--spacing-sm);
  background: var(--bg-tertiary);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-full);
  font-size: 0.75rem;
  color: var(--text-secondary);
  transition: all var(--transition-fast);
}

.tag:hover {
  border-color: var(--primary);
  color: var(--primary-light);
}

/* ========== 徽章样式 ========== */
.badge {
  display: inline-block;
  padding: var(--spacing-xs) var(--spacing-sm);
  border-radius: var(--radius-full);
  font-size: 0.75rem;
  font-weight: 600;
}

.badge-success {
  background: rgba(16, 185, 129, 0.2);
  color: #10b981;
}

.badge-warning {
  background: rgba(245, 158, 11, 0.2);
  color: #f59e0b;
}

.badge-danger {
  background: rgba(239, 68, 68, 0.2);
  color: #ef4444;
}

.badge-info {
  background: rgba(99, 102, 241, 0.2);
  color: #6366f1;
}
```

---

## 2. 公共脚本文件 (js/main.js)

```javascript
/**
 * CyberNet 数字安全中枢 - 公共脚本
 * 包含全局交互、导航、粒子背景等
 */

// ========== 命名空间 ==========
const CyberNet = window.CyberNet || {};

// ========== 页面加载动画 ==========
window.addEventListener('load', () => {
  const loader = document.querySelector('.page-loader');
  if (loader) {
    setTimeout(() => {
      loader.classList.add('hidden');
    }, 500);
  }
});

// ========== 导航栏滚动效果 ==========
const navbar = document.querySelector('.navbar');

window.addEventListener('scroll', () => {
  if (window.scrollY > 50) {
    navbar?.classList.add('scrolled');
  } else {
    navbar?.classList.remove('scrolled');
  }
});

// ========== 移动端菜单切换 ==========
const menuToggle = document.querySelector('.menu-toggle');
const navbarMenu = document.querySelector('.navbar-menu');

menuToggle?.addEventListener('click', () => {
  menuToggle.classList.toggle('active');
  navbarMenu?.classList.toggle('active');
});

navbarMenu?.querySelectorAll('a').forEach(link => {
  link.addEventListener('click', () => {
    menuToggle?.classList.remove('active');
    navbarMenu?.classList.remove('active');
  });
});

// ========== 粒子背景 ==========
class ParticleBackground {
  constructor(canvas) {
    this.canvas = canvas;
    this.ctx = canvas.getContext('2d');
    this.particles = [];
    this.mouseX = 0;
    this.mouseY = 0;
    this.particleCount = 80;
    this.connectionDistance = 150;
    
    this.init();
    this.animate();
    this.bindEvents();
  }
  
  init() {
    this.resize();
    for (let i = 0; i < this.particleCount; i++) {
      this.particles.push({
        x: Math.random() * this.canvas.width,
        y: Math.random() * this.canvas.height,
        vx: (Math.random() - 0.5) * 0.5,
        vy: (Math.random() - 0.5) * 0.5,
        radius: Math.random() * 2 + 1,
        color: `rgba(${99 + Math.random() * 50}, ${102 + Math.random() * 50}, 241, ${0.5 + Math.random() * 0.5})`
      });
    }
  }
  
  resize() {
    this.canvas.width = window.innerWidth;
    this.canvas.height = window.innerHeight;
  }
  
  bindEvents() {
    window.addEventListener('resize', () => this.resize());
    window.addEventListener('mousemove', (e) => {
      this.mouseX = e.clientX;
      this.mouseY = e.clientY;
    });
  }
  
  animate() {
    this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height);
    
    this.particles.forEach((p, i) => {
      p.x += p.vx;
      p.y += p.vy;
      
      if (p.x < 0 || p.x > this.canvas.width) p.vx *= -1;
      if (p.y < 0 || p.y > this.canvas.height) p.vy *= -1;
      
      const dx = this.mouseX - p.x;
      const dy = this.mouseY - p.y;
      const dist = Math.sqrt(dx * dx + dy * dy);
      
      if (dist < 100) {
        p.x -= dx * 0.02;
        p.y -= dy * 0.02;
      }
      
      this.ctx.beginPath();
      this.ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2);
      this.ctx.fillStyle = p.color;
      this.ctx.fill();
      
      for (let j = i + 1; j < this.particles.length; j++) {
        const p2 = this.particles[j];
        const dx = p.x - p2.x;
        const dy = p.y - p2.y;
        const dist = Math.sqrt(dx * dx + dy * dy);
        
        if (dist < this.connectionDistance) {
          this.ctx.beginPath();
          this.ctx.moveTo(p.x, p.y);
          this.ctx.lineTo(p2.x, p2.y);
          this.ctx.strokeStyle = `rgba(99, 102, 241, ${0.3 * (1 - dist / this.connectionDistance)})`;
          this.ctx.lineWidth = 0.5;
          this.ctx.stroke();
        }
      }
    });
    
    requestAnimationFrame(() => this.animate());
  }
}

const particlesCanvas = document.getElementById('particles-canvas');
if (particlesCanvas) {
  new ParticleBackground(particlesCanvas);
}

// ========== 视差效果 ==========
const heroTitle = document.querySelector('.hero-title');
window.addEventListener('mousemove', (e) => {
  if (heroTitle) {
    const moveX = (e.clientX - window.innerWidth / 2) * 0.01;
    const moveY = (e.clientY - window.innerHeight / 2) * 0.01;
    heroTitle.style.transform = `translate(${moveX}px, ${moveY}px)`;
  }
});

// ========== 滚动显示动画 ==========
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('revealed');
    }
  });
}, { threshold: 0.1, rootMargin: '0px 0px -50px 0px' });

document.querySelectorAll('.scroll-reveal').forEach(el => {
  observer.observe(el);
});

// ========== 回到顶部按钮 ==========
const backToTop = document.querySelector('.back-to-top');

window.addEventListener('scroll', () => {
  if (window.scrollY > 300) {
    backToTop?.classList.add('visible');
  } else {
    backToTop?.classList.remove('visible');
  }
});

backToTop?.addEventListener('click', () => {
  window.scrollTo({ top: 0, behavior: 'smooth' });
});

// ========== 数字动画 ==========
CyberNet.animateNumber = function(element, target, duration = 2000) {
  const start = 0;
  const startTime = performance.now();
  
  function update(currentTime) {
    const elapsed = currentTime - startTime;
    const progress = Math.min(elapsed / duration, 1);
    const easeProgress = 1 - Math.pow(1 - progress, 3);
    const current = Math.floor(start + (target - start) * easeProgress);
    element.textContent = current.toLocaleString();
    if (progress < 1) requestAnimationFrame(update);
  }
  
  requestAnimationFrame(update);
};

// ========== 模态框控制 ==========
CyberNet.openModal = function(modalId) {
  const modal = document.getElementById(modalId);
  modal?.classList.add('active');
  document.body.style.overflow = 'hidden';
};

CyberNet.closeModal = function(modalId) {
  const modal = document.getElementById(modalId);
  modal?.classList.remove('active');
  document.body.style.overflow = '';
};

// ========== Toast 提示 ==========
CyberNet.showToast = function(message, type = 'info') {
  const toast = document.createElement('div');
  toast.className = `toast toast-${type}`;
  toast.textContent = message;
  toast.style.cssText = `
    position: fixed;
    top: 20px;
    right: 20px;
    padding: 1rem 1.5rem;
    background: var(--bg-card);
    border: 1px solid var(--border-color);
    border-radius: var(--radius-lg);
    box-shadow: var(--shadow-lg);
    z-index: 9999;
    animation: slideIn 0.3s ease;
  `;
  document.body.appendChild(toast);
  
  setTimeout(() => {
    toast.style.animation = 'slideOut 0.3s ease';
    setTimeout(() => toast.remove(), 300);
  }, 3000);
};

// 导出到全局
window.CyberNet = CyberNet;
```

---

## 3. 项目配置文件 (.coze)

```toml
[project]
entrypoint = "index.html"
requires = ["python-3.12"]

[dev]
build = []
run = ["python", "-m", "http.server", "5000", "--bind", "0.0.0.0"]

[deploy]
build = []
run = ["python", "-m", "http.server", "5000", "--bind", "0.0.0.0"]
```

---

## 4. 项目说明文件 (AGENTS.md)

```markdown
# CyberNet 数字安全中枢

## 项目概述
CyberNet 是一个功能完整的网络安全平台，提供安全资讯、威胁监控、安全科普、在线工具、安全测评和学习资源等功能。

## 技术栈
- **前端**: HTML5 + CSS3 + JavaScript (ES6+)
- **样式**: 自定义 CSS (使用 CSS 变量)
- **图标**: Emoji + 图片
- **动画**: CSS 动画 + JavaScript
- **响应式**: 移动端优先设计

## 页面说明

### 1. index.html (首页)
- Hero 区域展示核心价值
- 快速入口卡片
- 数据统计动画
- 核心特性展示

### 2. news.html (安全资讯)
- 新闻卡片展示
- 筛选功能（全部、热点、预警、教程）
- 新闻详情弹窗
- 图片封面

### 3. dashboard.html (威胁监控)
- 威胁监控面板
- 实时数据展示
- 攻击趋势图表
- 防护统计

### 4. knowledge.html (安全科普)
- 分类标签（全部、钓鱼识别、密码安全、隐私防护、WiFi安全）
- 手风琴内容展示
- 安全知识普及

### 5. tools.html (在线工具)
- 密码生成器
- 加密解密工具
- 哈希计算工具
- 实用安全工具

### 6. quiz.html (安全测评)
- 安全知识测试
- 多选题和判断题
- 成绩计算
- 评估报告

### 7. resources.html (学习资源)
- 资源卡片展示
- 翻转卡片效果
- 拖拽排序功能
- 外部链接跳转

### 8. about.html (关于平台)
- 平台介绍
- 团队介绍
- 发展历程
- 联系方式

### 9. contact.html (留言反馈)
- 联系表单
- 留言板
- 反馈提交

## 公共功能

### 导航栏
- 响应式导航
- 移动端菜单
- 主题切换
- 滚动效果

### 页面加载动画
- 加载旋转动画
- 渐隐过渡

### 粒子背景
- 动态粒子效果
- 鼠标交互
- 网格连接

### 滚动动画
- 滚动显示效果
- 延迟动画
- 渐入渐出

## 图片资源
- **news-*.jpg**: 资讯封面图片 (6张)
- **resource-*.jpg**: 资源图标图片 (9张)
- **tag-*.jpg**: 标签图标图片 (8张)

## 部署说明
1. 将所有文件上传到服务器
2. 运行 `python -m http.server 5000 --bind 0.0.0.0`
3. 访问 `http://localhost:5000`
4. 或使用其他静态文件服务器

## 浏览器兼容性
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

## 开发规范
- 使用 ES6+ 语法
- 遵循语义化 HTML
- 使用 CSS 变量管理主题
- 响应式设计优先
- 性能优化

## 注意事项
1. 图片路径使用相对路径
2. 所有链接使用 `.html` 扩展名
3. 使用 CSS 变量统一样式
4. 避免使用 alert，使用 Toast 提示
5. 表单提交使用 JavaScript 处理
```

---

## 快速开始

### 1. 本地运行
```bash
cd CyberNet
python -m http.server 5000
```

### 2. 访问地址
- 首页: http://localhost:5000
- 安全资讯: http://localhost:5000/news.html
- 威胁监控: http://localhost:5000/dashboard.html
- 安全科普: http://localhost:5000/knowledge.html
- 在线工具: http://localhost:5000/tools.html
- 安全测评: http://localhost:5000/quiz.html
- 学习资源: http://localhost:5000/resources.html
- 关于平台: http://localhost:5000/about.html
- 留言反馈: http://localhost:5000/contact.html

### 3. 文件清单
- 9个 HTML 页面
- 1个 CSS 样式文件
- 1个 JavaScript 脚本文件
- 23个图片资源
- 1个配置文件
- 1个说明文档

## 总结
CyberNet 是一个功能完善、设计精美的网络安全平台，包含安全资讯、威胁监控、安全科普、在线工具、安全测评和学习资源等核心功能。所有页面采用统一的视觉风格和交互体验，支持响应式设计，适配各种设备。
