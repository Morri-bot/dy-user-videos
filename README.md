# dy-user-videos · 抖音用户作品查询

输入抖音链接，查看作者全部作品，翻页浏览，一键导出 Excel。

---

## ⚡ 快速开始

1. 将 `dy-user-videos/` 文件夹复制到项目的 `.agents/skills/` 下
2. 复制 `config.example.json` 为 `config.json`
3. 填 `douyin.apikey`（从 [www.rockmoons.com](https://www.rockmoons.com) 获取）
4. 发抖音链接 → 返回作者作品列表

---

## 📋 支持的输入

| 输入 | 示例 |
|------|------|
| 视频链接 | `https://www.douyin.com/video/xxx` |
| 用户主页链接 | `https://www.douyin.com/user/xxx` |
| sec_user_id | `MS4wLjABAAAA...` |

---

## 🎯 功能

- 查看作品列表（翻页浏览）
- 点某条看完整详情（含时长）
- 一键导出 Excel（断点续传）

---

## 💬 示例

```
用户：https://www.douyin.com/video/xxx
模型：📱 小熙宅剧 · 455个作品 · 225万赞 [列表]
      💡 下一页 | 查第3个看详情 | 导出

用户：下一页
模型：[第2页]

用户：导出
模型：✅ D:\xxx\dy_user_videos_小熙宅剧_20260714.xlsx
```

---

## ⚙️ 配置

```json
{
  "douyin": { "apikey": "你的APIKey" },
  "pagination": { "default_count": 20 }
}
```

---

## 🔌 APIKey

访问 [www.rockmoons.com](https://www.rockmoons.com) 注册获取。

---

## 📞 作者

阿南 rockmoons（抖音）· 微信 rockmoons
