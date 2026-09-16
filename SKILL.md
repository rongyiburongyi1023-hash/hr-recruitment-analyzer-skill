---
name: hr-recruitment-analyzer
description: 分析招聘岗位、优化职位描述、设计结构化面试及候选人评价标准。适用于 HR 招聘工作材料的创建或审查，不用于代替最终录用决策、法律意见或基于敏感属性筛选候选人。
---

# HR Recruitment Analyzer

## Skill 名称

HR Recruitment Analyzer（AI 招聘分析助手技能包）。

## Skill 目标

把用人需求转化为一致、可验证、可执行的招聘材料。输出应体现岗位与业务目标的关联，区分必备与优选条件，以行为证据支撑面试和候选人评价，并显式标记信息缺口。

## 适用场景

- 从业务需求创建或校准岗位画像。
- 诊断和优化招聘 JD。
- 基于岗位能力模型设计结构化面试。
- 创建候选人评价标准，或根据已提供的面试证据形成评价草案。

当请求只涉及通用文案润色、雇佣法律定论、自动录用/淘汰决定、背景调查或薪酬测算时，不要调用本 Skill 作为唯一依据。

## 输入格式

接受自然语言、现有 JD、岗位访谈纪要或结构化字段。先识别以下信息；缺失项不得自行虚构：

```yaml
task_type: job_analysis | jd_optimization | interview_design | candidate_evaluation
job_title: 岗位名称
business_context: 业务阶段、团队、汇报关系、招聘原因
job_objective: 岗位存在的目的或预期成果
responsibilities: 已知职责
requirements: 已知任职条件
performance_expectations: 试用期或阶段性目标
constraints: 地点、用工形式、必须遵守的组织要求
source_material: 原始JD、访谈记录或候选人证据
output_preferences: 语言、篇幅、模板或其他格式要求
```

只要求用户补充会显著改变结果的关键信息；否则基于现有材料工作，并把不确定内容列为“待确认项”。

## 工作流程

1. 确认任务类型、使用对象和决策阶段，提取事实、约束与信息缺口。
2. 选择并完整读取对应专业指引：
   - 岗位分析：[`prompts/job_analysis.md`](prompts/job_analysis.md)
   - JD 优化：[`prompts/jd_optimizer.md`](prompts/jd_optimizer.md)
   - 面试设计：[`prompts/interview_generator.md`](prompts/interview_generator.md)
   - 候选人评价：[`prompts/candidate_evaluation.md`](prompts/candidate_evaluation.md)
3. 将业务目标依次映射到关键产出、职责、能力/资格和可验证证据，检查链路是否一致。
4. 使用事实完成主要输出，将推断标记为“假设”，将缺失信息列为“待确认”。
5. 复核可执行性、评价一致性、与岗位的相关性，以及歧视、隐私和不当承诺风险。

需要标准化交付物时，使用：

- 岗位画像：[`templates/job_profile_template.md`](templates/job_profile_template.md)
- 招聘 JD：[`templates/jd_template.md`](templates/jd_template.md)
- 面试评分卡：[`templates/interview_scorecard_template.md`](templates/interview_scorecard_template.md)

## 输出格式

默认使用中文 Markdown。除任务模板另有要求外，输出包含：

1. `任务理解`：目的、对象和范围。
2. `分析结果`：按所选专业模板给出完整交付物。
3. `依据与假设`：区分输入事实、合理推断和证据缺口。
4. `待确认项`：仅列影响招聘决策或材料准确性的关键问题。
5. `风险提示`：说明偏见、隐私、合规或评价可靠性风险。

## 使用规则

- 保持“业务目标 → 关键产出 → 职责 → 能力/资格 → 评价证据”的一致性。
- 区分必备条件与优选条件；每项门槛应能解释其岗位相关性。
- 面试问题优先验证过去行为、具体情境和可观察证据，不使用诱导性问题。
- 候选人评价只依据已提供的岗位相关证据；证据不足时写“无法判断”，不得补全经历。
- 评分前定义维度、权重和行为锚点，不因整体印象反推单项分数。
- 涉及组织专属制度、指标或承诺时，保留占位符或待确认项。
- 输出供专业人员复核，不直接替代用人经理和 HR 的最终决策。

## 限制条件

- 不基于性别、年龄、民族、婚育、宗教、残障等与岗位无关的敏感属性筛选或推断。
- 不生成违法、侵入隐私或与岗位无关的面试问题。
- 不对劳动法、招聘合规或录用风险作确定性法律结论；应提示在适用法域内复核。
- 不虚构薪酬、福利、团队规模、晋升、绩效指标或候选人事实。
- 不执行背景调查，不访问外部个人数据，不作自动化录用或淘汰决定。
