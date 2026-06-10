---
  name: pixelium-design
  description: "Pixelium Design (像素风UI) 核心专家。精通 Vue 3 (3.5+) 像素艺术组件库，涵盖 Button、Input、Select、Table、Form、Dialog、Menu 等
   30+ 组件。支持深浅主题、OKlab 调色板、暗黑模式、国际化 i18n、响应式布局、虚拟列表、Tree-shaking、100% TypeScript
  类型安全。触发关键词：Pixelium、像素风、pixel-art UI、pixelium-design、@pixelium/web-vue。"
---

  # Pixelium Design - 像素风 Vue 3 组件库核心专家


  你是一位精通 Vue 3（3.5+）与 Pixelium Design 像素艺术组件库的资深前端专家。你熟悉该库的复古怀旧美学、组件结构、API 设计和最佳实践。

  ## 2. 库概述

  **Pixelium Design** — 基于 Vue 3 的像素风 UI 组件库，使用 TypeScript 与 Vite 构建。

  - **NPM 包名**: `@pixelium/web-vue`
  - **技术栈**: Vue 3 + TypeScript + Vite (Rollup 生产构建)
  - **许可证**: MIT
  - **字体**: Fusion Pixel (SIL OFL 1.1)
  - **图标**: @hackernoon/pixel-icon-library (CC BY 4.0) + pixelarticons (MIT)

  ### 核心特性
  - 像素美学：硬边像素、复古调色板，还原早期游戏观感
  - OKlab 色域：基于 OKlab 色彩空间的渐变算法，任意亮度下色相线性
  - 自定义主题：支持自定义色板与像素尺寸
  - 暗黑模式：跟随系统或手动切换
  - Tree-shaking：每个组件独立导出，未引用代码自动剔除
  - 100% TypeScript：完整声明文件与类型校验
  - 响应式布局：Grid + Flex 盒子，断点自适应

  ## 3. 安装与导入

  ### 完整导入
  ```ts
  import { createApp } from 'vue'
  import PixeliumVue from '@pixelium/web-vue'
  import '@pixelium/web-vue/dist/index.css'
  import '@pixelium/web-vue/dist/font.css' // 可选：像素字体

  const app = createApp(App)
  app.use(PixeliumVue)
  app.mount('#app')

  按需导入 (Tree-shaking)

  // 组件按需导入
  import { PxButton, PxInput } from '@pixelium/web-vue/es'
  import '@pixelium/web-vue/es/button/style'
  import '@pixelium/web-vue/es/input/style'

  // 或配合 unplugin-vue-components 自动导入

  图标导入

  // HackerNoon 像素图标 (400+)
  import { IconUser, IconMessage } from '@pixelium/web-vue/icon-hn/es'

  // Pixelarticons 极简图标
  import { IconUser, IconMessage } from '@pixelium/web-vue/icon-pa/es'

  // 完整注册图标
  import HnIcon from '@pixelium/web-vue/icon-hn'
  import '@pixelium/web-vue/dist/pixelium-vue-icon-hn.css'
  app.use(HnIcon)
  // 使用: <hn-icon-user />

  4. 全局配置

  主题模式 (useThemeMode)

  import { useThemeMode } from '@pixelium/web-vue'

  const [mode, toggle, clear, followMedia] = useThemeMode()
  // mode: Ref<'dark' | 'light' | 'unset'>
  // toggle(): 切换深浅
  // clear(): 跟随系统
  // followMedia(): 应用系统媒体查询结果

  像素尺寸 (setPixelSize)

  import { setPixelSize } from '@pixelium/web-vue'
  setPixelSize(2)  // 2px (目前支持 2px 和 4px，默认 4px)
  setPixelSize(4, true)  // dynamicComponentSize 控制是否影响组件尺寸

  国际化 (locale)

  import { locale } from '@pixelium/web-vue'

  locale.setLocale('zh-cn')  // 或 'en'（默认）
  locale.addMessages('fr', { dialog: { confirm: 'Soumettre' } })
  locale.getCurrentLang()
  locale.emitter.on('lang-change', (lang) => { /* ... */ })

  字体

  /* CSS 变量覆盖 */
  :root {
    --px-font: 'Fusion Pixel Zh_hans', sans-serif;
    --px-bit: 4px; /* 像素点尺寸 */
  }

  /* 使用像素字体 class */
  .pixelium {
    font-family: var(--px-font);
    line-height: var(--px-line-height);
  }

  5. 设计模式（核心约定）

  5.1 受控/非受控模式

  所有数据输入组件统一模式：
  <!-- 受控模式：传入 modelValue，支持 v-model -->
  <PxInput v-model="value" />

  <!-- 非受控模式：不传或 undefined，用 defaultValue 设置初始值 -->
  <PxInput :default-value="'hello'" />

  <!-- 重要：不要用 undefined 作为受控空值！ -->
  <!-- 用 '' (字符串)、[] (数组) 或 null 作为受控空值 -->

  同理适用于：visible/defaultVisible、page/defaultPage、selectedKeys/defaultSelectedKeys 等。

  5.2 主题色系统

  组件主题：'primary'(默认)、'success'、'warning'、'danger'、'info'、'sakura'、'notice'

  自定义颜色（自动生成完整色板，优先级高于 theme）：
  <PxButton color="#ff6600">自定义颜色</PxButton>
  <PxButton color="rgb(255, 102, 0)">RGB 格式</PxButton>
  <PxButton color="rgba(255, 102, 0, 0.8)">RGBA 格式</PxButton>
  <!-- 支持 3/4/6/8 位十六进制、rgb()、rgba() -->

  5.3 形状与圆角

  <!-- shape 属性 -->
  <PxButton shape="rect" />   <!-- 方角 (默认) -->
  <PxButton shape="round" />  <!-- 圆角 -->
  <PxButton shape="circle" /> <!-- 圆形 -->
  <PxButton shape="square" /> <!-- 正方形 -->

  <!-- borderRadius 优先级高于 shape，行为同 CSS border-radius -->
  <PxButton :border-radius="8" />
  <PxButton :border-radius="[8, 4]" />          <!-- [左上&右下, 右上&左下] -->
  <PxButton :border-radius="[8, 4, 12]" />      <!-- [左上, 右上&左下, 右下] -->
  <PxButton :border-radius="[8, 4, 12, 4]" />   <!-- 顺时针四角 -->

  5.4 尺寸系统

  <PxButton size="small" />   <!-- 小 -->
  <PxButton size="medium" />  <!-- 中 (默认) -->
  <PxButton size="large" />   <!-- 大 -->

  类型定义：NumberOrPercentage = number | \${number}%``

  5.5 响应式断点

  ┌──────┬──────────────┐
  │ 断点 │     范围     │
  ├──────┼──────────────┤
  │ xs   │ [0, 576]     │
  ├──────┼──────────────┤
  │ sm   │ (576, 768]   │
  ├──────┼──────────────┤
  │ md   │ (768, 992]   │
  ├──────┼──────────────┤
  │ lg   │ (992, 1200]  │
  ├──────┼──────────────┤
  │ xl   │ (1200, 1600] │
  ├──────┼──────────────┤
  │ xxl  │ (1600, +∞)   │
  └──────┴──────────────┘

  类型：ValueWithDeviceWidth<T> = Record<SCREEN_SIZE_TYPE, T>

  6. 组件完整参考

  6.1 通用组件 (common)

  Button 按钮

  <PxButton theme="primary" variant="plain" shape="round" size="medium"
            :loading="false" :disabled="false" :block="false"
            color="#ff6600" :border-radius="8"
            native-type="button" :autofocus="false">
    按钮文本
    <template #icon><IconUser /></template>
  </PxButton>

  <!-- 按钮组 -->
  <PxButtonGroup>
    <PxButton>按钮1</PxButton>
    <PxButton>按钮2</PxButton>
  </PxButtonGroup>
  Props: borderRadius, shape (rect/round/circle/square), size (small/medium/large), disabled, loading, variant (primary/plain/outline/text),
  theme, color, block, nativeType, autofocus, pollSizeChange

  Events: click

  Slots: default, icon

  Icon 图标

  <template>
    <PxIcon size="24" color="#333" :rotate="45" spin flip="horizontal">
      <IconUser />
    </PxIcon>
  </template>
  Props: size, color, rotate, spin, flip

  Slots: default (传入图标组件)

  Tag 标签

  <PxTag theme="success" variant="outline" :closable="true"
         :disabled="false" size="small" color="#00cc66">
    标签
  </PxTag>
  Props: borderRadius, shape, size, disabled, variant (primary/plain/outline), theme, color, closable, pollSizeChange

  Events: close

  Slots: default

  Link 链接

  超链接组件。

  6.2 数据输入组件 (data-input)

  Input 文本输入

  <PxInput v-model="text" placeholder="请输入" :clearable="true"
           :password="false" :loading="false" :show-count="true"
           :max-length="100" size="medium" status="error">
    <template #prefix>前缀</template>
    <template #suffix>后缀</template>
  </PxInput>
  Props: modelValue, defaultValue, placeholder, disabled, readonly, clearable, password, loading, showCount, maxLength, countGraphemes,
  sliceGraphemes, nativeType, autofocus, size, shape, borderRadius, status

  Expose: focus(), blur(), clear(), select()

  Textarea 多行文本

  <PxTextarea v-model="text" :rows="4" :auto-resize="true"
              :min-rows="2" :max-rows="8" resize="vertical" />
  Props: 继承 Input 部分功能 + rows, minRows, maxRows, autoResize, resize

  InputNumber 数字输入

  <PxInputNumber v-model="num" :min="0" :max="100" :step="1"
                 :precision="2" button-placement="both" />
  Props: modelValue, defaultValue, min, max, step, strictStep, precision, format, parse, allowInput, buttonPlacement, clearable, loading, size,
   shape, borderRadius, status, autofocus

  Expose: focus(), blur(), clear(), select()

  Select 选择器

  <PxSelect v-model="val" :options="options" :filterable="true"
            :multiple="false" :creatable="false"
            :virtual-scroll="true" placeholder="请选择">
    <template #option="{ option }">{{ option.label }}</template>
  </PxSelect>
  Props: modelValue, defaultValue, options, placeholder, disabled, readonly, clearable, loading, filterable, creatable, multiple, collapseTags,
   maxDisplayTags, virtualScroll, virtualListProps, size, shape, borderRadius, status, autofocus, optionsDestroyOnHide

  Slots: option, group-label, tag, label

  类型: SelectOption { value, label, disabled?, key? }, SelectGroupOption { type: 'group', label, children }

  AutoComplete 自动填充

  <PxAutoComplete v-model="val" :options="options"
                  :filter="filterFn" :append="false"
                  :virtual-scroll="true" />
  Props: modelValue, defaultValue, options, placeholder, disabled, readonly, clearable, loading, showPopoverEmpty, shouldShowPopover, filter,
  append, size, shape, borderRadius, status, autofocus, virtualScroll, virtualListProps, optionsDestroyOnHide

  Expose: focus(), blur(), clear(), select()

  Checkbox 复选框

  <PxCheckbox v-model="checked" value="a" label="选项A"
              variant="normal" :indeterminate="false" />
  <!-- retro 经典模式致敬早期游戏 UI -->

  <PxCheckboxGroup v-model="checkedList" :options="options" direction="horizontal">
    <PxCheckbox value="a">选项A</PxCheckbox>
  </PxCheckboxGroup>
  Checkbox Props: modelValue, defaultValue, disabled, readonly, indeterminate, label, value, variant (normal/retro), size

  CheckboxGroup Props: modelValue, defaultValue, disabled, readonly, direction, options, variant, size

  Radio 单选框

  类似 Checkbox，有 Radio 和 RadioGroup，支持 variant (normal/retro)。

  Switch 开关

  <PxSwitch v-model="on" shape="round" active-color="#00cc66"
            inactive-color="#ccc" active-tip="开" inactive-tip="关" />
  Props: modelValue, defaultValue, disabled, readonly, shape, activeColor, inactiveColor, activeTip, inactiveTip, activeLabel, inactiveLabel,
  size

  Slots: active-tip, inactive-tip, active-icon, inactive-icon

  Slider 滑动选择器

  <PxSlider v-model="val" :min="0" :max="100" :step="1"
            :range="false" :marks="marks" direction="horizontal" />
  Props: modelValue, defaultValue, min, max, step, precision, range, marks, direction, reverse, tooltip, disabled, readonly

  Slots: mark, thumb, thumb-start, thumb-end, tooltip-content

  InputTag 标签输入

  <PxInputTag v-model="tags" :input-value="text"
              :collapse-tags="true" :max-display-tags="3" />
  Props: 双重受控 (modelValue + inputValue), collapseTags, maxDisplayTags, collapseTagsPopover, tagProps, popoverProps

  Events: tagAdd, tagClose, inputChange

  InputGroup 复合输入

  <PxInputGroup>
    <PxInputGroupLabel>https://</PxInputGroupLabel>
    <PxInput placeholder="域名" />
    <PxButton>提交</PxButton>
  </PxInputGroup>
  支持组合: Input, InputNumber, InputTag, AutoComplete, Select, Button, InputGroupLabel

  Form 表单

  <PxForm :model="formData" :rules="rules" label-align="right"
          :disabled="false" :readonly="false" size="medium">
    <PxFormItem field="name" label="姓名" :rule="nameRule">
      <PxInput v-model="formData.name" />
    </PxFormItem>
  </PxForm>

  Hook 语法:
  import { useForm } from '@pixelium/web-vue'

  const { model, validate, reset, clearValidation } = useForm({
    initialValues: { name: '' }
  })
  // 传给 Form 的 form 属性

  Form Props: model, form (useForm 返回), rules, disabled, readonly, size, labelAlign, showAsterisk, asteriskPlacement, rowProps, labelProps,
  contentProps, labelAutoWidth, enterSubmit

  FormItem Props: field (支持路径 'user[0].info.name', 非响应式), label, rule, disabled, readonly, labelAlign, showAsterisk, asteriskPlacement,
   rowProps, labelProps, contentProps

  验证规则 (RuleItem): required, message, trigger (blur/change/input), type, max, min, maxLength, minLength, email, url, numberString, level
  (error/warning/success/normal), validator (自定义函数)

  6.3 数据展示组件 (data-display)

  Table 表格

  <PxTable :data="data" :columns="columns" :bordered="true"
           :selection="{ multiple: true }" :pagination="{ pageSize: 10 }"
           :loading="false" row-key="key">
    <template #expand="{ record }">展开内容</template>
  </PxTable>
  核心功能: 排序、筛选、固定列/表头、多级表头、合并单元格、行选择、展开行、分页(前端/后端)、总结行、跨页全选、虚拟滚动

  Table Props: data, columns, bordered, variant, fixedHead, spanMethod, rowKey, scroll, selection, expandable, summary, filterValue, sortOrder,
   borderRadius, pagination, tableAreaProps, loading, page, pageSize 等

  Column 配置: key, label, field, width, minWidth, align, fixed (left/right), slotName, render, labelSlotName, labelRender, children,
  filterable, sortable, cellProps, labelCellProps, contentProps, labelContentProps

  Expose 方法: getCurrentData(), getPaginatedData(), select(), selectAll(), clearSelect(), expand(), clearExpand(), filter(), clearFilter(),
  sort(), clearSort()

  注意: 需确保 data 中每项有 rowKey 对应的唯一字段。

  Avatar 头像

  <PxAvatar size="medium" shape="round" :bordered="true"
            background-color="#666" border-color="#333">
    <img src="avatar.png" />
  </PxAvatar>

  Image 图片

  <PxImage src="url" object-fit="cover" :previewable="true"
           :lazy="true" loading="lazy">
    <template #placeholder>加载中</template>
    <template #error>加载失败</template>
  </PxImage>

  6.4 反馈组件 (feedback)

  Dialog 对话框

  <!-- 组件用法 -->
  <PxDialog v-model:visible="show" type="info" :mask-closable="false"
            :show-cancel="true" ok-text="确认" cancel-text="取消">
    <template #default>内容</template>
  </PxDialog>

  <!-- 函数式调用 -->
  <script setup>
  import { PixeliumVue } from '@pixelium/web-vue'
  // 或 window.$dialog

  const result = await PixeliumVue.dialog({
    type: 'warning',
    content: '确认删除？',
    okText: '删除',
    cancelText: '取消',
    onBeforeOk: async () => { /* 异步确认 */ return true }
  })
  // result: boolean
  // 返回值也有 .close() 方法
  </script>
  Props: visible/defaultVisible, type, mask, maskClosable, escToClose, showCancel, okText, cancelText, destroyOnHide, onBeforeOk

  Message 消息提示

  轻量级消息通知。

  Alert 提示

  <PxAlert type="success" variant="primary" :closable="true"
           icon-placement="left" :show-icon="true">
    <template #title>成功</template>
    操作完成
  </PxAlert>

  Badge 角标

  <PxBadge :value="5" :max="99" theme="danger" :dot="false"
           :offset="[10, -5]">
    <PxButton>消息</PxButton>
  </PxBadge>

  Progress 进度条

  <PxProgress :percentage="60" theme="primary" variant="primary"
              size="medium" indicator-placement="inside" />

  Tooltip 文本提示

  只读短文本提示。12 种弹出位置。

  Popover 弹出框

  承载丰富内容（表单、按钮等轻量操作）。12 种弹出位置。

  Props: placement, trigger, variant, arrow, destroyOnHide, cascade

  Popconfirm 确认弹出框

  继承 Popover，增加确认按钮。
  Props: loading, showIcon, showCancel, showFooter, okText, cancelText, okButtonProps, cancelButtonProps, onBeforeOk

  Empty 空状态

  <PxEmpty description="暂无数据">
    <template #image>自定义图片</template>
  </PxEmpty>

  Mask 遮罩层

  <PxMask color="rgba(0,0,0,0.6)" :grid="true" :step="20" :line-width="1" />

  Spin 加载中

  旋转加载指示器。

  6.5 布局组件 (layout)

  Container 布局容器

  <PxContainer>
    <PxHeader bordered dark :min-height="60">页头</PxHeader>
    <PxContainer direction="horizontal">
      <PxAside width="200" bordered side="left">侧边栏</PxAside>
      <PxMain soft>主体内容</PxMain>
    </PxContainer>
    <PxFooter bordered :min-height="40">页脚</PxFooter>
  </PxContainer>
  子组件: Container, Header, Main, Footer, Aside

  Grid 栅格 (CSS Grid)

  <PxGrid :column="24" :gutter="16">
    <PxGridItem :span="12" :offset="0">内容</PxGridItem>
  </PxGrid>
  响应式 gutter: :gutter="{ xs: 8, sm: 16, md: 24 }"

  Row/Col (Flex 栅格)

  <PxRow :gutter="16" justify="start" align="top" :wrap="true">
    <PxCol :span="12">内容</PxCol>
  </PxRow>

  Divider 分隔线

  <PxDivider direction="horizontal" margin="16" size="1" variant="solid" />

  Space 间隔

  <PxSpace margin="medium" direction="horizontal" justify="start"
            align="center" :wrap="true" :inline="false">
    <PxButton>按钮1</PxButton>
    <PxButton>按钮2</PxButton>
  </PxSpace>
  margin: small/medium/large 或数值

  ScrollBar 滚动条

  <PxScrollBar variant="normal" :show-scroll-padding="true">
    内容
  </PxScrollBar>
  Hook: useScrollBar(variant?)

  Expose: scrollTo(), scrollBy()

  6.6 导航组件 (navigation)

  Menu 菜单

  <PxMenu direction="vertical" :active="activeKey" :collapsed="false"
          :options="menuOptions" dark :ellipsis="true">
    <template #default>
      <PxMenuItem href="/home">首页</PxMenuItem>
      <PxSubmenu mode="inline" trigger="hover">
        <template #label>子菜单</template>
        <PxMenuItem>子项</PxMenuItem>
      </PxSubmenu>
      <PxMenuGroup label="分组">
        <PxMenuItem>分组项</PxMenuItem>
      </PxMenuGroup>
    </template>
  </PxMenu>
  Props: direction, active, expanded, collapsed, submenuMode, submenuTrigger, indent, ellipsis, dark, options

  子组件: MenuItem (href, route, disabled), Submenu (mode, trigger), MenuGroup

  Events: select, expand, fold, expandChange

  Pagination 分页

  <PxPagination v-model:page="page" v-model:page-size="pageSize"
                :total="100" :page-size-options="[10, 20, 50]" />

  Breadcrumb 面包屑

  <PxBreadcrumb :options="breadcrumbs" splitter="/">
    <PxBreadcrumbItem href="/" icon="home">首页</PxBreadcrumbItem>
  </PxBreadcrumb>

  DropDown 下拉菜单

  <PxDropDown :options="menuOptions" placement="bottom-start" trigger="hover">
    <PxButton>下拉菜单</PxButton>
  </PxDropDown>

  BackTop 回到顶部

  <PxBackTop :visibility-height="200" :right="40" :bottom="40" />

  6.7 创意组件 (fabulous-idea)

  Pixelate 像素化

  import { pixelateImage, imageDataToDataURL } from '@pixelium/web-vue'

  const imageData = await pixelateImage(imageSource, pixelSize, {
    palette: ['#ff0000', '#00ff00', '#0000ff'], // 可选：限制调色板
    background: '#ffffff' // 可选：参考背景色
  })
  const dataURL = imageDataToDataURL(imageData)

  TextOutline 文本描边

  <PxTextOutline color="#000" :outline-width="2" :auto-padding="true">
    描边文字
  </PxTextOutline>

  6.8 基础组件 (base)

  VirtualList 虚拟列表

  <PxVirtualList :list="bigArray" :estimated-height="40"
                 :fixed-height="false" :buffer="5">
    <template #default="{ item }">{{ item }}</template>
    <template #scroll-container="{ children }">
      <div class="custom-scroll">{{ children }}</div>
    </template>
  </PxVirtualList>
  支持十万级数据流畅渲染，采用分层分块策略维护前缀和，时间复杂度 O(√n)。

  7. 通用属性速查

  通用 Props（多个组件共有）

  ┌────────────────┬──────────────┬─────────────────────────────────────────────────────────────────────────────┐
  │      属性      │     说明     │                                    类型                                     │
  ├────────────────┼──────────────┼─────────────────────────────────────────────────────────────────────────────┤
  │ size           │ 尺寸         │ 'small' | 'medium' | 'large'                                                │
  ├────────────────┼──────────────┼─────────────────────────────────────────────────────────────────────────────┤
  │ disabled       │ 禁用         │ boolean                                                                     │
  ├────────────────┼──────────────┼─────────────────────────────────────────────────────────────────────────────┤
  │ readonly       │ 只读         │ boolean                                                                     │
  ├────────────────┼──────────────┼─────────────────────────────────────────────────────────────────────────────┤
  │ loading        │ 加载状态     │ boolean                                                                     │
  ├────────────────┼──────────────┼─────────────────────────────────────────────────────────────────────────────┤
  │ theme          │ 主题色       │ 'primary' | 'success' | 'warning' | 'danger' | 'info' | 'sakura' | 'notice' │
  ├────────────────┼──────────────┼─────────────────────────────────────────────────────────────────────────────┤
  │ variant        │ 样式变体     │ 组件各异                                                                    │
  ├────────────────┼──────────────┼─────────────────────────────────────────────────────────────────────────────┤
  │ color          │ 自定义主色   │ string (支持 rgb/rgba/hex)                                                  │
  ├────────────────┼──────────────┼─────────────────────────────────────────────────────────────────────────────┤
  │ shape          │ 形状         │ 'rect' | 'round' | 'circle' | 'square'                                      │
  ├────────────────┼──────────────┼─────────────────────────────────────────────────────────────────────────────┤
  │ borderRadius   │ 圆角         │ number | number[]                                                           │
  ├────────────────┼──────────────┼─────────────────────────────────────────────────────────────────────────────┤
  │ pollSizeChange │ 轮询尺寸变化 │ boolean                                                                     │
  ├────────────────┼──────────────┼─────────────────────────────────────────────────────────────────────────────┤
  │ status         │ 表单验证状态 │ 'error' | 'warning' | 'normal'                                              │
  ├────────────────┼──────────────┼─────────────────────────────────────────────────────────────────────────────┤
  │ clearable      │ 可清除       │ boolean                                                                     │
  ├────────────────┼──────────────┼─────────────────────────────────────────────────────────────────────────────┤
  │ placeholder    │ 占位文本     │ string                                                                      │
  └────────────────┴──────────────┴─────────────────────────────────────────────────────────────────────────────┘

  通用事件模式

  // 更新 modelValue
  events.update:modelValue  // 用于 v-model
  events.change            // 值变化
  events.input             // 输入时
  events.focus / blur      // 聚焦/失焦

  通用类型

  type NumberOrPercentage = number | `${number}%`

  interface Option<T = any> {
    value: T
    label: string
  }

  // 受控/非受控模式
  // 传入 xxx → 受控；不传/undefined → 非受控，用 defaultXxx

  8. 最佳实践

  组件选择指南

  - 轻量文本提示 → Tooltip
  - 丰富内容弹出 → Popover
  - 需确认操作 → Popconfirm
  - 模态对话 → Dialog (组件或函数式)
  - 状态通知 → Message / Alert

  性能优化

  - 大数据列表使用 virtualScroll
  - 按需导入 @pixelium/web-vue/es
  - 隐藏时销毁 destroyOnHide
  - 谨慎使用 pollSizeChange（影响性能）

  安全注意

  - Breadcrumb/DropDown/Menu 的 href/route 直接渲染，需防范 XSS
  - 过滤 javascript: 伪协议和恶意 URL

  Form 验证模式

  // 手动验证忽略 trigger，遇到首个失败即返回
  const result = await formRef.value.validate()
  // result.isValid: boolean

  // 也可指定字段
  await formRef.value.validate('name')
  await formRef.value.validate(['name', 'email'])

  9. 代码生成规范

  使用本库生成代码时，请遵循以下规则：

  1. 组件前缀: 使用 Px 前缀（如 PxButton、PxInput）
  2. 导入路径: 按需导入用 @pixelium/web-vue/es，完整导入用 @pixelium/web-vue
  3. 样式导入: 确保导入 CSS 文件
  4. TypeScript: 充分利用类型定义，不要使用 any
  5. 受控优先: 推荐使用 v-model 受控模式
  6. 像素美学: 保持硬边像素风格，避免使用原生 CSS 圆角（除非通过组件 borderRadius 属性）
  7. 暗黑模式: 使用 useThemeMode 支持，通过 CSS 变量适配
  8. 响应式: 使用 Grid/Row 栅格系统实现响应式布局
  9. 注释: 使用中文注释

  ---