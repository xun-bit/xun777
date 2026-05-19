# FitSwap 换衣工作台

一个可本地运行的换衣应用 MVP：上传本人图片和服装图片，点击“一键换衣”调用 OpenAI 图像编辑接口生成试穿预览并下载结果。后端会把两张本地图片以 multipart 方式上传给图像编辑接口。

## 运行

方式一：复制 `.env.example` 为 `.env`，填入你的 API Key：

```text
OPENAI_API_KEY=你的 OpenAI API Key
```

方式二：在 PowerShell 当前窗口设置 API Key：

```powershell
$env:OPENAI_API_KEY="你的 OpenAI API Key"
```

启动本地服务：

```powershell
node server.js
```

然后访问 `http://localhost:5173`。

## 软件模式

项目已经加了 Electron 桌面外壳：

```powershell
cmd /c npm install
cmd /c npm run desktop
```

打包 Windows 安装包：

```powershell
cmd /c npm run build:win
```

如果 PowerShell 直接运行 `npm` 报执行策略错误，请继续使用 `cmd /c npm ...`。

安装版会把 API Key 保存到系统的用户应用数据目录，不会写到安装目录。

## 配置

可选环境变量：

- `OPENAI_IMAGE_MODEL`：默认 `gpt-image-2`
- `OPENAI_IMAGE_QUALITY`：默认 `medium`
- `AI_PROVIDER`：默认 `openai`，可改成 `fal` 使用 fal.ai，或改成 `demo` 使用本地免费演示预览
- `FAL_KEY`：`AI_PROVIDER=fal` 时必填
- `FAL_ENDPOINT`：默认 `fal-ai/kling/v1-5/kolors-virtual-try-on`
- `DASHSCOPE_API_KEY`：`AI_PROVIDER=aliyun` 时必填，使用阿里云百炼 API Key
- `ALIYUN_TRYON_MODEL`：默认 `aitryon`
- `ALIYUN_TRYON_RESOLUTION`：默认 `-1`，保持与原图尺寸一致
- `PORT`：默认 `5173`

建议正式上线前增加用户授权、内容审核、图片自动删除策略、用量限制和隐私提示。
