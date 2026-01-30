---
name: legco-hk-search
description: Query Hong Kong Legislative Council (LegCo) Open Data APIs for voting results, bills, meeting schedules, questions, hansard records, attendance records, reference briefs, subsidiary legislation, and historical archives. Supports Traditional Chinese and English.
license: MIT
metadata:
  author: opencode
  version: "1.0"
---

# LegCo HK Open Data Search

Search and retrieve data from the Hong Kong Legislative Council's Open Data APIs. Supports Traditional Chinese and English.

## Language Support

### Traditional Chinese (繁體中文)
- **Native support** - All LegCo APIs provide Traditional Chinese fields
- Field names typically end with `_chi`, `_chinese`, or `_ch`
- Example: `bill_title_chi`, `meeting_name_chinese`, `name_ch`

### English
- **Native support** - All LegCo APIs provide English fields
- Field names typically end with `_eng`, `_english`, or `_en`
- Example: `bill_title_eng`, `meeting_name_english`, `name_en`
- Separate endpoints available for Questions API (ViewOralQuestionsEng, ViewWrittenQuestionsEng)

## When to use this skill

Use this skill when the user needs to:
- Search for voting results from Council meetings, House Committee, Finance Committee, or subcommittees
- Find information about bills (法案) processed by LegCo
- Query meeting schedules for Council and committee meetings
- Search for oral or written questions asked by members
- Retrieve hansard records (meeting proceedings)
- Check attendance records for meetings
- Access legislative reference briefs (參考資料摘要) on policy issues
- Browse historical archives from previous Legislative Council terms (1997 onwards)
- Find subsidiary legislation (規例/附屬法例) such as traffic regulations, fee schedules

### Quick API Reference

| If you need... | Use this API | Coverage |
|----------------|--------------|----------|
| Voting records | Voting Results Database | 5th term (2012) onwards |
| Bill information | Bills Database | 1844 onwards |
| Meeting schedules | Meeting Schedule Database | 5th term (2012) onwards |
| Questions asked | Questions Database | 5th term (2012) onwards |
| Meeting transcripts | Hansard Database | 6th term (2016) onwards |
| Attendance records | Attendance Database | 6th term (2016) onwards |
| Reference briefs | Legislative Library Database (web) | 1998 onwards |
| Subsidiary legislation | Subsidiary Legislation Archive (PDF) | 2000+ (varies by term) |
| Historical documents | Historical Archive Page (web) | 1997 onwards |

### API vs Web Interface

| Type | Resources | Access Method |
|------|-----------|---------------|
| **OData APIs** (curl-able) | Voting Results, Bills, Schedule, Questions, Hansard, Attendance | Direct HTTP requests with curl or any HTTP client. Returns JSON/XML data. |
| **Web Interfaces** (requires scraping) | Legislative Library Database, Historical Archives | JavaScript-heavy web apps or HTML pages. Requires browser automation or web scraping tools. |

## Available APIs

### 1. Voting Results Database (投票結果資料庫)
Base URL: `https://app.legco.gov.hk/vrdb/odata/vVotingResult`

**Coverage:** 5th term (2012) onwards  
**Data:** Council meetings, House Committee, Finance Committee, Establishment Subcommittee, Public Works Subcommittee voting records

**Meeting Types:**
- `Council Meeting` - 立法會會議
- `House Committee` - 內務委員會
- `Finance Committee` - 財務委員會
- `Establishment Subcommittee` - 人事編制小組委員會
- `Public Works Subcommittee` - 工務小組委員會

**Language Fields:**
- Chinese: `motion_ch`, `name_ch`
- English: `motion_en`, `name_en`

**Metadata:** https://app.legco.gov.hk/vrdb/odata/$metadata

---

### 2. Bills Database (法案資料庫)
Base URL: `https://app.legco.gov.hk/BillsDB/odata/Vbills`

**Coverage:** 1844 onwards (all LegCo/Legislative Council bills)  
**Data:** Bill titles, gazette dates, committee documents, reports, meeting discussion links

**Warning:** Full dataset exceeds 15MB - use pagination ($top, $skip)

**Language Fields:**
- Chinese: `bill_title_chi`
- English: `bill_title_eng`

**Metadata:** https://app.legco.gov.hk/BillsDB/odata/$metadata

---

### 3. Meeting Schedule Database (會議時間表)
Base URLs:
- Terms: `https://app.legco.gov.hk/ScheduleDB/odata/Tterm`
- Sessions: `https://app.legco.gov.hk/ScheduleDB/odata/Tsession`
- Committees: `https://app.legco.gov.hk/ScheduleDB/odata/Tcommittee`
- Memberships: `https://app.legco.gov.hk/ScheduleDB/odata/Tmembership`
- Members: `https://app.legco.gov.hk/ScheduleDB/odata/Tmember`
- Member Terms: `https://app.legco.gov.hk/ScheduleDB/odata/Tmember_term`
- Meetings: `https://app.legco.gov.hk/ScheduleDB/odata/Tmeeting`
- Meeting Committees: `https://app.legco.gov.hk/ScheduleDB/odata/Tmeeting_committee`

**Coverage:** 5th term (2012) onwards  
**Data:** Council and committee meeting schedules with links to agendas

**Language Fields:**
- Chinese: `subject_chi`, `surname_chi`, `firstname_chi`, `post_chi`, `venue_name_chi`, `agenda_url_chi`, `meeting_name_chinese`, `member_name_chinese`
- English: `subject_eng`, `surname_eng`, `firstname_eng`, `post_eng`, `venue_name_eng`, `agenda_url_eng`, `meeting_name_english`, `member_name_english`

**Metadata:** https://app.legco.gov.hk/ScheduleDB/odata/$metadata

---

### 4. Questions Database (立法會會議質詢)
Base URLs:
- Oral Questions (Chinese): `https://app.legco.gov.hk/QuestionsDB/odata/ViewOralQuestionsChi`
- Written Questions (Chinese): `https://app.legco.gov.hk/QuestionsDB/odata/ViewWrittenQuestionsChi`
- Oral Questions (English): `https://app.legco.gov.hk/QuestionsDB/odata/ViewOralQuestionsEng`
- Written Questions (English): `https://app.legco.gov.hk/QuestionsDB/odata/ViewWrittenQuestionsEng`

**Coverage:** 5th term (2012) onwards  
**Data:** Question titles, asking members, links to Hansard records

**Note:** Use separate endpoints for Chinese vs English. Chinese endpoints provide Traditional Chinese only.

**Language Fields:**
- Chinese: `SubjectName`, `MemberName` (Traditional Chinese only)
- English: `SubjectName`, `MemberName`

**Metadata:** https://app.legco.gov.hk/QuestionsDB/odata/$metadata

---

### 5. Hansard Database (會議過程正式紀錄資料庫)
Base URLs:
- Hansard: `https://app.legco.gov.hk/OpenData/HansardDB/Hansard`
- Sections: `https://app.legco.gov.hk/OpenData/HansardDB/Sections`
- Subjects: `https://app.legco.gov.hk/OpenData/HansardDB/Subjects`
- Rundown: `https://app.legco.gov.hk/OpenData/HansardDB/Rundown`
- Speakers: `https://app.legco.gov.hk/OpenData/HansardDB/Speakers`
- Questions: `https://app.legco.gov.hk/OpenData/HansardDB/Questions`
- Bills: `https://app.legco.gov.hk/OpenData/HansardDB/Bills`
- Motions: `https://app.legco.gov.hk/OpenData/HansardDB/Motions`
- Petitions: `https://app.legco.gov.hk/OpenData/HansardDB/Petitions`
- Addresses: `https://app.legco.gov.hk/OpenData/HansardDB/Addresses`
- Statements: `https://app.legco.gov.hk/OpenData/HansardDB/Statements`
- Voting Results: `https://app.legco.gov.hk/OpenData/HansardDB/VotingResults`
- Summoning Bells: `https://app.legco.gov.hk/OpenData/HansardDB/SummoningBells`

**Coverage:** 6th term (2016) onwards  
**Data:** Meeting proceedings, speeches, questions, bills, motions, voting results, quorum bells

**Language Fields:**
- Filter by `HansardType eq 'Chinese'` (Traditional) or `HansardType eq 'English'`
- **Hansard table fields:** `MeetingDate`, `HansardType`, `HansardFileURL`
- **Questions table fields:** `MeetingDate`, `Subject`, `Speaker`, `HansardFileURL`
- **Motions table fields:** `MeetingDate`, `Subject`, `HansardFileURL`
- **Bills table fields:** `MeetingDate`, `Subject`, `HansardFileURL`

**Note:** Different Hansard endpoints use different field names. Check metadata for exact field names.

**Metadata:** https://app.legco.gov.hk/OpenData/HansardDB/$metadata

---

### 6. Attendance Database (出席會議紀錄)
Base URL: `https://app.legco.gov.hk/OpenData/AttendanceDB/TAttendance`

**Coverage:** 6th term (2016) onwards  
**Data:** Member attendance records for Council and committee public meetings

**Language Fields:**
- Chinese: `meeting_name_chinese`, `member_name_chinese`
- English: `meeting_name_english`, `member_name_english`

**Metadata:** https://app.legco.gov.hk/OpenData/AttendanceDB/$metadata

---

### 7. Legislative Library Database (LBDB) - Reference Briefs (立法會參考資料摘要資料庫)
Web Interface:
- Traditional Chinese: `https://app7.legco.gov.hk/lbdb/tc/`
- English: `https://app7.legco.gov.hk/lbdb/en/`

**Coverage:** 1998 onwards (all Legislative Council terms from 1st to 8th)
**Data:** Legislative Council reference briefs (參考資料摘要) on various policy issues and legislative matters

**Note:** This is a **web-based search interface** (not an OData API). It loads data dynamically via JavaScript and cannot be accessed directly via curl. Use browser automation or web scraping tools to extract data programmatically.

**Searchable Fields:**
- **內文/Content** - Full text search (options: contains/exact match)
- **題目/Title** - Document title
- **參考編號/Reference Number** - Document reference code
- **相關作者/Related Authors** - Government bureaus/departments or other organizations
- **主題/Topics** - Subject categories
- **發出日期/Issue Date** - Date range filter

**Data Structure:**
Each brief includes:
- Issue date
- Title
- Reference number (e.g., MPF/2/1/47C)
- Authoring organization(s)
- Brief description/extract
- Topic tags
- Download link (PDF)

**Example Usage:**
1. Visit the web interface URL
2. Enter search terms in appropriate fields
3. Filter by date range if needed
4. Sort results by date or title
5. Click on results to view/download PDF documents

---

### 8. Subsidiary Legislation Database (附屬法例)

**Important Note:** Subsidiary legislation (regulations/rules made under ordinances) are **NOT** in the Bills Database. They are separate documents.

**Archive URLs:**
- Current (7th term onwards): `https://www.legco.gov.hk/tc/legco-business/council/subsidiary-legislation.html`
- Historical archives: `https://www.legco.gov.hk/tc/general/archive.html` → Select term → "附屬法例"

**Accessing Subsidiary Legislation PDFs:**

The direct PDF URLs follow a pattern:
```
https://www.legco.gov.hk/yr{YEAR}/chinese/subleg/{TYPE}/{LAW_GAZETTE_NO}-c.pdf
```

**Example:**
- 《2025年道路交通（安全裝備）（修訂）規例》
- URL: `https://www.legco.gov.hk/yr2025/chinese/subleg/negative/2025ln195-c.pdf`

**Key Differences:**

| Type | Bills Database | Subsidiary Legislation |
|------|----------------|----------------------|
| **中文名稱** | 法案/條例草案 | 規例/規則/附屬法例 |
| **English Name** | Bills/Ordinances | Regulations/Rules/Subsidiary Legislation |
| **Legislative Process** | First reading → Second reading → Committee → Third reading | Gazette → Negative vetting (28 days) |
| **API Available** | ✅ Yes (BillsDB) | ❌ No - PDF only |
| **Format** | JSON via OData | PDF documents |
| **Coverage** | 1844 onwards | Varies by term (2000+ in archives) |

**When to Check Subsidiary Legislation:**
- Traffic regulations (道路交通規例)
- Fee schedules (收費規例)
- Licensing rules (牌照規則)
- Any "修訂規例" mentioned in reference briefs

**Searching for Subsidiary Legislation:**
1. Use the LBDB (Legislative Library Database) to find reference briefs about the topic
2. Look for "附屬法例" or "規例" in the brief
3. Access PDFs directly via the archive URLs
4. Extract text from PDFs using the tools documented below

---

## OData Query Options

All APIs support standard OData query parameters:

| Parameter | Description | Example |
|-----------|-------------|---------|
| `$format` | Response format (json/xml) | `$format=json` |
| `$top=N` | Return first N records | `$top=20` |
| `$skip=N` | Skip first N records | `$skip=100` |
| `$orderby` | Sort results | `$orderby=MeetingDate desc` |
| `$select` | Select specific fields | `$select=MeetingDate,Subject` |
| `$filter` | Filter results | `$filter=year(MeetingDate) eq 2024` |
| `$inlinecount=allpages` | Include total count | `$inlinecount=allpages` |
| `$expand` | Expand related data | `$expand=Tmembership/Tmember` |

### Common Filter Operators

- `eq` - Equal to: `year(MeetingDate) eq 2024`
- `gt/ge/lt/le` - Greater than, greater/equal, less than, less/equal
- `and/or` - Logical operators
- `substringof('text',field)` - Contains text (URL-encode Chinese characters)

### Term Date Ranges

| Term | Period | Filter |
|------|--------|--------|
| 8th | 2026-2030 | `datetime'2026-01-01'` to `datetime'2030-01-01'` |
| 7th | 2022-2026 | `datetime'2022-01-01'` to `datetime'2026-01-01'` |
| 6th | 2016-2022 | `datetime'2016-10-01'` to `datetime'2022-01-01'` |
| 5th | 2012-2016 | `datetime'2012-10-01'` to `datetime'2016-10-01'` |

**Important:** URL-encode Chinese characters when used in filters.

**Example:** `選舉` → `%E9%81%B8%E8%88%89`

---

## Examples

### Example 1: Search voting results by member (Bilingual)

Query voting records for a specific member during the 7th term:

**Traditional Chinese:**
```
GET https://app.legco.gov.hk/vrdb/odata/vVotingResult?$format=json&$select=motion_ch,name_ch,vote,vote_time&$filter=type eq 'Council Meeting' and term_no eq 7 and substringof('%E6%9B%BE%E9%88%BA%E6%88%90', name_ch) eq true&$orderby=vote_time desc
```

**English:**
```
GET https://app.legco.gov.hk/vrdb/odata/vVotingResult?$format=json&$select=motion_en,name_en,vote,vote_time&$filter=type eq 'Council Meeting' and term_no eq 7 and substringof('TSANG', name_en) eq true&$orderby=vote_time desc
```

### Example 2: Find bills by keyword (Bilingual)

Search for bills with titles containing "選舉" (election) or "election":

**Traditional Chinese:**
```
GET https://app.legco.gov.hk/BillsDB/odata/Vbills?$format=json&$inlinecount=allpages&$filter=substringof('%E9%81%B8%E8%88%89',bill_title_chi) eq true&$select=bill_title_chi,bill_gazette_date
```

**English:**
```
GET https://app.legco.gov.hk/BillsDB/odata/Vbills?$format=json&$inlinecount=allpages&$filter=substringof('election',bill_title_eng) eq true&$select=bill_title_eng,bill_gazette_date
```

### Example 3: Get meeting schedule for a committee (Bilingual)

Get meetings for a specific committee:

**Traditional Chinese:**
```
GET https://app.legco.gov.hk/ScheduleDB/odata/Tmeeting?$format=json&$filter=substringof('%E4%BA%BA%E5%8A%9B%E4%BA%8B%E5%8B%99%E5%A7%94%E5%93%A1%E6%9C%83',subject_chi) eq true&$select=subject_chi,start_date_time,venue_name_chi,agenda_url_chi&$orderby=start_date_time
```

**English:**
```
GET https://app.legco.gov.hk/ScheduleDB/odata/Tmeeting?$format=json&$filter=substringof('Panel on Manpower',subject_eng) eq true&$select=subject_eng,start_date_time,venue_name_eng,agenda_url_eng&$orderby=start_date_time
```

### Example 4: Search questions (Language-specific endpoints)

Find written questions by a specific member:

**Traditional Chinese:**
```
GET https://app.legco.gov.hk/QuestionsDB/odata/ViewWrittenQuestionsChi?$format=json&$inlinecount=allpages&$filter=substringof('%E6%9E%97%E5%A4%A7%E8%BC%9D',MemberName) eq true
```

**English:**
```
GET https://app.legco.gov.hk/QuestionsDB/odata/ViewWrittenQuestionsEng?$format=json&$inlinecount=allpages&$filter=substringof('LAM Tai-fai',MemberName) eq true
```

### Example 5: Search Hansard Questions (Bilingual)

Search for questions about seat belts in Hansard:

**Traditional Chinese:**
```
GET https://app.legco.gov.hk/OpenData/HansardDB/Questions?$format=json&$filter=substringof('%E5%AE%89%E5%85%A8%E5%B8%B6',Subject) eq true and HansardType eq 'Chinese'&$select=MeetingDate,Subject,Speaker&$top=10
```

**English:**
```
GET https://app.legco.gov.hk/OpenData/HansardDB/Questions?$format=json&$filter=substringof('seat belt',Subject) eq true and HansardType eq 'English'&$select=MeetingDate,Subject,Speaker&$top=10
```

**Note:** Different Hansard endpoints (Questions, Motions, Bills, etc.) may have different field structures. Use the metadata endpoint to verify available fields.

### Example 6: Check attendance for a member (Bilingual)

Query attendance records for a member:

**Traditional Chinese:**
```
GET https://app.legco.gov.hk/OpenData/AttendanceDB/TAttendance?$format=json&$inlinecount=allpages&$filter=substringof('%E7%9F%B3%E7%A6%AE%E8%AC%99',member_name_chinese) eq true and meeting_start_date_time ge datetime'2024-01-01' and meeting_start_date_time lt datetime'2024-02-01'&$orderby=meeting_start_date_time&$select=meeting_start_date_time,meeting_name_chinese,member_name_chinese,present_absent
```

**English:**
```
GET https://app.legco.gov.hk/OpenData/AttendanceDB/TAttendance?$format=json&$inlinecount=allpages&$filter=substringof('Abraham SHEK',member_name_english) eq true and meeting_start_date_time ge datetime'2024-01-01' and meeting_start_date_time lt datetime'2024-02-01'&$orderby=meeting_start_date_time&$select=meeting_start_date_time,meeting_name_english,member_name_english,present_absent
```

---

## Best practices

- **Always URL-encode Chinese characters** in query parameters (UTF-8 encoding)
- **Use pagination** ($top, $skip) for large datasets to avoid timeouts
- **Use $select** to limit fields and reduce response size - select appropriate language fields
- **Use $filter** with date ranges to narrow results
- **Add $inlinecount=allpages** when you need the total record count
- **Check metadata** endpoints to understand available fields and data types
- **Start with $top=10** to test queries before retrieving full datasets
- **Use datetime format** for date comparisons: `datetime'YYYY-MM-DD'`
- **For Chinese searches:** Use shorter, common terms (e.g., "安全帶" rather than "座位安全帶") as LegCo typically uses concise terminology
- **For bilingual results:** Query both `_chi` and `_eng` fields or make separate requests
- **Check field names:** Different endpoints within the same API may use different field names (e.g., Hansard Questions uses `Subject`, not `SubjectName`)

---

## Error Handling

### Common HTTP Status Codes

| Status | Meaning | Solution |
|--------|---------|----------|
| `400 Bad Request` | Invalid query syntax | Check filter syntax (e.g., `eq` not `=`, proper datetime format) |
| `404 Not Found` | Endpoint doesn't exist | Verify the API base URL and endpoint name |
| `500 Internal Server Error` | Server issue | Retry after a few minutes; report persistent issues to enquiry@legco.gov.hk |

### Troubleshooting Tips

- **Empty results**: Try broadening your filter (e.g., remove date restrictions) or check that the URL-encoded Chinese characters are correct
- **Timeout errors**: Use pagination (`$top`, `$skip`) to retrieve data in smaller chunks
- **Wrong language**: Verify you're using the correct field suffix (`_chi` for Traditional Chinese, `_eng` for English)
- **Invalid dates**: Ensure datetime format is `datetime'YYYY-MM-DD'` with single quotes

---

## Historical Archive Documents

For historical LegCo documents not available through the OData APIs, access the **Historical Archive Page** (昔日議會文件):

**URL:** https://www.legco.gov.hk/tc/general/archive.html

### Coverage

| Term | Period | Available Content |
|------|--------|-------------------|
| 8th | 2026-2030 | Member profiles, meetings, committees, bills, rulings, subsidiary legislation |
| 7th | 2022-2026 | Same as above |
| 6th | 2016-2022 | Same as above |
| 5th | 2012-2016 | Same as above |
| 4th | 2008-2012 | Member list, meetings, committees, bills, rulings, subsidiary legislation |
| 3rd | 2004-2008 | Same as above |
| 2nd | 2000-2004 | Same as above |
| 1st | 1998-2000 | Same as above |
| Provisional | 1997-1998 | Member list, PLC meetings, committees, bills, rulings, annual reports |
| Pre-1997 | Before 1997 | Legislative Council meetings, committees, rulings |

### Available Document Types

- **議員履歷/議員名單** - Member biographies and profiles
- **立法會會議** - Council meeting records and hansard
- **委員會** - Committee documents and reports
- **法案** - Bills and legislative proposals
- **主席裁決** - President's rulings on procedural matters
- **附屬法例** - Subsidiary legislation
- **其他法律文書** - Other legal instruments
- **訪問活動** - Visit reports (local and overseas)
- **年報** - Annual reports

### How to Use

1. Navigate to the archive page
2. Select the desired Legislative Council term
3. Click on the document type link
4. Browse or search within the specific term's archive

**Note:** These are **HTML-based archives**, not OData APIs. They return web pages with HTML/JavaScript content and cannot be accessed directly via curl for structured data. Use browser automation or web scraping tools to extract data programmatically.

---

## Working with PDF Documents

Many LegCo documents, especially from the Legislative Library Database (LBDB), are available as PDFs. Here's how to work with them programmatically.

### Downloading PDFs

PDFs from LBDB can be downloaded via direct URLs:

```
https://app7.legco.gov.hk/lbdb/tc/file.aspx?id={FILE_ID}&lang=tc
```

**Example workflow:**
1. Use browser automation to extract PDF URLs from LBDB search results
2. Download PDFs using HTTP requests
3. Extract text/content for analysis

### PDF Text Extraction Tools

#### Python

**pdfplumber** (Recommended for structured text)
```python
import pdfplumber

with pdfplumber.open('document.pdf') as pdf:
    text = "\n".join(page.extract_text() for page in pdf.pages if page.extract_text())
```

**PyPDF2** (Lightweight, simple extraction)
```python
from PyPDF2 import PdfReader

reader = PdfReader('document.pdf')
text = "\n".join(page.extract_text() for page in reader.pages)
```

**pymupdf (fitz)** (Fast, good for complex layouts)
```python
import fitz  # PyMuPDF

doc = fitz.open('document.pdf')
text = "\n".join(page.get_text() for page in doc)
```

#### Node.js

**pdf-parse**
```javascript
const pdfParse = require('pdf-parse');
const fs = require('fs');

const data = await pdfParse(fs.readFileSync('document.pdf'));
console.log(data.text);
```

#### CLI Tools

**pdftotext** (Poppler utilities)
```bash
pdftotext document.pdf output.txt
```

**pdf2txt.py** (pdfminer.six - most accurate for Chinese)
```bash
pip install pdfminer.six
pdf2txt.py document.pdf > output.txt
```

**pdftoppm** (Convert PDF to images for OCR)
```bash
pdftoppm -png document.pdf output_prefix
```

### PDF to Text Conversion Examples

#### Method 1: pdf2txt.py (Best for text-based PDFs)
```bash
# Basic extraction
pdf2txt.py input.pdf > output.txt

# With layout preservation
pdf2txt.py -t text input.pdf > output.txt

# Extract from specific pages
pdf2txt.py -p 1,5,10 input.pdf > output.txt

# Output as HTML (preserves formatting)
pdf2txt.py -t html input.pdf > output.html
```

#### Method 2: Python with pdfminer.six
```python
from pdfminer.high_level import extract_text

# Extract all text
text = extract_text('document.pdf')

# Extract specific pages
text = extract_text('document.pdf', page_numbers=[0, 1, 2])

# Extract with layout analysis
from pdfminer.layout import LAParams
text = extract_text('document.pdf', laparams=LAParams())

# Save to file
with open('output.txt', 'w', encoding='utf-8') as f:
    f.write(text)
```

#### Method 3: OCR for Scanned PDFs
```python
# Convert PDF to images, then OCR
from pdf2image import convert_from_path
import pytesseract

images = convert_from_path('scanned_document.pdf')
text = ""
for image in images:
    text += pytesseract.image_to_string(image, lang='chi_sim+eng')

with open('output.txt', 'w', encoding='utf-8') as f:
    f.write(text)
```

### Searching Extracted Text

After extracting text from PDFs, you can search programmatically:

```python
# Load extracted text
with open('output.txt', 'r', encoding='utf-8') as f:
    content = f.read()

# Simple keyword search
if 'seat belt' in content.lower():
    print("Document mentions seat belts")

# Regex search for specific patterns
import re
# Find all dates
matches = re.findall(r'\d{4}年\d{1,2}月\d{1,2}日', content)

# Find citations
matches = re.findall(r'第\d+章', content)

# Context search - find sentences containing keywords
import re
keyword = '安全帶'
pattern = rf'[^。]*{keyword}[^。]*。'
matches = re.findall(pattern, content)
for match in matches:
    print(match)
```

### Batch Processing Multiple PDFs

```python
import os
from pdfminer.high_level import extract_text

pdf_dir = './legco_pdfs/'
output_dir = './extracted_text/'

for filename in os.listdir(pdf_dir):
    if filename.endswith('.pdf'):
        pdf_path = os.path.join(pdf_dir, filename)
        text = extract_text(pdf_path)
        
        output_filename = filename.replace('.pdf', '.txt')
        output_path = os.path.join(output_dir, output_filename)
        
        with open(output_path, 'w', encoding='utf-8') as f:
            f.write(text)
        
        print(f"Processed: {filename}")
```

### Example: Full Workflow

Download and extract text from an LBDB reference brief:

```python
import requests
import pdfplumber
import io

# Step 1: Download PDF
url = "https://app7.legco.gov.hk/lbdb/tc/file.aspx?id=FILE_ID&lang=tc"
response = requests.get(url)
pdf_bytes = io.BytesIO(response.content)

# Step 2: Extract text
with pdfplumber.open(pdf_bytes) as pdf:
    full_text = "\n".join(
        page.extract_text() for page in pdf.pages if page.extract_text()
    )

# Step 3: Search within extracted text
if "安全帶" in full_text:
    print("Document mentions seat belts")
```

### Example: Extracting Subsidiary Legislation

Download and extract text from a subsidiary legislation PDF:

```python
import requests
from pdfminer.high_level import extract_text
import io

# Example: 《2025年道路交通（安全裝備）（修訂）規例》
pdf_url = "https://www.legco.gov.hk/yr2025/chinese/subleg/negative/2025ln195-c.pdf"

# Download PDF
response = requests.get(pdf_url)
pdf_bytes = io.BytesIO(response.content)

# Extract text
text = extract_text(pdf_bytes)

# Save to file
with open('traffic_regulation_2025.txt', 'w', encoding='utf-8') as f:
    f.write(text)

# Search for specific provisions
if "安全帶" in text:
    print("Found seat belt provisions")

if "2026年1月25日" in text:
    print("Found effective date")
```

### Best Practices for PDF Extraction

- **Use pdfplumber** for documents with tables or complex layouts
- **Handle encoding issues**: LegCo PDFs are typically UTF-8 for Chinese text
- **Check for scanned PDFs**: Some old documents may be images; use OCR (Tesseract, pytesseract)
- **Respect rate limits**: Don't hammer the server with rapid PDF downloads
- **Cache downloaded PDFs**: Save locally to avoid re-downloading

### Common Issues

| Issue | Solution |
|-------|----------|
| Extracted text is garbled | Try different encoding (UTF-8, Big5) |
| PDF is image-based | Use OCR: `pytesseract` + `pdf2image` |
| Tables not extracted well | Use pdfplumber's table extraction features |
| Missing Chinese characters | Ensure font support in your extraction library |

---

## Contact

For API inquiries: enquiry@legco.gov.hk

## Data Disclaimer

See https://www.legco.gov.hk/tc/general/disclaimer.html for terms of use and copyright notice.

---

## Alternative Data Access (Data.Gov.HK)

These APIs are also catalogued on the Hong Kong Government's open data portal:

| Dataset | data.gov.hk URL | API Endpoint |
|---------|-----------------|--------------|
| Reference Data | https://data.gov.hk/en-data/dataset/legco-refdb-reference-database | ScheduleDB endpoints |
| Questions Database | https://data.gov.hk/en-data/dataset/legco-questiondb-questions-database | QuestionsDB endpoints |
| Bills Database | https://data.gov.hk/en-data/dataset/legco-billsdb-bills-database | BillsDB endpoints |
| Meeting Schedule | https://data.gov.hk/en-data/dataset/legco-scheduledb-schedule-database | ScheduleDB endpoints |
| Voting Results | https://data.gov.hk/en-data/dataset/legco-vrdb-voting-results | VRDB endpoints |

**Note:** These are the same APIs documented above, accessible through the data.gov.hk portal. Use the direct LegCo API endpoints in this skill for queries.
