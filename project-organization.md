# 项目组织与文件管理规范

## 核心原则
项目开发过程中产生的与项目本身运行无关的文档、脚本等文件，不应放在项目根目录下，而应放在专门的文件夹下并妥善整理。

## 文件分类

### 1. 运行相关文件（可放在根目录）
- `README.md`：项目主要说明文档
- `docker-compose.yml`：Docker 编排配置
- `.env.example`：环境变量示例文件
- `.gitignore`：Git 忽略配置
- `package.json`、`pom.xml` 等：项目依赖配置文件
- 其他项目运行必需的配置文件

### 2. 开发辅助文件（应放在专门目录）
以下类型的文件应该放在专门的目录中：

#### 测试和验证文档
- 测试结果报告（如 `TASK2_TEST_RESULTS.md`）
- 验证文档（如 `TASK2_VERIFICATION.md`）
- 测试说明（如 `DOCKER_TEST.md`）

#### 故障排查文档
- 问题排查指南（如 `TROUBLESHOOTING.md`）
- 快速修复指南（如 `QUICK_FIX.md`）

#### 开发脚本
- 验证脚本（如 `verify-docker-setup.bat`、`verify-setup.bat`）
- 重置脚本（如 `reset-database.bat`、`reset-database.sh`）
- 其他开发辅助脚本

#### 分析报告
- 性能分析报告
- 代码分析报告（如 `nofx-analysis-report.md`）

## 推荐的目录结构

### 方案一：使用 `docs` 目录
```
project-root/
├── docs/
│   ├── testing/              # 测试相关文档
│   │   ├── 测试结果.md
│   │   └── 验证报告.md
│   ├── troubleshooting/      # 故障排查文档
│   │   ├── 常见问题.md
│   │   └── 快速修复.md
│   └── reports/              # 分析报告
│       └── 分析报告.md
├── scripts/                  # 开发脚本
│   ├── verify-setup.bat
│   ├── verify-setup.sh
│   ├── reset-database.bat
│   └── reset-database.sh
├── src/                      # 源代码
├── README.md
└── docker-compose.yml
```

### 方案二：使用 `dev` 目录
```
project-root/
├── dev/
│   ├── docs/                 # 开发文档
│   ├── scripts/              # 开发脚本
│   └── reports/              # 测试报告和分析
├── src/                      # 源代码
├── README.md
└── docker-compose.yml
```

## 实施规则

### 创建新文件时
1. **评估文件用途**：判断文件是否为项目运行必需
2. **选择合适位置**：
   - 运行必需 → 根目录或相应的配置目录
   - 开发辅助 → `docs/`、`scripts/` 或 `dev/` 目录
3. **使用清晰命名**：
   - 文件名应清晰表达其用途
   - 测试文档、故障排查文档、分析报告等使用中文命名，便于理解
   - 脚本文件使用英文命名，保持兼容性

### 整理现有文件时
1. **识别可移动文件**：找出所有开发辅助文件
2. **创建目标目录**：根据文件类型创建合适的目录
3. **移动并更新引用**：移动文件并更新相关文档中的引用
4. **更新 .gitignore**：如果需要，更新忽略规则

## 具体示例

### ❌ 不推荐的做法
```
project-root/
├── TASK2_TEST_RESULTS.md          # 测试文档散落在根目录
├── TASK2_VERIFICATION.md
├── TROUBLESHOOTING.md
├── QUICK_FIX.md
├── DOCKER_TEST.md
├── verify-docker-setup.bat         # 脚本散落在根目录
├── verify-docker-setup.sh
├── reset-database.bat
├── reset-database.sh
├── nofx-analysis-report.md         # 报告散落在根目录
├── README.md
└── docker-compose.yml
```

### ✅ 推荐的做法
```
project-root/
├── docs/
│   ├── testing/
│   │   ├── 任务2测试结果.md
│   │   ├── 任务2验证报告.md
│   │   └── Docker测试说明.md
│   ├── troubleshooting/
│   │   ├── 故障排查指南.md
│   │   └── 快速修复指南.md
│   └── reports/
│       └── NOFX分析报告.md
├── scripts/
│   ├── verify-docker-setup.bat
│   ├── verify-docker-setup.sh
│   ├── reset-database.bat
│   └── reset-database.sh
├── src/
├── README.md
└── docker-compose.yml
```

## 优势

1. **清晰的项目结构**：根目录保持简洁，一目了然
2. **易于维护**：相关文件集中管理，便于查找和更新
3. **专业性**：体现良好的项目管理实践
4. **可扩展性**：便于后续添加更多开发辅助文件
5. **团队协作**：团队成员能快速找到所需文档和脚本

## 注意事项

- 移动文件后，记得更新 README.md 中的相关链接
- 如果脚本之间有相互引用，需要更新路径
- 考虑在各个目录下添加 README.md 说明目录用途
- 保持目录结构的一致性，避免频繁变更

## 适用范围
- 所有新创建的开发辅助文件
- 现有项目的文件整理
- 多人协作的项目
- 需要长期维护的项目
