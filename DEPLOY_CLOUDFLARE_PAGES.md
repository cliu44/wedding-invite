# Cloudflare Pages 部署指南（婚礼请帖）

这份指南用于把当前静态站点部署到 Cloudflare Pages，以获得更稳定的国内访问体验。

## 1) 前置准备

- GitHub 仓库：`cliu44/wedding-invite`
- Cloudflare 账号（免费版即可）
- 仓库主分支：`main`

## 2) 在 Cloudflare 创建 Pages 项目

1. 打开 Cloudflare Dashboard
2. 进入 **Workers & Pages** -> **Create** -> **Pages** -> **Connect to Git**
3. 授权并选择仓库 `cliu44/wedding-invite`
4. Build settings 按下面填写：
   - Framework preset: `None`
   - Build command: 留空
   - Build output directory: `/`
   - Root directory: `/`
5. 点击 **Save and Deploy**

> 这是纯静态页面，不需要构建命令。

## 3) 首次验证

Cloudflare 会分配一个默认域名，例如：

`https://<project-name>.pages.dev`

访问以下地址确认成功：

- `https://<project-name>.pages.dev/index.html`
- `https://<project-name>.pages.dev/smart.html`

## 4) 绑定自定义域名（推荐）

1. 在 Pages 项目中进入 **Custom domains** -> **Set up a custom domain**
2. 输入你要使用的域名（如 `invite.yourdomain.com`）
3. 按页面提示添加 DNS 记录（通常 CNAME）
4. 等待证书签发完成（状态 Active）

## 5) 分享链接建议

优先分享智能入口页：

- `https://你的域名/smart.html`

它会优先尝试当前域名，再自动回退到 jsDelivr / Statically / GitHub / GitHack。

## 6) 后续更新方式

每次更新页面后：

1. 提交并推送到 `main`
2. Cloudflare Pages 自动触发新部署
3. 几十秒到几分钟后生效

## 7) 常见问题

### Q1: 微信内打开慢或空白？

- 优先发 `smart.html` 链接
- 提醒宾客“如异常可点页面内备用入口”

### Q2: 自定义域名证书未生效？

- 检查 DNS 是否在 Cloudflare 侧正确生效
- 等待证书签发完成后再测试

### Q3: 想完全不用第三方回退？

- 当你确认自定义域名长期稳定后，可在 `smart.html` 中把回退列表只保留当前域名。
