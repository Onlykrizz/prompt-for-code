# 优化后的任务细则

## 任务概述

将当前AI-AGENT指令体系的六步流程拆分为两个独立部分（A和B），形成两套可独立使用的指令系统。

## 涉及文件

**源文件**：
- `claude.md`
- `ai-agent-memory/AI-AGENT_criterion.md`
- `ai-agent-memory/AI-AGENT_step-before.md`
- `ai-agent-memory/undetermined-template.md`
- `ai-agent-memory/now-task.md`

## 交付物结构

```
result-A/
├── claude.md                          # A的入口文件
└── ai-agent-memory/
    ├── AI-AGENT_preparation.md        # A的核心规范（任务前置准备）
    ├── AI-AGENT_step-before.md        # 前置准备详细流程
    ├── undetermined-template.md       # 待定项模板
    └── now-task.md                    # 任务输入文件

result-B/
├── claude.md                          # B的入口文件
└── ai-agent-memory/
    ├── AI-AGENT_execution.md          # B的核心规范（5个执行环节）
    └── task-spec.md                   # 任务细则（由A产出，作为B的输入）
```

## A部分设计规范

### 职责定位
专注于**任务前置准备**，引导用户优化任务描述，产出清晰明确、可落地的最终任务细则。

### 核心流程
```
now-task.md → 分析优化 → undetermined.md → 用户确认 → optimized-task.md → 用户确认满意 → 重命名为task-spec.md → A结束
```

### 设计要点
1. **轻量化运行**：无csv状态记录、无git提交操作
2. **无ai-agent-output目录**：中间产物直接存放于当前工作目录或ai-agent-memory/
3. **"全程通用"内容精简**：去除状态记录、git提交、PlantUML等与A无关的内容
4. **保留内容**：
   - 任务分析与优化流程
   - 待定项处理机制
   - undetermined-template.md模板
   - MCP调用规范（mcp-sequential-thinking等分析工具）

### 包含文件
| 文件 | 说明 |
|------|------|
| claude.md | A的快速指引入口 |
| AI-AGENT_preparation.md | 任务前置准备的完整规范 |
| AI-AGENT_step-before.md | 前置准备详细流程（保留原内容） |
| undetermined-template.md | 待定项记录模板（保留原内容） |
| now-task.md | 任务输入文件（保留原内容） |

## B部分设计规范

### 职责定位
依据**通用守则模板**和**A产出的任务细则**，执行完整的任务实施闭环。

### 核心流程
```
task-spec.md → 读取项目文件 → 制作PlantUML流程图 → 流程设计 → 任务主体流程循环 → 验证结果 → 文档更新 → 收尾 → B结束
```

### 设计要点
1. **完整流程**：包含5个环节（流程设计→收尾）
2. **保留ai-agent-output目录机制**：用于状态记录和工作追溯
3. **保留完整"全程通用"内容**：状态记录、git提交、PlantUML命令等
4. **起始环节调整**：首次进入"流程设计"环节时创建工作目录和状态文件
5. **输入依赖**：task-spec.md（由A产出或用户直接提供）

### 包含文件
| 文件 | 说明 |
|------|------|
| claude.md | B的快速指引入口 |
| AI-AGENT_execution.md | 5个执行环节的完整规范 |
| task-spec.md | 任务细则模板/示例（说明格式要求） |

## 执行步骤

### 第1步：创建目录结构
创建`result-A/`和`result-B/`目录及其子目录。

### 第2步：编写A部分文件
1. 编写`result-A/claude.md`（A的入口文件）
2. 编写`result-A/ai-agent-memory/AI-AGENT_preparation.md`（精简版规范）
3. 复制`AI-AGENT_step-before.md`到A目录
4. 复制`undetermined-template.md`到A目录
5. 复制`now-task.md`到A目录

### 第3步：编写B部分文件
1. 编写`result-B/claude.md`（B的入口文件）
2. 编写`result-B/ai-agent-memory/AI-AGENT_execution.md`（执行环节规范）
3. 创建`result-B/ai-agent-memory/task-spec.md`（任务细则模板/说明）

### 第4步：验证
1. 检查A部分文件完整性和内容准确性
2. 检查B部分文件完整性和内容准确性
3. 验证A与B的接口一致性（task-spec.md格式）

## 验证标准

1. **A部分**：
   - 包含完整的任务前置准备流程
   - 无状态记录和git提交相关内容
   - undetermined-template.md格式正确

2. **B部分**：
   - 包含完整的5个执行环节
   - 保留状态记录和git提交机制
   - task-spec.md格式说明清晰

3. **接口一致性**：
   - A产出的task-spec.md格式与B期望的输入格式一致

## 执行前约束

| 约束项 | 说明 | 状态 |
|--------|------|------|
| A无状态记录 | A过程不使用csv状态记录和git提交 | 已确认 |
| A无ai-agent-output | A不使用ai-agent-output目录机制 | 已确认 |
| 语义化命名 | A用preparation，B用execution | 已确认 |
| B起始环节 | B从"流程设计"环节开始 | 已确认 |
| task-spec.md | A的最终产出，B的输入依赖 | 已确认 |
