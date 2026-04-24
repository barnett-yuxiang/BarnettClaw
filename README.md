## Roadmap

### 2026-04 WIP
- [ ] Keep tracking upgrades and fixing issues to maintain availability
- [x] Switch embedding provider to Gemini or Qwen

### 2026-03 Done

- [x] Metabase data pipeline
- [x] Telegram / Feishu
  - [x] 支持 PDF 文件，PDF / CSV / MD 上传后，通常也会先落到 ~/.openclaw/media/inbound/，然后进入当前 session 的 attachment/context；给一句明确指令后，再按文件类型调用对应处理链路
  - [x] 支持语音：音频转写走 `tools.media.audio`，使用 `gemini-2.5-flash-lite`。与 Whisper 这类专用 ASR 模型不同——Whisper 做的是声学特征匹配，将频谱映射到音素序列，本质是 audio → text 的 pattern matching，因此需要 `language` 参数来缩小解码搜索空间。Gemini 走的是 multimodal chat 路径，音频被 tokenize 后与文字 token 在同一个 transformer 的表示空间中联合处理，不经过独立的 ASR 步骤，而是直接从音频理解语义，因此天然支持多语言混合，无需指定语言。
  - [x] 支持图片： ~/.openclaw/media/inbound/
- [x] 记忆层改造
- [x] 监控面板
  - [x] 启动：postgresql 16.x, grafana-server, wenziday-api
  - [x] 跑通数据管线：Metabase CSV Export → ETL/清洗 → Database → 可视化层（Grafana）
- [x] Wenzday Web Site
  - [x] https
  - [x] 反向代理
    - [x] API 服务 wenzday-status，GET /api/status，返回 uptime/内存/CPU 实时信息
    - [x] 用 systemd 托管 node，不设开机自启
    - [x] Nginx 反向代理，增加了 location ^~ /api/，反代到 127.0.0.1:3001，nginx -t 和 reload 成功
