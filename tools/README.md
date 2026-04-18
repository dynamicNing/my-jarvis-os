# tools/

共享工具注册表。**工具不是 agent**：

- Tools are registered objects, not agents
- Agents decide; tools execute
- Tool access must be limited by domain, risk, workflow stage, or allowlist
- Important tool behavior must be documented in schemas, not only prompts

每个工具一个文件夹或一份 schema，明确：输入、输出、副作用、风险等级、调用方白名单。
