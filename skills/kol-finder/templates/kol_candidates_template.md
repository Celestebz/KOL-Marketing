# KOL Candidates XLSX Template

Copy this structure when creating a new KOL candidates spreadsheet.

## Sheet Structure

**Sheet Name:** `KOL候选人`

## Column Headers

| Column | Example |
|---|---|
| 合作产品 | AI Notetaker Pro |
| 频道名称 | Tech Review Hub |
| 联系人 | John Smith |
| YouTube链接 | https://youtube.com/@techreviewhub |
| YouTube 粉丝量 | 150000 |
| Instagram链接 | https://instagram.com/techreviewhub |
| Instagram 粉丝量 | 45000 |
| Email | contact@techreviewhub.com |
| 国家地区 | US / English |
| 推荐理由 | Covers AI tools, strong engagement, aligns with premium positioning |

## Creating XLSX with Python

```python
from openpyxl import Workbook
from openpyxl.styles import Font, Alignment, PatternFill, Border, Side

wb = Workbook()
ws = wb.active
ws.title = "KOL候选人"

headers = [
    "合作产品",
    "频道名称",
    "联系人",
    "YouTube链接",
    "YouTube 粉丝量",
    "Instagram链接",
    "Instagram 粉丝量",
    "Email",
    "国家地区",
    "推荐理由"
]

header_fill = PatternFill(start_color="4472C4", end_color="4472C4", fill_type="solid")
header_font = Font(bold=True, color="FFFFFF")
thin_border = Border(
    left=Side(style='thin'),
    right=Side(style='thin'),
    top=Side(style='thin'),
    bottom=Side(style='thin')
)

for col, header in enumerate(headers, 1):
    cell = ws.cell(row=1, column=col, value=header)
    cell.fill = header_fill
    cell.font = header_font
    cell.alignment = Alignment(horizontal='center', vertical='center')
    cell.border = thin_border
    ws.column_dimensions[cell.column_letter].width = 20

wb.save("kol_candidates_template.xlsx")
```

## Creating XLSX with JavaScript (ExcelJS)

```javascript
const ExcelJS = require('exceljs');

const workbook = new ExcelJS.Workbook();
const worksheet = workbook.addSheet('KOL候选人');

const headers = [
    "合作产品",
    "频道名称",
    "联系人",
    "YouTube链接",
    "YouTube 粉丝量",
    "Instagram链接",
    "Instagram 粉丝量",
    "Email",
    "国家地区",
    "推荐理由"
];

worksheet.addRow(headers);
worksheet.getRow(1).eachCell(cell => {
    cell.fill = { type: 'pattern', pattern: 'solid', fgColor: { argb: 'FF4472C4' } };
    cell.font = { bold: true, color: { argb: 'FFFFFFFF' } };
    cell.alignment = { horizontal: 'center' };
});

await workbook.xlsx.writeFile('kol_candidates_template.xlsx');
```

## Notes

- YouTube 粉丝量 and Instagram 粉丝量 columns should contain numeric values only (no commas).
- URLs should be full links including https://
- Use separate rows for each platform if a creator is active on multiple platforms, or combine in one row with both URLs.
