# YOLO-TXT-Label-Filter
A lightweight, browser-based tool for filtering and managing YOLO TXT annotations. Supports batch processing, label selection, and exporting filtered files. No installation required.
YOLO TXT

YOLO TXT Label Filter

A simple, browser-based tool for filtering and managing YOLO (Darknet) annotation files.

Features

Batch process hundreds of YOLO TXT annotation files.

Automatically detect and count label classes.

Filter files based on selected labels.

Keep additional labels within matching files.

Preview filtering results before processing.

Export filtered annotations as a ZIP file.

Runs locally without Python installation or internet access.

How to Use

Open YOLO_TXT_篩選工具.html in your browser.

Select a folder containing YOLO TXT annotation files.

Choose the labels you want to filter by.

Optionally select additional labels to keep.

Preview the results and export the filtered files.

Example

If you select mod as the primary label and person as an additional label, the tool will only keep files containing mod, while preserving both mod and person annotations within those files.

Technology

HTML, CSS, JavaScript — No installation required.

Privacy

All processing is performed locally in your browser. No files are uploaded to external servers.


類別篩選工具
=================================

【新增功能】
可以區分「主要 Label」與「附帶保留 Label」。
主要 Label：只要一份 TXT 包含其中任一主要 Label，就保留該 TXT。
附帶 Label：只決定保留 TXT 內另外留下哪些標註行，不會讓更多檔案通過篩選。

【操作】
1. 用 Microsoft Edge 或 Chrome 雙擊開啟「YOLO_TXT_篩選工具.html」。
   也可雙擊「啟動工具.bat」。不需安裝 Python、啟動伺服器或連線。
2. 點「選擇整個資料夾」；若瀏覽器不支援，改選「相容模式：讀取資料夾」。
3. 在「主要 Label」勾選要用來篩選 TXT 的類別，例如 mod (ID 4)。
4. 在「附帶保留其他 Label」選擇：
   - 只保留主要 Label：只保留 mod 標註行（相容舊版行為）。
   - 指定要附帶保留的 Label：再勾選 person (ID 0)，只保留 mod/person。
   - 保留所有其他 Label：符合 mod 條件的 TXT 中原本有什麼 Label 就全保留。
5. 按「預覽篩選結果」，檢查保留檔案與移除標註行數量。
6. 建議先用「安全模式」下載篩選 ZIP，驗證正確後再評估直接修改模式。

【例子】
若主要 Label = mod (ID 4)，附帶 Label = person (ID 0)：
- 影格中有 mod、person、helmet：保留該 TXT，只留下 mod/person 的行。
- 影格中有 mod、helmet：保留該 TXT，只留下 mod 的行。
- 影格中只有 person、helmet：整個 TXT 排除，即使 person 是附帶 Label 也一樣。

【關於原始資料】
- 只需要 TXT，不需要圖片。TXT 檔名可以是影格編號。
- 若用安全模式，原始 TXT 完全不會被修改。
- 若用直接修改模式，會先在來源資料夾內建立
  _YOLO_label_backup_時間_亂數 的子資料夾，備份並驗證所有原始 TXT，
  確認完成後才刪除不符合主要 Label 的檔案及修改保留檔案內容。
- 可掃描子資料夾中的 TXT，自動跳過本工具產生的備份子資料夾。
- 預設採 darklabel.yml 中 format1 使用的 ppe_classes_4class：
  0 person, 1 pack, 2 helmet, 3 mask, 4 mod。
- 如資料夾中有格式不符標準 YOLO 五欄的 TXT，會停止並報錯，防止誤刪。
- 工具純前端、離線，不會將資料送到雲端。
