# holo-tavern-assets

《赫萝的黄昏酒馆》素材包 —— 由 dsh-theme-holo 插件按需下载。

## 这是什么

酒馆分两半，分开发布：

| 部分 | 在哪 | 体积 | 什么时候拿到 |
|---|---|---|---|
| 代码 + 第三方库 | `dsh-theme-holo` 仓库的 `tavern/lesson/{js,css,index.html,favicon.svg}` 和 `tavern/vendor/` | 约 1.53 MB | 装插件就有 |
| 素材 | **本仓库** | 约 5.38 MB | 插件设置里点「下载酒馆」才拉 |

这样装插件的人不会附带酒馆素材，节省 5.38 MB。

## 目录

```
tavern/
├── assets/
│   └── holo.glb                      3D 赫萝模型（1868424 B）
└── lesson/
    └── assets/
        ├── holo2d/                   2D 立绘 + 尾巴三姿态
        ├── items/final/              11 件收藏品
        ├── stage/                    8 张舞台素材
        └── voice/                    17 条配音 + index.json
```

共 43 个文件，5638013 字节。

## 发布流程

素材改完后（在本仓库工作副本里改）：

```powershell
$NODE = "C:\Users\10156\.dsh\dsh-runtimes\dsh-primary-runtime\dependencies\node\bin\node.exe"
cd A:\大肥鱼工作区\dsh-theme-holo

# 打包（默认读同级目录的 holo-tavern-assets\tavern）
& $NODE scripts\pack-tavern.mjs

# 打包 + 上传到 Release
& $NODE scripts\pack-tavern.mjs --upload

# 指定 tag
& $NODE scripts\pack-tavern.mjs --tag v1.1.0 --upload
```

**注意事项：**

1. 目标 Release 必须**已存在** —— 脚本只删同名旧附件再上传，不会新建 Release。发新 tag 要先在 GitHub 上建好 Release。
2. 包内路径固定为 `tavern/...`，因为插件端 `index.js` 的 `safeRel` 只认这个前缀，写盘时会剥掉它。
3. 上传用的 PAT 从 `A:/git密钥.txt` 读，不进仓库。
4. tar 的数字字段必须是**八进制**（`toString(8)`）。曾用十进制写过，导致 `parseInt` 遇 8 停下、只解出 1 个文件。`_test_tar.mjs` 第 7 节有回归断言。

## 版本

| tag | 内容 | 说明 |
|---|---|---|
| v1.0.0 | 62 个文件 | 旧包：素材 + 代码 + vendor 全在一起 |
| **v1.1.0** | **43 个文件** | 搬家后：只含素材，代码随插件走 |

插件端 `index.js` 的 `ASSET_URL` 指向当前使用的 tag。
