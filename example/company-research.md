设计用于市场调研的 Agent Skill，关键在于将宽泛的“调研”拆解为可以被大语言模型和外部工具（如爬虫、API）稳定执行的具体动作。

针对大型装备制造、跨国工程项目以及B2B工业营销的场景，这里为您设计了四个高价值的专属市场调研 Agent Skill 框架。您可以直接将这些逻辑转化为 OpenAPI Schema 或 Python 脚本供 Agent 调用。

### 1. 展会情报与竞品雷达 (Exhibition & Competitor Radar)

这个 Skill 专门用于在行业大型展会（如 Hannover Messe、Chinaplas 等）开展前，系统性地摸排竞争对手的动向。

* **核心功能**：自动检索特定工业展会的参展商名录，定向抓取核心竞品的最新发布（新闻稿、官网新品页面）。
* **输入参数 (`Input`)**：
* `exhibition_name` (string): 展会名称及年份。
* `competitor_domains` (array): 竞品公司的官网域名列表。


* **输出结果 (`Output`)**：
* 竞品此次参展的核心主题与视觉 Slogan。
* 主推的新产品线（例如，除了传统的重型自动扶梯外，是否开始推介电梯产品或新能源解决方案）。
* 展位面积估算与馆内位置优势分析。


* **适用场景**：用于指导己方展位布局规划、视觉物料设计以及制定展会现场的话术对策。

### 2. B2B 工业招标与项目追踪 (B2B Project Tender Scraper)

在工业工程和合同制造领域，公开的招投标和项目环评信息是极具价值的商业线索。

* **核心功能**：监控特定工业领域（如核电站设施改造、大型机电安装）的全球或区域性公开项目信息。
* **输入参数 (`Input`)**：
* `industry_keywords` (array): 行业关键词（如 nuclear power plant engineering, contract manufacturing）。
* `region` (string): 目标区域（如欧洲、东南亚、华南）。


* **输出结果 (`Output`)**：
* 近期发布的潜在招标项目列表及预算估值。
* 项目背后的潜在总包方及关键时间节点（如现场审计时间、交付时间）。


* **适用场景**：辅助销售和商务团队提前介入重大工程项目，规划资源并安排技术团队的现场干预与审计计划。

### 3. 目标客户商业画像透视 (Target Client Deep-Dive Profiler)

B2B 的商务合作与接待需要极高的定制化，这个 Skill 用于在与重要外宾（如海外商务伙伴）会面前生成深度简报。

* **核心功能**：聚合目标企业的财务年报摘要、近期媒体报道、现有的供应链生态以及核心高管的公开言论。
* **输入参数 (`Input`)**：
* `company_name` (string): 目标客户或合作伙伴公司名称。
* `focus_areas` (array): 关注点（如供应链转移、新工厂建设、可持续发展等）。


* **输出结果 (`Output`)**：
* 客户近期的业务痛点与战略调整方向。
* 现有供应商矩阵的潜在缺口。
* 定制化的合作切入点及商务接待中的建议交流话题。


* **适用场景**：跨国商务接待筹备、高层谈判前的背景尽调。

### 4. 行业趋势与宏观政策提炼总结 (Macro Trend & Policy Summarizer)

市场调研不仅需要盯紧对手和客户，还需要对宏观的技术迭代和政策壁垒保持敏感。

* **核心功能**：检索并提炼权威工业研报、进出口关税政策变化及行业技术标准更新。
* **输入参数 (`Input`)**：
* `tech_domain` (string): 技术与业务领域。
* `time_frame` (string): 回溯时间范围（如 "past 3 months"）。


* **输出结果 (`Output`)**：
* 政策与关税壁垒预警（特别是针对跨国制造与出口）。
* 技术趋势总结。
* 自动生成的“市场洞察段落”，可直接嵌入到商业企划书或用于向管理层汇报的 PPT 中。



---

**技术实现建议**

如果您使用代码来定义这些 Skill，以“展会竞品雷达”为例，它的 JSON Schema 描述可以这样设计：

```json
{
  "name": "analyze_competitor_exhibition_strategy",
  "description": "分析特定竞争对手在即将到来的工业展会上的参展策略和新产品动向。",
  "parameters": {
    "type": "object",
    "properties": {
      "exhibition_name": {
        "type": "string",
        "description": "例如：Hannover Messe 2026"
      },
      "competitor_url": {
        "type": "string",
        "description": "竞争对手的官网或新闻中心链接"
      }
    },
    "required": ["exhibition_name", "competitor_url"]
  }
}

```

您目前打算将这些市场调研 Skill 接入到具体的业务流中（比如自动生成展会策划案，还是常规的竞品监控日报）？我们可以进一步探讨具体的工作流设计。
