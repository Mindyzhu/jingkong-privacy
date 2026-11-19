# Lighterly 英文隐私与支持页面

## 本地预览

直接用浏览器打开 `privacy.html` 或 `support.html`。两份页面共用本地样式、App 图标和字体，无需安装依赖或联网即可查看和展开 FAQ。邮箱链接会交给系统邮件客户端，Apple 帮助链接需要联网。

## 只读审计记录

| 项目 | 当前工程所见 |
| --- | --- |
| 现有法律入口 | `dist/profile.js` 的 Me → Legal 包含 Privacy Policy 和 Terms of Use；Me → Help & Support 提供英文内页和联系入口。Plus 购买页的 Privacy Policy 打开内页，Terms of Use 指向 Apple 标准 EULA。现有内页用作参考。工程中未发现独立的 `privacy.html` 或 `support.html`。 |
| 品牌 | 复用 App 图标、Cormorant Garamond 字体与应用的灰绿色系。字体许可证随资源保留。 |
| 本地数据 | `dist/app.js`、`dist/profile.js` 将核心记录、个人资料和设置存入本地。没有应用账号同步。可选语音输入在 `ios/Lighter.swift` 要求本机识别。 |
| Screen Time | `ios/Lighter.entitlements`、`ios/ScreenTimeBridge.swift` 使用 Family Controls 个体授权和系统选择器。原生层存储不透明 token，用于显示选择和关联规则。当前目标没有统计报表或规则执行能力。 |
| 健康与戒指 | `ios/HealthKitBridge.swift` 请求只读 HealthKit 访问。`ios/RingBridge.swift` 和 `dist/ring-bridge.js` 支持兼容 JY Ring 的直接蓝牙连接与本地缓存。`dist/health-data.js` 合并来源用于视图展示。 |
| AI | `dist/config.js` 指向 Cloudflare Worker。`dist/features.js` 与 `dist/ai-service.js` 组装并发送反思请求，`dist/quests.js` 单独提交挑战摘要。`worker/index.mjs` 默认使用 APiBox，可通过部署环境改变上游与模型。 |
| 订阅 | `dist/profile.js` 和 `ios/Lighter.swift` 连接 StoreKit，核验交易和到期状态，支持恢复。项目配置中有月、季、年三个产品 ID。最终上架产品和地区供应须在 App Store Connect 核对。 |
| 清除数据 | `dist/profile.js` 清除核心本地记录、偏好和原生 Screen Time 选择。戒指设备列表和读数缓存使用独立键。`dist/health.js` 的 Remove ring 解除关联并保留已同步数据。 |

## 发布前待确认

- **发布主体与日期**。截图仅显示开发团队选择器中的名称 Shenzhen Lesheng Technology Media Co., Ltd.（深圳乐笙科技传媒有限公司）。请以英文版 App Store Connect 对应应用的开发者账号、销售主体和实际负责数据处理的主体为准。网页使用产品名与已提供邮箱，未将公司写为已经核实的发布主体。页面日期是本地稿件更新日期，正式生效日期待确认。
- **AI 服务与留存**。核实生产 Worker 的实际网关、模型运营方、数据处理地区、请求和日志的保留期限、用途、训练政策、删除机制，以及支持邮箱的保留和删除流程。策略草稿描述已查到的默认路径，没有承诺具体保留天数。
- **AI 同意**。反思入口检查 AI Sharing，当前 `requestQuestSummary` 只检查 Plus 权限和缓存等条件，没有同样的独立同意判断。请求可带目标、对象及备注。发布前应核实发行构建中每条第三方 AI 传输路径的同意流程，并核对 Apple 的数据共享要求。 [Apple App Review Guidelines §5.1](https://developer.apple.com/app-store/review/guidelines/#privacy)
- **删除范围与设备**。在发行构建和真机核验戒指缓存的清除范围，确认支持的戒指型号、HealthKit 与蓝牙权限文案、Screen Time 分发授权和设备入口。核对设备备份行为及最终网页托管日志。
- **儿童与地区隐私**。确认目标年龄、发行地区、适用的儿童政策及隐私请求处理流程。当前儿童条款提供家长或监护人联系渠道。
- **上架信息**。核对测试版本、订阅商品供售状况、App Privacy 标签和 App 内网页入口。当前 Me 及 Plus 仍使用既有入口。邮箱链接格式已经检查，实际收件需用负责发布的邮箱确认。 [Apple App Store Connect 隐私信息说明](https://developer.apple.com/help/app-store-connect/manage-app-information/manage-app-privacy)

## 本地验证

使用 WebKit 分别以 375、390 和 1440 CSS px 打开两页，确认页面无横向溢出、目录锚点有效且品牌图标加载。三个宽度下均逐项测试了 18 个 FAQ 的展开和收起。另检查了两页互链、跨页锚点、资源路径和邮件链接格式，并核对了 Apple 帮助页面。六张对应的首屏截图位于 `preview/`，支持页截图展示第一项 FAQ 展开状态。

## GitHub Pages 后续路径

确认发布内容后，可在独立 Pages 仓库使用 **Settings → Pages → Deploy from a branch**，将两个 HTML、样式及 `assets/` 放到发布来源根目录。若沿用应用仓库，可通过 GitHub Actions 只打包上述公开网页文件。预览截图和本审计说明可留在本地。项目站点 URL 通常如下，需以 Pages 显示的正式地址为准。

- Privacy Policy URL  `https://<owner>.github.io/<repository>/privacy.html`
- Support URL  `https://<owner>.github.io/<repository>/support.html`

正式网址生效后，可在 App Store Connect 填入相应字段，另行接入 App 内入口。 [GitHub Pages 发布来源文档](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
