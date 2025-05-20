# Day14-AI Agent定制与优化

欢迎来到《自学30天掌握AI开发》的第14天！在前面的课程中，我们学习了AI Agent的基础概念、构建简单工作流，以及多Agent协作系统。今天，我们将深入探讨如何定制和优化AI Agent，使其性能更强大，行为更可控，应用更广泛。

随着你对AI Agent的理解不断深入，你可能会发现标准的Agent配置无法完全满足特定场景的需求。就像一把通用工具需要根据具体任务进行调整一样，AI Agent也需要针对特定目标进行定制和优化。今天的课程将帮助你掌握Agent性能评估方法、提示词优化技术、记忆与知识管理策略，以及领域特定Agent的定制方法，让你的AI助手更加智能高效。

## 🎯 学习目标

完成今天的学习后，你将能够：

1. 系统评估AI Agent的性能并识别优化点
2. 掌握Agent提示词优化和行为调整技术
3. 理解并实现Agent的记忆与知识管理机制
4. 为特定专业领域定制和优化AI Agent
5. 提升Agent的可靠性、安全性和用户体验

## ⏱️ 学习建议

今天的内容涉及AI Agent系统的深度优化，建议按以下方式规划你的学习时间：

| 学习内容 | 建议时间 |
|---------|---------|
| 核心知识点学习 | 60分钟 |
| Agent性能评估方法研究 | 40分钟 |
| 提示词优化技术实践 | 45分钟 |
| 记忆与知识管理实现 | 40分钟 |
| 领域Agent定制练习 | 50分钟 |
| 自测检验 | 20分钟 |
| 项目实践 | 90-120分钟 |

**学习方法建议**：

1. **循序渐进**：先了解基本评估方法，再深入到具体的优化技术
2. **对比实验**：通过对比测试不同的优化策略，体会其效果差异
3. **文档记录**：记录每次优化的参数和结果，形成个人最佳实践
4. **结构思考**：绘制Agent系统的结构图，明确各组件的优化方向
5. **实例分析**：分析优秀Agent案例，学习其优化思路和方法
6. **反馈循环**：实施优化-测试-评估-再优化的迭代过程

## 🔑 核心知识点

### 1. Agent性能评估方法

有效的优化首先需要科学的评估。了解如何评估Agent性能是优化的基础。

#### 1.1 评估指标体系

评估AI Agent性能需要从多个维度建立综合指标体系：

**1. 任务完成度指标**
- **成功率**：成功完成任务的比例
- **准确性**：输出结果的正确程度
- **完整性**：任务要求的覆盖程度
- **质量评分**：输出内容的质量水平

**2. 效率指标**
- **响应时间**：从接收指令到开始响应的时间
- **任务完成时间**：完成整个任务的总时间
- **交互次数**：完成任务所需的交互轮次
- **资源消耗**：Token使用量、API调用次数等

**3. 用户体验指标**
- **满意度评分**：用户对结果的满意程度
- **易用性**：交互过程的流畅度和直观性
- **有用性**：提供信息的实用价值
- **信任度**：用户对Agent回答的信任程度

**4. 专业能力指标**
- **专业准确性**：专业知识的正确程度
- **推理能力**：逻辑分析和推理的质量
- **创新能力**：提供创新思路和解决方案的能力
- **适应性**：处理不同类型任务的能力

#### 1.2 评估与测试方法

**1. 基准测试（Benchmark Testing）**

基准测试是通过一组标准化的任务评估Agent性能，并与预定标准或其他Agent进行比较：

```python
def run_benchmark_test(agent, test_cases, metrics):
    """
    运行基准测试并返回性能报告
    
    参数:
    - agent: 待测试的Agent对象
    - test_cases: 测试用例列表
    - metrics: 需要评估的指标列表
    
    返回:
    - 性能报告字典
    """
    results = {metric: [] for metric in metrics}
    
    for test_case in test_cases:
        # 执行测试
        start_time = time.time()
        response = agent.run(test_case['input'])
        end_time = time.time()
        
        # 评估结果
        if 'response_time' in metrics:
            results['response_time'].append(end_time - start_time)
        
        if 'accuracy' in metrics:
            accuracy = calculate_accuracy(response, test_case['expected'])
            results['accuracy'].append(accuracy)
        
        # 其他指标评估...
    
    # 计算平均值
    report = {metric: sum(values)/len(values) for metric, values in results.items()}
    return report
```

**2. A/B测试**

A/B测试通过比较两个或多个版本的Agent在相同条件下的表现，确定哪种配置更有效：

```
┌─────────────────┐     ┌─────────────────┐
│     Agent A     │     │     Agent B     │
│ (当前版本/基线)  │     │ (优化版本/变体)  │
└────────┬────────┘     └────────┬────────┘
         │                       │
         ▼                       ▼
┌─────────────────┐     ┌─────────────────┐
│  相同测试任务集  │     │  相同测试任务集  │
└────────┬────────┘     └────────┬────────┘
         │                       │
         ▼                       ▼
┌─────────────────┐     ┌─────────────────┐
│    性能指标A     │     │    性能指标B     │
└────────┬────────┘     └────────┬────────┘
         │                       │
         └───────────┬───────────┘
                     ▼
           ┌──────────────────┐
           │  统计显著性分析  │
           └──────────────────┘
```

A/B测试适用场景：
- 测试不同的提示词策略
- 比较不同的记忆机制
- 评估不同的工具组合
- 验证新功能的效果

**3. 用户反馈收集**

直接从用户获取反馈是评估Agent实际价值的重要方法：

```python
def collect_user_feedback(session_id, response, user=None):
    """收集用户对Agent响应的反馈"""
    feedback_form = {
        "session_id": session_id,
        "response_id": generate_id(),
        "timestamp": current_timestamp(),
        "rating": None,  # 1-5评分
        "aspects": {
            "accuracy": None,  # 1-5评分
            "helpfulness": None,  # 1-5评分
            "clarity": None  # 1-5评分
        },
        "comments": "",
        "improvement_suggestions": "",
        "user_id": user.id if user else "anonymous"
    }
    
    return feedback_form
```

**4. 错误分析**

系统性分析Agent的失败案例，识别模式和根本原因：

```
┌───────────────────┐
│    错误收集      │
└────────┬──────────┘
         │
         ▼
┌───────────────────┐
│    错误分类      │
│                   │
│ ┌───────────────┐ │
│ │理解错误       │ │
│ └───────────────┘ │
│ ┌───────────────┐ │
│ │推理错误       │ │
│ └───────────────┘ │
│ ┌───────────────┐ │
│ │知识错误       │ │
│ └───────────────┘ │
│ ┌───────────────┐ │
│ │执行错误       │ │
│ └───────────────┘ │
└────────┬──────────┘
         │
         ▼
┌───────────────────┐
│    根因分析      │
└────────┬──────────┘
         │
         ▼
┌───────────────────┐
│    优化方案      │
└───────────────────┘
```

分析时应记录：
- 错误的具体表现
- 触发错误的输入特征
- 失败的环节（理解/推理/执行等）
- 可能的改进方向

#### 1.3 评估工具与框架

**1. 性能监控工具**

为持续评估Agent性能，可以使用各种监控工具：

- **LangSmith**：LangChain提供的评估和监控工具
  ```python
  from langsmith import Client
  
  client = Client()
  
  # 在LangSmith中跟踪运行
  with client.trace("agent_conversation", project_name="agent_optimization") as tracer:
      result = agent.run("用户输入")
      tracer.record_metrics({
          "tokens_used": count_tokens(result),
          "response_time": response_time,
          "success": success_flag
      })
  ```

- **Weights & Biases**：用于实验跟踪和可视化
  ```python
  import wandb
  
  # 初始化W&B项目
  wandb.init(project="agent-optimization")
  
  # 记录Agent性能指标
  wandb.log({
      "accuracy": accuracy_score,
      "response_time": response_time,
      "satisfaction": user_rating
  })
  ```

**2. 自动化测试框架**

构建自动化测试框架确保Agent性能评估的一致性：

```python
class AgentEvaluator:
    def __init__(self, test_suite, metrics):
        self.test_suite = test_suite
        self.metrics = metrics
        self.results_history = []
    
    def evaluate(self, agent, version_id):
        """评估Agent并记录结果"""
        results = {
            "version_id": version_id,
            "timestamp": datetime.now().isoformat(),
            "metrics": {}
        }
        
        for test_set_name, test_cases in self.test_suite.items():
            set_results = self._run_test_set(agent, test_cases)
            results["metrics"][test_set_name] = set_results
        
        # 记录评估结果
        self.results_history.append(results)
        return results
    
    def _run_test_set(self, agent, test_cases):
        """运行一组测试并计算指标"""
        # 实现测试逻辑
        pass
    
    def compare_versions(self, version_id1, version_id2):
        """比较两个版本的性能差异"""
        # 查找两个版本的结果
        v1_results = next((r for r in self.results_history if r["version_id"] == version_id1), None)
        v2_results = next((r for r in self.results_history if r["version_id"] == version_id2), None)
        
        if not v1_results or not v2_results:
            return "一个或两个版本的结果不存在"
        
        # 计算并返回差异
        comparison = {}
        for metric_category in v1_results["metrics"]:
            if metric_category in v2_results["metrics"]:
                category_diff = {}
                for metric, value in v1_results["metrics"][metric_category].items():
                    if metric in v2_results["metrics"][metric_category]:
                        v2_value = v2_results["metrics"][metric_category][metric]
                        diff = v2_value - value
                        percent_change = (diff / value) * 100 if value != 0 else float('inf')
                        category_diff[metric] = {
                            "v1": value,
                            "v2": v2_value,
                            "absolute_diff": diff,
                            "percent_change": percent_change
                        }
                comparison[metric_category] = category_diff
        
        return comparison
```

### 2. 提示词优化技术

Agent的性能很大程度上取决于其系统提示词(System Prompt)的质量。优化提示词是提升Agent性能的关键步骤。

#### 2.1 系统提示改进

系统提示是Agent行为的基础框架，决定了其角色、能力和行为模式。

**1. 角色定义精确化**

明确定义Agent的角色，使其有清晰的职责边界：

```
你是一位专业的[具体角色]，具有[X年]相关经验，专长于[具体领域/技能]。
你曾成功解决过[相关典型问题]，并擅长使用[专业工具/方法]。

你的工作方式：
- 始终保持[专业特质]的态度
- 优先考虑[核心价值/原则]
- 在面对不确定性时，会[处理策略]
```

例如，数据分析Agent的角色定义：

```
你是一位拥有10年经验的高级数据分析师，专长于业务数据解读和预测分析。
你曾帮助多家财富500强企业通过数据分析优化业务决策，并擅长使用统计模型、
可视化技术和机器学习方法提炼数据洞见。

你的工作方式：
- 始终保持客观、精确和数据驱动的态度
- 优先考虑数据质量和分析结论的实用性
- 在面对不完整数据时，会明确说明假设和局限性
```

**2. 指令结构优化**

使用结构化指令提高Agent的行为一致性：

```
在执行任务时，请遵循以下工作流程：

1. 理解阶段
   - 分析用户需求的核心问题
   - 确认关键信息是否完整
   - 需要时请求澄清不明确的部分

2. 规划阶段
   - 制定解决问题的步骤
   - 确定需要使用的工具和方法
   - 评估可能的解决路径

3. 执行阶段
   - 按计划系统性解决问题
   - 记录关键决策和结果
   - 处理异常情况

4. 总结阶段
   - 提供清晰的结论或建议
   - 解释推理过程和依据
   - 提出相关的后续步骤
```

**3. 约束条件明确化**

为Agent设置明确的行为约束，避免常见问题：

```
工作限制与规范：

1. 知识界限：
   - 你的知识截止到[日期]
   - 对于超出知识范围的问题，明确表示并避免猜测
   - 不要假装访问实时信息或最新数据

2. 输出规范：
   - 回答应简洁明了，避免不必要的冗长
   - 复杂内容使用分点或分段格式增强可读性
   - 技术术语应提供简明解释

3. 安全与道德边界：
   - 拒绝生成[具体限制内容]
   - 避免提供可能导致[负面结果]的建议
   - 在涉及[敏感领域]时，强调咨询专业人士
```

#### 2.2 任务提示优化

除了系统提示，针对具体任务的提示词也需要优化：

**1. 目标分解策略**

将复杂目标分解为明确的子任务：

```
为完成[主要目标]，请按以下步骤行动：

1. 首先，[子任务1]，需要关注[关键点]
2. 然后，[子任务2]，确保考虑[重要因素]
3. 接着，[子任务3]，使用[特定方法]
4. 最后，[子任务4]，输出[预期结果格式]

每个步骤完成后，请简要总结发现，然后继续下一步。
```

**2. 思维引导技术**

引导Agent进行结构化思考：

```
在回答这个问题时，请使用以下思考框架：

1. 事实分析：列出与问题相关的已知事实和信息
2. 假设识别：明确需要做出的关键假设
3. 多角度思考：从[角度1]、[角度2]和[角度3]考虑问题
4. 利弊权衡：评估每种可能方案的优缺点
5. 结论总结：基于以上分析提出最佳建议

请确保思考过程清晰可见，避免跳过任何步骤。
```

这种方法被称为"思考链"（Chain of Thought）提示，能显著提升复杂问题的解决质量。

**3. 示例驱动提示**

通过具体示例引导Agent理解期望的输出格式和质量：

```
请按照以下示例格式提供产品分析报告：

示例输入：
分析苹果iPhone 13的市场表现

示例输出：
# iPhone 13市场分析报告

## 核心发现
- 全球销量达到X百万台，同比增长Y%
- 在高端智能手机市场份额为Z%
- 最受欢迎功能：相机系统和处理器性能

## 竞争态势
- 主要竞争对手：三星S22系列、小米12系列
- 差异化优势：生态系统整合、品牌忠诚度
- 劣势领域：充电速度、定制化选项

## 发展趋势与建议
- 未来趋势：可持续材料、AI功能整合
- 改进机会：提升充电性能、增强本地AI处理能力
- 营销方向：注重隐私安全、生态系统价值

请按照上述格式分析[用户指定的产品]
```

### 3. Agent记忆与知识管理

高效的记忆和知识管理机制是提升Agent智能表现的关键因素。

#### 3.1 记忆系统架构

AI Agent需要不同类型的记忆系统来处理不同时间跨度和重要性的信息：

**1. 多层次记忆结构**

```
┌───────────────────────────────────────────┐
│              Agent记忆系统                 │
├───────────────┬───────────────┬───────────┤
│   工作记忆     │   情景记忆     │  长期记忆  │
│ (短期/即时)    │  (会话级别)    │ (持久知识) │
├───────────────┼───────────────┼───────────┤
│• 当前任务状态  │• 对话历史      │• 领域知识  │
│• 临时推理结果  │• 用户偏好      │• 过往经验  │
│• 中间计算数据  │• 最近交互模式  │• 规则流程  │
│• 注意力焦点    │• 上下文理解    │• 概念模型  │
└───────────────┴───────────────┴───────────┘
```

**2. 短期记忆实现**

短期记忆存储当前交互所需的即时信息：

```python
class WorkingMemory:
    def __init__(self, capacity=5):
        """初始化工作记忆，设置容量限制"""
        self.capacity = capacity
        self.items = []
        self.attention_focus = None
    
    def add_item(self, item, importance=1.0):
        """添加项目到工作记忆"""
        if len(self.items) >= self.capacity:
            # 移除最不重要的项目
            self.items.sort(key=lambda x: x['importance'])
            self.items.pop(0)
        
        self.items.append({
            'content': item,
            'timestamp': time.time(),
            'importance': importance
        })
    
    def get_current_state(self):
        """获取当前工作记忆状态"""
        return {
            'items': self.items,
            'focus': self.attention_focus
        }
    
    def set_focus(self, item_index):
        """设置注意力焦点"""
        if 0 <= item_index < len(self.items):
            self.attention_focus = item_index
    
    def clear(self):
        """清空工作记忆"""
        self.items = []
        self.attention_focus = None
```

**3. 会话记忆管理**

会话记忆存储当前对话的历史和上下文：

```python
class ConversationMemory:
    def __init__(self, max_history_length=10):
        """初始化对话记忆"""
        self.history = []
        self.max_length = max_history_length
        self.summary = ""
        self.user_preferences = {}
    
    def add_exchange(self, user_input, agent_response):
        """添加一轮对话交流"""
        exchange = {
            'user': user_input,
            'agent': agent_response,
            'timestamp': datetime.now().isoformat()
        }
        
        self.history.append(exchange)
        
        # 如果历史超出最大长度，压缩旧对话
        if len(self.history) > self.max_length:
            self._compress_history()
    
    def _compress_history(self):
        """压缩旧对话历史，保留重要信息"""
        # 提取最早的几轮对话
        to_compress = self.history[:3]
        
        # 生成这些对话的摘要
        compressed = {
            'summary': "这是前几轮对话的摘要...",  # 实际中使用LLM生成摘要
            'compressed_rounds': len(to_compress),
            'timestamp_range': [to_compress[0]['timestamp'], to_compress[-1]['timestamp']]
        }
        
        # 用摘要替换原始对话
        self.history = [compressed] + self.history[3:]
    
    def get_relevant_history(self, current_input, full=False):
        """获取与当前输入相关的历史记录"""
        if full:
            return self.history
        
        # 实际实现中，可以使用相关性计算选择历史
        # 这里简化为返回最近的几轮对话
        return self.history[-3:]
    
    def update_user_preferences(self, key, value):
        """更新用户偏好"""
        self.user_preferences[key] = {
            'value': value,
            'updated_at': datetime.now().isoformat()
        }
```

**4. 长期知识存储**

长期记忆存储持久化的知识和经验：

```python
class LongTermMemory:
    def __init__(self, vector_store):
        """初始化长期记忆，使用向量存储"""
        self.vector_store = vector_store
        self.episodic_memories = []
        self.semantic_knowledge = {}
        self.last_consolidated = None
    
    def store_fact(self, fact, source=None):
        """存储语义知识"""
        # 为事实生成唯一ID
        fact_id = str(uuid.uuid4())
        
        # 准备知识条目
        knowledge_entry = {
            'id': fact_id,
            'content': fact,
            'source': source,
            'created_at': datetime.now().isoformat(),
            'access_count': 0,
            'last_accessed': None
        }
        
        # 存储到语义知识库
        self.semantic_knowledge[fact_id] = knowledge_entry
        
        # 同时存储到向量数据库以便相似性搜索
        embedding = self._get_embedding(fact)
        self.vector_store.add_item(fact_id, embedding, metadata=knowledge_entry)
        
        return fact_id
    
    def store_experience(self, experience):
        """存储情节记忆/经验"""
        experience_id = str(uuid.uuid4())
        
        # 准备记忆条目
        memory_entry = {
            'id': experience_id,
            'content': experience,
            'created_at': datetime.now().isoformat(),
            'importance': 1.0,  # 初始重要性
            'access_count': 0,
            'last_accessed': None
        }
        
        # 添加到情节记忆
        self.episodic_memories.append(memory_entry)
        
        # 同时存储到向量数据库
        embedding = self._get_embedding(experience)
        self.vector_store.add_item(experience_id, embedding, metadata=memory_entry)
        
        return experience_id
    
    def retrieve_relevant(self, query, limit=5):
        """检索与查询相关的知识和记忆"""
        # 生成查询的嵌入向量
        query_embedding = self._get_embedding(query)
        
        # 搜索相似内容
        results = self.vector_store.search(query_embedding, limit=limit)
        
        # 更新访问统计
        for result in results:
            item_id = result['id']
            if item_id in self.semantic_knowledge:
                self.semantic_knowledge[item_id]['access_count'] += 1
                self.semantic_knowledge[item_id]['last_accessed'] = datetime.now().isoformat()
        
        return results
    
    def _get_embedding(self, text):
        """获取文本的嵌入向量"""
        # 实际实现中调用嵌入模型API
        # 这里返回模拟的嵌入向量
        return [0.1, 0.2, 0.3]  # 示例
    
    def consolidate_memories(self):
        """记忆整合，提取重要经验形成一般性知识"""
        # 实际实现中可能包含复杂的记忆整合逻辑
        self.last_consolidated = datetime.now().isoformat()
        # 这里简化实现
```

#### 3.2 知识库设计

为Agent设计高效的知识库，可以显著提升其专业表现：

**1. 知识表示方法**

根据知识类型选择合适的表示方法：

| 知识类型 | 表示方法 | 适用场景 |
|---------|---------|---------|
| 事实性知识 | 三元组(实体-关系-实体) | 客观事实、定义、属性 |
| 过程性知识 | 步骤序列 | 操作指南、方法论、工作流程 |
| 条件性知识 | 规则集(if-then) | 判断标准、决策依据、专业规范 |
| 概念性知识 | 概念图或树状结构 | 分类体系、层次关系、概念间联系 |

**2. 向量数据库应用**

使用向量数据库存储和检索知识：

```python
from langchain.vectorstores import Chroma, FAISS
from langchain.embeddings import OpenAIEmbeddings

class KnowledgeBase:
    def __init__(self, embedding_model=None):
        """初始化知识库"""
        self.embedding_model = embedding_model or OpenAIEmbeddings()
        self.vector_db = FAISS.from_texts(
            ["初始化知识库"], self.embedding_model
        )
        self.knowledge_metadata = {}
    
    def add_knowledge(self, content, metadata=None):
        """添加知识到知识库"""
        # 生成唯一ID
        knowledge_id = str(uuid.uuid4())
        
        # 准备元数据
        entry_metadata = metadata or {}
        entry_metadata.update({
            "id": knowledge_id,
            "added_at": datetime.now().isoformat(),
            "source": entry_metadata.get("source", "manual"),
            "type": entry_metadata.get("type", "general")
        })
        
        # 存储元数据
        self.knowledge_metadata[knowledge_id] = entry_metadata
        
        # 添加到向量数据库
        self.vector_db.add_texts([content], metadatas=[entry_metadata])
        
        return knowledge_id
    
    def query_knowledge(self, query, limit=5, filter_criteria=None):
        """查询相关知识"""
        # 构建过滤器
        filter_dict = None
        if filter_criteria:
            filter_dict = {}
            for key, value in filter_criteria.items():
                filter_dict[key] = value
        
        # 执行相似性搜索
        results = self.vector_db.similarity_search(
            query, k=limit, filter=filter_dict
        )
        
        return results
    
    def batch_import(self, documents):
        """批量导入知识文档"""
        texts = []
        metadatas = []
        
        for doc in documents:
            knowledge_id = str(uuid.uuid4())
            metadata = doc.get("metadata", {})
            metadata["id"] = knowledge_id
            metadata["added_at"] = datetime.now().isoformat()
            
            texts.append(doc["content"])
            metadatas.append(metadata)
            self.knowledge_metadata[knowledge_id] = metadata
        
        self.vector_db.add_texts(texts, metadatas=metadatas)
        return len(texts)
```

**3. 知识更新机制**

实现知识的动态更新和调整：

```python
def update_knowledge(self, knowledge_id, new_content, update_metadata=None):
    """更新现有知识"""
    if knowledge_id not in self.knowledge_metadata:
        raise ValueError(f"知识ID {knowledge_id} 不存在")
    
    # 获取原始元数据
    metadata = self.knowledge_metadata[knowledge_id].copy()
    
    # 更新元数据
    if update_metadata:
        metadata.update(update_metadata)
    
    # 添加更新记录
    metadata["updated_at"] = datetime.now().isoformat()
    metadata["update_count"] = metadata.get("update_count", 0) + 1
    
    # 删除旧版本
    self._delete_by_id(knowledge_id)
    
    # 添加新版本
    self.vector_db.add_texts([new_content], metadatas=[metadata])
    self.knowledge_metadata[knowledge_id] = metadata
    
    return knowledge_id

def _delete_by_id(self, knowledge_id):
    """从向量库中删除指定ID的知识项"""
    # 实际实现根据使用的向量数据库有所不同
    # 对于大多数向量数据库，需要通过检索然后过滤删除
    # 此处为简化实现
    pass
```

#### 3.3 上下文管理技术

有效的上下文管理可以帮助Agent在有限的上下文窗口中传递更多信息：

**1. 对话历史压缩**

当对话历史过长时，使用摘要压缩技术保留关键信息：

```python
def compress_conversation_history(conversation_history, max_tokens=1000):
    """压缩对话历史以适应上下文窗口"""
    # 计算当前历史的token数
    current_tokens = count_tokens(conversation_history)
    
    # 如果没有超过限制，直接返回
    if current_tokens <= max_tokens:
        return conversation_history
    
    # 提取最近的几轮对话（保持完整）
    recent_exchanges = conversation_history[-3:]
    recent_tokens = count_tokens(recent_exchanges)
    
    # 剩余token预算
    remaining_budget = max_tokens - recent_tokens
    
    # 压缩早期对话
    earlier_exchanges = conversation_history[:-3]
    
    # 生成摘要
    summary = summarize_exchanges(earlier_exchanges)
    
    # 组合摘要和最近对话
    compressed_history = [
        {"role": "system", "content": f"以下是之前对话的摘要: {summary}"}
    ] + recent_exchanges
    
    return compressed_history
```

**2. 重要信息提取**

自动识别和保留对话中的关键信息：

```python
def extract_key_information(message, context=None):
    """从消息中提取关键信息"""
    # 定义关键信息类型及其模式
    information_patterns = {
        "user_goal": r"目标|需要|希望|想要|计划",
        "constraints": r"限制|条件|要求|必须|不能|应该",
        "preferences": r"喜欢|偏好|更倾向于|首选",
        "decisions": r"决定|选择|确定|采用",
        "questions": r"\?|问题|如何|为什么|是否"
    }
    
    extracted_info = {}
    
    # 对每种信息类型应用模式匹配
    for info_type, pattern in information_patterns.items():
        matches = re.findall(f".*({pattern}).*", message)
        if matches:
            # 提取包含关键词的完整句子
            sentences = re.split(r'[.!?；。！？]', message)
            relevant_sentences = [
                s for s in sentences 
                if any(re.search(pattern, s) for term in matches)
            ]
            
            if relevant_sentences:
                extracted_info[info_type] = relevant_sentences
    
    # 使用LLM提取更复杂的信息（实际应用中）
    # 此处简化实现
    
    return extracted_info
```

**3. 会话状态追踪**

维护对话的关键状态信息：

```python
class ConversationStateTracker:
    def __init__(self):
        """初始化会话状态跟踪器"""
        self.state = {
            "current_task": None,
            "task_progress": 0,
            "identified_goals": [],
            "user_preferences": {},
            "decisions_made": {},
            "pending_questions": [],
            "topics_discussed": set(),
            "entities_mentioned": {}
        }
    
    def update_from_exchange(self, user_message, agent_response):
        """从一轮对话更新状态"""
        # 更新讨论的主题
        topics = extract_topics(user_message)
        self.state["topics_discussed"].update(topics)
        
        # 识别实体
        entities = extract_entities(user_message)
        for entity, entity_type in entities.items():
            if entity not in self.state["entities_mentioned"]:
                self.state["entities_mentioned"][entity] = {
                    "type": entity_type,
                    "first_mentioned": datetime.now().isoformat(),
                    "mention_count": 1
                }
            else:
                self.state["entities_mentioned"][entity]["mention_count"] += 1
        
        # 提取用户偏好
        preferences = extract_preferences(user_message)
        self.state["user_preferences"].update(preferences)
        
        # 检测任务进展
        if "task_progress" in agent_response:
            self.state["task_progress"] = agent_response["task_progress"]
        
        # 更新其他状态...
    
    def get_relevant_state(self, current_context):
        """获取与当前上下文相关的状态信息"""
        # 根据当前上下文筛选相关状态
        # 简化实现
        return self.state
```

### 4. 领域特定Agent定制

为特定领域定制Agent可以显著提升其在专业场景中的表现。

#### 4.1 领域知识注入

为Agent注入特定领域的专业知识：

**1. 专业术语库构建**

```python
def build_domain_terminology(domain):
    """构建领域专业术语库"""
    terminology_sources = {
        "legal": "legal_terms.json",
        "medical": "medical_terminology.json",
        "finance": "financial_terms.json",
        "tech": "technical_glossary.json"
    }
    
    if domain not in terminology_sources:
        raise ValueError(f"不支持的领域: {domain}")
    
    # 加载术语库
    with open(terminology_sources[domain], "r") as f:
        terminology = json.load(f)
    
    # 构建术语解释字符串
    terminology_primer = "领域术语解释:\n\n"
    for term, explanation in terminology.items():
        terminology_primer += f"- {term}: {explanation}\n"
    
    return terminology_primer
```

**2. 领域规则与流程**

```python
def inject_domain_rules(domain):
    """注入领域特定规则和流程"""
    domain_rules = {
        "legal": [
            "所有法律建议都必须基于现行法律法规",
            "明确区分法律事实和个人观点",
            "需要引用具体法律条款支持观点",
            "提醒用户复杂法律问题应咨询专业律师",
            "不得提供规避法律的建议"
        ],
        "medical": [
            "不得提供具体诊断或治疗建议",
            "所有医疗信息必须基于公认医学共识",
            "强调重要医疗决策需咨询医生",
            "区分普通健康建议和专业医疗建议",
            "不应替代专业医疗咨询"
        ],
        # 其他领域规则...
    }
    
    if domain not in domain_rules:
        return "该领域没有特定规则列表"
    
    rules_text = f"{domain}领域规则:\n\n"
    for i, rule in enumerate(domain_rules[domain], 1):
        rules_text += f"{i}. {rule}\n"
    
    return rules_text
```

**3. 参考资源集成**

```python
class DomainReferences:
    def __init__(self, domain):
        """初始化领域参考资源"""
        self.domain = domain
        self.references = self._load_references()
        self.citation_style = self._get_citation_style()
    
    def _load_references(self):
        """加载领域参考资源"""
        # 实际实现中可能从数据库或文件加载
        references = {
            "legal": {
                "statutes": ["刑法", "民法典", "合同法", "公司法"],
                "cases": ["最高人民法院指导案例"],
                "articles": ["中国法学", "法律评论"]
            },
            "medical": {
                "guidelines": ["临床实践指南", "诊疗规范"],
                "research": ["医学研究期刊", "医学综述"],
                "databases": ["PubMed", "医学知识库"]
            }
            # 其他领域资源...
        }
        
        return references.get(self.domain, {})
    
    def _get_citation_style(self):
        """获取领域引用格式"""
        styles = {
            "legal": "法学引用格式",
            "medical": "医学期刊引用格式",
            "finance": "经济学引用格式"
            # 其他引用风格...
        }
        
        return styles.get(self.domain, "标准引用格式")
    
    def get_relevant_references(self, topic):
        """获取与特定主题相关的参考资源"""
        # 实际实现中应该进行语义匹配
        # 此处简化实现
        return self.references
    
    def format_citation(self, source):
        """格式化引用"""
        # 根据引用风格格式化引用
        # 简化实现
        return f"({source}, 根据{self.citation_style})"
```

#### 4.2 行为模式定制

根据不同领域调整Agent的行为模式：

**1. 专业语言风格**

```python
def set_professional_tone(domain):
    """设置专业语言风格"""
    tone_guidelines = {
        "legal": {
            "formality": "high",
            "precision": "high",
            "language_style": "正式法律用语，避免口语化表达",
            "sentence_structure": "清晰完整的复合句，准确表达条件和关系",
            "examples": [
                "根据《合同法》第X条规定，当事人一方违约，应当承担继续履行、采取补救措施或者赔偿损失等违约责任。",
                "考虑到本案的具体情况，建议依法行使合同撤销权，同时保留索赔权利。"
            ]
        },
        "medical": {
            "formality": "medium-high",
            "precision": "very high",
            "language_style": "专业医学术语与通俗解释相结合",
            "sentence_structure": "简洁明了，关键医学信息突出",
            "examples": [
                "高血压（血压持续≥140/90 mmHg）是心血管疾病的主要危险因素之一。",
                "建议保持规律作息、均衡饮食，并定期监测血压。如有不适，请及时就医。"
            ]
        }
        # 其他领域风格...
    }
    
    if domain not in tone_guidelines:
        return "未找到该领域的语言风格指南"
    
    style_guide = tone_guidelines[domain]
    
    return (
        f"语言风格指南 - {domain}领域：\n\n"
        f"正式程度：{style_guide['formality']}\n"
        f"精确程度：{style_guide['precision']}\n"
        f"语言风格：{style_guide['language_style']}\n"
        f"句式结构：{style_guide['sentence_structure']}\n\n"
        f"示例表达：\n"
        f"1. {style_guide['examples'][0]}\n"
        f"2. {style_guide['examples'][1]}"
    )
```

**2. 专业推理路径**

根据领域调整思考和分析方法：

```python
def domain_reasoning_framework(domain):
    """领域特定的推理框架"""
    reasoning_frameworks = {
        "legal": {
            "name": "IRAC法律分析",
            "steps": [
                "Issue (问题): 明确识别法律问题",
                "Rule (规则): 找出适用的法律规则和原则",
                "Application (应用): 将规则应用于事实",
                "Conclusion (结论): 得出法律结论"
            ]
        },
        "medical": {
            "name": "临床推理模型",
            "steps": [
                "症状识别: 确认主要症状和体征",
                "鉴别诊断: 考虑可能的疾病",
                "证据评估: 分析支持或反对各诊断的证据",
                "管理计划: 提出进一步检查或治疗建议"
            ]
        },
        "finance": {
            "name": "财务分析框架",
            "steps": [
                "数据收集: 获取相关财务数据",
                "比率分析: 计算关键财务比率",
                "趋势评估: 分析历史趋势和行业对比",
                "风险评估: 识别潜在风险和机会",
                "建议形成: 提出基于分析的行动建议"
            ]
        }
        # 其他领域推理框架...
    }
    
    if domain not in reasoning_frameworks:
        return None
    
    framework = reasoning_frameworks[domain]
    
    result = f"{framework['name']}推理框架：\n\n"
    for i, step in enumerate(framework['steps'], 1):
        result += f"{i}. {step}\n"
    
    return result
```

#### 4.3 专用工具集成

为领域专家Agent配置专用工具：

**1. 领域API连接**

```python
def configure_domain_apis(domain):
    """配置领域专用API"""
    domain_apis = {
        "legal": [
            {
                "name": "法规查询",
                "description": "搜索相关法律法规和条款",
                "parameters": ["法规类型", "关键词", "生效状态"],
                "endpoint": "legal_search_api"
            },
            {
                "name": "案例检索",
                "description": "查找相关判例和案例",
                "parameters": ["案由", "法院级别", "判决年份"],
                "endpoint": "case_search_api"
            }
        ],
        "finance": [
            {
                "name": "市场数据",
                "description": "获取金融市场实时数据",
                "parameters": ["资产类型", "时间范围", "指标"],
                "endpoint": "market_data_api"
            },
            {
                "name": "财务分析",
                "description": "分析公司财务数据",
                "parameters": ["公司代码", "报表类型", "分析维度"],
                "endpoint": "financial_analysis_api"
            }
        ]
        # 其他领域API...
    }
    
    return domain_apis.get(domain, [])
```

**2. 专业分析工具**

```python
def setup_analysis_tools(domain):
    """设置领域分析工具"""
    analysis_tools = {
        "medical": [
            {
                "name": "症状分析器",
                "function": analyze_symptoms,
                "description": "分析症状组合，提供可能的健康问题"
            },
            {
                "name": "药物交互检查",
                "function": check_drug_interactions,
                "description": "检查多种药物之间的潜在交互作用"
            }
        ],
        "finance": [
            {
                "name": "投资组合分析",
                "function": analyze_portfolio,
                "description": "分析投资组合的风险和回报特性"
            },
            {
                "name": "财务比率计算器",
                "function": calculate_financial_ratios,
                "description": "计算关键财务比率和指标"
            }
        ]
        # 其他领域工具...
    }
    
    tools = analysis_tools.get(domain, [])
    
    # 绑定实际函数
    for tool in tools:
        # 在实际实现中连接真实函数
        pass
    
    return tools
```

**3. 数据源整合**

```python
class DomainDataSources:
    def __init__(self, domain):
        """初始化领域数据源"""
        self.domain = domain
        self.data_sources = self._get_data_sources()
    
    def _get_data_sources(self):
        """获取领域数据源配置"""
        sources = {
            "healthcare": [
                {
                    "name": "医学研究数据库",
                    "type": "academic",
                    "access_method": "api",
                    "update_frequency": "monthly"
                },
                {
                    "name": "健康指南数据库",
                    "type": "guidelines",
                    "access_method": "file",
                    "update_frequency": "quarterly"
                }
            ],
            "finance": [
                {
                    "name": "市场数据流",
                    "type": "realtime",
                    "access_method": "stream",
                    "update_frequency": "realtime"
                },
                {
                    "name": "公司财报数据库",
                    "type": "structured",
                    "access_method": "api",
                    "update_frequency": "quarterly"
                }
            ]
            # 其他领域数据源...
        }
        
        return sources.get(self.domain, [])
    
    def connect_data_source(self, source_name):
        """连接到指定数据源"""
        # 实际实现中连接到真实数据源
        # 此处简化实现
        source = next((s for s in self.data_sources if s["name"] == source_name), None)
        if not source:
            return None
        
        print(f"连接到数据源: {source_name} (类型: {source['type']})")
        return {"status": "connected", "source": source}
    
    def query_data(self, source_name, query_params):
        """查询数据源数据"""
        # 实际实现中查询真实数据
        # 此处简化实现
        return {"status": "success", "data": {"sample": "data"}}
```

### 5. 工具使用优化

Agent使用工具的效率和准确性对其整体性能有重大影响。

#### 5.1 工具选择与组合

优化Agent对工具的选择和组合能力：

**1. 工具功能分析**

```python
def analyze_tool_capabilities(tools):
    """分析工具集的功能覆盖和重叠"""
    # 提取工具功能
    capabilities = {}
    
    for tool in tools:
        # 获取工具能力关键词
        tool_caps = extract_capabilities(tool.description)
        
        for cap in tool_caps:
            if cap not in capabilities:
                capabilities[cap] = []
            capabilities[cap].append(tool.name)
    
    # 分析结果
    results = {
        "total_tools": len(tools),
        "capability_coverage": list(capabilities.keys()),
        "overlapping_capabilities": {
            cap: tools for cap, tools in capabilities.items() if len(tools) > 1
        },
        "unique_capabilities": {
            cap: tools[0] for cap, tools in capabilities.items() if len(tools) == 1
        }
    }
    
    return results

def extract_capabilities(description):
    """从工具描述中提取能力关键词"""
    # 实际实现应使用NLP分析
    # 此处简化实现，假设关键词已存在
    keywords = description.lower().split()
    return [k for k in keywords if len(k) > 4]  # 简单过滤
```

**2. 工具组合策略**

针对不同任务类型配置最佳工具组合：

```python
class ToolSetOptimizer:
    def __init__(self, available_tools):
        """初始化工具集优化器"""
        self.available_tools = available_tools
        self.task_tool_mapping = self._build_task_mapping()
    
    def _build_task_mapping(self):
        """构建任务类型到工具的映射"""
        mapping = {
            "information_search": ["web_search", "database_query", "document_retriever"],
            "content_creation": ["text_generator", "image_creator", "code_writer"],
            "data_analysis": ["data_analyzer", "chart_creator", "statistical_tool"],
            "planning": ["task_planner", "scheduler", "priority_tool"],
            "communication": ["email_sender", "message_formatter", "translator"]
        }
        
        # 过滤只保留可用的工具
        available_names = [tool.name for tool in self.available_tools]
        for task, tools in mapping.items():
            mapping[task] = [t for t in tools if t in available_names]
        
        return mapping
    
    def recommend_tools_for_task(self, task_description):
        """根据任务描述推荐工具组合"""
        # 实际实现应使用任务分类或相似度匹配
        # 此处简化实现
        recommended_tools = []
        
        for task_type, tools in self.task_tool_mapping.items():
            if task_type.lower() in task_description.lower():
                recommended_tools.extend(tools)
        
        # 移除重复项
        recommended_tools = list(set(recommended_tools))
        
        # 获取实际工具对象
        return [
            tool for tool in self.available_tools 
            if tool.name in recommended_tools
        ]
```

**3. 工具依赖分析**

分析工具之间的依赖关系，优化调用顺序：

```python
def analyze_tool_dependencies(tools):
    """分析工具间的依赖关系"""
    # 构建依赖图（简化实现）
    tool_map = {tool.name: tool for tool in tools}
    dependency_graph = {}
    
    for tool in tools:
        dependencies = []
        
        # 检查该工具的输入是否依赖其他工具的输出
        for other in tools:
            if other.name != tool.name:
                if tool_depends_on(tool, other):
                    dependencies.append(other.name)
        
        dependency_graph[tool.name] = dependencies
    
    return dependency_graph

def tool_depends_on(tool1, tool2):
    """检查tool1是否依赖tool2的输出"""
    # 实际实现应分析参数和返回值类型
    # 此处为简化实现，返回假数据
    return False  # 样例返回
```

#### 5.2 工具调用效率

提升Agent对工具的调用效率：

**1. 参数传递优化**

```python
def optimize_tool_parameters(tool, parameters, context):
    """优化传递给工具的参数"""
    optimized = parameters.copy()
    
    # 检查必要参数
    required_params = get_required_parameters(tool)
    for param in required_params:
        if param not in optimized or not optimized[param]:
            # 尝试从上下文中提取
            optimized[param] = extract_from_context(param, context)
    
    # 去除冗余参数
    allowed_params = get_all_parameters(tool)
    for param in list(optimized.keys()):
        if param not in allowed_params:
            del optimized[param]
    
    # 格式化参数值
    for param, value in optimized.items():
        param_type = get_parameter_type(tool, param)
        optimized[param] = format_parameter_value(value, param_type)
    
    return optimized

def extract_from_context(param_name, context):
    """从上下文中提取参数值"""
    # 实际实现应使用更复杂的上下文分析
    # 此处简化实现
    keywords = {
        "query": ["搜索", "查询", "寻找", "查找"],
        "limit": ["限制", "数量", "条目"],
        "start_date": ["开始日期", "从", "起始"],
        "end_date": ["结束日期", "到", "截止"]
    }
    
    if param_name in keywords:
        for keyword in keywords[param_name]:
            pattern = f"{keyword}[：:]*\\s*([\\w\\d\\-]+)"
            matches = re.findall(pattern, context)
            if matches:
                return matches[0]
    
    return None
```

**2. 结果缓存策略**

缓存工具调用结果以减少重复调用：

```python
class ToolResultCache:
    def __init__(self, cache_lifetime=3600):  # 默认缓存1小时
        """初始化工具结果缓存"""
        self.cache = {}
        self.cache_lifetime = cache_lifetime  # 缓存生命周期（秒）
    
    def get(self, tool_name, parameters):
        """获取缓存的结果"""
        cache_key = self._generate_key(tool_name, parameters)
        
        if cache_key in self.cache:
            entry = self.cache[cache_key]
            
            # 检查是否过期
            if time.time() - entry["timestamp"] < self.cache_lifetime:
                entry["hits"] += 1
                return entry["result"]
            else:
                # 缓存过期，删除
                del self.cache[cache_key]
        
        return None
    
    def store(self, tool_name, parameters, result):
        """存储工具调用结果"""
        cache_key = self._generate_key(tool_name, parameters)
        
        self.cache[cache_key] = {
            "result": result,
            "timestamp": time.time(),
            "hits": 0
        }
    
    def _generate_key(self, tool_name, parameters):
        """生成缓存键"""
        # 将参数转换为可哈希形式
        param_str = json.dumps(parameters, sort_keys=True)
        return f"{tool_name}:{param_str}"
    
    def clear_expired(self):
        """清除过期缓存"""
        now = time.time()
        expired_keys = [
            key for key, entry in self.cache.items()
            if now - entry["timestamp"] >= self.cache_lifetime
        ]
        
        for key in expired_keys:
            del self.cache[key]
        
        return len(expired_keys)
```

**3. 并行调用技术**

实现工具的并行调用以提高整体效率：

```python
async def parallel_tool_execution(tools_with_params):
    """并行执行多个工具调用"""
    async def execute_tool(tool, params):
        try:
            result = await tool.arun(**params)
            return {
                "tool": tool.name,
                "success": True,
                "result": result,
                "error": None
            }
        except Exception as e:
            return {
                "tool": tool.name,
                "success": False,
                "result": None,
                "error": str(e)
            }
    
    # 创建所有工具调用的任务
    tasks = []
    for tool_data in tools_with_params:
        task = execute_tool(tool_data["tool"], tool_data["parameters"])
        tasks.append(task)
    
    # 并行执行所有任务
    results = await asyncio.gather(*tasks)
    return results
```

#### 5.3 工具描述优化

优化工具描述以帮助Agent更准确地选择和使用工具：

**1. 功能说明精确化**

```python
def optimize_tool_description(tool):
    """优化工具描述"""
    # 原始描述
    original_desc = tool.description
    
    # 结构化的改进描述
    improved_desc = f"""
{tool.name}: {get_concise_description(original_desc)}

用途: {get_purpose(original_desc)}

适用场景: 
{get_use_cases(original_desc)}

输出格式: 
{get_output_format(tool)}

注意事项: 
{get_limitations(original_desc)}
""".strip()
    
    return improved_desc

def get_concise_description(desc):
    """提取简洁描述"""
    # 实际实现应使用NLP提取摘要
    # 此处简化实现
    first_sentence = desc.split('.')[0]
    return first_sentence if first_sentence else desc
```

**2. 使用示例增加**

```python
def add_tool_examples(tool):
    """为工具添加使用示例"""
    examples = []
    
    # 根据工具类型生成示例（实际实现应有预定义示例库）
    if "search" in tool.name.lower():
        examples.append({
            "description": "搜索关于气候变化的最新研究",
            "parameters": {"query": "最新气候变化研究", "limit": 5},
            "sample_output": "返回5篇关于气候变化的最新研究文章信息..."
        })
    elif "analyze" in tool.name.lower():
        examples.append({
            "description": "分析公司季度销售数据",
            "parameters": {"data_source": "sales_q2_2023.csv", "metrics": ["growth", "regions"]},
            "sample_output": "销售增长分析结果，包括区域对比..."
        })
    # 添加其他类型的示例...
    
    if not examples:
        # 通用示例
        examples.append({
            "description": f"使用{tool.name}的基本示例",
            "parameters": {"param1": "value1"},
            "sample_output": "工具执行结果示例..."
        })
    
    # 格式化示例
    examples_text = "\n示例用法:\n\n"
    for i, example in enumerate(examples, 1):
        examples_text += f"示例{i}: {example['description']}\n"
        examples_text += f"参数: {json.dumps(example['parameters'], ensure_ascii=False)}\n"
        examples_text += f"输出: {example['sample_output']}\n\n"
    
    return examples_text
```

### 6. 用户体验与安全优化

Agent与用户的交互体验和安全性是其实用价值的重要组成部分。

#### 6.1 交互体验改进

提升Agent与用户交互的流畅性和友好度：

**1. 响应格式优化**

```python
def optimize_response_format(response, user_preference=None):
    """优化Agent响应格式"""
    # 默认格式化选项
    format_options = {
        "use_markdown": True,
        "include_headings": True,
        "list_style": "bullet",
        "code_style": "block",
        "emphasis_style": "bold"
    }
    
    # 应用用户偏好
    if user_preference:
        format_options.update(user_preference)
    
    # 应用格式化（简化实现）
    formatted = response
    
    # 添加Markdown格式
    if format_options["use_markdown"]:
        # 转换列表
        if format_options["list_style"] == "bullet":
            formatted = re.sub(r'(?m)^(\d+)\.\s+(.*)', r'- \2', formatted)
        
        # 添加代码块格式
        if format_options["code_style"] == "block":
            formatted = re.sub(r'```(\w*)\n(.*?)\n```', r'```\1\n\2\n```', formatted, flags=re.DOTALL)
    
    return formatted
```

**2. 进度反馈机制**

```python
class ProgressTracker:
    def __init__(self, total_steps):
        """初始化进度跟踪器"""
        self.total_steps = total_steps
        self.completed_steps = 0
        self.current_step = None
        self.steps = []
        self.start_time = time.time()
        self.step_times = {}
    
    def set_steps(self, steps):
        """设置任务步骤"""
        self.steps = steps
        self.total_steps = len(steps)
    
    def start_step(self, step_name):
        """开始一个步骤"""
        self.current_step = step_name
        self.step_times[step_name] = {
            "start": time.time(),
            "end": None,
            "duration": None
        }
        
        return self.get_progress_message()
    
    def complete_step(self, step_name=None):
        """完成当前步骤"""
        step_to_complete = step_name or self.current_step
        
        if step_to_complete:
            self.completed_steps += 1
            self.step_times[step_to_complete]["end"] = time.time()
            self.step_times[step_to_complete]["duration"] = (
                self.step_times[step_to_complete]["end"] - 
                self.step_times[step_to_complete]["start"]
            )
        
        return self.get_progress_message()
    
    def get_progress_message(self):
        """获取进度消息"""
        percent = (self.completed_steps / self.total_steps) * 100 if self.total_steps > 0 else 0
        
        message = f"进度: {self.completed_steps}/{self.total_steps} ({percent:.1f}%)"
        
        if self.current_step:
            message += f"\n当前步骤: {self.current_step}"
        
        # 估算剩余时间
        if self.completed_steps > 0:
            elapsed_time = time.time() - self.start_time
            time_per_step = elapsed_time / self.completed_steps
            remaining_steps = self.total_steps - self.completed_steps
            estimated_remaining = time_per_step * remaining_steps
            
            message += f"\n预计剩余时间: {format_time(estimated_remaining)}"
        
        return message

def format_time(seconds):
    """格式化时间显示"""
    if seconds < 60:
        return f"{seconds:.1f}秒"
    elif seconds < 3600:
        minutes = seconds / 60
        return f"{minutes:.1f}分钟"
    else:
        hours = seconds / 3600
        return f"{hours:.1f}小时"
```

**3. 错误信息友好化**

```python
def user_friendly_error(error, context=None):
    """将技术错误转换为用户友好的消息"""
    error_messages = {
        "RateLimitError": {
            "message": "我处理请求的速度需要稍微放慢一些。请稍等片刻再继续。",
            "suggestion": "可以尝试简化您的问题，或者稍后再试。"
        },
        "AuthenticationError": {
            "message": "系统访问权限出现了一点问题。",
            "suggestion": "请联系管理员确认您的账号设置正确。"
        },
        "ServiceUnavailableError": {
            "message": "服务暂时无法响应，这可能是临时性的问题。",
            "suggestion": "请稍后再尝试，如果问题持续存在，可能需要检查系统状态。"
        },
        "InvalidRequestError": {
            "message": "您的请求包含一些我无法处理的内容。",
            "suggestion": "请尝试重新表述您的问题，确保所有必要信息都已提供。"
        },
        "APIConnectionError": {
            "message": "我现在无法连接到需要的服务。",
            "suggestion": "请检查您的网络连接，或稍后再试。"
        },
        "ToolExecutionError": {
            "message": "我在使用相关工具时遇到了问题。",
            "suggestion": "请尝试提供更清晰的指令，或使用其他方式实现您的目标。"
        }
    }
    
    # 提取错误类型
    error_type = type(error).__name__
    
    if error_type in error_messages:
        friendly = error_messages[error_type]
        return f"{friendly['message']} {friendly['suggestion']}"
    else:
        # 通用友好错误消息
        return "抱歉，处理您的请求时遇到了一些技术问题。请尝试重新表述或稍后再试。"
```

#### 6.2 可靠性增强

提高Agent在各种情况下的稳定性：

**1. 错误恢复策略**

```python
class ResilientAgent:
    def __init__(self, base_agent, max_retries=3):
        """初始化可靠性增强的Agent"""
        self.agent = base_agent
        self.max_retries = max_retries
        self.error_counters = {}
        self.recovery_strategies = self._setup_recovery()
    
    def _setup_recovery(self):
        """设置错误恢复策略"""
        return {
            "RateLimitError": {
                "action": "wait_and_retry",
                "params": {"wait_time": 5, "backoff_factor": 2}
            },
            "APIConnectionError": {
                "action": "retry_with_backoff",
                "params": {"initial_wait": 1, "backoff_factor": 3, "max_wait": 15}
            },
            "ToolExecutionError": {
                "action": "try_alternative",
                "params": {"alternative_tools": ["fallback_tool_1", "fallback_tool_2"]}
            },
            "ContextLengthError": {
                "action": "reduce_context",
                "params": {"reduction_percent": 30}
            }
        }
    
    async def run(self, input_text):
        """执行Agent操作，包含错误恢复"""
        attempts = 0
        last_error = None
        
        while attempts < self.max_retries:
            try:
                result = await self.agent.arun(input_text)
                return result
            except Exception as e:
                attempts += 1
                last_error = e
                error_type = type(e).__name__
                
                # 记录错误
                self.error_counters[error_type] = self.error_counters.get(error_type, 0) + 1
                
                # 应用恢复策略
                if error_type in self.recovery_strategies:
                    strategy = self.recovery_strategies[error_type]
                    
                    if strategy["action"] == "wait_and_retry":
                        wait_time = strategy["params"]["wait_time"]
                        backoff = strategy["params"]["backoff_factor"]
                        
                        # 计算等待时间
                        adjusted_wait = wait_time * (backoff ** (attempts - 1))
                        await asyncio.sleep(adjusted_wait)
                        continue
                        
                    elif strategy["action"] == "try_alternative":
                        # 尝试使用替代工具
                        alt_tools = strategy["params"]["alternative_tools"]
                        if attempts <= len(alt_tools):
                            # 更换为替代工具
                            alternative = alt_tools[attempts - 1]
                            input_text = f"使用{alternative}工具: {input_text}"
                            continue
                
                # 如果没有恢复策略或策略失败，等待短暂时间后重试
                await asyncio.sleep(1 * attempts)
        
        # 所有重试都失败
        return user_friendly_error(last_error)
```

**2. 不确定性管理**

```python
def handle_uncertainty(query, confidence_threshold=0.7):
    """处理不确定性情况"""
    # 评估对查询的理解置信度
    understanding_confidence = assess_understanding(query)
    
    if understanding_confidence < confidence_threshold:
        # 识别不确定的部分
        unclear_aspects = identify_unclear_aspects(query)
        
        if unclear_aspects:
            # 生成澄清问题
            clarification = generate_clarification_questions(unclear_aspects)
            return {
                "action": "seek_clarification",
                "message": clarification,
                "confidence": understanding_confidence,
                "unclear_aspects": unclear_aspects
            }
    
    # 评估回答置信度
    answer_confidence = assess_answer_confidence(query)
    
    if answer_confidence < confidence_threshold:
        # 提供透明的低置信度回答
        return {
            "action": "transparent_low_confidence",
            "message": f"以下是我的回答，但请注意我的把握不是很大(约{answer_confidence*100:.0f}%):",
            "confidence": answer_confidence
        }
    
    # 正常高置信度回答
    return {
        "action": "confident_response",
        "confidence": answer_confidence
    }

def assess_understanding(query):
    """评估对查询的理解置信度"""
    # 实际实现应基于查询分析
    # 此处简化实现
    ambiguous_terms = ["可能", "或许", "也许", "有时", "不确定"]
    vague_terms = ["一些", "很多", "大概", "某种", "某些"]
    
    # 检查模糊词汇出现率
    ambiguity_score = sum(term in query for term in ambiguous_terms) * 0.1
    vagueness_score = sum(term in query for term in vague_terms) * 0.1
    
    base_confidence = 0.9  # 基础置信度
    final_confidence = base_confidence - ambiguity_score - vagueness_score
    
    return max(0.3, min(final_confidence, 1.0))  # 约束在0.3-1.0范围
```

#### 6.3 安全与伦理控制

增强Agent的安全性和合规性：

**1. 输入过滤机制**

```python
def safety_filter_input(user_input):
    """过滤用户输入中的潜在风险内容"""
    # 定义敏感内容类别
    sensitive_categories = {
        "harmful_instructions": [
            "编写恶意代码", "黑客攻击", "绕过安全", "破解密码"
        ],
        "illegal_activities": [
            "制作非法物品", "逃税方法", "盗窃技巧", "伪造文件"
        ],
        "personal_identification": [
            "身份证号码", "信用卡号", "银行账号", "密码"
        ],
        "hate_speech": [
            # 仇恨言论关键词
        ]
    }
    
    # 检查敏感内容
    detected_categories = []
    
    for category, keywords in sensitive_categories.items():
        for keyword in keywords:
            if keyword in user_input.lower():
                detected_categories.append(category)
                break
    
    if detected_categories:
        return {
            "filtered": True,
            "categories": detected_categories,
            "message": "您的请求包含无法处理的内容。请修改您的请求，避免敏感或不当内容。"
        }
    
    return {
        "filtered": False,
        "input": user_input
    }
```

**2. 输出审查机制**

```python
def safety_check_output(response):
    """审查Agent输出内容的安全性"""
    # 定义潜在问题模式
    problematic_patterns = {
        "unsafe_code": r"rm\s+-rf|system\(|exec\(|eval\(|sudo|chmod\s+777",
        "harmful_instructions": r"如何黑客|如何绕过|如何入侵|破解密码",
        "excessive_disclosure": r"完整代码如下|使用这个漏洞|绕过限制的方法",
        "misleading_claims": r"百分百有效|绝对安全|完全匿名|无法追踪"
    }
    
    # 检查模式匹配
    detected_issues = {}
    
    for issue, pattern in problematic_patterns.items():
        if re.search(pattern, response, re.IGNORECASE):
            detected_issues[issue] = True
    
    if detected_issues:
        # 应用缓解策略
        mitigated_response = mitigate_safety_issues(response, detected_issues)
        
        return {
            "original": response,
            "issues_detected": detected_issues,
            "mitigated": mitigated_response,
            "modified": True
        }
    
    return {
        "original": response,
        "modified": False
    }

def mitigate_safety_issues(response, issues):
    """缓解检测到的安全问题"""
    mitigated = response
    
    if "unsafe_code" in issues:
        # 替换不安全代码
        mitigated = re.sub(
            r"(rm\s+-rf|system\(|exec\(|eval\(|sudo|chmod\s+777)",
            "[不安全的代码已移除]",
            mitigated
        )
    
    if "harmful_instructions" in issues:
        # 添加警告信息
        mitigated = "请注意：以下回答仅供教育目的，不应用于任何可能造成损害的活动。\n\n" + mitigated
    
    if "excessive_disclosure" in issues:
        # 模糊化过于详细的指导
        mitigated = re.sub(
            r"(完整代码如下|使用这个漏洞|绕过限制的方法)",
            "为了安全考虑，无法提供详细指南。",
            mitigated
        )
    
    return mitigated
```

**3. 隐私保护措施**

```python
def privacy_protection(text, level="medium"):
    """应用隐私保护措施"""
    # 定义敏感数据模式
    sensitive_patterns = {
        "email": r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b',
        "phone": r'\b(?:\+?86)?1[3-9]\d{9}\b',
        "id_card": r'\b[1-9]\d{5}(?:19|20)\d{2}(?:0[1-9]|1[0-2])(?:0[1-9]|[12]\d|3[01])\d{3}[\dXx]\b',
        "address": r'\b(?:北京|上海|广州|深圳|天津|重庆|成都|武汉|西安|南京)市[\w\s\d路街道号室]{5,30}\b',
        "financial": r'\b(?:6\d{15}|4\d{15}|5[1-5]\d{14})\b'  # 简化的信用卡格式
    }
    
    # 根据保护级别选择处理方式
    if level == "high":
        # 高级保护：移除所有可能的敏感信息
        for pattern_name, pattern in sensitive_patterns.items():
            text = re.sub(pattern, f"[{pattern_name}_已保护]", text)
    
    elif level == "medium":
        # 中级保护：部分隐藏
        text = re.sub(sensitive_patterns["email"], 
                      lambda m: m.group(0).split('@')[0][:3] + "***@" + m.group(0).split('@')[1], text)
        
        text = re.sub(sensitive_patterns["phone"], 
                      lambda m: m.group(0)[:3] + "****" + m.group(0)[-4:], text)
        
        text = re.sub(sensitive_patterns["id_card"], 
                      lambda m: m.group(0)[:6] + "********" + m.group(0)[-4:], text)
    
    elif level == "low":
        # 低级保护：仅处理最敏感信息
        text = re.sub(sensitive_patterns["id_card"], 
                      lambda m: m.group(0)[:6] + "********" + m.group(0)[-4:], text)
        
        text = re.sub(sensitive_patterns["financial"], 
                      lambda m: m.group(0)[:4] + " **** **** " + m.group(0)[-4:], text)
    
    return text
```

## 💻 实践活动与代码示例

让我们通过实际案例来练习Agent优化的关键技术。

### 实践1：Agent性能评估与改进

在本实践中，我们将评估一个简单AI Agent的性能，并应用前面学习的优化技术进行改进。

**步骤1：创建基础Agent**

首先，我们需要创建一个基础Agent作为优化的起点：

```python
from langchain.llms import OpenAI
from langchain.agents import initialize_agent, Tool
from langchain.agents import AgentType
from langchain.prompts import StringPromptTemplate
from langchain.chains import LLMChain

# 简单工具定义
tools = [
    Tool(
        name="搜索",
        func=lambda query: f"搜索结果: 关于'{query}'的信息...",
        description="用于搜索信息的工具"
    ),
    Tool(
        name="计算器",
        func=lambda expression: f"计算结果: {eval(expression)}",
        description="用于执行数学计算"
    )
]

# 创建基础Agent
llm = OpenAI(temperature=0)
agent = initialize_agent(
    tools, 
    llm, 
    agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION,
    verbose=True
)
```

**步骤2：定义评估指标和测试用例**

```python
# 定义测试用例
test_cases = [
    {
        "id": "fact_query",
        "input": "水的化学式是什么？",
        "expected_tool": "搜索",
        "complexity": "low"
    },
    {
        "id": "math_problem",
        "input": "计算15*27的结果",
        "expected_tool": "计算器",
        "complexity": "low" 
    },
    {
        "id": "mixed_task",
        "input": "太阳系有多少颗行星？然后计算这个数字的平方",
        "expected_tools": ["搜索", "计算器"],
        "complexity": "medium"
    }
]

# 定义评估函数
def evaluate_agent(agent, test_cases):
    results = {}
    
    for test in test_cases:
        start_time = time.time()
        try:
            response = agent.run(test["input"])
            success = True
            error = None
        except Exception as e:
            response = None
            success = False
            error = str(e)
        
        end_time = time.time()
        
        # 记录结果
        results[test["id"]] = {
            "success": success,
            "response": response,
            "error": error,
            "response_time": end_time - start_time
        }
        
        # 分析工具使用
        if success and "expected_tool" in test:
            tool_correct = test["expected_tool"] in response
            results[test["id"]]["tool_correct"] = tool_correct
    
    return results
```

**步骤3：执行基准评估**

```python
# 评估基础Agent
baseline_results = evaluate_agent(agent, test_cases)

# 打印评估结果
print("基础Agent评估结果:")
for test_id, result in baseline_results.items():
    print(f"测试: {test_id}")
    print(f"  成功: {result['success']}")
    print(f"  响应时间: {result['response_time']:.2f}秒")
    if "tool_correct" in result:
        print(f"  工具选择正确: {result['tool_correct']}")
    print("")
```

**步骤4：优化Agent提示词**

```python
# 自定义提示模板
class CustomPromptTemplate(StringPromptTemplate):
    template: str
    tools: list
    
    def format(self, **kwargs):
        # 获取中间变量
        intermediate_steps = kwargs.pop("intermediate_steps")
        thoughts = ""
        
        # 增强提示词结构
        for action, observation in intermediate_steps:
            thoughts += f"行动: {action.log}\n"
            thoughts += f"观察: {observation}\n"
        
        # 工具描述优化
        tools_description = ""
        for tool in self.tools:
            tools_description += f"{tool.name}: {tool.description}\n"
        
        # 使用优化的提示词模板
        kwargs["agent_scratchpad"] = thoughts
        kwargs["tools"] = tools_description
        kwargs["tool_names"] = ", ".join([tool.name for tool in self.tools])
        
        # 扩展提示词
        prompt = self.template.format(**kwargs)
        
        return prompt

# 增强的提示词模板
optimized_template = """你是一个智能助手，能够利用工具解决各种问题。

可用工具:
{tools}

执行任务时请遵循以下步骤:
1. 理解用户需求
2. 确定需要使用的工具
3. 使用工具获取信息或执行操作
4. 给出清晰的最终答案

用户问题: {input}

{agent_scratchpad}

思考你的下一步行动。
使用格式:
思考: 分析问题和考虑使用哪个工具
行动: 工具名[工具输入]
观察: 工具返回的结果
... (可重复以上步骤)
回答: 给用户的最终回答
"""

# 创建优化Agent
optimized_prompt = CustomPromptTemplate(
    template=optimized_template,
    tools=tools,
    input_variables=["input", "intermediate_steps"]
)

# 使用优化后的提示词重新初始化Agent
from langchain.agents import AgentExecutor, LLMSingleActionAgent

llm_chain = LLMChain(llm=llm, prompt=optimized_prompt)
optimized_agent = LLMSingleActionAgent(
    llm_chain=llm_chain,
    output_parser=agent.agent.output_parser,
    stop=["\nObservation:"],
    allowed_tools=[tool.name for tool in tools]
)

optimized_agent_executor = AgentExecutor.from_agent_and_tools(
    agent=optimized_agent,
    tools=tools,
    verbose=True
)
```

**步骤5：比较优化前后的性能**

```python
# 评估优化后的Agent
optimized_results = evaluate_agent(optimized_agent_executor, test_cases)

# 比较结果
print("性能对比:")
for test_id in baseline_results.keys():
    baseline = baseline_results[test_id]
    optimized = optimized_results[test_id]
    
    time_diff = baseline["response_time"] - optimized["response_time"]
    time_improvement = (time_diff / baseline["response_time"]) * 100
    
    print(f"测试: {test_id}")
    print(f"  响应时间改进: {time_improvement:.2f}%")
    print(f"  基准: {baseline['response_time']:.2f}秒 -> 优化后: {optimized['response_time']:.2f}秒")
    
    if "tool_correct" in baseline and "tool_correct" in optimized:
        print(f"  工具选择: {'改进' if optimized['tool_correct'] and not baseline['tool_correct'] else '无变化' if optimized['tool_correct'] == baseline['tool_correct'] else '变差'}")
    
    print("")
```

### 实践2：专业领域Agent定制

在这个实践中，我们将创建一个专门用于法律咨询的专业领域Agent。

**步骤1：收集领域知识**

```python
# 法律领域知识（简化示例）
legal_terminology = {
    "合同": "具有法律约束力的双方或多方当事人之间的约定",
    "侵权": "违反法定义务或侵犯他人合法权益的行为",
    "诉讼时效": "法律规定的权利人可以向法院请求保护民事权利的期限",
    "不可抗力": "不能预见、不能避免且不能克服的客观情况",
    "违约金": "合同当事人约定的在违约情况下应当支付的金钱赔偿"
}

legal_principles = [
    "合同自由原则：当事人在法律允许范围内自由订立合同",
    "诚实信用原则：民事主体从事民事活动应当遵循诚实信用",
    "公平原则：确定民事权利义务应当公平，权利义务相一致",
    "禁止权利滥用原则：行使权利不得损害国家、集体或他人利益"
]

common_legal_questions = [
    {"question": "什么是合同违约？", "answer": "合同违约是指合同当事人不履行合同义务或者履行不符合约定的行为。"},
    {"question": "租房合同到期房东不退押金怎么办？", "answer": "可以先与房东协商，协商不成可以申请调解或提起诉讼，并提供相关证据如合同、支付凭证等。"}
]
```

**步骤2：创建专业知识库**

```python
from langchain.vectorstores import FAISS
from langchain.docstore.document import Document
from langchain.embeddings import OpenAIEmbeddings

# 创建法律知识文档
legal_documents = []

# 添加术语解释
for term, definition in legal_terminology.items():
    doc = Document(
        page_content=f"术语: {term}\n定义: {definition}",
        metadata={"source": "legal_terminology", "term": term}
    )
    legal_documents.append(doc)

# 添加法律原则
for principle in legal_principles:
    doc = Document(
        page_content=f"法律原则: {principle}",
        metadata={"source": "legal_principles"}
    )
    legal_documents.append(doc)

# 添加常见问题
for qa in common_legal_questions:
    doc = Document(
        page_content=f"问题: {qa['question']}\n回答: {qa['answer']}",
        metadata={"source": "common_questions"}
    )
    legal_documents.append(doc)

# 创建向量存储
embeddings = OpenAIEmbeddings()
vector_store = FAISS.from_documents(legal_documents, embeddings)

# 创建检索工具
legal_knowledge_tool = Tool(
    name="法律知识库",
    func=lambda q: vector_store.similarity_search(q, k=2),
    description="用于查询法律术语、原则和常见问题的工具"
)
```

**步骤3：定制法律专家Agent**

```python
# 法律专家系统提示
legal_expert_prompt = """你是一位拥有多年经验的法律顾问，专长于合同法、民法和消费者权益保护。

你的工作准则:
1. 始终基于法律事实提供建议，不掺杂个人观点
2. 引用相关法律条款支持你的分析
3. 明确区分法律事实和个人意见
4. 使用专业但易懂的语言表达法律概念
5. 当问题超出你的专业范围时，明确告知用户

在回答问题时，请遵循以下结构:
1. 法律问题分析: 明确识别涉及的法律问题
2. 适用法律规定: 指出相关法律条款
3. 法律分析: 将法律应用于具体情况
4. 建议: 提供可行的解决方案
5. 注意事项: 指出需要注意的风险或限制

请记住，你的建议不构成正式法律意见，复杂问题应建议用户咨询执业律师。

可用工具:
{tools}

用户问题: {input}

{agent_scratchpad}
"""

# 创建法律专家Agent
legal_expert_prompt_template = CustomPromptTemplate(
    template=legal_expert_prompt,
    tools=[legal_knowledge_tool],
    input_variables=["input", "intermediate_steps"]
)

legal_llm_chain = LLMChain(llm=llm, prompt=legal_expert_prompt_template)
legal_expert_agent = LLMSingleActionAgent(
    llm_chain=legal_llm_chain,
    output_parser=agent.agent.output_parser,
    stop=["\nObservation:"],
    allowed_tools=[legal_knowledge_tool.name]
)

legal_expert = AgentExecutor.from_agent_and_tools(
    agent=legal_expert_agent,
    tools=[legal_knowledge_tool],
    verbose=True
)
```

**步骤4：测试法律专家Agent**

```python
# 测试案例
legal_test_cases = [
    "我签了一份租房合同，但房东现在要提前终止，我有什么权利？",
    "消费者在网购商品后发现质量问题，退货被拒，如何维权？",
    "什么是不可抗力？它对合同履行有什么影响？"
]

# 执行测试
for i, test in enumerate(legal_test_cases, 1):
    print(f"测试 {i}: {test}")
    try:
        response = legal_expert.run(test)
        print(f"回答: {response}\n")
    except Exception as e:
        print(f"错误: {str(e)}\n")
```

### 实践3：记忆系统实现

这个实践中，我们将为Agent实现一个简单的记忆系统，使其能够保持上下文连贯性。

**步骤1：实现会话记忆**

```python
from langchain.memory import ConversationBufferMemory

# 创建基本记忆
memory = ConversationBufferMemory(return_messages=True)

# 初始化一些对话历史
memory.chat_memory.add_user_message("我叫张三，今年35岁")
memory.chat_memory.add_ai_message("你好张三！很高兴认识你。有什么我能帮助你的吗？")
memory.chat_memory.add_user_message("我有一个关于合同法的问题")
memory.chat_memory.add_ai_message("当然，请告诉我你的问题，我会尽力提供法律方面的帮助。")
```

**步骤2：实现自定义记忆管理**

```python
class EnhancedConversationMemory:
    def __init__(self, max_history=10):
        self.messages = []
        self.max_history = max_history
        self.user_info = {}
        self.conversation_summary = ""
        self.important_points = []
    
    def add_message(self, role, content):
        # 添加新消息
        self.messages.append({"role": role, "content": content})
        
        # 如果超出历史限制，进行压缩
        if len(self.messages) > self.max_history:
            self._compress_history()
        
        # 从用户消息中提取信息
        if role == "user":
            self._extract_user_info(content)
            self._identify_important_points(content)
    
    def _compress_history(self):
        # 保留最近的消息，最旧的消息压缩为摘要
        oldest_messages = self.messages[:2]  # 取最旧的两条
        self.messages = self.messages[2:]  # 移除最旧的两条
        
        # 生成摘要（实际应用中使用LLM生成）
        summary = f"之前的对话：用户提到 {oldest_messages[0]['content'][:30]}..."
        self.conversation_summary = summary
        
        # 在消息列表开头添加摘要
        self.messages.insert(0, {"role": "system", "content": summary})
    
    def _extract_user_info(self, message):
        # 提取用户信息（简化实现）
        name_match = re.search(r"我叫\s*(\w+)", message)
        if name_match:
            self.user_info["name"] = name_match.group(1)
        
        age_match = re.search(r"(\d+)\s*岁", message)
        if age_match:
            self.user_info["age"] = int(age_match.group(1))
    
    def _identify_important_points(self, message):
        # 识别重要信息（简化实现）
        if "记住" in message or "重要" in message or "不要忘记" in message:
            self.important_points.append(message)
    
    def get_context_for_llm(self):
        """获取用于LLM的上下文"""
        context = ""
        
        # 添加用户信息
        if self.user_info:
            context += "用户信息:\n"
            for key, value in self.user_info.items():
                context += f"- {key}: {value}\n"
            context += "\n"
        
        # 添加重要点
        if self.important_points:
            context += "重要信息:\n"
            for point in self.important_points:
                context += f"- {point}\n"
            context += "\n"
        
        # 添加对话历史
        context += "对话历史:\n"
        for msg in self.messages:
            prefix = "用户: " if msg["role"] == "user" else "助手: "
            context += f"{prefix}{msg['content']}\n"
        
        return context
```

**步骤3：整合记忆系统到Agent**

```python
# 创建带记忆的Agent
from langchain.chains.conversation.memory import ConversationBufferWindowMemory

# 使用LangChain的窗口记忆
window_memory = ConversationBufferWindowMemory(
    k=5,  # 保留最近5轮对话
    return_messages=True,
    memory_key="chat_history"
)

# 创建工具
tools_with_memory = tools.copy()  # 使用之前定义的工具

# 创建记忆Agent的提示词
memory_prompt = """你是一个能够记住对话历史的智能助手。

可用工具:
{tools}

对话历史:
{chat_history}

请根据对话历史回答用户的问题。如果需要，可以使用工具获取更多信息。

用户问题: {input}

{agent_scratchpad}
"""

memory_prompt_template = CustomPromptTemplate(
    template=memory_prompt,
    tools=tools_with_memory,
    input_variables=["input", "chat_history", "intermediate_steps"]
)

memory_llm_chain = LLMChain(llm=llm, prompt=memory_prompt_template)
memory_agent = LLMSingleActionAgent(
    llm_chain=memory_llm_chain,
    output_parser=agent.agent.output_parser,
    stop=["\nObservation:"],
    allowed_tools=[tool.name for tool in tools_with_memory]
)

memory_agent_executor = AgentExecutor.from_agent_and_tools(
    agent=memory_agent,
    tools=tools_with_memory,
    memory=window_memory,
    verbose=True
)
```

**步骤4：测试记忆能力**

```python
# 开始对话
print("开始记忆测试对话：")

# 第一轮对话
first_input = "你好，我叫李明"
print(f"用户: {first_input}")
response = memory_agent_executor.run(first_input)
print(f"助手: {response}\n")

# 第二轮对话
second_input = "我想了解国家发展银行的情况"
print(f"用户: {second_input}")
response = memory_agent_executor.run(second_input)
print(f"助手: {response}\n")

# 第三轮对话 - 测试记忆能力
third_input = "你还记得我的名字吗？"
print(f"用户: {third_input}")
response = memory_agent_executor.run(third_input)
print(f"助手: {response}\n")
```

### 实践4：工具使用优化

在本实践中，我们将优化Agent使用工具的效率。

**步骤1：为Agent添加多种工具**

```python
# 定义更多工具
search_tool = Tool(
    name="网络搜索",
    func=lambda q: f"搜索结果: 关于'{q}'的信息...",
    description="用于在网络上搜索信息，适用于查找事实、新闻和一般知识"
)

calculator_tool = Tool(
    name="计算器",
    func=lambda exp: f"计算结果: {eval(exp)}",
    description="用于执行数学计算，支持基本运算如加减乘除、幂运算等"
)

weather_tool = Tool(
    name="天气查询",
    func=lambda loc: f"{loc}天气: 晴天，25°C，微风",
    description="查询指定位置的天气情况，包括温度、天气状况和风力等"
)

translator_tool = Tool(
    name="翻译助手",
    func=lambda text: f"翻译: {text} -> [翻译结果]",
    description="将文本从一种语言翻译成另一种语言，支持多种语言对"
)

# 创建工具集
advanced_tools = [search_tool, calculator_tool, weather_tool, translator_tool]
```

**步骤2：实现工具选择优化**

```python
class ToolSelectionOptimizer:
    def __init__(self, tools):
        self.tools = tools
        self.usage_stats = {tool.name: {"count": 0, "success_rate": 1.0} for tool in tools}
        self.tool_map = {tool.name: tool for tool in tools}
    
    def select_tools_for_task(self, task_description):
        """为特定任务选择最合适的工具"""
        relevant_tools = []
        
        # 关键词匹配（简化实现）
        keywords = {
            "搜索": ["搜索", "查找", "了解", "信息", "是什么"],
            "计算器": ["计算", "等于", "加", "减", "乘", "除", "数学"],
            "天气查询": ["天气", "温度", "下雨", "气候", "热", "冷"],
            "翻译助手": ["翻译", "中文", "英文", "语言"]
        }
        
        for tool_name, words in keywords.items():
            if any(word in task_description for word in words) and tool_name in self.tool_map:
                relevant_tools.append(self.tool_map[tool_name])
        
        # 如果没有匹配任何工具，返回搜索工具作为默认
        if not relevant_tools and "网络搜索" in self.tool_map:
            relevant_tools.append(self.tool_map["网络搜索"])
        
        return relevant_tools
    
    def update_stats(self, tool_name, success):
        """更新工具使用统计"""
        if tool_name in self.usage_stats:
            stats = self.usage_stats[tool_name]
            stats["count"] += 1
            
            # 更新成功率（加权平均）
            weight = min(0.1, 1.0 / stats["count"])  # 随使用次数增加权重减小
            new_success = 1.0 if success else 0.0
            stats["success_rate"] = stats["success_rate"] * (1 - weight) + new_success * weight
    
    def get_tool_recommendations(self):
        """获取工具推荐，基于使用频率和成功率"""
        recommendations = sorted(
            self.usage_stats.items(),
            key=lambda x: (x[1]["success_rate"], x[1]["count"]),
            reverse=True
        )
        return recommendations
```

**步骤3：创建具有工具优化的Agent**

```python
# 工具选择优化器
tool_optimizer = ToolSelectionOptimizer(advanced_tools)

# 自定义Agent类，整合工具选择优化
class ToolOptimizedAgent:
    def __init__(self, agent_executor, tool_optimizer):
        self.agent = agent_executor
        self.tool_optimizer = tool_optimizer
    
    def run(self, input_text):
        # 为任务选择最佳工具
        selected_tools = self.tool_optimizer.select_tools_for_task(input_text)
        
        # 动态更新Agent的工具集
        self.agent.tools = selected_tools
        
        # 记录工具选择
        selected_tool_names = [tool.name for tool in selected_tools]
        print(f"为任务选择的工具: {selected_tool_names}")
        
        # 执行Agent
        try:
            result = self.agent.run(input_text)
            
            # 假设使用了第一个工具，并且成功
            if selected_tools:
                self.tool_optimizer.update_stats(selected_tools[0].name, True)
                
            return result
        except Exception as e:
            # 更新失败统计
            if selected_tools:
                self.tool_optimizer.update_stats(selected_tools[0].name, False)
            
            return f"执行错误: {str(e)}"

# 创建优化的Agent执行器
tool_optimized_agent_executor = AgentExecutor.from_agent_and_tools(
    agent=memory_agent,  # 使用之前的记忆Agent
    tools=advanced_tools,
    verbose=True
)

# 创建最终的优化Agent
optimized_agent = ToolOptimizedAgent(tool_optimized_agent_executor, tool_optimizer)
```

**步骤4：测试工具优化效果**

```python
# 测试案例
tool_test_cases = [
    "巴黎的埃菲尔铁塔有多高？",
    "计算123乘以456的结果",
    "北京明天的天气怎么样？",
    "把'你好，世界'翻译成英语"
]

# 执行测试
for test in tool_test_cases:
    print(f"\n用户: {test}")
    response = optimized_agent.run(test)
    print(f"助手: {response}")

# 查看工具使用统计
print("\n工具使用统计:")
recommendations = tool_optimizer.get_tool_recommendations()
for tool_name, stats in recommendations:
    print(f"{tool_name}: 使用次数 {stats['count']}, 成功率 {stats['success_rate']:.2f}")
```

## 📝 自测问题

完成学习后，回答以下问题以检验你的理解：

1. Agent性能评估的主要指标包括哪些方面？
2. 什么是A/B测试，它如何应用于Agent优化？
3. 优化系统提示词的三个关键方面是什么？
4. Agent记忆系统通常包括哪几种类型的记忆？它们各自的作用是什么？
5. 如何有效管理长对话历史以适应Token限制？
6. 专业领域Agent定制的主要步骤有哪些？
7. 提高Agent工具使用效率的三种方法是什么？
8. 为什么需要为Agent设计安全与伦理控制机制？常见的方法有哪些？
9. 如何评估Agent优化的效果？需要关注哪些变化？
10. Agent在处理不确定性时应采取什么策略？

### 参考答案

1. **Agent性能评估的主要指标**：
   - 任务完成度指标：成功率、准确性、完整性、质量评分
   - 效率指标：响应时间、任务完成时间、交互次数、资源消耗（Token使用量、API调用次数）
   - 用户体验指标：满意度评分、易用性、有用性、信任度
   - 专业能力指标：专业准确性、推理能力、创新能力、适应性

2. **A/B测试及其应用**：
   A/B测试是通过比较两个或多个版本的Agent在相同条件下的表现，确定哪种配置更有效的方法。在Agent优化中，它可用于测试不同的提示词策略、比较不同的记忆机制、评估不同的工具组合、验证新功能的效果等。关键是确保测试条件相同，只变更一个要素，并进行统计显著性分析。

3. **优化系统提示词的三个关键方面**：
   - 角色定义精确化：明确Agent的专业身份、经验水平和专长领域
   - 指令结构优化：使用分步骤、结构化的指令提高行为一致性
   - 约束条件明确化：设置清晰的行为边界、输出规范和知识限制

4. **Agent记忆系统类型及作用**：
   - 工作记忆（短期/即时）：存储当前任务状态、临时推理结果、注意力焦点等
   - 情景记忆（会话级别）：保存对话历史、用户偏好、交互模式等
   - 长期记忆（持久知识）：存储领域知识、过往经验、规则流程等
   这三种记忆协同工作，分别管理不同时间跨度和重要性的信息。

5. **管理长对话历史的方法**：
   - 对话历史压缩：将早期对话生成摘要替换原始内容
   - 重要信息提取：识别并保留关键信息，丢弃次要内容
   - 上下文窗口控制：动态调整保留的上下文长度
   - 分层记忆管理：将频繁使用的信息保留在即时记忆，其他内容存储在外部

6. **专业领域Agent定制的主要步骤**：
   - 领域知识注入：添加专业术语、领域规则、参考资源
   - 行为模式定制：调整语言风格、推理路径、专业判断标准
   - 专用工具集成：配置领域API、专业分析工具、数据源
   - 测试与反馈：使用领域专家验证、在真实场景测试、迭代改进

7. **提高Agent工具使用效率的三种方法**：
   - 工具选择与组合优化：分析工具功能、设计最佳组合策略、处理工具依赖
   - 参数传递优化：从上下文提取参数、去除冗余参数、格式化参数值
   - 结果缓存策略：缓存重复调用结果、实现并行调用、优化工具描述

8. **Agent安全与伦理控制机制**：
   需要设计这些机制是因为Agent可能面临各种安全和伦理风险，如隐私泄露、有害内容、偏见放大等。常见方法包括：
   - 输入过滤机制：识别并过滤敏感内容、有害指令等
   - 输出审查机制：检查输出内容的安全性，缓解潜在问题
   - 行为边界设定：明确定义允许和禁止的行为
   - 隐私保护措施：对敏感信息进行脱敏处理

9. **评估Agent优化效果**：
   应关注以下变化：
   - 性能指标改进：响应时间、任务完成率、准确性的提升
   - 资源利用变化：Token消耗、API调用次数的减少
   - 用户体验提升：满意度、易用性、交互轮次的改进
   - 错误率降低：失败案例减少、边缘情况处理改善
   - 专业能力提升：领域准确性、推理质量的增强

10. **Agent处理不确定性的策略**：
    - 透明沟通：明确表达不确定程度，避免虚假自信
    - 主动澄清：识别不明确的问题部分，请求用户提供更多信息
    - 备选方案提供：提供多个可能答案并解释依据
    - 概率表述：使用概率语言表达不同可能性
    - 信息来源引用：引用信息源，让用户自行判断可靠性

## 📚 拓展资源

### 学术论文

1. **[ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629)**
   - 发表于2022年，介绍了将推理与行动结合的Agent框架
   - 提供了Agent思维链与工具使用的理论基础

2. **[Toolformer: Language Models Can Teach Themselves to Use Tools](https://arxiv.org/abs/2302.04761)**
   - 发表于2023年，探讨语言模型自主学习使用工具的能力
   - 提供了自动工具选择和调用的技术实现

3. **[Evaluating and Improving Tool-Augmented Computation-Intensive Reasoning](https://arxiv.org/abs/2310.00749)**
   - 专注于如何评估和提升Agent的推理能力
   - 提供了一套系统化的Agent评估方法论

### 视频教程

1. **[如何优化GPT提示词框架](https://www.youtube.com/watch?v=H4YK_7MAckk)**
   - Andrew Ng和OpenAI合作的提示词优化教程 (此为DeepLearning.AI系列课程介绍，建议查看完整播放列表或相关视频)
   - 详细讲解了提示词工程的最佳实践

2. **[Harrison Chase - Agents Masterclass from LangChain](https://www.youtube.com/watch?v=DWUdGhRrv2c)**
   - 由LangChain创始人Harrison Chase主讲
   - 介绍如何构建生产级别的AI Agent

3. **[Anthropic's Blueprint for Building Lean, Powerful AI Agents](https://www.youtube.com/watch?v=JEERoZQbG9k)**
   - 由AnthropicAI工程师主讲
   - 详细介绍Agent系统从原型到生产的全流程

4. **[AutoGen Agents with Unlimited Memory Using MemGPT (Tutorial)](https://www.youtube.com/watch?v=VJ6bK81meu8)**
   - 专注于Agent记忆管理的技术讲解 (此视频以AutoGen和MemGPT为例)
   - 包含实际代码实现和案例分析

### 工具与框架

1. **[LangChain](https://github.com/langchain-ai/langchain)**
   - 功能全面的AI应用开发框架
   - 提供了丰富的Agent组件和评估工具

2. **[LlamaIndex](https://github.com/jerryjliu/llama_index)**
   - 专注于知识检索和管理的框架
   - 适合构建有记忆和知识库的Agent

3. **[Ragas](https://github.com/explodinggradients/ragas)**
   - 专门用于评估和基准测试RAG系统的工具
   - 可用于Agent相关组件的性能测试

4. **[LangSmith](https://smith.langchain.com/)**
   - LangChain推出的评估和监控平台
   - 提供Agent行为追踪和性能分析

5. **[MemGPT](https://github.com/cpacker/MemGPT)**
   - 专注于长期记忆管理的Agent框架
   - 实现了高效的上下文压缩和检索

### 在线课程与教程

1. **[Prompt Engineering for ChatGPT](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/)**
   - DeepLearning.AI课程，完全免费
   - 提供提示词优化的系统知识

2. **[LangChain for LLM Application Development](https://www.deeplearning.ai/short-courses/langchain-for-llm-application-development/)**
   - 快速入门LangChain的免费课程
   - 包含Agent构建实践

3. **[Building Systems with the ChatGPT API](https://www.deeplearning.ai/short-courses/building-systems-with-chatgpt/)**
   - 介绍如何构建基于ChatGPT的系统
   - 包含评估和优化部分

4. **[Function Calling and Agents with LangChain](https://learn.deeplearning.ai/functions-tools-agents-langchain/lesson/1/introduction)**
   - 专注于函数调用和Agent开发
   - 提供详细的代码示例

### 博客与文章

1. **[Agent-Based LLM Architectures](https://eugeneyan.com/writing/llm-patterns/#agents-to-orchestrate-action)**
   - Eugene Yan的权威博客
   - 全面综述Agent架构模式和优化策略

2. **[Building, Testing, and Improving LLM Agents](https://www.promptingguide.ai/research/agents)**
   - PromptingGuide网站的Agent指南
   - 提供系统化的Agent构建方法

3. **[How to evaluate LLMs for production](https://www.surgehq.ai/blog/evaluating-llms-for-production)**
   - 关于LLM评估的详细指南
   - 适用于Agent性能评估

4. **[Emerging Architectures for LLM Applications](https://a16z.com/emerging-architectures-for-llm-applications/)**
   - a16z发布的LLM应用架构综述
   - 包含对Agent架构的分析

## 📝 作业与思考题

### 基础作业

1. **Agent性能分析报告**
   选择一个现有的AI Agent（可以是课程中的示例或公开的项目），对其性能进行分析，并撰写一份评估报告。报告应包含：
   - 至少3种评估指标的具体数据
   - 识别出的2-3个主要性能瓶颈
   - 明确的优化建议和预期效果

2. **提示词优化实验**
   设计一个提示词优化实验，对同一任务使用3种不同的系统提示词，并比较效果差异：
   - 创建基准版、优化版A和优化版B的系统提示词
   - 使用相同的5个测试用例评估三个版本
   - 记录并分析性能差异，总结最有效的提示策略

3. **记忆系统设计**
   为特定类型的Agent（如长期个人助手）设计一个适合的记忆系统，包括：
   - 记忆架构图（包含短期、会话和长期记忆组件）
   - 详细说明各组件的数据结构和存储内容
   - 描述记忆更新和检索的机制和算法
   - 提供示例代码实现关键功能

### 进阶作业

4. **专业领域Agent定制**
   选择一个专业领域（如医疗、法律、金融、教育等），将通用Agent改造成该领域的专家Agent：
   - 收集并组织至少30条领域专业知识
   - 设计专业化的系统提示词
   - 实现领域特定的工具接口（可以模拟实现）
   - 通过10个专业问题测试并评估效果
   - 撰写领域Agent的优化报告

5. **Agent自动化测试框架实现**
   设计并实现一个自动化测试框架，用于评估和优化AI Agent：
   - 创建多个测试用例集，覆盖不同能力和场景
   - 实现自动执行测试并收集性能指标的功能
   - 提供测试结果可视化和报告生成功能
   - 支持A/B测试比较不同Agent配置
   - 包含自动识别问题并提出优化建议的功能

### 思考题

1. Agent优化过程中如何平衡通用性和专业性？过度专业化会带来什么问题，如何避免？

2. 随着Agent变得更加复杂和自主，可能会出现哪些安全和伦理风险？作为开发者，应该如何负责任地设计和部署Agent系统？

3. 当Agent使用多个LLM模型协作时（如不同层次或不同功能的模型组合），会出现哪些特殊的优化挑战？如何解决这些挑战？

4. Agent系统的可解释性对用户信任有何影响？如何在保持高性能的同时提高Agent决策和行为的可解释性？

5. 未来五年内，Agent技术可能会如何发展？这些发展会如何改变当前的Agent优化方法和最佳实践？

## 🔮 明日预告

明天我们将进入课程的第三阶段，开始探索MCP（Multi-agent Collaborative Programming，多智能体协作编程）技术。我们将从MCP的基本概念、核心原理和技术基础开始，了解这一革命性的开发范式如何提升AI辅助编程的效率和质量。

准备好你的编程环境，我们将在实践中体验多智能体系统如何协同工作，共同完成复杂的编程任务！


---

> [点击链接加入群聊【Aries - AIGC自学交流群】：https://qm.qq.com/q/q88ZpofKLY](https://qm.qq.com/q/q88ZpofKLY) 