使用 skill-creator，帮我创建一个 Codex skill。

Skill 名称：
prd-frontend-analysis

Skill 安装路径：
~/.codex/skills/prd-frontend-analysis/SKILL.md

目标：
创建一个面向企业级前端团队的 PRD 分析 skill。这个 skill 用于当前端工程师收到产品 PRD、功能说明、设计需求、业务流程文档、Figma 链接或验收标准时，让 Codex 作为 senior frontend engineer / frontend tech lead，先完成需求澄清、仓库分析、技术方案拆解和验证计划，而不是直接开始写代码。

触发场景：
当用户说到以下任意场景时，应触发该 skill：
- 分析前端 PRD
- 收到产品需求文档
- 根据 PRD 做技术方案
- 把 PRD 转成 implementation spec
- 先分析需求，不要改代码
- 评估某个前端功能怎么实现
- 根据 Figma / 设计稿 / 产品说明拆开发计划
- 做前端技术拆解
- 做前端需求澄清
- 作为 senior frontend engineer 读 PRD

核心原则：
1. 默认 analysis-only，不改代码。
2. 只有用户明确说“开始实现”“修改代码”“生成 patch”“落地开发”时，才允许进入实现阶段。
3. 必须先读 PRD，再读仓库。
4. 必须优先理解当前仓库已有架构、设计系统、组件库、状态管理、接口层、测试体系和工程规范。
5. 必须把产品语言转换成可执行的前端工程规格。
6. 必须显式标注 assumptions，不允许把不确定需求当事实。
7. 不允许在 PRD 不明确时编造 API contract、权限规则、埋点规则或交互细节。
8. 必须优先复用现有组件、hooks、utils、API client、types、test helpers 和 UI patterns。
9. 不允许为了单个需求引入不必要的新抽象或新依赖。
10. 输出必须面向真实工程落地，而不是泛泛而谈。

请创建一个符合 Codex skill 标准结构的 SKILL.md，包含 YAML frontmatter：
- name: prd-frontend-analysis
- description: 写得足够明确，使 Codex 在用户提供前端 PRD、产品需求、设计需求、Figma、功能说明，或要求“先分析不要改代码”“生成 implementation spec”“做技术拆解”时自动触发。

Skill 内容请包含以下部分：

1. Role
定义 Codex 在该 skill 下扮演 senior frontend engineer / frontend tech lead，负责把 PRD 转换成可执行的前端工程方案。

2. Default Behavior
说明默认只分析，不改代码，不生成 patch，不安装依赖，不启动实现，除非用户明确要求。

3. Required Inputs
说明可以接受的输入：
- PRD 文档
- 用户故事
- 设计稿说明
- Figma 链接或截图
- API 草案
- 验收标准
- 业务流程描述
- 现有 issue / ticket / task 描述

4. Repository Inspection Workflow
要求 Codex 在输出技术方案前检查当前仓库：
- package manager 和 scripts
- framework 和路由结构
- pages/routes
- components
- design system
- layout patterns
- forms
- tables/lists
- modals/drawers
- hooks
- state management
- data fetching
- API client layer
- schemas/types
- validation
- permissions/auth
- i18n
- accessibility patterns
- analytics/tracking
- tests
- Storybook 或组件示例
- E2E 测试
- visual regression 配置
- lint/typecheck/test 命令
- feature flag / rollout 机制

5. PRD Analysis Workflow
要求 Codex 分析：
- product goal
- target users
- main user journeys
- entry points
- happy path
- loading state
- empty state
- error state
- success state
- disabled state
- permission denied state
- validation behavior
- edge cases
- responsive behavior
- accessibility needs
- i18n needs
- analytics/tracking needs
- rollout requirements
- dependencies on backend, design, data, product, legal, security, or ops

6. Output Format
输出必须使用以下结构：

## Summary
简要总结业务目标、目标用户、主流程、预期结果。

## Affected Areas
列出可能影响的 routes、pages、components、hooks、stores、API clients、types、schemas、tests、design-system surfaces、analytics files，并在仓库中发现时包含文件路径。

## Existing Patterns
列出现有可复用组件、hooks、utils、API clients、types、layout patterns、form patterns、table/list patterns、modal/drawer patterns、loading/empty/error patterns、permission patterns、test helpers、Storybook examples。

## Open Questions
按 product、design、backend/API、data model、permissions、analytics、i18n、accessibility、rollout、edge cases 分组列出不明确问题。

## Assumptions
列出为了推进分析而做出的假设，并明确标注这些是假设，不是事实。

## Risks
列出 product risk、UX risk、engineering risk、API risk、state management risk、performance risk、accessibility risk、responsive risk、i18n risk、analytics risk、test coverage risk、rollout risk。

## Proposed Acceptance Criteria
如果 PRD 没有完整验收标准，则生成建议版验收标准，并标注 proposed。

## Implementation Spec
输出可执行工程规格，包含：
- UI states
- interactions
- validation rules
- API/data contract requirements
- error handling
- permissions
- analytics/tracking
- responsive behavior
- accessibility requirements
- i18n requirements
- edge cases
- non-goals

## Phased Development Plan
把实现拆成小阶段。每个阶段包含：
- goal
- likely files/modules
- deliverable
- validation step
- risk addressed

## Verification Plan
列出建议执行的验证：
- typecheck
- lint
- unit tests
- component tests
- E2E tests
- visual regression
- accessibility checks
- responsive screenshots
- manual QA scenarios
- monitoring/rollout checks

## Clarification Request
如果存在阻塞实现的问题，最后列出需要用户、产品、设计、后端或数据团队确认的问题。

7. Guardrails
加入这些约束：
- Prefer existing repo patterns over new abstractions.
- Prefer existing design-system components over custom UI.
- Do not invent API contracts.
- Do not skip non-happy-path states.
- Do not ignore permissions, analytics, i18n, accessibility, mobile, or rollout.
- Keep implementation phases small enough for code review.
- Mark uncertainty explicitly.
- Ask clarifying questions when implementation would be risky.
- Do not implement unless explicitly asked.

8. Optional Implementation Mode
说明如果用户明确要求“开始实现”，该 skill 可以切换到 implementation mode，但必须：
- 先复述批准的 implementation spec
- 小步改动
- 遵守仓库现有模式
- 每阶段后运行相关验证
- 失败后先修复再继续
- 最后总结改动、测试结果和剩余风险

9. Keep It Concise
请让 SKILL.md 足够完整但不要冗长，避免无意义解释。它应该像企业前端团队的工作流规约，而不是教程文章。

请直接创建文件：
~/.codex/skills/prd-frontend-analysis/SKILL.md

如果路径不存在，请创建目录。
创建后请展示生成的文件路径和 SKILL.md 的完整内容。
