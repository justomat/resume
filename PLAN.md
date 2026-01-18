# Resume Typst Migration Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Recreate Geraldi Sutanto's resume using the typst basic-resume package and publish to GitHub.

**Architecture:** Create a single `resume.typ` file using the `@preview/basic-resume:0.2.9` package, compile to PDF, commit and force-push to overwrite the existing GitHub repository.

**Tech Stack:** Typst, basic-resume package, gh CLI

---

## Task 1: Setup Typst Environment

**Files:**
- Verify: `typst` CLI installed

**Step 1: Check if typst is installed**

Run: `typst --version`
Expected: Version number output (e.g., `typst 0.12.0`)

**Step 2: If not installed, install via Homebrew**

Run: `brew install typst`
Expected: Successful installation

---

## Task 2: Create Resume Typst File

**Files:**
- Create: `resume.typ`

**Step 1: Create the resume.typ file**

```typst
#import "@preview/basic-resume:0.2.9": *

#show: resume.with(
  author: "Geraldi Sutanto",
  email: "contact@geraldisutanto.com",
  phone: "0811-1010-950",
  github: "justomat",
  linkedin: "geraldisutanto",
  accent-color: "#000000",
  font: "New Computer Modern",
  paper: "a4",
)

== Certification

#generic-one-by-two(
  [*Google* Advanced Data Analytics (Certificate ID: ZOGNHJ0T6PZM)],
  [2024],
)

== Work Experience

#work(
  title: "Senior Engineer",
  company: "ShopeePay",
  location: "Jakarta",
  dates: dates-helper(start-date: "2025", end-date: "Present"),
)
- Lead admin portal team

#work(
  title: "Senior Engineer",
  company: "Bitwyre AG",
  location: "Jakarta",
  dates: dates-helper(start-date: "2024", end-date: "2025"),
)
- Develop MVP iOS and Android mobile clients within tight time constraints.
- Setup observability into business and engineering metrics to aid decision making and detect potential issues.
- Gained exposure to legal process and compliance requirements for crypto/financial business.

#work(
  title: "Web3 Developer",
  company: "Contract Work",
  location: "Remote",
  dates: dates-helper(start-date: "2022", end-date: "2023"),
)
- Develop landing page, raffle web app, and hardware-wallet-based login in Sui blockchain for a web3 company.
- Various projects under NDA.

#work(
  title: "Software Engineer",
  company: "Kargo",
  location: "Jakarta",
  dates: dates-helper(start-date: "2021", end-date: "2022"),
)
- Championed the efforts towards reusable UI/UX. Collaborated with designers to eliminate duplicate design effort across teams and produce an agreed-upon set of values (colors, sizes, etc) to reuse. No more similar looking components designed and implemented multiple times by different teams.
- Maintain internal UI library: typescript migration, setup CI/CD, storybooks, tests.
- Wrote a tool that generates typescript types from backend APIs, eliminating huge manual labor and reducing likelihood of mistakes.

#work(
  title: "Software Engineer",
  company: "Ruangguru",
  location: "Jakarta",
  dates: dates-helper(start-date: "2020", end-date: "2021"),
)
- Recruited to lend expertise on SkillAcademy migration from Cordova to React Native.
- Subject Matter Expert for React Native platform/tools, unlocked the rest of the team to focus on business logic. (CI/CD, codesigning, DRM video playback, virtual keyboard handling, push notification, app store submission)
- Ownership over payment domain: ported payment code into ReasonML, conduct bugfix, reviews as codeowner.
- Actively involved in finding creative solutions to meet the time constraints imposed by both the internal product team and PraKerja team (government program).

#work(
  title: "Software Engineer",
  company: "Traveloka",
  location: "Jakarta",
  dates: dates-helper(start-date: "2018", end-date: "2020"),
)
- Successfully resurrected a legacy cross-platform mobile app for B2B partners during a 3mo probation period.
- Transferred to a full-stack team working on a customer facing web app running on Java with a React front-end.

#work(
  title: "Career Break",
  company: "",
  location: "Xiamen, Fujian",
  dates: dates-helper(start-date: "2017", end-date: "2018"),
)
- Attended Chinese language program

#work(
  title: "Software Engineer",
  company: "3Enix Consulting Sdn. Bhd.",
  location: "Kuala Lumpur",
  dates: dates-helper(start-date: "2016", end-date: "2017"),
)
- Full-stack development for major Malaysian banks (Silverlake, HongLeong)

== Education

#edu(
  institution: "Asia Pacific University",
  location: "Kuala Lumpur, Malaysia",
  degree: "B.Sc. Software Engineering",
  dates: dates-helper(start-date: "", end-date: "2016"),
)
- Honors Thesis: "Docker Container Based Java IDE"

== Skills & Interests

- *Languages:* Indonesian (Native Proficiency), English (Professional Proficiency), Chinese (Professional Proficiency)

== Projects

#project(
  name: "Sui Raffle App",
  url: "https://github.com/spruceid/siwe",
  dates: "",
  role: "",
)
- Ported wallet sign-in from ethereum to sui for raffle.suimonstrx.com. Implemented account linking to discord account and raffle system. Solo dev for backend and frontend. (Next.JS, TypeScript, AWS, react-query, ky, Cloudflare Worker, WebAssembly).

#project(
  name: "SkillAcademy",
  url: "",
  dates: "",
  role: "",
)
- Worked on the top on-demand learning app in Indonesia. Used ReactJS and ReasonML on mobile and web. Took the rating from 3.4 to 4.9 on Google Play Store. (ReasonML, TypeScript, JS, React Native, Redux, Firebase, Midtrans)

#project(
  name: "Traveloka AXES",
  url: "",
  dates: "",
  role: "",
)
- Solo dev for mobile and part of the web team for Indonesia leading online travel agency. Fully automated the build process using CI/CD and improved performance so much so that we needed to add a delay/fake loading for UX reasons.
```

**Step 2: Verify file created**

Run: `eza -la resume.typ`
Expected: File exists with content

---

## Task 3: Compile Resume to PDF

**Files:**
- Input: `resume.typ`
- Output: `resume.pdf`

**Step 1: Compile the typst file**

Run: `typst compile resume.typ`
Expected: `resume.pdf` generated without errors

**Step 2: Verify PDF created**

Run: `eza -la resume.pdf`
Expected: PDF file exists

---

## Task 4: Clean Up and Commit

**Files:**
- Remove: `current-resume.pdf` (old resume)
- Remove: `memory.txt` (personal context, not for public repo)
- Remove: `PLAN.md` (implementation artifact)
- Keep: `resume.typ`, `resume.pdf`

**Step 1: Remove old files**

Run: `rm -f current-resume.pdf memory.txt PLAN.md`
Expected: Files removed

**Step 2: Stage all changes**

Run: `git add -A`
Expected: All changes staged

**Step 3: Commit changes**

Run:
```bash
git commit -m "$(cat <<'EOF'
Migrate resume to typst basic-resume format

- Replace markdown-resume with typst basic-resume package
- Generate PDF from typst source
EOF
)"
```
Expected: Commit created

---

## Task 5: Force Push to GitHub

**Files:**
- Remote: `https://github.com/justomat/resume`

**Step 1: Force push to overwrite remote**

Run: `git push --force origin main`
Expected: Push successful, remote updated

**Step 2: Verify on GitHub**

Run: `gh repo view justomat/resume --web`
Expected: Browser opens to repo showing new files

---

## Summary

After completion:
- `resume.typ` - Source file (typst format using basic-resume package)
- `resume.pdf` - Compiled PDF output
- GitHub repo updated with new resume format
