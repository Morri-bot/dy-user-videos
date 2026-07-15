# Excel 导出

用 API 03 数据导出，不逐条调 API 01（省积分省时间）。

---

## 表头（18 列）

```
序号 | 作品ID | 作品简介 | 作品标题 | 点赞数 | 评论数 | 分享数 | 收藏数 | 播放数 | 转发数 | 下载数 | 推荐数 | 视频话题 | 创建时间 | 分享链接 | 视频链接 | 音频链接 | 作品封面
```

全部从 API 03 的 `metadata.fields` 直接取值。

---

## 前置检查

```bash
pip show openpyxl || pip install openpyxl
```

---

## 生成流程

```python
from openpyxl import Workbook
from datetime import datetime

wb = Workbook()
ws = wb.active
ws.title = "作者作品"

headers = ["序号","作品ID","作品简介","作品标题","点赞数","评论数","分享数","收藏数","播放数","转发数","下载数","推荐数","视频话题","创建时间","分享链接","视频链接","音频链接","作品封面"]
ws.append(headers)

# 逐页拉取，每页完成即写入（断点续传）
for page in pages:
    for i, record in enumerate(page):
        fields = json.loads(record['fields'])
        row = [start_num + i] + [fields.get(h, "") for h in headers[1:]]
        ws.append(row)

filename = f"dy_user_videos_{author_name}_{datetime.now().strftime('%Y%m%d')}.xlsx"
wb.save(filename)
```

---

## 格式规则

- 点赞/评论/收藏等数字列：千分位格式
- 链接列：HYPERLINK 公式
- 创建时间：Unix 秒 → 北京时间 `YYYY-MM-DD HH:MM:SS`

---

## 断点续传

每页完成即写入 Excel，中途失败不丢数据。用户说「继续导出」从断点继续。

---

## 完成提示

```
✅ 文件在这里，双击打开：
   D:\xxx\dy_user_videos_{作者名}_{日期}.xlsx
💡 需要时长？说「查第N个」看完整详情
```
