# 贡献指南

感谢你愿意帮助改进 Grant-Master。本项目是一个实验性的中文项目申请书工作流，因此所有贡献都应尽量保持流程可审计、合规、可断点续跑，并且便于他人理解和维护。

## 开发流程

1. 从最新主分支 fork 或创建新分支。
2. 保持改动聚焦。不要在同一个 PR 中混合行为修改、格式化重排和大段文档重写。
3. 修改 skill 行为、workflow 产物、文件路径或用户命令时，同步更新相关文档。
4. 提交 PR 前运行下方适用的轻量检查。
5. 在 PR 描述中说明修改动机、影响文件、兼容性影响和仍然存在的风险。

## 检查命令

根据你的改动范围运行适用检查：

```bash
git diff --check
bash -n scripts/academic-search/check-deps.sh
bash -n scripts/academic-search/self-test.sh
node --check scripts/academic-search/oa-pdf-download.mjs
```

如果修改了 workflow 或 skill，请额外人工检查受影响的 `SKILL.md`，确认 required outputs 仍然与 `workflow_contract.md` 保持一致。

## 合规要求

学术搜索相关贡献必须遵守 [COMPLIANCE.md](COMPLIANCE.md)。

- 不要加入任何绕过付费墙的逻辑、prompt、示例或站点经验。
- 不要把 Sci-Hub、LibGen 或类似未授权来源作为论文获取路径进行搜索、推荐、自动化或文档说明。
- 只能下载合法开放全文，例如 arXiv、PubMed Central、Semantic Scholar `openAccessPdf`、OpenAlex、Unpaywall、出版商明确开放的 PDF，或用户手动提供的本地文件。
- 对非 OA 论文，只记录 DOI、出版社 URL、开放获取状态和明确原因，例如 `paywalled_do_not_bypass`。
- HTTP 403、登录跳转、授权页面、验证码和反爬拦截都应视为访问限制，不应反复重试或尝试绕过。

## 第三方来源

如果你从其他项目、论文、数据集或文档中改造内容：

- 先确认其许可证允许复用。
- 保留必要的版权和许可证声明。
- 新增或更新 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。
- 对实质性来源改造，在 README 致谢中说明。
- 避免复制大段原文；能用摘要和链接说明时，优先使用摘要和链接。

当前学术搜索模块参考并改造自 `ustc-ai4science/academic-search`；修改相关文件时请保留其第三方声明。

## Workflow 设计规则

- `auto` 独占管理 `workflow/proposal_state.yaml`。
- 各阶段 skill 通过自己的 result 文件汇报完成状态。
- 只有在 required outputs 全部存在且非空时，才能把阶段标记为完成。
- 生成产物应写入使用者的项目目录，不应写入 plugin 源码目录。
- 优先使用明确、可审计的磁盘文件，不依赖隐藏的内存状态。

## 文档风格

- README 示例应尽量安全、可复制。
- 公开文档中避免破坏性 shell 命令。
- 如实说明已知限制。
- 修改命令时，写清楚命令应在哪个目录执行。

## PR 检查清单

- [ ] 改动范围聚焦，并已清楚说明。
- [ ] 相关文档已更新。
- [ ] 合规政策已遵守。
- [ ] 如涉及第三方来源，已更新第三方声明。
- [ ] 轻量检查已通过，或已说明无法运行的原因。
