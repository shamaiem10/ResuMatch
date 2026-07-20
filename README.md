<div align="center">

<br>

# **ResuMatch**

<img src="https://img.shields.io/badge/-RESUMATCH-10B981?style=for-the-badge&labelColor=0D1117" alt="ResuMatch" height="50">

<br><br>

### The AI recruiter that reads every resume so you only see the ones worth your time

<br>

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=20&pause=1500&color=10B981&center=true&vCenter=true&width=650&lines=parses+the+resume;scores+it+against+the+role;logs+it+quietly;interrupts+you+only+when+it+matters" alt="Typing SVG" />

<br>

[![n8n](https://img.shields.io/badge/n8n-workflow-EA4B71?style=flat-square&logo=n8n&logoColor=white)](#)
[![Gmail](https://img.shields.io/badge/Gmail-trigger-D93025?style=flat-square&logo=gmail&logoColor=white)](#)
[![OpenRouter](https://img.shields.io/badge/OpenRouter-LLM-10B981?style=flat-square)](#)
[![Sheets](https://img.shields.io/badge/Sheets-tracking-34A853?style=flat-square&logo=googlesheets&logoColor=white)](#)


<br>

</div>

---

<br>

> *"Every candidate deserves a fair, consistent read. No hiring manager has time to give every resume the same careful attention on their tenth cup of coffee. ResuMatch does."*

<br>

## Contents

- [What it does](#what-it-does)
- [The pipeline](#the-pipeline)
- [Scoring guide](#scoring-guide)
- [Stack](#stack)
- [The tracking sheet](#the-tracking-sheet)
- [Setup](#setup)

<br>

## What it does

**ResuMatch** watches a Gmail inbox for incoming job applications. The moment one lands, it pulls the resume straight out of the attachment, reads it in full, and evaluates it against your job description the way a sharp technical hiring manager would — skills, frameworks, education, experience, certifications, all of it.

Every candidate is scored, logged, and filed. Only the ones who clear your bar trigger a notification. The rest are still tracked, still fair, just quiet.

<table>
<tr>
<td width="33%" valign="top">

**No skimming**
Every resume gets the same full, careful read — no fatigue, no bias from being the 40th application that day.

</td>
<td width="33%" valign="top">

**No assumptions**
Scores are based only on what's explicitly in the resume. Nothing inferred, nothing assumed.

</td>
<td width="33%" valign="top">

**No noise**
You're only notified for candidates who actually clear the threshold you set.

</td>
</tr>
</table>

<br>

## The pipeline

```mermaid
flowchart TD
    A[📧 Gmail Trigger<br/>watches for applications] --> B[📋 Pull job context<br/>description + HR email]
    B --> C[📎 Fetch the email<br/>+ resume attachment]
    C --> D[📄 Extract text<br/>from PDF resume]
    D --> E[🧠 LLM evaluation<br/>vs. job description]
    E --> F[📊 Score + structure<br/>the candidate profile]
    F --> G[📑 Log to<br/>tracking sheet]
    G --> H{Score > 80?}
    H -- yes --> I[📬 Alert HR<br/>with candidate details]
    H -- no --> J[🗂️ Filed silently]
    I --> K[✅ Mark email as read]
    J --> K

    style A fill:#D93025,color:#fff,stroke:none
    style E fill:#10B981,color:#fff,stroke:none
    style H fill:#0D1117,color:#10B981,stroke:#10B981
    style I fill:#10B981,color:#fff,stroke:none
    style J fill:#6B7280,color:#fff,stroke:none
```

<br>

## Scoring guide

<div align="center">

| Range | Verdict | What it means |
|:--:|:--|:--|
| 🟢 **90–100** | Excellent match | Exceeds most requirements |
| 🟢 **75–89** | Strong match | Ready for an interview |
| 🟡 **60–74** | Partial match | Worth a look if the pool is thin |
| 🔴 **< 60** | Poor match | Not recommended |

</div>

<br>

## Stack

<div align="center">

| Layer | Tool | Role |
|:--|:--|:--|
| Orchestration | `n8n` | Runs the whole pipeline |
| Inbox monitoring | `Gmail Trigger` | Watches for new applications |
| Resume parsing | `Extract From File` | PDF → raw text |
| Evaluation | `OpenRouter` | Scores against the job description |
| Tracking | `Google Sheets` | Every candidate, logged |
| Notifications | `Gmail` | Alerts HR on strong matches |

</div>

<br>

## The tracking sheet

<div align="center">

| Column | Meaning |
|:--|:--|
| `Name` | Candidate name |
| `Match Score` | 0–100 against the job description |
| `Recommendation` | Strong Hire · Hire · Consider · Reject |
| `Strengths` | Matched skills and qualifications |
| `Weakness` | Missing requirements |
| `Email` | Candidate email — also the matching key |

</div>

<br>

## Setup

```
1.  Create the tracking sheet with the columns above
2.  Create a second sheet holding: job description, HR email, expected subject line
3.  Connect credentials — Gmail OAuth2 · OpenRouter API · Google Sheets OAuth2
4.  Point the Gmail Trigger filter at your application subject line
5.  Set your match-score threshold in the If node   (default: 80)
6.  Set the HR alert recipient
7.  Activate
```

<br>

---

<br>

<div align="center">

**It reads. It scores. It only interrupts you for the ones worth interviewing.**

</div>
