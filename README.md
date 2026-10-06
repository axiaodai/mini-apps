# 小工具页

三个单文件网页，托管在 GitHub Pages 上。纯静态、无后端、无追踪，打开即用。

🌐 站点：https://axiaodai.github.io/mini-apps/

| 路径 | 页面 | 说明 |
| --- | --- | --- |
| `/running-blank/` | 跑步记录 · 奖牌统计 | 记录里程与用时，汇总月度/周度、奖牌进度，图表展示 |
| `/blood-blank/` | 献血记录 · 管理统计 | 献血日期/类型/血量，按折算规则统计次数与奖牌进度 |
| `/kaoqin/` | 考勤与工资计算器 | 月度考勤 → 工资计算（休班额度、加班、积欠结转、季节工时） |

## 使用说明

- 打开页面后直接录入，数据保存在**你自己浏览器的 localStorage** 里：不上传、不同步、互不干扰。
- 想换设备：页面内一般有"导出/导入"或数据面板，导出 JSON 再在另一台设备导入即可。
- 三个页面各自自包含，可以单独下载那个 `index.html` 离线使用（图表库已一并本地化）。

## 说明

- `running-blank` 与 `blood-blank` 是**清空数据**的版本：保留界面、图表与全部逻辑，仅把记录数组置空
  （`DATA = {records:[],monthly:[],weekly:[]}` / `DATA = {records:[]}`），因此不含任何个人信息。
- `kaoqin` 是**脱敏示例版**：已移除内嵌考勤表、默认人员与月薪、规则示例中的具体金额。
- 图表库 `vendor/echarts.min.js` 来自 [Apache ECharts](https://echarts.apache.org/) 5.6.0，
  本地化存放（原页面引用 `cdn.jsdelivr.net`，部分网络不可达），授权见 `vendor/ECHARTS-NOTICE.txt`。

## 部署

仓库 Settings → Pages → Source 选 `main` 分支根目录。
