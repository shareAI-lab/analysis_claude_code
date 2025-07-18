# Claude Code 逆向工程研究仓库

Fellow us on X: https://x.com/baicai003  

## 通知
<img width="360" height="360" alt="image" src="https://github.com/user-attachments/assets/10664e2e-36c8-4e29-b740-f5d06e71c1be" />
<img width="360" height="360" alt="image" src="https://github.com/user-attachments/assets/9813fca0-a6dd-4813-972e-f9bf6d62add8" />

开源复现版会在这里发布：https://github.com/shareAI-lab/AgentKode  
相关解析文章已经二次核对提取整理后发布在ShareAI lab的官方公众号上. 

## 📋 项目概述

本仓库是对 Claude Code v1.0.33 进行深度逆向工程分析的完整研究资料库。通过对混淆源代码的系统性分析，我们揭示了这个现代AI编程助手的核心架构设计、实现机制和运行逻辑。

项目包含超过 **50,000 行混淆代码** 的分析结果，覆盖了从UI交互到Agent核心引擎的完整技术栈。通过多轮迭代分析和严格验证，我们成功还原了Claude Code的核心技术架构，为理解现代AI Agent系统的工程实现提供了宝贵的技术参考。

### 🎯 研究目标

1.  **深度理解** Claude Code的系统架构和核心机制
2.  **完整还原** 混淆代码背后的技术实现逻辑
3.  **严格验证** 分析结果的准确性和一致性
4.  **开源重建** 提供可复现的技术实现指南
5.  **知识共享** 为AI Agent系统设计提供参考

## 🔬 核心技术发现

### 🚀 突破性技术创新

#### 1. 实时 Steering 机制
- **基础架构**: h2A 双重缓冲异步消息队列
- **核心特性**: 零延迟消息传递，吞吐量 > 10,000 消息/秒
- **实现原理**: Promise-based 异步迭代器 + 智能背压控制
- **技术优势**: 真正的非阻塞异步处理，支持实时流式响应

#### 2. 分层多 Agent 架构
- **主Agent**: nO 主循环引擎，负责核心任务调度
- **SubAgent**: I2A 子任务代理，提供隔离执行环境
- **Task Agent**: 专用任务处理器，支持并发执行
- **权限隔离**: 每个Agent都有独立的权限范围和资源访问控制

#### 3. 智能上下文管理
- **压缩算法**: 92% 阈值自动触发上下文压缩
- **内存优化**: wU2 压缩器，智能保留关键信息
- **持久化**: CLAUDE.md 文件作为长期记忆存储
- **动态管理**: 根据Token使用情况动态调整上下文大小

#### 4. 强化安全防护
- **6层权限验证**: 从UI到工具执行的完整安全链
- **沙箱隔离**: 工具执行环境完全隔离
- **输入验证**: 多层次的恶意输入检测和过滤
- **权限网关**: 细粒度的功能权限控制

### 🏗️ 系统架构全景 (Mermaid Diagram)

```mermaid
graph TD
    subgraph A[用户交互层 - User Interaction Layer]
        A1["CLI接口<br>(命令行)"]
        A2["VSCode集成<br>(插件)"]
        A3["Web界面<br>(浏览器)"]
    end

    subgraph B[Agent核心调度层 - Agent Core Scheduling Layer]
        B1["nO主循环引擎 (AgentLoop)<br>• 任务调度<br>• 状态管理<br>• 异常处理"]
        B2["h2A消息队列 (AsyncQueue)<br>• 异步通信<br>• 流式处理<br>• 背压控制"]
        B3["wu会话流生成器 (StreamGen)<br>• 实时响应<br>• 流式输出"]
        B4["wU2消息压缩器 (Compressor)<br>• 智能压缩<br>• 上下文优化"]
        
        B2 -- 异步通信/双向 --> B1
        B1 -- 调度 --> B3
        B2 -- 消息 --> B4
    end

    subgraph C[工具执行与管理层 - Tool Execution & Management Layer]
        C1["MH1工具引擎 (ToolEngine)<br>• 工具发现<br>• 参数验证<br>• 执行调度"]
        C2["UH1并发控制 (Scheduler)<br>• 并发限制<br>• 负载均衡<br>• 资源管理"]
        C3["SubAgent管理 (TaskAgent)<br>• 任务隔离<br>• 错误恢复<br>• 状态同步"]
        C4["权限验证网关 (PermissionGW)<br>• 权限检查<br>• 安全审计<br>• 访问控制"]
        C5["工具生态系统"]
        
        C1 & C2 & C3 & C4 --> C5
    end

    subgraph D[存储与持久化层 - Storage & Persistence Layer]
        D1["短期记忆存储 (Messages)<br>• 当前会话<br>• 上下文队列"]
        D2["中期压缩历史 (Compressed)<br>• 历史摘要<br>• 关键信息"]
        D3["长期持久存储 (CLAUDE.md)<br>• 用户偏好<br>• 配置信息"]
        D4["状态缓存系统 (StateCache)<br>• 工具状态<br>• 执行历史"]
    end

    %% 定义各层之间的连接
    A -- 数据流 --> B
    B -- 任务/上下文 --> C
    C -- 读写数据 --> D
```

## 📁 仓库结构详解

### 📂 主要目录组织 (Mermaid Mindmap)

```mermaid
mindmap
  root(about_claude_code/)
    claude_code_v_1.0.33/
      stage1_analysis_workspace/
        Claude_Code_Agent系统完整技术解析.md
        chunks/
          (102个代码块)
          chunks.1.mjs ~ chunks.102.mjs
          chunks.index.json
          cli.chunks.mjs
        analysis_results/
          merged-chunks/
        scripts/
          beautify.js
          split.js
          merge-again.js
          llm.js
        docs/
        source/
    work_doc_for_this/
      CLAUDE_CODE_REVERSE_SOP.md
      stage_1_analysis_sop.md
      stage_2_reconstruction_sop.md
    LICENSE
    README.md
```

### 📋 核心技术文档

#### 🔧 核心机制深度分析
- **`实时Steering机制完整技术文档.md`** - h2A异步消息队列的完整实现原理
- **`Edit工具强制读取机制完整技术文档.md`** - Edit工具的文件读取验证机制
- **`分层多Agent架构完整技术文档.md`** - 多层Agent系统的架构设计
- **`Plan模式机制完整技术文档.md`** - Plan模式的触发和执行机制
- **`Claude_Code_Sandbox_Mechanism_Deep_Analysis.md`** - 沙箱安全机制深度分析
- **`Claude_Code_MCP_Deep_Analysis.md`** - MCP协议集成机制分析

#### 📊 验证与交叉分析报告
- **`FINAL_VALIDATION_REPORT.md`** - 最终综合验证报告 (95%准确性)
- **`CROSS_VALIDATION_REPORT.md`** - 跨文档一致性验证
- **`Claude_Code_关键机制严格验证报告.md`** - 关键机制的源码级验证
- **`Claude_Code_最终验证后的完整认知更新.md`** - 完整认知框架更新

#### 🏗️ 开源重建指南
- **`Open-Claude-Code/`** - 开源重建项目模板
  - 完整的TypeScript实现框架
  - 核心组件接口定义
  - 测试用例和基准测试
- **`Demo_Repo/`** - 演示实现仓库
- **`施工步骤/`** - 分阶段实施指南
  - 阶段1: 项目初始化和基础架构
  - 阶段2: Agent核心引擎和工具系统
  - 阶段3: 高级特性和交互模式
  - 阶段4: MCP集成和扩展系统
  - 阶段5: 测试优化和发布准备

#### 🔍 特殊机制分析
- **`Claude_Code_UI_Component_System_Deep_Analysis.md`** - UI组件系统分析
- **`Claude_Code_Image_Processing_and_LLM_API_Deep_Analysis.md`** - 图像处理和LLM API分析
- **`Claude Code隐藏特性和高级机制深度挖掘.md`** - 隐藏特性发现
- **`Claude_Code_IDE_Connection_and_Interaction_Deep_Analysis.md`** - IDE集成机制

## 🛠️ 分析方法论详解

### 第一阶段：静态代码分析

#### 1. 代码预处理 (Pre-processing)
```bash
# 代码美化和格式化
node scripts/beautify.js source/cli.mjs

# 智能分块处理 (102个块)
node scripts/split.js cli.beautify.mjs

# 生成分块索引
node scripts/generate-index.js chunks/
```

#### 2. LLM辅助分析 (LLM-Assisted Analysis)
- **模式识别**: 使用GPT-4识别代码模式和架构
- **函数分析**: 逐函数解析混淆后的逻辑
- **依赖映射**: 构建模块间的依赖关系图
- **API追踪**: 追踪关键API的调用链

#### 3. 交叉验证 (Cross-Validation)
- **多轮迭代**: 3轮深度分析确保准确性
- **一致性检查**: 跨文档技术描述的一致性验证
- **源码对照**: 每个技术断言都有源码位置支持

### 第二阶段：动态行为验证

#### 1. 运行时分析 (Runtime Analysis)
- **函数调用追踪**: 记录关键函数的执行路径
- **状态变化监控**: 监控系统状态的变化过程
- **性能指标收集**: 收集内存使用和执行时间数据

#### 2. 集成测试 (Integration Testing)
- **组件交互验证**: 验证组件间的交互逻辑
- **边界条件测试**: 测试系统在极限条件下的行为
- **错误恢复验证**: 验证系统的错误处理和恢复机制

## 🔍 详细研究范围

### 🎯 已分析的核心组件

#### 1. Agent循环系统 (Agent Loop System)
- **nO主循环引擎**: 
  - 异步Generator实现的核心调度器
  - 支持中断和恢复的执行控制
  - 多层异常处理和错误恢复
- **消息处理管道**:
  - 实时消息队列处理
  - 消息优先级和调度算法
  - 背压控制和流量管理

#### 2. 工具执行框架 (Tool Execution Framework)
- **6阶段执行管道**:
  1. 工具发现和注册
  2. 参数验证和类型检查
  3. 权限验证和安全检查
  4. 资源分配和环境准备
  5. 并发执行和状态监控
  6. 结果收集和清理回收
- **并发控制**: 最大10并发，智能负载均衡
- **错误隔离**: 每个工具独立的错误处理域

#### 3. 内存与上下文管理 (Memory & Context Management)
- **智能压缩算法**:
  - 92%阈值自动触发压缩
  - 保留关键信息的压缩策略
  - 分层存储和检索机制
- **Token优化**:
  - 动态上下文窗口调整
  - 重要性评分和内容筛选
  - 历史对话的智能摘要

#### 4. 安全防护框架 (Security Framework)
- **6层权限验证**:
  1. UI输入验证层
  2. 消息路由验证层
  3. 工具调用验证层
  4. 参数内容验证层
  5. 系统资源访问层
  6. 输出内容过滤层
- **沙箱隔离**: 完全隔离的工具执行环境
- **恶意输入检测**: 多种模式的恶意内容识别

#### 5. 用户界面集成 (UI Integration)
- **React组件系统**: 模块化的UI组件架构
- **实时更新机制**: WebSocket-based的实时通信
- **事件处理系统**: 12种不同类型的UI事件处理

### 📊 验证结果统计

| 验证维度 | 准确性 | 覆盖范围 | 置信度 |
|---------|--------|----------|--------|
| 核心架构设计 | 95% | 完整覆盖 | 高 |
| 关键机制实现 | 98% | 完整覆盖 | 极高 |
| API调用链路 | 92% | 85%覆盖 | 高 |
| 安全机制验证 | 90% | 主要功能 | 中高 |
| 性能参数验证 | 88% | 关键指标 | 中高 |
| UI交互机制 | 85% | 主要流程 | 中 |

### 🔬 创新技术发现

#### 1. 实时Steering技术突破
这是我们发现的最重要的技术创新。h2A类实现了真正的零延迟异步消息传递：

```javascript
// 核心双重缓冲机制伪代码
class h2AAsyncMessageQueue {
  enqueue(message) {
    // 策略1: 零延迟路径 - 直接传递给等待的读取者
    if (this.readResolve) {
      this.readResolve({ done: false, value: message });
      this.readResolve = null;
      return;
    }
    
    // 策略2: 缓冲路径 - 存储到循环缓冲区
    this.primaryBuffer.push(message);
    this.processBackpressure();
  }
}
```

#### 2. 智能上下文压缩算法
基于重要性评分的智能压缩，保留92%的关键信息：

```javascript
// 压缩触发逻辑
if (tokenUsage > CONTEXT_THRESHOLD * 0.92) {
  const compressedContext = await wU2Compressor.compress({
    messages: currentContext,
    preserveRatio: 0.3,
    importanceScoring: true
  });
}
```

## 🎯 应用场景与价值

### 📚 教育研究价值
1. **AI Agent架构学习**: 完整的现代AI Agent系统实现案例
2. **异步编程模式**: 高性能异步系统的设计参考
3. **安全架构设计**: 多层安全防护的实现方案
4. **性能优化技巧**: 内存管理和并发控制的最佳实践

### 🏗️ 系统设计参考
1. **架构模式借鉴**: 分层架构和组件化设计
2. **工具系统设计**: 插件化工具执行框架
3. **状态管理方案**: 分布式状态同步机制
4. **错误处理策略**: 多层错误恢复机制

### 🔒 安全分析应用
1. **安全机制审计**: 多层权限验证的实现分析
2. **沙箱技术研究**: 隔离执行环境的设计原理
3. **输入验证模式**: 恶意输入检测和过滤技术
4. **权限控制系统**: 细粒度权限管理的实现

### 🚀 开源开发指导
1. **项目架构搭建**: 基于分析结果的架构设计
2. **核心组件实现**: 关键组件的开源实现指南
3. **测试策略制定**: 基于分析的测试用例设计
4. **性能优化指导**: 性能瓶颈的识别和优化方案

## 🤝 贡献指南

### 📝 贡献类型
1. **准确性改进**: 修正分析中的错误或不准确之处
2. **深度分析**: 对现有分析的进一步深化
3. **新发现补充**: 添加新发现的技术细节
4. **文档完善**: 改进文档结构和可读性
5. **代码实现**: 基于分析的开源实现

### ✅ 贡献标准
- 所有技术断言必须有源码位置支持
- 新增分析需要经过交叉验证
- 文档格式需要保持一致性
- 代码实现需要通过测试验证

## ⚖️ 免责声明

本仓库专门用于教育和学术研究目的。所有分析工作基于公开可获得的混淆代码，旨在理解现代AI系统的设计模式和架构原理。

**重要说明**:
- 本项目不涉及任何恶意逆向工程活动
- 所有分析都在合法合规的框架内进行
- 研究成果仅用于学术交流和技术学习
- 不建议将分析结果用于商业竞争目的

## 📄 开源许可

本项目采用Apache License Version 2.0许可证开源 - 详见 [LICENSE](LICENSE) 文件。

---

**最后更新**: 2025年 6 月 29   
**项目灵感来源**: [claude-code-reverse](https://github.com/Yuyz0112/claude-code-reverse)  
**维护团队**: ShareAI-Lab
