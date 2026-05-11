# camera-dialog

现场打卡 H5 — 扫码进入，相机实时叠加相框拍照并保存。

- 线上：https://camera-dialog.vercel.app/
- 仓库：https://github.com/siriusharrison-png/camera-dialog

## 项目结构

```
camera-dialog/
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

## 部署

当前已部署到 Vercel（连接 GitHub 自动部署）。更新流程：

```bash
cd ~/Desktop/camera-dialog
git add .
git commit -m "update"
git push
```

推送后 Vercel 会在 30 秒内自动重新部署。

### 本地调试（只能看 UI，相机/定位需 HTTPS）

```bash
cd ~/Desktop/camera-dialog
python3 -m http.server 8000
# 打开 http://localhost:8000
```

## 二维码

当前二维码文件：`~/Desktop/camera-dialog-qrcode.png`

如需重新生成：
```bash
curl -sL "https://api.qrserver.com/v1/create-qr-code/?size=600x600&margin=20&data=https%3A%2F%2Fcamera-dialog.vercel.app%2F" -o ~/Desktop/camera-dialog-qrcode.png
```

## 功能说明

1. 打开页面 → 主动请求定位授权
2. 在 500m 范围内：显示 4 个相框；否则只显示 2 个
3. 点"拍照打卡"：实时相机预览 + 相框叠加 + 底部切换相框 + 快门
4. 点"上传图片"：从相册选图进入编辑页
5. 编辑页可切换相框、重新选择、保存图片
6. iOS/微信环境：保存时会弹出大图，长按即可保存到相册
7. 定位失败/拒绝：状态卡片里有"重新授权/重新尝试"按钮，授权通过后按钮消失

## 换正式相框

6 张正式相框 PNG 做好后，替换 `frames/` 下同名文件，然后 `git push` 即可。
