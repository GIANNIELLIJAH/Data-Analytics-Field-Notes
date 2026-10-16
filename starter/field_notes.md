# Data Literacy Field Notes & Terminal Log

**The scenario:** A climate-and-energy nonprofit wants to use this
country-level energy and emissions dataset to help decide where to direct
community-protection and climate-support efforts — but the file just
landed with zero documentation. Before anyone can trust a decision built
on top of it, you need to figure out what's actually in it — what each
column really holds, and anything that looks off. That's what this whole
file walks through: the real, everyday first pass any analyst runs on an
unfamiliar file, and the real answers you need before this data is safe
to act on.

Dataset: `../data/co2_emissions_2022.csv` (see `../data/SOURCE.md`). Each
section below describes what you're trying to find out — **figuring out
which command (and which flags) actually gets you there is part of what
this project tests**, so the exact command isn't given. Where a command
belongs, you'll see a `# TODO:` comment describing the goal instead of a
ready-to-run command; replace the comment with the real command you used.
Paste the **real output** you got underneath, then write your answer based
on what you actually saw, not what you'd expect. Work through this in
order; open the raw file before anything else.

Run all commands from the repo root — the top-level folder you land in
after cloning *your own* copy of this repo (`git clone ...` then `cd
your-repo-name`, see `README.md` Step 3; not this template) — or `cd` into
`data/` first and drop the `data/` prefix — your choice, just be
consistent.

**This one file is your whole record** — the commands you ran, their real
output, and your written answers, all together in the order you actually
did the work. There's no separate log file to keep in sync with this one;
whenever you write a command down anywhere in this file, use a fenced code
block tagged `bash`, like this:

````
```bash
git status
```
````

Three backticks, the word `bash`, your command, three backticks to close —
it renders with syntax highlighting and makes the command copy-pasteable.

## Setup log

Before jumping into the dataset, log the commands you actually ran to set
this repo up (see `README.md`) — `git init`/clone, creating your
`.gitignore`, your first commit. Add to this as you go, don't
reconstruct it from memory at the end.

```bash
mkdir DA-Analytics-Field-Notes
cd DA-Analytics-Field-Notes
git clone <https://github.com/GIANNIELLIJAH/Data-Analytics-Field-Notes.git>
```

## 1. First look at the raw file

Before trusting anything about this file's structure, you want a quick,
safe peek at it — not the whole 254-row file, just the **first 5 lines**,
enough to see the shape of it without scrolling past everything.

```bash
head -n 5 co2_emissions
```

**Output:**
Afghanistan,AFG,2022,40578847,53303471617,10.170
Africa,,2022,1445862695,,1459.114
Africa (GCP),,2022,,,1459.103
Albania,ALB,2022,2827614,36171005594,4.498

**What I notice: What I notice is that the population column from Africa is missing in the fourth row.

## 2. Column names

Next you want to see just the column names by themselves — one per line is
a lot easier to scan than one long comma-separated row.

```bash
head -n 1 co2_emissions
```

**Output:**
country,iso_code,year,population,gdp,co2

## 3. Column-by-column data type table

For each column, you want to preview real values — **the first 6 values**
of just that one column — without scrolling through every field on every
row. Column numbers for reference: `country`=1, `iso_code`=2, `year`=3,
`population`=4, `gdp`=5, `co2`=6.

```bash

```

Fill in the table from what you actually saw — not a guess from the column
name alone:

| Column | Inferred type | How I can tell |
|---|---|---|
| Afghanistan| AFG, 2022, 40578847, 53303471617 | I can tell because in my code I put the terminal in the order of the table. |
| Africa |  | 2022, 1445862695|
| Africa|  | 2022 | With this one there wasnt any values that correlate in the population or the gdp.
| Albania | ALB, 2827614, 36171005594, | Albania, had all the variables that I was looking for compared to the table. |
| Algeria | DZA, 45477391, 595820067103 | Algeria had the highest population compared to the other countries; since i coded the command: f1, f2 it made sure to list them in orderly manner.  |

**In your own words:** what's the actual difference between a list/array
and a table? (Not a definition you looked up — explain it the way you'd
explain it to a friend who's never coded. No command needed for this one,
just think about the table you just filled in above.)

A difference I noticed between list and columns was that without adding a variable, it doesnt necessarily have a title, so without the commands being labeled by numbers according to the column I wouldnt know what the numbers correlated in comparison to the chart.

## 4. Structured or unstructured?

State whether this dataset is structured or unstructured, and why.

Structured due to the columns and rows having the same variables.

## 5. Before you trust this data

Your first look (see section 1) turned up a row with a suspiciously
**blank** `iso_code`. Before you build anything on this data, you want to
know exactly how many of the 254 rows share that blank — is it a one-off,
or a real pattern worth flagging before anyone draws conclusions from it?
You may need more than one command for this — piping (`|`) feeds one
command's output into the next as input.

```bash
awk -f',' '$2 == "" {print}' co2_emissions_2022.csv | wc -l
```

**Output:**
36

```bash 
awk -f',' '$4 == "" {print}' co2_emissions-2022.csv | grep '^$' | wc -l
```

**Output:**
89

List **at least 2** specific things you'd want to know about how this
dataset was collected, before trusting any conclusion drawn from it — ground
at least one in the counts you just found.

**My 2 concerns:**
1. One specific thing I want to know how this data set was collected was contempalting it if it was surveyed and or if it was sattelite; Did anything change in the process?
2. Were there any changes made to this data set after given the results? If so what was the change?

## 6. Data-quality question for the source

Take the **most specific and checkable** of the two concerns above, and
phrase it as a real question you'd send to the data's source/maintainer. A
good test: could they actually answer it with a concrete yes/no or fact —
not "is this data good?"

How was this Data surveyed? Is this data surely across the entirety of 2022?

## 7. Something you're actually curious about

Different question from #6 — that one was about checking the data's
trustworthiness. This one's about you: what's something you're genuinely
curious to explore using this data? Pick two specific countries you're
curious to compare, and look up their full rows.

```bash
grep -n "$1" co2_comissions.csv
```

**Output:**
The 

**My question:** What is the difference in Afghanistan and Algeria in gdp? Did the following years affect the data?

## 8. AI-literacy reflection

Name **2 concrete risks** of trusting an AI assistant's output about this
dataset (or any data question) without checking it yourself. Then state
**one specific personal rule** for when you'll double-check an AI-provided
fact before relying on it professionally — specific enough that you could
actually follow it, not "I'll be careful."

**Risks:**
1. Risk one would be mainly about code error, this can happen if the ai isn't viable to the entire line of command in the terminal.
2. Another risk, is us as well when inputting a question into AI this can leave room for human error as well.

**My rule:** My rule is to always ask the AI how did they get this answer if there is flaw then I know that there is error.

## 9. Something that went wrong (and how you figured it out)

Somewhere in this project you're going to run a command that either throws
an error or gives you output that isn't what you expected — everyone hits
this at least once. Paste the actual command and what actually happened
(not a paraphrase), then explain what that told you and how it led to the
fix — not "I googled it and it worked."

```bash
git status 
ls -a 
ls -l 
```

**What happened:**
_TODO:  When I was trying to put in the awk command it was shown as an error, this is due to the precise spacing of code. 

**What it told me and how I fixed it:** I actually troubleshooted with AI, and asked it how it got the answer.
