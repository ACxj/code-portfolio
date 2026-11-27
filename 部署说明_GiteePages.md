# 作品集部署说明（Gitee Pages 静态托管）

> 适用：门面站 + 三个 Demo 样例，纯静态 HTML，无需后端、数据库、构建工具。
> 本地目录：`D:\DouBao\抖音视频\portfolio\`

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

1. 注册 / 登录 Gitee（https://gitee.com ）；
2. **先完成实名认证**：头像 → 设置 → 实名认证。Gitee Pages 未实名无法启动服务；
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

## 四、启动 Gitee Pages

1. 进入 Gitee 仓库页面 → 顶部「服务」→「Gitee Pages」；
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

把线上站点地址填回三份 README 的「在线地址」一栏（当前为占位）：
- `README_官网Demo.md`
- `README_预约H5_Demo.md`
- `README_管理后台Demo.md`

如门面站首页需要放自己的联系方式入口，按合规要求只走站内私信 / 独立站表单，不在页面留微信、QQ、二维码或外部联系方式。

## 七、备选部署方式（可选）

- **GitHub Pages**：同样静态托管，仓库公开后 Settings → Pages 选分支即可自动部署，适合接海外单展示；国内访问偏慢。
- **Vercel / Netlify**：直接拖拽静态目录上线，自带 HTTPS 和全球 CDN，免配置；国内访问速度一般。
- **自有服务器 / 对象存储（OSS / COS）**：有域名后可绑定，需备案；后期正式商用再考虑。

> 当前阶段先用 Gitee Pages 跑通国内可访问的作品集即可，后续有稳定客户再绑独立域名。
