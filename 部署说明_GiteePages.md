# 作品集部署说明（静态托管）

> 适用：门面站 + 三个 Demo 样例，纯静态 HTML，无需后端、数据库、构建工具。
> 本地目录：`D:\DouBao\抖音视频\portfolio\`
>
> **2026-11-27 更新：Gitee Pages 服务已下线，暂无上线计划，Gitee 仓库仅作代码备份 / 展示，不能再用来挂静态站。** 本次公网上线已选用 **GitHub Pages**，站点已上线并验证可访问：
> - 门面站：https://acxj.github.io/code-portfolio/
> - 官网 Demo：https://acxj.github.io/code-portfolio/demo-website.html
> - 预约 H5 Demo：https://acxj.github.io/code-portfolio/demo-booking.html
> - 管理后台 Demo：https://acxj.github.io/code-portfolio/demo-admin.html
> - GitHub 仓库：`https://github.com/ACxj/code-portfolio`（公开，`main` 分支）
>
> 其余备选平台（Netlify / Vercel / Cloudflare Pages / 国内云 OSS）见第七节留档。

## 一、文件摆放（仓库根目录结构）

把 `portfolio/` 里的内容整体作为一个 Git 仓库推送。**部署目录选仓库根目录 `/`**，文件位置如下，不要改动文件名和相对层级：

```
code-portfolio/                 ← Gitee 仓库根目录（部署目录留空 = 根目录）
├── index.html                  ← 门面站首页（站点入口，文件名必须是 index.html）
├── demo-website.html           ← Demo1 品牌官网样例
├── demo-booking.html           ← Demo2 预约小程序 H5 样例
├── demo-admin.html             ← Demo3 管理后台样例
├── assets/                     ← 页面截图（供仓库 README 展示用）
│   ├── portal-home.png
│   ├── website-desktop.png
│   ├── website-mobile.png
│   ├── booking-home.png
│   ├── booking-mine.png
│   ├── admin-list.png
│   └── admin-modal.png
├── README_官网Demo.md
├── README_预约H5_Demo.md
└── README_管理后台Demo.md
```

### 引用关系（为什么必须保持这个层级）

- `index.html` 里三个"查看样例"按钮用同级相对路径链接：`demo-website.html`、`demo-booking.html`、`demo-admin.html` —— **三个 Demo 必须和 `index.html` 放在同一层**，不能各自套子文件夹，否则链接 404。
- 三份 README 里的截图用 `assets/xxx.png` 相对路径引用 —— `assets/` 必须和 README 同级。
- 线上站点本身不依赖 `assets/` 图片（HTML 里没有引用本地图片）；截图只用于仓库 README 展示，随仓库一起上传即可。
- 字体走公网 CDN（思源黑体 VF），无需本地上传字体文件。

## 二、部署前准备

> **当前进度（2026-11-27 实测）**
> - ✅ Gitee 备份仓库：`https://gitee.com/ace0306/code-portfolio`（公开，`main` 分支，16 个文件），仅作代码备份与仓库展示；
> - ✅ GitHub 仓库：`https://github.com/ACxj/code-portfolio`（公开，`main` 分支），本机 SSH 公钥已加到账号，推送免密；
> - ✅ GitHub Pages 已开启：Source = Deploy from a branch，分支 `main`，目录 `/ (root)`，HTTPS 强制开启；
> - ✅ 线上四个页面与 7 张截图均返回 200，已在浏览器核验门面站视觉正常；
> - ⛔ Gitee Pages 已下线，无法用它挂静态站。

1. 注册 / 登录 Gitee（https://gitee.com ）；
2. **先完成实名认证**：在 Gitee 网页内按提示进入实名认证（首次开启 Pages 时通常会在 Pages 页面引导填写），上传身份证人像面 / 国徽面 / 手持身份证照，等待审核通过；Gitee Pages 未实名无法启动服务；
3. 本地已安装 Git（命令行 `git --version` 能出版本号即可）。

## 三、创建仓库并推送（命令行）

1. 在 Gitee 网页右上角「+ → 新建仓库」：
   - 仓库名：建议 `code-portfolio`（地址即 `https://gitee.com/你的用户名/code-portfolio`）；
   - **是否开源：选「公开」**（私有仓库 Pages 访问受限）；
   - **不要勾选**「初始化仓库 / 生成 README」，避免和本地提交冲突；
   - 创建后复制仓库 HTTPS 地址。

2. 在本地 `portfolio` 目录打开终端，执行（把最后一行地址换成你自己的仓库地址）：

```powershell
cd D:\DouBao\抖音视频\portfolio
git init
git add .
git commit -m "作品集门面站 + 三个 Demo 样例"
git branch -M main
git remote add origin https://gitee.com/你的用户名/code-portfolio.git
git push -u origin main
```

> 若推送时要求登录，输入 Gitee 用户名和私人令牌（不是登录密码；令牌在「设置 → 私人令牌」生成，勾选仓库权限）。

## 四、~~启动 Gitee Pages~~（已下线，废弃）

> Gitee Pages 服务已下线、暂无上线计划，以下步骤仅留档，不可再用。上线请直接看第七节备选平台。

1. ~~进入 Gitee 仓库页面 → 顶部「服务」→「Gitee Pages」；~~
2. 部署分支选 `main`（或 `master`，与推送分支一致）；部署目录**留空（根目录 `/`）**；
3. 勾选「强制使用 HTTPS」→ 点「启动」；
4. 启动后得到站点地址，形如：
   - 子目录形式：`https://你的用户名.gitee.io/code-portfolio/`
   - （若仓库名与个性地址同名，可得到不带子目录的 `https://你的用户名.gitee.io/`，非必需）
5. 浏览器打开该地址，应先看到门面站 `index.html`，三个"查看样例"分别能跳到对应 Demo。

## 五、后续更新

- 免费版 Gitee Pages **不会自动更新**：每次改完代码 `git push` 后，回到仓库「服务 → Gitee Pages」手动点一次「更新」，线上才会刷新；
- 截图 / 文案有改动，重新推送并点更新即可。

## 六、部署后回填

线上站点地址已填回三份 README 的「在线地址」一栏：
- `README_官网Demo.md` → `demo-website.html`
- `README_预约H5_Demo.md` → `demo-booking.html`
- `README_管理后台Demo.md` → `demo-admin.html`

如门面站首页需要放自己的联系方式入口，按合规要求只走站内私信 / 独立站表单，不在页面留微信、QQ、二维码或外部联系方式。

## 七、备选部署平台（Gitee Pages 已下线，改用这些）

> 说明：海外免费平台在大陆访问普遍偏慢、个别域名可能被 DNS 污染；国内快的方案（云 OSS/COS、自有服务器）需要云账号实名和少量配置。前期先把作品集挂出去给客户看，后期有预算再绑国内加速 / 独立域名。

- **Netlify Drop（最快上手，推荐先试）**：打开 `app.netlify.com/drop`，把 `portfolio` 文件夹（或打包的 ZIP）直接拖进去，**不用先注册账号**即可即时得到 `xxx.netlify.app` 公网链接，之后可注册账号认领站点；纯静态 HTML 直接发布，无需构建。
- **Vercel Drop**：`vercel.com/drop`，需先登录（可用 GitHub 账号），拖文件或 ZIP 发布到 `xxx.vercel.app`；注意 `vercel.app` 域名在大陆可能被 DNS 污染，必要时绑自定义域名。
- **Cloudflare Pages**：全球 CDN、免费带宽充足，可连 Git 仓库或直接上传；大陆访问速度一般，`pages.dev` 域名偶有不稳。
- **GitHub Pages（长期稳定，本次已采用）**：仓库推到 GitHub，Settings → Pages 选 `main` 分支、根目录即自动部署；国内访问偏慢但稳定，适合接海外单展示。本站即托管于此。
- **国内云 OSS / COS 静态网站托管（国内最快）**：阿里云 OSS / 腾讯云 COS 开静态网站托管，上传文件即可访问；需云账号实名，临时子域名可先用，正式商用绑域名需备案。

### 本次纯静态站部署要点（任一平台通用）

- 站点根目录必须含 `index.html`（门面站入口）；
- 四个 HTML 同级，`assets/` 与 README 同级，相对链接不要改；
- 平台若要求指定发布目录 / 根目录，选存放 `index.html` 的那一层；
- 无需构建命令（无 `package.json`、无框架），发布目录即 `portfolio` 根。

> 当前阶段作品集已通过 GitHub Pages 跑通公网可访问；后续若国内客户打开偏慢，或有稳定商用客户，再考虑国内云托管（OSS/COS）或绑定独立域名。
