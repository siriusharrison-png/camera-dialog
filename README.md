# 现场打卡 H5

## 项目结构

```
checkin-h5/
├── index.html          ← 主页面（所有代码都在里面）
├── frames/             ← 相框资源
│   ├── frame-1.png     ← 现场相框 1（当前均为测试图）
│   ├── frame-2.png     ← 现场相框 2
│   ├── frame-3.png     ← 现场相框 3
│   ├── frame-4.png     ← 现场相框 4
│   ├── frame-off-1.png ← 非现场相框 1
│   └── frame-off-2.png ← 非现场相框 2
└── README.md
```

## 当前配置

- **活动坐标**：31.451889, 121.124306（31°27'06.8"N 121°07'27.5"E）
- **半径**：500m
- **相框**：6 张均为测试图（同一张金色相框 PNG）

改坐标/半径：编辑 `index.html` 顶部 `CONFIG` 对象。
换相框：直接替换 `frames/` 目录下的 PNG，文件名保持不变。

## 必须部署到 HTTPS 才能用

**相机和定位 API 都要求 HTTPS**，本地双击打开 index.html 只能看到界面，**无法实际拍照或定位**。

必须部署到支持 HTTPS 的静态托管平台。

## 部署方式（推荐 Cloudflare Pages）

### 方案 A：Cloudflare Pages（推荐，国内访问快）

1. 在 [GitHub](https://github.com) 新建一个仓库，把整个 `checkin-h5` 文件夹 push 上去
2. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/) → Pages → Connect to Git
3. 选择刚才的仓库，构建配置留空（纯静态）
4. 部署完成后会得到一个 `xxx.pages.dev` 的 HTTPS 链接

### 方案 B：Vercel（最简单）

1. 把文件夹拖到 [vercel.com/new](https://vercel.com/new)
2. 直接拿到 `xxx.vercel.app` 链接

### 方案 C：本地调试（只在电脑上预览）

```bash
cd ~/Desktop/checkin-h5
python3 -m http.server 8000
# 打开 http://localhost:8000
```

## 生成二维码

拿到部署链接后，访问 [https://cli.im](https://cli.im) 或 [https://www.qrcode-monkey.com/](https://www.qrcode-monkey.com/) 输入链接即可生成二维码。

## 功能说明

1. 打开页面 → 主动请求定位授权
2. 在 500m 范围内：显示 4 个相框；否则只显示 2 个
3. 点"拍照打卡"：实时相机预览 + 相框叠加 + 底部切换相框 + 快门
4. 点"上传图片"：从相册选图进入编辑页
5. 编辑页可切换相框、重新选择、保存图片
6. iOS/微信环境：保存时会弹出大图，长按即可保存到相册
7. 定位失败/拒绝：状态卡片里有"重新授权/重新尝试"按钮，授权通过后按钮消失

## 需要我帮你的时候

- 部署、GitHub 推送、二维码生成，如果卡住直接告诉我
- 6 张正式相框 PNG 做好后，替换 `frames/` 下同名文件即可，无需改代码
