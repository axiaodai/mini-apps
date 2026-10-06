# 小工具页

三个单文件网页，托管在 GitHub Pages 上。纯静态、无后端、无追踪，打开即用。

🌐 站点：https://axiaodai.github.io/mini-apps/

| 路径 | 页面 | 说明 |
| --- | --- | --- |
| `/running-blank/` | 跑步记录 · 奖牌统计 | 记录里程与用时，自动汇总月度/周度与奖牌进度，图表展示 |
| `/blood-blank/` | 献血记录 · 管理统计 | 记录献血日期、类型与血量，按折算规则统计次数与奖牌 |
| `/kaoqin/` | 考勤与工资计算器 | 月度考勤 → 工资计算（休班额度、加班、积欠结转、季节工时） |

## 数据存在哪（重要）

**存在你自己的浏览器里**（localStorage），不上传、不同步、各人互不干扰：

| 页面 | 存储键 |
| --- | --- |
| 跑步记录 | `mini-apps-running-v1` |
| 献血记录 | `mini-apps-blood-v1` |

因此有两条注意事项：

1. **右下角有「导出 / 导入」按钮** —— 想换设备、换浏览器、或清理浏览器数据前，先点「导出」存一个 JSON 备份；在新设备上点「导入」即可恢复。**没有导出就可能丢**。
2. **不要用无痕/隐私模式**：关掉窗口数据就没了。

## 说明

- `running-blank` 与 `blood-blank` 是**清空数据**的版本：界面、图表与逻辑完整保留，仅把记录数组置空
  （`DATA = {records:[],monthly:[],weekly:[]}` / `DATA = {records:[]}`），不含任何个人信息。
- 这两个页面原本是**某个家庭自用服务的前端**：它们通过 `GET /api/data`、`POST|PUT /api/records`、
  `DELETE /api/records?index=N` 访问服务端。放到 GitHub Pages 后这些请求会 404（数据读不到、新记录也存不了），
  所以公开版在页面最前面注入了一层**本地存储代理**：拦截 `/api/*` 并改用 localStorage 应答，
  并顺带提供导出/导入。**页面自身代码一行未改**。
- 代理会按页面原有格式重算聚合数据（`monthly: [年月, 公里, 次数, 平均配速]`、
  `weekly: [第N周, 起止, 公里, 次数]`），因为原页面从接口接收聚合值、并不自行重算。
- `kaoqin` 是**脱敏示例版**：已移除内嵌考勤表、默认人员与月薪、规则示例中的具体金额。
- 图表库 `vendor/echarts.min.js` 来自 [Apache ECharts](https://echarts.apache.org/) 5.6.0，
  本地化存放（原页面引用 `cdn.jsdelivr.net`，部分网络不可达），授权见 `vendor/ECHARTS-NOTICE.txt`。

## 这些页面是怎么验证的

用无头 Chrome 打开本地副本，在**同一个页面里**完成：新增 → 读取 → 删除 → 再新增，
再调用页面自身的 `initData()` 确认记录被渲染出来，并检查 localStorage 已写入。两个页面均通过。

## 部署

仓库 Settings → Pages → Source 选 `main` 分支根目录。
