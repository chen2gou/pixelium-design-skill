# pixelium-design-skill

Pixelium Design Skill 是面向 Claude Code / AI Agent 的像素风 Vue 3 组件库专家技能，适合在开发 `@pixelium/web-vue` 项目时辅助完成组件选型、API 使用、示例编写、页面实现和问题排查。

> AI 组件知识来源：[`shika-works/pixelium-design`](https://github.com/shika-works/pixelium-design)。本 Skill 基于该组件库的公开信息整理，用于帮助 AI Agent 更准确地生成和修改 Pixelium Design 相关代码。

## 30 秒开始

```bash
npx skills add https://github.com/chen2gou/pixelium-design-skill --skill pixelium-design
```

安装完成后，在 Claude Code 中直接描述你的需求，例如：

```text
帮我用 Pixelium Design 做一个像素风登录页，使用 Vue 3 + TypeScript，包含账号、密码、记住我和提交按钮。
```

## 也可以让有 shell 权限的 AI Agent 安装

把下面这段话直接发给有 shell 权限的 AI Agent：

```text
帮我安装 pixelium-design。请把 https://github.com/chen2gou/pixelium-design-skill 克隆到 ~/.claude/skills/pixelium-design，安装完成后检查 SKILL.md、assets/、references/ 是否存在。
```

## 已经安装过的话，用这段话更新

```text
帮我更新 pixelium-design。请进入 ~/.claude/skills/pixelium-design 执行 git pull，然后告诉我当前最新 commit。
```

## 安装后可以这样使用

```text
帮我基于 Pixelium Design 实现一个像素风后台 Dashboard，包含侧边栏、顶部导航、数据卡片和表格。
```

也可以试这些请求：

```text
帮我把这个表单改成 Pixelium Design 组件写法，保持 Vue 3 + TypeScript。
```

```text
帮我检查这段 Pixelium Design 代码的受控/非受控用法是否正确。
```

```text
帮我用 PxTable、PxPagination 和 PxDialog 做一个用户管理页面。
```

```text
帮我把这个页面优化成复古像素风，同时支持暗黑模式。
```

## 技能覆盖范围

- Pixelium Design 组件 API 使用说明
- Vue 3 + TypeScript 代码生成
- `@pixelium/web-vue` 完整导入与按需导入
- Button、Input、Select、Table、Form、Dialog、Menu 等常用组件实践
- 受控 / 非受控模式检查
- 主题色、像素尺寸、暗黑模式和响应式布局建议
- 像素风 UI 页面与组件实现建议
