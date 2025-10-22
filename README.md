# Data Agent 项目文档

## 项目概述

这是一个基于 LangGraph 构建的智能数据分析助手，专门用于处理数据库查询、数据分析和可视化任务。该项目集成了多种工具，能够自动执行 SQL 查询、Python 代码、数据提取和图表生成等功能。

## 技术栈

- **核心框架**: LangGraph + LangChain
- **语言模型**: DeepSeek Chat (通过 langchain-deepseek)
- **数据库**: MySQL (通过 pymysql)
- **数据处理**: pandas, numpy, scikit-learn
- **可视化**: matplotlib, seaborn
- **搜索工具**: TavilySearch
- **环境管理**: python-dotenv

## 项目结构

```
data_agent/
├── graph.py           # 主要的图定义和工具实现
├── requirements.txt   # Python 依赖列表
├── langgraph.json     # LangGraph 配置文件
├── .env              # 环境变量配置
├── .venv/            # Python 虚拟环境
└── IFLOW.md          # 项目文档
```

## 核心功能

### 1. 数据库查询工具 (`sql_inter`)
- 执行 SQL 查询语句并返回结果
- 自动连接到 MySQL 数据库
- 支持复杂查询和数据处理

### 2. 数据提取工具 (`extract_data`)
- 从 MySQL 数据库提取数据表到 pandas DataFrame
- 将数据保存为全局变量供后续分析使用

### 3. Python 代码执行工具 (`python_inter`)
- 执行非绘图类的 Python 代码
- 支持数据处理、计算和变量操作

### 4. 可视化工具 (`fig_inter`)
- 执行绘图代码并生成图像
- 自动保存图像到指定目录
- 支持 matplotlib 和 seaborn

### 5. 搜索工具 (`search_tool`)
- 基于 Tavily 的网络搜索功能
- 用于获取实时信息和外部数据

### 6. 人工协助工具 (`human_assistance`)
- 支持人在环路的交互
- 在需要人工干预时请求帮助

## 环境配置

在 `.env` 文件中配置以下变量：

```env
DEEPSEEK_API_KEY=your_api_key
LANGSMITH_TRACING=True
LANGSMITH_API_KEY=your_api_key
LANGSMITH_PROJECT=Agent1
TAVILY_API_KEY=your_api_key
HOST=localhost
PORT=3306
USER=root
MYSQL_PW=root
DB_NAME=langgraph_agent
```

## 安装和运行

### 1. 创建虚拟环境
```bash
python -m venv .venv
source .venv/bin/activate  # Linux/Mac
.venv\Scripts\activate     # Windows
```

### 2. 安装依赖
```bash
pip install -r requirements.txt
```

### 3. 配置环境变量
复制 `.env` 文件并填入正确的 API 密钥和数据库连接信息

### 4. 运行项目
```bash
langgraph dev
```

## 使用说明

### 数据库查询
```
用户: 查询用户表中的所有数据
助手: [调用 sql_inter 工具执行 SELECT * FROM users]
```

### 数据分析
```
用户: 分析用户年龄分布情况
助手: [调用 extract_data 提取数据] → [调用 python_inter 进行分析]
```

### 数据可视化
```
用户: 生成用户年龄分布的直方图
助手: [调用 fig_inter 生成并保存图表]
```

## 开发约定

1. **代码风格**: 遵循 Python PEP 8 规范
2. **工具调用**: 优先使用专用工具而非通用执行器
3. **错误处理**: 所有工具都包含异常处理机制
4. **语言**: 所有用户交互使用简体中文
5. **图像保存**: 自动保存到 `public/images/` 目录

## 注意事项

- 确保数据库连接参数正确配置
- 图像保存路径需要预先创建目录
- 所有绘图代码必须创建 fig 对象并避免使用 plt.show()
- 环境变量中的 API 密钥需要有效配置

## 扩展开发

如需添加新工具：

1. 在 `graph.py` 中定义新的工具函数
2. 使用 `@tool` 装饰器和 Pydantic 模型进行参数验证
3. 将新工具添加到 `tools` 列表中
4. 更新提示词模板以包含新工具的使用说明



<img width="2331" height="1278" alt="test1" src="https://github.com/user-attachments/assets/43562466-dd9a-48cf-83bc-03915a61fb24" />
