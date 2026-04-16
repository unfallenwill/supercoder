# Supercoder

## Commit Convention

Every git commit must include this trailer at the end of the message:

```
Co-Authored-By: GLM 5.1 <noreply@z.ai>
```

## Skill Writing Conventions

This project is itself a Claude Code skill. All content edits must follow these rules:

### Description & Triggering
- `description` + `when_to_use` 合计不超过 1,536 字符，前置最关键的触发词
- 包含同义表达和反向触发条件（"DO NOT TRIGGER when..."）
- 明确作用域，不要写泛泛的描述

### Body Style
- 祈使句："Read the file"，不用 "You should read the file"
- 有序步骤用编号，规则约束用列表
- 最重要指令放最前面（自动压缩时前 5,000 token 优先保留）
- 每个规则只说一次，不重复

### Size Control
- SKILL.md 控制在 500 行以内
- 模板拆到 `template.md`，参考文档拆到 `reference.md`，示例拆到 `examples/`
- 不写 Claude 已知的知识（语言特性、常见工具用法）

### What Not to Write
- 不重复 CLAUDE.md 已有的内容
- 不写教程式解释，skill 是指令不是教材
- 不硬编码经常变化的值，用 `` `!`command`` `` 动态注入
