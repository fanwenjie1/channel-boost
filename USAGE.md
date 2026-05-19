# 使用指南

## 🎯 快速开始

### 1. 初始化环境

```bash
# 克隆仓库
git clone https://github.com/fanwenjie1/channel-boost.git
cd channel-boost

# 创建虚拟环境（推荐）
python3 -m venv venv
source venv/bin/activate  # Linux/Mac
# 或
venv\Scripts\activate  # Windows

# 安装依赖
pip install -r requirements.txt
```

### 2. 更新排期数据

编辑 `data/schedule.csv` 文件，添加或修改频道排期信息：

```csv
频道,开始日期,结束日期,保量目标(PV),实际PV,保量目标(UV),实际UV,转化率(%),状态,负责人,备注
抖音,2026-05-01,2026-05-31,1000000,950000,100000,95000,3.2,进行中,张三,
微博,2026-05-01,2026-05-31,500000,480000,50000,48000,2.8,进行中,李四,需跟进
```

**字段说明：**
- `频道`: 运营频道名称
- `开始日期`: 排期开始日期 (YYYY-MM-DD)
- `结束日期`: 排期结束日期 (YYYY-MM-DD)
- `保量目标(PV)`: 预定的 PV 目标值
- `实际PV`: 实际达成的 PV 值
- `保量目标(UV)`: 预定的 UV 目标值
- `实际UV`: 实际达成的 UV 值
- `转化率(%)`: 频道转化率百分比
- `状态`: 排期状态 (进行中/已完成/暂停)
- `负责人`: 频道负责人名字
- `备注`: 其他备注信息

### 3. 生成报告

```bash
# 方式一: 使用 Python 脚本
python scripts/generate_report.py

# 方式二: 直接从命令行
cd scripts
python generate_report.py
```

### 4. 查看报告

生成成功后，在浏览器中打开报告文件：

```
file:///path/to/channel-boost/reports/experiment_report.html
```

或者在文件浏览器中双击 `reports/experiment_report.html`

---

## 📊 报告功能详解

### HTML 实验报告包含：

#### 1. **摘要卡片** (Summary Cards)
- 总 PV：所有频道实际 PV 之和
- 总 UV：所有频道实际 UV 之和
- 平均转化率：所有频道转化率的平均值
- 完成度：总体任务完成进度

#### 2. **排期表** (Schedule Table)
- 展示所有频道的详细排期信息
- 自动计算完成率和状态标记
- 支持按列排序（在支持的浏览器中）

#### 3. **数据可视化** (Charts)
包含 4 个互动图表：
- **PV 对比柱状图**：目标 vs 实际
- **UV 对比柱状图**：展示各频道 UV 数据
- **转化率分布圆环图**：转化率占比分析
- **PV 完成度雷达图**：完成度多维度展示

#### 4. **关键发现与建议** (Insights)
- 主要成果总结
- 改进建议清单

### 文本摘要报告
- 快速查看关键数据
- 便于邮件分享
- 易于比较和分析

---

## 🔄 工作流程

```
┌─────────────────┐
│  编辑排期数据   │
│ data/schedule.csv
└────────┬────────┘
         │
         ▼
┌─────────────────────────────┐
│  运行生成脚本               │
│ python scripts/generate_report.py
└────────┬────────────────────┘
         │
         ▼
┌──────────────────────────────┐
│  生成 HTML 和文本报告        │
│ reports/experiment_report.html
│ reports/experiment_summary.txt
└────────┬─────────────────────┘
         │
         ▼
┌──────────────────────┐
│  在浏览器中查看    │
│  分享和分析报告    │
└──────────────────────┘
```

---

## 💡 高级用法

### 自定义报告模板

修改 `templates/report_template.html` 中的样式和结构：

```html
<!-- 修改颜色方案 -->
<style>
  .card.pv {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  }
</style>

<!-- 修改图表类型 -->
<canvas id="pvChart"></canvas>
```

### 扩展数据字段

在 `data/schedule.csv` 中添加新列，然后修改 `templates/report_template.html` 的表格和图表部分。

### 批量处理多个报告

```bash
# 创建一个 bash 脚本来处理多个报告
for month in {01..12}; do
  cp data/schedule.csv data/schedule_2026_$month.csv
  python scripts/generate_report.py
done
```

---

## 🐛 常见问题

### Q1: 报告中的图表显示不出来
**A:** 
- 检查浏览器控制台是否有错误
- 确保 CSV 数据格式正确
- 检查数值字段是否为数字类型

### Q2: 能否自动定期生成报告？
**A:**
使用 GitHub Actions 或系统任务计划：

**GitHub Actions 示例** (`.github/workflows/generate-report.yml`):
```yaml
name: Generate Report
on:
  schedule:
    - cron: '0 9 * * 1'  # 每周一上午 9 点
jobs:
  generate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
        with:
          python-version: '3.9'
      - run: pip install -r requirements.txt
      - run: python scripts/generate_report.py
      - run: git add reports/ && git commit -m "Auto-generate report"
      - run: git push
```

### Q3: 如何导出为 PDF？
**A:**
```bash
# 方式一: 用浏览器的打印功能
# 在报告中按 Ctrl+P，选择 "保存为 PDF"

# 方式二: 使用工具
pip install weasyprint
# 然后修改脚本来支持 PDF 导出
```

### Q4: 报告支持离线使用吗？
**A:** 支持的，但图表需要 Chart.js 库。可以：
1. 下载 Chart.js 到本地
2. 修改模板中的 CDN 链接为本地路径
3. 离线使用

---

## 📱 优化提示

### 性能优化
- 对于超过 100 个频道的大型报告，考虑使用服务端渲染
- 压缩图表库大小
- 启用浏览器缓存

### 可访问性
- 报告支持 WCAG 2.1 AA 标准
- 支持屏幕阅读器
- 支持键盘导航

### 跨浏览器兼容性
- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- 不支持 IE 11

---

## 📞 支持和反馈

- 💬 在 GitHub Issues 中提出问题
- 🐛 报告 Bug
- 💡 提出功能建议

---

## 📄 许可证

MIT License - 详见 LICENSE 文件

---

**最后更新**: 2026-05-19
**维护者**: fanwenjie1
