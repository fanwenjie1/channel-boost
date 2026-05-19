# 📊 Channel Boost - 频道保量排期和实验报告系统

> 一个专业的频道保量排期管理和 HTML 实验报告生成系统

## 🎯 功能概览

✅ **频道排期管理** - 创建和管理多频道的保量排期  
✅ **自动报告生成** - 一条命令生成专业的 HTML 实验报告  
✅ **互动数据可视化** - 使用 ECharts 绘制动态图表  
✅ **对照组对比分析** - 支持实验组与对照组的数据对比  
✅ **多阶段支持** - 支持多个实验阶段的数据展示  
✅ **响应式设计** - 支持所有设备和屏幕尺寸  
✅ **专业样式** - 现代化的梯度设计和企业级配色  

## 📦 快速开始

### 1️⃣ 安装依赖

```bash
# 克隆仓库
git clone https://github.com/fanwenjie1/channel-boost.git
cd channel-boost

# 创建虚拟环境
python3 -m venv venv
source venv/bin/activate  # Linux/Mac
# 或
venv\Scripts\activate  # Windows

# 安装依赖
pip install -r requirements.txt
```

### 2️⃣ 准备数据

编辑 `data/schedule.csv` 或创建您自己的数据文件：

```csv
频道,开始日期,结束日期,保量目标(PV),实际PV,保量目标(UV),实际UV,转化率(%),状态,负责人,备注
抖音,2026-05-01,2026-05-31,1000000,950000,100000,95000,3.2,进行中,张三,
微博,2026-05-01,2026-05-31,500000,480000,50000,48000,2.8,进行中,李四,需跟进
```

### 3️⃣ 生成报告

```bash
python scripts/generate_report.py
```

### 4️⃣ 查看报告

在浏览器中打开生成的报告：

```
reports/experiment_report.html
```

## 📂 项目结构

```
channel-boost/
├── README.md                      # 项目说明
├── USAGE.md                       # 详细使用指南
├── requirements.txt               # Python 依赖
├── .gitignore                     # Git 忽略规则
├── data/
│   └── schedule.csv              # 📊 排期数据
├── templates/
│   ├── report_template.html       # 基础模板
│   └── bloomberg_tv_example.html  # Bloomberg TV 示例
├── scripts/
│   └── generate_report.py         # 报告生成脚本
└── reports/                       # 📁 输出目录
```

## 🎨 报告功能

生成的 HTML 报告包含：

### 1. **核心指标卡片** (KPI Cards)
- 显示关键指标的提升情况
- 彩色卡片设计，易于扫一眼了解
- 支持自定义指标

### 2. **互动图表** (Interactive Charts)
- 📊 **柱状图** - 实验组 vs 对照组对比
- 📈 **折线图** - 时间序列趋势
- 🔵 **圆环图** - 占比分布
- 📡 **雷达图** - 多维度数据展示

### 3. **详细数据表** (Data Table)
- 所有原始数据的详细展示
- 支持多个阶段的标签
- 交替行背景，易于阅读

### 4. **结论与建议** (Conclusion)
- 实验效果总结
- 关键发现
- 后续行动建议

## 🌟 示例报告

仓库包含 **Bloomberg TV 实验报告示例**，展示了专业报告的完整结构：

```
templates/bloomberg_tv_example.html
```

**示例包含的内容：**
- ✅ 西班牙地区 DHM 实验（4.15-4.25）
- ✅ 两个实验阶段的对比
- ✅ 5 个高质量的交互图表
- ✅ 详细的数据表格（14+ 行数据）
- ✅ 专业的结论分析

## 📊 数据格式

### CSV 数据格式

```csv
频道,开始日期,结束日期,保量目标(PV),实际PV,保量目标(UV),实际UV,转化率(%),状态,负责人,备注
Channel1,2026-05-01,2026-05-31,1000000,950000,100000,95000,3.2,进行中,张三,
Channel2,2026-05-01,2026-05-31,500000,480000,50000,48000,2.8,已完成,李四,
```

**字段说明：**
| 字段 | 说明 | 示例 |
|------|------|------|
| 频道 | 频道名称 | 抖音、微博、B 站 |
| 开始日期 | 排期开始日期 | 2026-05-01 |
| 结束日期 | 排期结束日期 | 2026-05-31 |
| 保量目标(PV) | 目标 PV | 1000000 |
| 实际PV | 实际达成的 PV | 950000 |
| 保量目标(UV) | 目标 UV | 100000 |
| 实际UV | 实际达成的 UV | 95000 |
| 转化率(%) | 转化率百分比 | 3.2 |
| 状态 | 排期状态 | 进行中/已完成/暂停 |
| 负责人 | 频道负责人 | 张三 |
| 备注 | 其他备注 | 需跟进 |

## 🔧 高级用法

### 自定义报告模板

编辑 `templates/report_template.html`：

```html
<!-- 修改颜色主题 -->
<style>
  .card {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  }
</style>
```

### 添加新的图表

在模板中添加新的 ECharts 图表：

```html
<div id="myChart" class="chart"></div>

<script>
  var chart = echarts.init(document.getElementById('myChart'));
  chart.setOption({ /* 配置 */ });
</script>
```

### 自动定期生成报告

使用 GitHub Actions 自动化（见 USAGE.md）

## 📋 技术栈

- **Python 3.7+** - 数据处理和模板渲染
- **Pandas** - 数据处理库
- **Jinja2** - 模板引擎
- **ECharts 5** - 数据可视化
- **HTML5 + CSS3** - 前端展示

## 📦 依赖

```txt
pandas>=1.3.0
Jinja2>=3.0.0
```

安装依赖：
```bash
pip install -r requirements.txt
```

## 🚀 常见用途

### 频道运营
- 📊 跟踪频道保量目标完成情况
- 📈 对比不同时期的频道表现
- 🎯 管理多个频道的并发排期

### 实验分析
- 🧪 设计和管理 A/B 测试
- 📉 对比实验组和对照组的数据
- 💡 生成实验报告和分析结论

### 数据展示
- 📑 生成专业的演讲演示文稿
- 📧 通过邮件分享交互式报告
- 🌐 发布到内部知识库或仪表板

## 🤝 贡献指南

欢迎提交 Issue 和 Pull Request！

## 📄 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

## 📞 支持

- 📖 查看 [USAGE.md](USAGE.md) 了解详细使用指南
- 💬 在 GitHub Issues 中提问
- 🐛 报告 Bug
- 💡 提出功能建议

---

**快速链接：**
- [详细使用指南](USAGE.md)
- [示例报告](templates/bloomberg_tv_example.html)
- [数据文件](data/schedule.csv)
- [生成脚本](scripts/generate_report.py)

**最后更新**: 2026-05-19  
**维护者**: fanwenjie1
