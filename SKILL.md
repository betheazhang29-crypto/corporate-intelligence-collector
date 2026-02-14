---
name: corporate-intelligence-collector
description: 企业情报采集专家。从10+公开渠道采集企业全方位信息，包括工商信息、财务数据、行业数据、风险信息、市场情报。支持Browser自动化、深度搜索、文档解析等多种工具策略。适用于企业尽职调查、信用评估、投资分析等场景。
version: 1.0.0
author: Manus AI
created: 2026-02-14
updated: 2026-02-14
tools: Browser, Search, File, Shell
model: sonnet
category: business
color: blue
displayName: 企业情报采集专家
---

# 企业情报采集专家

## 技能概述

专业的企业情报采集技能，支持从10+公开渠道自动采集企业全方位信息。使用Browser自动化、深度搜索、文档解析等多种工具策略，实现高效、准确、全面的企业情报采集。

### 核心价值

企业尽职调查、信用评估、投资分析等场景都需要全面的企业信息。传统人工采集需要2-3天，且容易遗漏关键信息。本技能将这一过程缩短到10-60分钟，并提供标准化的数据输出。

### 主要功能

1. **多源数据采集**：从10+公开渠道采集企业信息
2. **智能工具选择**：根据数据源特点自动选择最佳工具策略
3. **并行采集**：同时启动多个采集任务，提高效率
4. **证据保存**：自动保存截图和原始文档作为证据
5. **标准化输出**：生成结构化JSON数据，便于后续分析

### 适用场景

- 银行授信尽职调查
- 企业信用评估
- 投资尽职调查
- 供应商背景调查
- 竞争对手分析
- 企业风险监控

---

## 核心工作流程

### 决策树（优先执行）

```
任务分析
|-- 只需要基础工商信息？ -> 快速核查模式（5-10分钟）
|-- 需要完整企业信息？ -> 标准采集模式（15-30分钟）
+-- 需要深度调查？ -> 深度调查模式（30-60分钟）

工具选择
|-- 需要交互的网站（企查查、裁判文书网）？ -> Browser
|-- 公开搜索信息（新闻、报告）？ -> Search
|-- 需要解析文档（PDF、Excel）？ -> File
+-- 批量数据处理？ -> Shell + Python脚本

采集策略
|-- 并行采集：同时启动6个采集任务
|-- 证据保存：自动保存截图和文档
+-- 质量检查：验证数据完整性
```

---

## 工作模式

### 模式A：快速核查（Quick Verification）

**适用场景**：只需要基础工商信息和风险信息

**时间**：5-10分钟
**工具调用**：5-10次
**数据源**：3-5个核心渠道

**采集内容**：
- 企业基本信息（企查查/天眼查）
- 工商登记信息（国家企业信用信息公示系统）
- 基础风险信息（涉诉、被执行人）

**输出**：
- `intelligence_data.json`（基础版）
- `screenshots/`（关键截图）
- `collection_report.md`（简要报告）

---

### 模式B：标准采集（Standard Collection）**[默认]**

**适用场景**：完整的企业尽职调查

**时间**：15-30分钟
**工具调用**：15-25次
**数据源**：8-10个渠道

**采集内容**：
- 企业基本信息（工商、股权、管理层）
- 财务数据（年报、财务报表）
- 行业数据（行业报告、市场数据）
- 风险信息（涉诉、执行、处罚、舆情）
- 市场情报（官网、产品、竞争对手）

**输出**：
- `intelligence_data.json`（完整版）
- `screenshots/`（所有截图）
- `documents/`（原始文档）
- `collection_report.md`（详细报告）

---

### 模式C：深度调查（Deep Investigation）

**适用场景**：高风险企业的深度背景调查

**时间**：30-60分钟
**工具调用**：30-50次
**数据源**：10+渠道 + 并行代理

**采集内容**：
- 标准采集的所有内容
- 关联企业深度调查
- 管理层背景深度调查
- 历史舆情深度挖掘
- 行业专家访谈（如需要）

**输出**：
- `intelligence_data.json`（深度版）
- `screenshots/`（完整截图）
- `documents/`（所有文档）
- `related_companies/`（关联企业数据）
- `collection_report.md`（深度报告）

---

## 数据源与工具策略

### 1. 企查查/天眼查（工商信息）

**数据内容**：
- 企业基本信息（名称、法人、注册资本、成立日期、经营范围）
- 股权结构（股东信息、持股比例、实际控制人）
- 对外投资（投资企业、投资金额）
- 管理层信息（高管姓名、职位）
- 分支机构
- 变更记录

**工具策略**：Browser
```
1. 导航到 qcc.com 或 tianyancha.com
2. 搜索企业名称或统一社会信用代码
3. 提取企业基本信息
4. 提取股权结构
5. 提取对外投资
6. 保存截图作为证据
```

**输出字段**：
- `company_basic`
- `shareholders`
- `investments`
- `management`
- `branches`

---

### 2. 国家企业信用信息公示系统

**数据内容**：
- 营业执照信息
- 年报信息
- 行政许可
- 行政处罚
- 经营异常
- 严重违法失信

**工具策略**：Browser
```
1. 访问 gsxt.gov.cn
2. 搜索统一社会信用代码
3. 提取营业执照信息
4. 提取年报信息
5. 提取行政许可和处罚
6. 保存截图
```

**输出字段**：
- `company_basic`（补充）
- `annual_reports`
- `licenses`
- `penalties`

---

### 3. 上市公司年报（交易所网站）

**数据内容**：
- 年度报告PDF
- 季度报告PDF
- 财务数据（资产负债表、利润表、现金流量表）

**工具策略**：Browser + File
```
1. 判断是否为上市公司（股票代码）
2. Browser：访问上交所/深交所
3. Browser：搜索股票代码，下载年报PDF
4. File：解析PDF，提取财务数据
5. 使用 pdfplumber 提取表格数据
```

**输出字段**：
- `financial_data.balance_sheet`
- `financial_data.income_statement`
- `financial_data.cash_flow`
- `documents/annual_report_2023.pdf`

---

### 4. 非上市公司财务报表

**数据内容**：
- 资产负债表
- 利润表
- 现金流量表

**工具策略**：File
```
1. 引导用户上传财务报表（Excel或PDF格式）
2. File：解析Excel（openpyxl）或PDF（pdfplumber）
3. 识别三大报表
4. 提取财务数据
5. 标准化数据格式
```

**输出字段**：
- `financial_data.balance_sheet`
- `financial_data.income_statement`
- `financial_data.cash_flow`

---

### 5. 行业研究报告

**数据内容**：
- 行业概况
- 市场规模
- 竞争格局
- 发展趋势

**工具策略**：Search + Browser + File
```
1. Search：搜索行业研究报告
   - "【行业名称】 行业研究报告 IDC"
   - "【行业名称】 市场分析 艾瑞咨询"
2. Browser：访问报告网站，下载PDF
3. File：解析PDF，提取关键数据
4. 整理成结构化数据
```

**输出字段**：
- `industry_data.market_size`
- `industry_data.competition`
- `industry_data.trends`
- `documents/industry_report_*.pdf`

---

### 6. 裁判文书网（涉诉信息）

**数据内容**：
- 案件信息
- 案由
- 判决结果
- 涉案金额

**工具策略**：Browser
```
1. 访问 wenshu.court.gov.cn
2. 搜索企业名称
3. 提取案件列表
4. 提取每个案件的详细信息
5. 保存截图
```

**输出字段**：
- `risk_data.litigation`
- `screenshots/wenshu_*.png`

---

### 7. 执行信息公开网（被执行人信息）

**数据内容**：
- 被执行人信息
- 执行金额
- 执行法院
- 执行状态

**工具策略**：Browser
```
1. 访问 zxgk.court.gov.cn
2. 搜索企业名称
3. 提取被执行人信息
4. 保存截图
```

**输出字段**：
- `risk_data.enforcement`
- `screenshots/zxgk_*.png`

---

### 8. 企业官网

**数据内容**：
- 企业介绍
- 产品/服务信息
- 发展历程
- 企业文化
- 联系方式

**工具策略**：Search + Browser
```
1. Search：搜索企业官网地址
2. Browser：访问官网
3. 提取企业介绍、产品信息
4. 保存首页截图和关键页面截图
```

**输出字段**：
- `market_intelligence.website_info`
- `market_intelligence.products`
- `screenshots/website_*.png`

---

### 9. 新闻舆情

**数据内容**：
- 企业相关新闻（近1年）
- 负面新闻
- 重大事件

**工具策略**：Search
```
1. 搜索企业相关新闻
   - "【企业名称】 新闻"
   - "【企业名称】 负面"
   - "【企业名称】 事件"
2. 识别负面新闻关键词
3. 提取关键信息
```

**输出字段**：
- `risk_data.negative_news`

---

### 10. 竞争对手信息

**数据内容**：
- 同行业企业
- 市场份额
- 产品对比

**工具策略**：Search + Browser
```
1. Search：搜索同行业企业
2. Browser：访问竞争对手官网
3. 提取产品、优势信息
4. 对比分析
```

**输出字段**：
- `market_intelligence.competitors`

---

## 并行采集策略

为了提高效率，采用并行采集策略：

### 并行任务分组

**任务组1：企业基础信息**（同时启动）
- 任务1-1：企查查/天眼查（Browser）
- 任务1-2：国家企业信用信息公示系统（Browser）

**任务组2：财务数据**（同时启动）
- 任务2-1：上市公司年报（Browser + File）
- 任务2-2：非上市公司财报（File，如用户提供）

**任务组3：行业数据**（同时启动）
- 任务3-1：行业研究报告（Search + Browser + File）
- 任务3-2：竞争对手信息（Search + Browser）

**任务组4：风险数据**（同时启动）
- 任务4-1：裁判文书网（Browser）
- 任务4-2：执行信息公开网（Browser）
- 任务4-3：新闻舆情（Search）

**任务组5：市场情报**（同时启动）
- 任务5-1：企业官网（Search + Browser）

### 并行执行流程

```
初始化（1-2分钟）
  ↓
启动任务组1（3-5分钟）
  ↓
启动任务组2（5-10分钟）
  ↓
启动任务组3（5-10分钟）
  ↓
启动任务组4（5-10分钟）
  ↓
启动任务组5（2-5分钟）
  ↓
数据整合（2-5分钟）
  ↓
质量检查（1-2分钟）
  ↓
生成报告（1-2分钟）
```

---

## 输出标准

### 主数据文件：intelligence_data.json

```json
{
  "metadata": {
    "company_name": "珠海金智维人工智能股份有限公司",
    "credit_code": "91440400MA4UKDGM8E",
    "collection_date": "2026-02-14",
    "collection_mode": "standard",
    "data_completeness": 0.85,
    "collection_time_minutes": 25,
    "data_sources": [
      "企查查",
      "国家企业信用信息公示系统",
      "上交所",
      "裁判文书网",
      "执行信息公开网",
      "企业官网",
      "新闻搜索"
    ]
  },
  "company_basic": {
    "name": "珠海金智维人工智能股份有限公司",
    "credit_code": "91440400MA4UKDGM8E",
    "legal_representative": "张三",
    "registered_capital": "5000万元",
    "establishment_date": "2015-03-15",
    "business_scope": "人工智能技术开发...",
    "address": "珠海市香洲区...",
    "company_type": "股份有限公司",
    "status": "存续",
    "source": "企查查",
    "screenshot": "screenshots/qichacha_basic.png"
  },
  "shareholders": [
    {
      "name": "张三",
      "type": "自然人",
      "shareholding_ratio": "60%",
      "investment_amount": "3000万元"
    },
    {
      "name": "李四",
      "type": "自然人",
      "shareholding_ratio": "40%",
      "investment_amount": "2000万元"
    }
  ],
  "actual_controller": {
    "name": "张三",
    "control_ratio": "60%",
    "control_path": "直接持股"
  },
  "investments": [
    {
      "company_name": "珠海金智维科技有限公司",
      "investment_ratio": "100%",
      "investment_amount": "1000万元",
      "establishment_date": "2018-06-01"
    }
  ],
  "management": [
    {
      "name": "张三",
      "position": "董事长兼总经理",
      "background": "清华大学计算机硕士，10年AI行业经验"
    },
    {
      "name": "王五",
      "position": "技术总监",
      "background": "北京大学计算机博士，AI算法专家"
    }
  ],
  "branches": [],
  "annual_reports": [
    {
      "year": 2023,
      "revenue": "8000万元",
      "profit": "1200万元",
      "employees": 150,
      "source": "国家企业信用信息公示系统"
    }
  ],
  "licenses": [
    {
      "name": "软件企业认定证书",
      "issue_date": "2020-05-10",
      "valid_until": "2025-05-10"
    }
  ],
  "financial_data": {
    "source": "上交所年报",
    "year": 2023,
    "balance_sheet": [
      {
        "item": "资产总计",
        "2023": 50000000,
        "2022": 40000000,
        "2021": 30000000
      },
      {
        "item": "负债总计",
        "2023": 20000000,
        "2022": 15000000,
        "2021": 10000000
      },
      {
        "item": "所有者权益",
        "2023": 30000000,
        "2022": 25000000,
        "2021": 20000000
      }
    ],
    "income_statement": [
      {
        "item": "营业收入",
        "2023": 80000000,
        "2022": 60000000,
        "2021": 45000000
      },
      {
        "item": "营业成本",
        "2023": 48000000,
        "2022": 36000000,
        "2021": 27000000
      },
      {
        "item": "净利润",
        "2023": 12000000,
        "2022": 9000000,
        "2021": 6000000
      }
    ],
    "cash_flow": [
      {
        "item": "经营活动现金流",
        "2023": 15000000,
        "2022": 10000000,
        "2021": 7000000
      },
      {
        "item": "投资活动现金流",
        "2023": -5000000,
        "2022": -3000000,
        "2021": -2000000
      },
      {
        "item": "筹资活动现金流",
        "2023": 2000000,
        "2022": 5000000,
        "2021": 3000000
      }
    ],
    "files": ["documents/annual_report_2023.pdf"]
  },
  "industry_data": {
    "industry_name": "人工智能",
    "industry_code": "I65",
    "market_size": {
      "2023": "500亿元",
      "2022": "400亿元",
      "2021": "300亿元",
      "growth_rate": "25%"
    },
    "competition": {
      "top_companies": [
        "科大讯飞",
        "商汤科技",
        "旷视科技",
        "云从科技"
      ],
      "market_share_cr4": "40%"
    },
    "trends": [
      "大模型技术快速发展",
      "AI+行业应用深化",
      "政策支持力度加大"
    ],
    "source": "IDC中国人工智能市场研究报告2023",
    "files": ["documents/industry_report_ai_2023.pdf"]
  },
  "risk_data": {
    "litigation": [
      {
        "case_number": "（2023）粤0402民初1234号",
        "case_type": "合同纠纷",
        "plaintiff": "某某公司",
        "defendant": "珠海金智维人工智能股份有限公司",
        "amount": "50万元",
        "status": "已结案",
        "result": "调解结案",
        "date": "2023-05-15",
        "source": "裁判文书网",
        "screenshot": "screenshots/wenshu_case_1234.png"
      }
    ],
    "enforcement": [],
    "penalties": [],
    "tax_credit": {
      "level": "A级",
      "year": 2023,
      "source": "国家税务总局"
    },
    "negative_news": [
      {
        "title": "某某公司起诉金智维合同违约",
        "date": "2023-03-10",
        "source": "南方都市报",
        "url": "https://..."
      }
    ]
  },
  "market_intelligence": {
    "website_info": {
      "url": "https://www.jinzhiwei.com",
      "description": "专注于人工智能技术研发和应用",
      "products": [
        "智能客服系统",
        "智能语音识别",
        "智能图像识别"
      ],
      "screenshot": "screenshots/website_homepage.png"
    },
    "competitors": [
      {
        "name": "科大讯飞",
        "products": ["语音识别", "智能翻译"],
        "advantages": ["技术领先", "市场份额大"]
      },
      {
        "name": "商汤科技",
        "products": ["图像识别", "智能驾驶"],
        "advantages": ["算法先进", "融资能力强"]
      }
    ]
  },
  "evidence_files": {
    "screenshots": [
      "screenshots/qichacha_basic.png",
      "screenshots/gsxt_license.png",
      "screenshots/wenshu_case_1234.png",
      "screenshots/website_homepage.png"
    ],
    "documents": [
      "documents/annual_report_2023.pdf",
      "documents/industry_report_ai_2023.pdf"
    ]
  }
}
```

### 目录结构

```
/home/ubuntu/due_diligence/珠海金智维人工智能股份有限公司/
├── intelligence_data.json        # 主数据文件
├── collection_report.md          # 采集报告
├── screenshots/                  # 截图证据
│   ├── qichacha_basic.png
│   ├── gsxt_license.png
│   ├── wenshu_case_1234.png
│   └── website_homepage.png
├── documents/                    # 文档证据
│   ├── annual_report_2023.pdf
│   └── industry_report_ai_2023.pdf
└── logs/
    └── collection_log.txt        # 采集日志
```

### 采集报告：collection_report.md

```markdown
# 企业情报采集报告

## 基本信息

- **企业名称**：珠海金智维人工智能股份有限公司
- **统一社会信用代码**：91440400MA4UKDGM8E
- **采集日期**：2026-02-14
- **采集模式**：标准采集
- **采集时长**：25分钟

## 数据完整性

- **总体完整度**：85%
- **企业基本信息**：100%
- **财务数据**：90%
- **行业数据**：80%
- **风险数据**：85%
- **市场情报**：75%

## 数据源清单

1. 企查查 ✓
2. 国家企业信用信息公示系统 ✓
3. 上交所 ✓
4. 裁判文书网 ✓
5. 执行信息公开网 ✓
6. 企业官网 ✓
7. 新闻搜索 ✓
8. 行业研究报告 ✓

## 关键发现

### 企业基本情况
- 成立于2015年，注册资本5000万元
- 实际控制人为张三，持股60%
- 管理层背景优秀，技术实力强

### 财务状况
- 2023年营收8000万元，净利润1200万元
- 近三年营收和利润持续增长
- 经营现金流良好

### 风险情况
- 存在1起合同纠纷，已调解结案
- 无被执行人记录
- 无行政处罚记录
- 纳税信用等级A级

### 行业情况
- 所处人工智能行业，市场规模500亿元
- 行业增长率25%，前景良好
- 竞争激烈，需关注技术创新

## 缺失数据

- 部分行业数据需要付费报告
- 竞争对手详细财务数据未获取
- 管理层详细履历需进一步调查

## 建议

1. 补充获取付费行业研究报告
2. 深度调查管理层背景
3. 关注后续涉诉情况
4. 定期更新财务数据
```

---

## 质量保证

### 数据完整性检查

在采集完成后，自动执行以下检查：

```python
def check_data_completeness(data):
    """检查数据完整性"""
    completeness = {}
    
    # 企业基本信息（必需）
    required_basic = ['name', 'credit_code', 'legal_representative', 
                     'registered_capital', 'establishment_date']
    completeness['company_basic'] = check_fields(data['company_basic'], required_basic)
    
    # 财务数据（重要）
    if 'financial_data' in data:
        completeness['financial_data'] = 1.0
    else:
        completeness['financial_data'] = 0.0
    
    # 风险数据（重要）
    completeness['risk_data'] = check_risk_data(data['risk_data'])
    
    # 计算总体完整度
    total_completeness = sum(completeness.values()) / len(completeness)
    
    return total_completeness, completeness
```

### 数据质量标准

- **完整性**：必需字段完整度 > 90%
- **准确性**：数据来源明确，有截图证据
- **时效性**：数据采集日期明确
- **可追溯性**：保存原始文档和截图

---

## 使用方法

### 方法1：在 Manus 中直接调用（推荐）

```
使用 corporate-intelligence-collector 技能采集【珠海金智维】的企业信息
统一社会信用代码：91440400MA4UKDGM8E
```

Manus 会自动：
1. 从10+公开渠道采集数据
2. 并行执行采集任务
3. 保存截图和文档证据
4. 生成标准化JSON数据

### 方法2：指定采集模式

```
使用 corporate-intelligence-collector 技能以快速核查模式采集【某某公司】的基础信息
```

### 方法3：指定采集内容

```
使用 corporate-intelligence-collector 技能采集【某某公司】的财务数据和风险信息
```

---

## 核心脚本说明

### 1. company_info_collector.py - 企业基础信息采集

**功能**：从企查查/天眼查、国家企业信用信息公示系统采集企业基础信息

**主要方法**：
- `collect_from_qichacha(company_name)` - 从企查查采集
- `collect_from_tianyancha(company_name)` - 从天眼查采集
- `collect_from_gsxt(credit_code)` - 从国家企业信用信息公示系统采集
- `merge_company_info(data1, data2)` - 合并多源数据

### 2. financial_data_collector.py - 财务数据采集

**功能**：采集上市公司年报或解析用户上传的财务报表

**主要方法**：
- `is_listed_company(company_name)` - 判断是否为上市公司
- `download_annual_report(stock_code, year)` - 下载年报PDF
- `parse_financial_pdf(pdf_path)` - 解析PDF提取财务数据
- `parse_financial_excel(excel_path)` - 解析Excel提取财务数据

### 3. industry_data_collector.py - 行业数据采集

**功能**：采集行业研究报告和市场数据

**主要方法**：
- `search_industry_reports(industry_name)` - 搜索行业研究报告
- `download_industry_report(url)` - 下载行业报告
- `parse_industry_report(pdf_path)` - 解析行业报告
- `extract_market_data(report_data)` - 提取市场数据

### 4. risk_data_collector.py - 风险数据采集

**功能**：采集涉诉、被执行人、行政处罚等风险信息

**主要方法**：
- `collect_litigation(company_name)` - 采集涉诉信息
- `collect_enforcement(company_name)` - 采集被执行人信息
- `collect_penalties(company_name)` - 采集行政处罚信息
- `collect_negative_news(company_name)` - 采集负面新闻

### 5. market_intel_collector.py - 市场情报采集

**功能**：采集企业官网、产品、竞争对手信息

**主要方法**：
- `collect_website_info(company_name)` - 采集官网信息
- `collect_product_info(website_url)` - 采集产品信息
- `collect_competitor_info(industry_name)` - 采集竞争对手信息

---

## 最佳实践

### 1. 数据准备

- 提供完整的企业名称和统一社会信用代码
- 如有财务报表，准备好PDF或Excel格式
- 如需深度调查，准备好关联企业清单

### 2. 模式选择

- 快速核查：只需要基础工商信息和风险信息
- 标准采集：完整的企业尽职调查（推荐）
- 深度调查：高风险企业或重要投资决策

### 3. 数据验证

- 检查数据完整性报告
- 查看截图证据
- 对比多个数据源
- 标记不确定的数据

---

## 常见问题

### Q1: 采集需要多长时间？
A: 快速核查5-10分钟，标准采集15-30分钟，深度调查30-60分钟。

### Q2: 支持哪些类型的企业？
A: 支持所有类型的企业，包括上市公司、非上市公司、国有企业、民营企业等。

### Q3: 财务数据从哪里获取？
A: 上市公司从交易所网站自动下载，非上市公司需要用户提供财务报表。

### Q4: 数据的准确性如何保证？
A: 所有数据都标注来源，并保存截图和原始文档作为证据。

### Q5: 如果某些数据采集失败怎么办？
A: 系统会标记缺失的数据，并在采集报告中说明原因。用户可以手动补充或选择其他数据源。

---

## 技术支持

如有问题或建议，请联系：
- 邮箱：support@manus.im
- 网站：https://help.manus.im

---

## 版本历史

- **v1.0.0** (2026-02-14) - 初始版本，支持10+数据源，3种采集模式

---

## 许可证

Copyright © 2026 Manus AI. All rights reserved.
