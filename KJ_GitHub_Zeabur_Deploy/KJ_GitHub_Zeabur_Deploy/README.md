# KJ / KEJAPJUDI 独立六语言部署包

原始文件 source-text (4).json 共 835 条。六种语言 en/ms/zh/vi/th/bn 各 835 条，原始 key 原样保留，不删除金额、时间、电话掩码、游戏名称或图标标识。

## GitHub 与 Zeabur
1. 解压 ZIP，可看到 `KJ_GitHub_Zeabur_Deploy` 文件夹。
2. 建立新的 GitHub 仓库，建议名称 `kj-translation-service`。将整个 `KJ_GitHub_Zeabur_Deploy` 文件夹拖到仓库根目录上传并提交；不要上传 ZIP 本身，也不要再多套一层同名文件夹。
3. Zeabur 新建独立项目，添加 GitHub 服务，选择这个仓库及 main 分支。
4. 根目录填写 `/KJ_GitHub_Zeabur_Deploy/public`。确认 Provider 为 static。不需要数据库、环境变量或 AI Dockerfile。
5. 部署完成后，在网络中生成公网域名；建议前缀 `kj-translation-service`，若已占用则换一个。端口保持服务检测到的 HTTP 8080。
6. 打开实际域名下 `/health.txt`、`/version.json`、`/translations/zh.json`，应分别显示服务提示、版本 JSON、中文语言 JSON。

如果你只把文件夹内部内容上传到仓库根目录，Zeabur 根目录应改为 `/public`。上面的默认步骤是上传整个外层文件夹。

## 后台 Loader
`KJ_Translation_Loader.txt` 是完整后台 JavaScript，使用 KJ 独立缓存及全局标识。
目前 SERVICE_URL 填的是建议地址 `https://kj-translation-service.zeabur.app`，不是已验证地址。
绑定域名后核对这一行；实际域名不同就修改为实际 HTTPS 地址，不带末尾斜杠。
复制全部代码到 KJ 后台翻译 JS 区，替换旧的翻译 Loader，其他功能代码保留。不需要额外加 script 标签。
刷新 KJ 网站，测试 EN/MS/ZH/VI/TH/BN，尤其首页、优惠详情、幸运轮盘、VIP、存款、提款和弹窗。

## 更新
以后只修改对应语言文件，并更新 public/version.json 的 version（例如 1.0.1）及 updated_at，再提交 GitHub。新版本部署后刷新网站，Loader 会检查版本并下载更新。

## 校验范围
VALIDATION.json 记录源 key 覆盖、空值、数字、品牌和重复规范化键检查。
SOURCE_COVERAGE.json 对每条原文列出六语已收录状态与中文预览。
本包尚未替你上传 GitHub 或部署 Zeabur，未完成真实网页测试。
完整覆盖指这次上传的 835 条文本；未扫描到的页面、图片内文字、跨域 iframe 或前端刻意排除的节点不能由这个 JSON 保证覆盖。

官方静态部署说明：https://zeabur.com/docs/en-US/guides/static
