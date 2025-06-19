# 🚀 Vue CLI Template

## 📋 项目概述

这是一个专门针对打包配置进行优化的 Vue 脚手架模板，支持 PC 端和移动端 H5 应用开发。该模板具有以下特点：

- ✅ 对打包配置进行了全面优化，提升应用性能
- 📱 针对 H5 和 PC 场景分别提供了不同的启动命令
- 🔄 封装了针对 Element UI 和 Vant 组件库的 Axios 请求
- 🎨 集成了 SVG 图标组件系统
- ⚡ 支持多环境配置和构建

## 🛠️ 技术栈

- 核心框架：Vue 2.x
- UI 组件库：Element UI (PC 端)、Vant (移动端)
- 状态管理：Vuex
- 路由管理：Vue Router
- HTTP 请求：Axios
- 打包工具：Webpack (Vue CLI)

## 🔧 项目配置

### Webpack 配置亮点 (vue.config.js)

```javascript
// vue.config.js 主要优化配置

// 1. 代码压缩和优化
// - 生产环境使用CompressionPlugin进行Gzip压缩
// - 使用TerserPlugin移除console.log和debugger
// - 提取公共代码，减少重复

// 2. 路径别名配置
resolve: {
  alias: {
    '@': resolve('src'),
    '@c': resolve('src/components'),
    '@u': resolve('src/utils'),
  }
}

// 3. 缓存优化
cache: {
  type: 'filesystem', // 使用文件系统级别的缓存
  buildDependencies: {
    config: [__filename]
  }
}

// 4. 代码分割与优化
optimization: {
  usedExports: true, // 移除未使用代码
  minimize: true,    // 代码压缩
  splitChunks: {     // 分离公共模块
    cacheGroups: {
      vendors: {
        test: /[\\/]node_modules[\\/]/,
        name: 'vendors',
        chunks: 'all',
        minChunks: 2  // 至少被引用2次
      }
    }
  },
  concatenateModules: true // 作用域提升
}

// 5. SVG图标加载配置
// 将SVG图标转换为Vue组件
```

### Babel 配置亮点 (babel.config.js)

```javascript
// 1. 按需加载polyfill，支持旧浏览器
[
  "@babel/preset-env",
  {
    useBuiltIns: "usage",
    corejs: 3,
  },
][
  // 2. 组件库按需加载
  // Vant组件按需引入
  ("import",
  {
    libraryName: "vant",
    libraryDirectory: "es",
    style: true,
  })
][
  // Element UI组件按需引入
  ("component",
  {
    libraryName: "element-ui",
    styleLibraryName: "theme-chalk",
  })
];

// 3. 开发环境优化
// 动态导入节点加速热更新
("dynamic-import-node");
// 可选链支持
("@babel/plugin-proposal-optional-chaining");
```

### PostCSS 配置 (postcss.config.js)

针对 H5 环境，自动将 px 单位转换为 vw 单位，实现移动端适配：

```javascript
// H5环境下的视口配置
'postcss-px-to-viewport': {
  viewportWidth: 375, // 设计稿宽度
  unitPrecision: 5,   // 转换精度
  viewportUnit: 'vw', // 转换单位
  minPixelValue: 1    // 最小转换像素
}
```

## 📂 项目结构

```
vue-cli-template/
├── public/               # 静态资源目录
│   ├── index.html        # HTML模板
│   └── ...
├── src/                  # 源代码目录
│   ├── assets/           # 资源文件
│   │   └── icons/        # SVG图标
│   ├── components/       # 公共组件
│   │   ├── IconFont/     # 字体图标组件
│   │   └── SvgIcon/      # SVG图标组件
│   ├── router/           # 路由配置
│   ├── store/            # Vuex状态管理
│   ├── utils/            # 工具函数
│   │   ├── auth.js       # 权限相关
│   │   └── axios.js      # 请求封装
│   ├── App.vue           # 根组件
│   └── main.js           # 入口文件
├── .env.*                # 环境变量配置文件
├── babel.config.js       # Babel配置
├── vue.config.js         # Vue CLI配置
├── postcss.config.js     # PostCSS配置
└── package.json          # 项目依赖
```

## 📦 主要功能

### 1. 打包优化

- ✂️ Tree Shaking：移除未使用代码
- 🧵 多线程构建
- 🗜️ 代码压缩和去除调试代码
- 📊 Bundle 分析可视化
- 💾 构建缓存加速

### 2. 跨端适配

- 📱 H5 环境自动启用 px 转 vw 适配
- 💻 PC 环境保持原始尺寸
- 🔄 根据环境自动切换 UI 组件库

### 3. 组件库集成

- 🖥️ PC 端集成 Element UI
- 📱 移动端集成 Vant
- 🔍 均支持按需加载

### 4. SVG 图标系统

使用方式：

1. 将 SVG 文件放入`src/assets/icons/svg`目录
2. 在组件中使用：`<svg-icon class="icon-name"></svg-icon>`

## 🚀 快速开始

### 安装依赖

```bash
npm install
# 或
pnpm install
```

### 开发环境

```bash
# PC端开发
npm run dev

# H5端开发
npm run dev:h5
```

### 构建生产版本

```bash
# PC端生产版本
npm run build:prod

# H5端生产版本
npm run build:prod:h5
```

## 📝 项目配置环境说明

- `dev`: 开发环境 (PC)
- `devh5`: 开发环境 (H5)
- `prod`: 生产环境 (PC)
- `prodh5`: 生产环境 (H5)
- `pre`: 预发布环境
- `test`: 测试环境

## 👨‍💻 关于作者

```javascript
const author = {
  nickName: "ZsTs119",
  email: "zsts@foxmail.com",
  site: "https://github.com/ZsTs119",
};
```

## 🤝 贡献

欢迎提交问题或改进建议！

## 📄 许可

[MIT](LICENSE)
