# LegCo HK Search

Search and retrieve data from the Hong Kong Legislative Council's Open Data APIs.

## Installation

```bash
npx skills add yellowcandle/legco-hk-search
```

## What it does

This skill enables AI agents to query the Hong Kong Legislative Council's Open Data APIs, providing access to:

- **Voting Results** - Council, House Committee, Finance Committee votes
- **Bills Database** - Bills from 1844 to present
- **Meeting Schedules** - Council and committee meetings (2012+)
- **Questions** - Oral and written questions by members (2012+)
- **Hansard** - Meeting transcripts and proceedings (2016+)
- **Attendance Records** - Member meeting attendance (2016+)
- **Reference Briefs** - Legislative research summaries (1998+)
- **Historical Archives** - Previous council terms (1997+)
- **Subsidiary Legislation** - Regulations, fee schedules, traffic rules

## Language Support

- **Traditional Chinese (繁體中文)** - Native support for all APIs
- **English** - Full support with separate endpoints

## Usage Examples

Once installed, ask your AI agent:

```
"Search LegCo for bills about seat belts"
"Find voting records on the National Security Bill"
"Get the meeting schedule for next week"
"Show me questions about housing from last month"
"Find the hansard for the July 2024 meeting"
```

## API Coverage

| Data Type | API | Coverage |
|-----------|-----|----------|
| Voting records | Voting Results Database | 2012 onwards |
| Bills | Bills Database | 1844 onwards |
| Schedules | Meeting Schedule Database | 2012 onwards |
| Questions | Questions Database | 2012 onwards |
| Transcripts | Hansard Database | 2016 onwards |
| Attendance | Attendance Database | 2016 onwards |
| Research | Legislative Library | 1998 onwards |
| Archives | Historical Archives | 1997 onwards |
| Regulations | Subsidiary Legislation | All current |

## Data Sources

All data comes from official LegCo sources:
- https://www.legco.gov.hk/ (Voting, Bills, Schedules, Questions, Hansard, Attendance)
- https://library.legco.gov.hk/ (Reference Briefs)
- https://www.legco.gov.hk/research/ (Historical Archives)
- https://www.elegislation.gov.hk/ (Subsidiary Legislation)

## License

MIT - See LICENSE file for details

## More Information

- [Agent Skills Specification](https://agentskills.io/specification)
- [Official LegCo Open Data](https://www.legco.gov.hk/en/open-data/)
- [Skill Details](./skills/legco-hk-search/SKILL.md)

---

Made with ❤️ for Hong Kong
