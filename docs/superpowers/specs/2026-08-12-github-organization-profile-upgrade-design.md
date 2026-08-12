# 乐可开源 GitHub 组织主页升级设计

## 1. 目标与定位

本次升级把 `github.com/lekeopen` 从“近期工作汇总”调整为乐可开源面向开发者的公开技术名片。

主页不复制公司官网，也不承担完整产品营销。它需要让开发者快速确认三件事：

1. 乐可开源是一家持续交付真实软件产品的公司；
2. 公司具备可以公开验证的工程实践和开源成果；
3. 每个公开入口的开放边界、维护状态和下一步访问路径都清楚可信。

核心表达原则是“产品事实优先、工程证据优先、开放边界透明”。避免口号堆叠、夸大技术能力、虚构数据和把私有仓库伪装成公开项目。

## 2. 工作范围

### 本次包含

- 重写公开组织主页 `.github/profile/README.md`；
- 将“核心产品”和“精选开源项目”分开表达；
- 修复或移除公众无法访问的私有仓库链接；
- 精简 Codex Skills 展示；
- 保留自动更新的最近动态区域；
- 优化四个精选公开仓库的 description、homepage 和 topics；
- 设置四个公开置顶仓库并检查顺序；
- 以 Public 视角验收页面和全部外链。

### 本次不包含

- 修改公司官网或产品功能；
- 公开任何私有源码或调整仓库可见性；
- 迁移 `rockts/xiaole-ai` 仓库；
- 创建新的产品仓库；
- 更换组织头像、组织名称或法律主体信息；
- 引入宣传横幅、访问量徽章、虚构客户数据或未经确认的合作标识；
- 修改 README 自动更新工作流的职责和实现。

## 3. 受众与语气

### 主要受众

- 希望判断公司技术能力的开发者和潜在合作方；
- 需要了解产品开放边界的用户；
- 希望复用 Codex Skills 或其他开源成果的工程人员；
- 从官网、搜索或仓库页面进入组织主页的访客。

### 语气原则

- 中文优先，产品名和通用技术名保留规范英文；
- 专业、直接、克制，避免广告式形容词；
- 一段只解决一个问题，尽量使用短句；
- 描述产品价值时不暗示其源码一定开放；
- 描述开源项目时明确源码、许可证或发布仓库性质。

## 4. 页面信息架构

### 4.1 顶部身份与快速入口

标题保留：

```markdown
# 👋 乐可开源 · LekeOpen
```

定位文案使用：

```markdown
乐可开源是一家位于中国天水的软件与 AI 工程公司。

我们专注于本地优先工具、教育软件、知识系统与生产级 AI 应用，持续把真实产品、工程方法和可复用能力开放出来。
```

紧接一行快速入口：

```markdown
[公司官网](https://lekeopen.com) · [产品与项目](https://lekeopen.com/products/) · [技术动态](https://lekeopen.com/news/) · [联系我们](https://lekeopen.com/contact/)
```

### 4.2 核心产品

核心产品说明公司正在构建什么，不以仓库公开作为入选条件。

按以下顺序展示：

1. **乐可点名**
   - 定位：本地优先的课堂随机点名工具；
   - 产品入口：`https://lekeopen.com/products/leke-picker/`；
   - 源码入口：`https://github.com/lekeopen/leke-picker`；
   - 边界：公开源码，Apache-2.0。
2. **归个类**
   - 定位：本地文件智能整理工具；
   - 产品入口：`https://lekeopen.com/products/guigelei/`；
   - 发布入口：`https://github.com/lekeopen/guigelei-releases`；
   - 边界：公开仓库只提供官方版本与下载，不暗示完整源码开放。
3. **小乐 AI**
   - 定位：具备记忆与行动能力的个人 AI 助手；
   - 对外入口：`https://docs.xiaole.app`；
   - 边界：不链接个人账户下的说明仓库，不宣称完整源码开放。
4. **乐教库**
   - 定位：面向 K12 教育场景的教学资源平台；
   - 对外入口：`https://lejiaoku.com`；
   - 边界：不链接私有前端或后端仓库。

页面文案采用四条紧凑列表，不使用对齐依赖较强的 Markdown 表格。

### 4.3 精选开源与工程

按以下顺序展示：

1. `leke-picker`：产品型开源项目；
2. `codex-skills`：可复用 Codex 技能集合；
3. `lekee-official-site`：React、Vite、静态渲染、性能门禁和技术 SEO 的生产官网工程；
4. `uvindex240370sensor`：面向行空板、PinPong 和 I2C 的硬件扩展。

每项只保留一句用途和一个主要仓库入口。许可证已经存在时可以标明；没有可验证许可证时不写“开源许可证”。

### 4.4 Codex Skills

Codex Skills 保留独立小节，但从六项缩减为三个代表能力：

- 品牌系统构建；
- 开源工具评估；
- 社交内容分发。

保留“查看全部技能与安装说明”链接。该小节承担深度能力证明，不与“精选开源与工程”重复列出仓库介绍。

### 4.5 最近动态

保留现有：

```text
<!-- BLOG-POST-LIST:START -->
...
<!-- BLOG-POST-LIST:END -->
```

自动区块最多保留最近三条内容。人工改写 README 时不得删除或改名标记，否则会破坏现有自动更新流程。

### 4.6 页尾

页尾只保留稳定入口：

```markdown
[官网](https://lekeopen.com) · [产品与项目](https://lekeopen.com/products/) · [技术动态](https://lekeopen.com/news/) · [Facebook](https://www.facebook.com/lekeopen/) · [X](https://x.com/lekeopen) · [contact@lekeopen.com](mailto:contact@lekeopen.com)
```

## 5. 仓库元信息

### 5.1 `leke-picker`

- Description：`乐可点名：本地优先的课堂随机点名工具`；
- Homepage：`https://lekeopen.com/products/leke-picker/`；
- Topics：`lekeopen`, `education`, `classroom`, `local-first`, `desktop-app`, `typescript`。

### 5.2 `codex-skills`

- Description：`乐可开源维护的可复用 Codex 技能集合`；
- Homepage：`https://github.com/lekeopen/codex-skills/blob/main/README.zh-CN.md`；
- Topics：`lekeopen`, `codex`, `ai-tools`, `developer-tools`, `automation`, `open-source`。

### 5.3 `guigelei-releases`

- Description：`归个类官方版本发布与下载仓库｜本地文件整理工具`；
- Homepage：`https://lekeopen.com/products/guigelei/`；
- Topics：`lekeopen`, `desktop-app`, `local-first`, `file-management`, `releases`。

该仓库 README 的首屏必须明确：这是官方版本发布与下载仓库，不代表完整源码开放。若现有 README 已准确表达，则不重复修改。

### 5.4 `lekee-official-site`

- Description：`乐可开源公司官网｜React、Vite、静态渲染与技术 SEO`；
- Homepage：`https://lekeopen.com`；
- Topics：`lekeopen`, `company-website`, `react`, `vite`, `static-site`, `technical-seo`。

## 6. 置顶仓库

Public 视角按以下顺序置顶四个公开仓库：

1. `leke-picker`
2. `codex-skills`
3. `guigelei-releases`
4. `lekee-official-site`

不置顶 `.github`、私有仓库、长期停更项目或个人账户仓库。置顶操作只改变组织主页展示，不改变仓库权限和内容。

## 7. 视觉与格式规则

- 使用 GitHub 原生 Markdown，不引入自定义 HTML 布局；
- 不使用大幅横幅、动态 GIF、访问计数器或大量状态徽章；
- 一级标题只出现一次，主要区块使用二级标题；
- emoji 只用于区分主要区块，每个标题最多一个；
- 每个项目说明控制在两行以内；
- 页面在深色和浅色模式下都不能依赖图片背景或特殊颜色；
- 不展示 stars、下载量、用户数等易过期或尚无意义的数据。

## 8. 安全与开放边界

- Public 视角不得出现 `lejiaoku-web`、`lejiaoku-backend`、`ai-file-organizer`、`classroom-random-picker` 等私有仓库入口；
- 不公开内部架构、凭据、团队隐私、客户信息或未发布项目；
- 小乐 AI 和乐教库只链接公开产品或文档入口；
- 归个类发布仓库必须明确“发布与下载”性质；
- 不因为仓库位于 GitHub 就统一称为“开源”；
- 仓库 topics 只描述真实技术和场景，不使用无关热门词。

## 9. 验收标准

### 内容验收

- 首屏可以在短时间内回答公司是谁、做什么、去哪里看产品；
- 核心产品和精选开源项目边界清楚；
- Codex Skills 不再压过产品信息；
- 最近动态自动标记完整且只显示三条；
- 不存在无法公开访问的私有仓库链接。

### 仓库验收

- 四个精选仓库的 description、homepage 和 topics 与本设计一致；
- `guigelei-releases` 对发布仓库性质说明清楚；
- Public 视角只置顶指定四个公开仓库，顺序正确。

### 链接与视觉验收

- 所有 GitHub、官网、产品、文档和社交入口均可访问；
- Public 视角 README 渲染层级清楚，没有表格错位或过长段落；
- 桌面端深色主题下首屏、核心产品和精选项目可清晰扫描；
- 组织基本资料继续显示公司名称、官网、邮箱和中国天水位置。

## 10. 发布与回滚

1. 在独立分支修改 `.github/profile/README.md` 和必要文档；
2. 本地检查 Markdown、链接清单和自动标记；
3. 通过 PR 审查后合并 `.github` 仓库；
4. 仓库元信息逐仓库更新并记录变更前值；
5. 置顶仓库通过组织 Public 视角设置；
6. 最终使用 Public 视角检查组织主页；
7. 如展示效果不符合预期，README 回滚到上一提交，仓库元信息恢复记录值，置顶设置恢复原状态。

仓库元信息、置顶顺序和 GitHub 页面修改都是外部状态变更，执行前必须获得明确授权。登录、MFA、CAPTCHA 或权限确认由组织所有者处理。
