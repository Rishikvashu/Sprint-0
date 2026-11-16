# 📘 Sprint-0 — Complete Study Guide & Interview Prep (Poori Sprint)

> **Ek hi file se poori Sprint-0 ka study.** Is guide mein sprint backlog ke saare topics hain, **concept-focused** (SOPs hata diye, repeat hone wale topics ek hi baar): Ubuntu, Python ecosystem, Java/Maven, Golang, React/npm, JQ, Make, Migrate, Ansible, Jenkins Shared Library, SonarQube, VCS aur Branching Strategy. Har topic ke saath commands, diagrams, common errors aur **interview Q&A** hain.
>
> **Source:** Sections 3, 4, 5 (JQ, Maven, Python installer) repo `Rishikvashu/sprint-0-tickets` (branch `main`) ke docs/code se hain. Sections 8 se 19 repo mein nahi the, woh general knowledge se bane hain. Jo cheezein main ne interview ke liye **extra** jodi hain unpar `🆕 Extra` tag hai.

---

## 📑 Table of Contents

1. [Repo ka Map aur Ticket Mapping](#1-repo-ka-map-aur-ticket-mapping)
2. [Interview Mein Kaise Bolna Hai (60-second Pitch)](#2-interview-mein-kaise-bolna-hai-60-second-pitch)
3. [JQ](#3-jq)
4. [Maven](#4-maven)
5. [Python Installation via Bash Script (SCRUM-11)](#5-python-installation-via-bash-script-scrum-11)
6. [Bash Concepts Cheat Sheet](#6-bash-concepts-cheat-sheet)
7. [Big Picture (CI/CD)](#7-big-picture-cicd)
8. [Ubuntu (Common Stack — Operating System)](#8-ubuntu-common-stack--operating-system)
9. [Python Ecosystem (Intro, venv, Poetry, requirements.txt, Gunicorn)](#9-python-ecosystem-intro-venv-poetry-requirementstxt-gunicorn)
10. [Java (Intro + pom.xml)](#10-java-intro--pomxml)
11. [Golang](#11-golang)
12. [React JS aur NPM](#12-react-js-aur-npm)
13. [Make](#13-make)
14. [Migrate (Database Migrations)](#14-migrate-database-migrations)
15. [Ansible (Role, Playbook, Inventory, Jinja2, CI/CD)](#15-ansible-role-playbook-inventory-jinja2-cicd)
16. [Jenkins Shared Library](#16-jenkins-shared-library)
17. [SonarQube](#17-sonarqube)
18. [VCS (Version Control System)](#18-vcs-version-control-system)
19. [Branching Strategy](#19-branching-strategy)
20. [Master Interview Q&A](#20-master-interview-qa)
21. [Last-Minute Revision Cheat Sheet](#21-last-minute-revision-cheat-sheet)
22. [Repo ki Gaps / Placeholders (Honest Notes)](#22-repo-ki-gaps--placeholders-honest-notes)

---


# 1. Repo ka Map aur Ticket Mapping

## 1.1 Folder structure (branch `main`)

```text
sprint-0-tickets/
├── JQ/
│   └── doc/
│       └── README.md                  → JQ documentation
├── maven/
│   └── doc/
│       └── README.MD                  → Maven (build + local/remote repository) documentation
└── python-installation/
    ├── README.md                      → Project overview + quick start
    ├── @nd-readme.md                  → Python Installation SOP (3 methods, version mgmt, FAQs)
    ├── python-installer.sh            → ASLI SCRIPT (SCRUM-11 ka main deliverable)
    ├── python-manager-explained.md    → Line-by-line explanation of ek alag script: python_manager.sh
    ├── docs/
    │   └── installation.md            → Detailed SCRUM-11 documentation
    └── tests/
        ├── README.md                  → Test documentation (TC-01 ... TC-12)
        └── test-installation.sh       → Automated test script
```

## 1.2 Ticket → Concept mapping

| Ticket / Topic | Folder | Main Deliverable | Core Concepts |
|---|---|---|---|
| **JQ** (ticket number repo mein nahi likha) | `JQ/doc/` | Documentation (POC link placeholder hai) | JSON processing, filters, `select()`, pipe, `-r`, CI/CD use, jq vs yq vs fx vs Python |
| **Maven** (ticket number repo mein nahi likha) | `maven/doc/` | Documentation (POC link placeholder hai) | POM, lifecycle, dependency mgmt, local vs remote repository, `mvn install` vs `mvn deploy`, Nexus/Artifactory |
| **SCRUM-11 — Python Installation via Bash Script** | `python-installation/` | `python-installer.sh` + docs + tests | Bash scripting, APT vs tarball vs auto, SHA256, idempotency, upgrade, logging, trap/cleanup, testing |

> 📝 **Interview tip:** Agar interviewer ticket number puche toh sirf **SCRUM-11** (Python installer) repo ke docs mein explicitly likha hai. JQ aur Maven ke ticket IDs docs mein nahi hain, toh unhe guess mat karo. Jo Jira mein dikhta hai wahi bolo.

## 1.3 Docs ka common format (har document mein same structure)

Teeno tickets ke docs ek hi **12-section template** follow karte hain. Ye khud ek interview point hai ("documentation standardized thi"):

```text
Author Table (Author, Created On, Version, Reviewers L0/L1/L2)
1. Introduction
2. What is <Tool>
3. Why <Tool> is Required
4. Workflow (+ 4.1 Workflow Diagram)
5. Different Tools / Methods
6. Tool Comparison
7. Advantages and Disadvantages
8. Best Practices
9. Recommendation / Conclusion
10. Proof of Concept (POC)
11. Contact Information
12. References
```

## 1.4 Poori Sprint-0 Backlog → Is Guide ke Sections

> ⭐ = Backlog mein `Vashishtha Prakash` ke naam wale tickets (repo se detail). Baaki topics general knowledge se, **concept-focused**. Jo cheezein repeat hoti thi (har language ki "Installation Guide" aur "Installation via Bash script", SOPs, Role/Playbook CI/CD) unhe ek hi baar cover kiya hai.

| Epic / Task | Backlog items | Guide mein kahan |
|---|---|---|
| Setup | API's Setup (OT-Microservice) | ❌ Cover nahi (Jira comment mein instructions) |
| Ubuntu | Concepts + SOPs (common commands, services, software mgmt, disk & ulimit, cron, logrotate, sysctl) | **§8** (SOPs concept ke andar merge) |
| Python | Intro, venv doc+SOP, Poetry doc+SOP, Gunicorn doc+SOP, requirements.txt doc+SOP | **§9** |
| Python ⭐ | Installation guide + **Installation via Bash script** | **§5** (deep dive) |
| Java | Intro, Installation guide/script | **§10.1** (script pattern §5 jaisa) |
| Java ⭐ | **Maven Documentation** + SOP | **§4** (deep dive) |
| Java | pom.xml doc + SOP | **§10.2** |
| Golang | Intro, Installation guide/script | **§11** |
| React JS | Intro, Installation guide/script | **§12.1** |
| React JS | NPM doc + SOP | **§12.2** |
| Others ⭐ | **JQ Intro Documentation** + SOP | **§3** (deep dive) |
| Others | Make | **§13** |
| Others | Migrate | **§14** |
| Ansible | Role (intro, directory structure, Jinja, CI, CD) | **§15.1, 15.4, 15.5, 15.6** |
| Ansible ⭐ | Playbook (intro, **CI**, CD, SOP) | **§15.3, 15.6** |
| Ansible | Inventory (static, dynamic) | **§15.2** |
| Shared Library | vars + src concepts | **§16** |
| SonarQube | Detailed doc | **§17** |
| VCS | Types, workflow, best practices | **§18** |
| Branching Strategy | Strategies, comparison | **§19** |

**Sprint-0 ek line mein:** *"Foundation DevOps stack: OS (Ubuntu), languages aur unke package/build tools (Python, Java, Go, Node), utilities (JQ, Make, Migrate), automation (Ansible), CI/CD (Jenkins Shared Library), code quality (SonarQube) aur source control (VCS + Branching)."*

---

# 2. Interview Mein Kaise Bolna Hai (60-second Pitch)

### 🎤 Overall pitch
> "Sprint-0 mein humne DevOps ke foundation tools par kaam kiya: **JQ** (command line par JSON process karne ke liye), **Maven** (Java build aur dependency management, local aur remote repository ke saath) aur ek **Bash script jo Python ko automatically install karti hai** (APT package, source tarball ya auto mode se). Har tool ke liye maine standard documentation banayi: kya hai, kyun chahiye, alternatives ka comparison, best practices, aur POC. Python installer ke liye maine ek working script bhi likhi jisme validation, SHA256 verification, idempotency, upgrade handling, logging, cleanup aur automated test suite hai."

### 🎤 JQ ka 30-second answer
> "JQ ek lightweight command-line JSON processor hai. CI/CD mein AWS CLI ya REST API ka output JSON hota hai. Poora JSON padhne ke bajaye jq se sirf zaroori field nikaal lete hain, jaise `jq -r '.status'`, aur shell script mein `if` se pipeline ka decision lete hain."

### 🎤 Maven ka 30-second answer
> "Maven Java ka build aur dependency management tool hai. `pom.xml` mein dependencies aur build config hoti hai. Dependencies pehle local repository `~/.m2/repository` mein dhundhi jaati hain, nahi mili toh remote repository (Maven Central / Nexus / Artifactory) se download hoti hain. `mvn install` artifact ko local repo mein rakhta hai aur `mvn deploy` remote repo mein bhejta hai."

### 🎤 Python installer ka 30-second answer
> "`python-installer.sh` teen method support karti hai: `package` (APT), `tarball` (source se build, SHA256 verify karke, `make altinstall` se) aur `auto` (pehle APT check, nahi mila toh tarball). Script idempotent hai, yaani agar version already installed hai toh dobara install nahi karti. Upgrade ke liye `--upgrade` flag hai, downgrade support nahi hai. Har run ka log `logs/python-installer.log` mein jaata hai."

---

# 3. JQ

## 3.1 JQ kya hai?

**jq** ek lightweight aur flexible **command-line JSON processor** hai. Iska kaam JSON data ko **parse, filter, extract, transform aur format** karna hai.

DevOps/CI-CD mein bahut saare tools (REST APIs, AWS CLI, kubectl, Terraform output) apna output **JSON** mein dete hain. Hazaaron lines ke JSON mein se engineer ko kabhi sirf 1-2 values chahiye hoti hain. jq yehi kaam ek chhoti command mein kar deta hai.

**Official description:** jq ek lightweight command-line JSON processor hai jo structured data ko slice, filter, map aur transform kar sakta hai.

**Typical use cases (repo se):**
- JSON se specific fields nikalna
- Condition ke basis par JSON objects filter karna
- JSON arrays process karna
- JSON ko required structure mein transform karna
- Readability ke liye JSON format karna (pretty print)
- API responses process karna
- AWS CLI output se information nikalna
- Shell scripts aur CI/CD pipelines mein JSON data use karna
- Config ya deployment-related JSON validate/process karna

## 3.2 Basic syntax

```bash
jq '<filter>' <input-file>
```

Example JSON (`employee.json`):

```json
{
  "id": 101,
  "name": "Vashishtha",
  "department": "IT"
}
```

```bash
jq '.name' employee.json
# Output:
"Vashishtha"
```

| Component | Matlab |
|---|---|
| `jq` | JSON processing command |
| `.name` | Filter: `name` field select karo |
| `employee.json` | Input JSON file |

**Kaise kaam karta hai:** jq JSON input leta hai, us par **filter** (jq language mein likha hua) apply karta hai, aur result print karta hai.

## 3.3 Core concepts (repo ke docs ke hisaab se)

| Concept | Syntax | Example | Kya karta hai |
|---|---|---|---|
| **Current input (identity)** | `.` | `jq '.' employee.json` | Poora input return karta hai. Pretty-print ke liye bhi use hota hai |
| **Field extraction** | `.fieldName` | `jq '.name' employee.json` | Ek field nikalta hai |
| **Nested field** | `.a.b.c` | `jq '.employee.address.city' employee.json` | Field names chain karke andar ki value |
| **Array iterate** | `[]` | `jq '.employees[]' employees.json` | Array ke har element par kaam |
| **Pipe** | `\|` | `jq '.employees[] \| .name' employees.json` | Ek filter ka output doosre ko input |
| **Filter / condition** | `select()` | `jq '.employees[] \| select(.department == "IT")' employees.json` | Sirf wahi objects jo condition satisfy karein |

### Samajhne ke liye ek chhota example

`employees.json`:
```json
{
  "employees": [
    { "id": 1, "name": "Amit",  "department": "IT" },
    { "id": 2, "name": "Neha",  "department": "HR" },
    { "id": 3, "name": "Rahul", "department": "IT" }
  ]
}
```

| Command | Output |
|---|---|
| `jq '.employees[0].name' employees.json` | `"Amit"` |
| `jq '.employees[].name' employees.json` | `"Amit"` `"Neha"` `"Rahul"` (har ek alag line) |
| `jq -r '.employees[].name' employees.json` | `Amit` `Neha` `Rahul` (quotes ke bina) |
| `jq '.employees[] \| select(.department == "IT") \| .name' employees.json` | `"Amit"` `"Rahul"` |

## 3.4 Kyun chahiye? (Why JQ)

AWS CLI example (repo se):

```bash
aws ec2 describe-instances
```
Ye bahut bada JSON deta hai. Agar sirf instance IDs chahiye:

```bash
aws ec2 describe-instances \
  | jq -r '.Reservations[].Instances[].InstanceId'
```

### jq ke bina problems
- Bade JSON response padhna mushkil
- Required information manually dhoondhni padti hai
- Shell scripts mein JSON filter karna mushkil
- Nested values manually nikalna inefficient
- Automation scripts complicated ho jaati hain
- Data transform karne ke liye extra scripting chahiye

### jq ke fayde
- Structured JSON filtering
- Field extraction
- Array processing
- Conditional selection
- Data transformation
- Sorting aur aggregation
- Shell-friendly **raw output**
- Dusre command-line tools ke saath aasaan integration

## 3.5 JQ CI/CD mein kaise fit hota hai

> ⚠️ **Important point:** JQ khud CI/CD platform **nahi** hai. Ye CI/CD pipeline ke andar ek **JSON processing component** hai.

```text
Developer
    |  Code Commit
    v
Source Code Repository
    |
    v
CI/CD Pipeline
    |
    +----------------------+
    |                      |
    v                      v
Build / Test          CLI / API Command
                           |
                           v
                      JSON Response
                           |
                           v
                          JQ   ← Extract / Filter / Validate / Transform
                           |
                           v
                      CI Decision
                           |
                 +---------+---------+
                 |                   |
              Success              Failure
                 |                   |
              Deploy             Stop / Report
```

### Repo ka CI/CD scenario

API ka response:
```json
{ "status": "success", "environment": "production", "version": "1.8.2" }
```

Pipeline script:
```bash
STATUS=$(jq -r '.status' response.json)

if [ "$STATUS" = "success" ]; then
    echo "Validation successful"
else
    echo "Validation failed"
    exit 1
fi
```

**Yahan kya ho raha hai:**
1. `jq -r '.status'` → `success` (bina quotes ke, kyunki `-r` raw output hai)
2. `$(...)` command ka output variable `STATUS` mein daalta hai
3. `if` se compare. Fail hone par `exit 1`, jisse **CI pipeline fail** ho jaati hai

> 🔑 **`-r` kyun zaroori hai?** `-r` ke bina output `"success"` (quotes ke saath) aata, aur `[ "$STATUS" = "success" ]` false ho jaata. Isliye shell variables ke liye hamesha `-r`.

## 3.6 JSON processing ke alag tools

| Tool | Description |
|---|---|
| **jq** | JSON ke liye command-line processor. Filtering, extraction, transformation |
| **yq** | Mainly YAML ke liye, JSON bhi support karta hai |
| **fx** | Interactive terminal JSON viewer aur processor |
| **Python** | General-purpose language; JSON parse/manipulate kar sakti hai, par simple kaam ke liye zyada code |

### Comparison

| Tool | Main Purpose | Speed | Ease of Use | Best Use Case |
|---|---|---|---|---|
| **jq** | JSON filtering aur transformation | Fast | CLI users ke liye easy | DevOps, APIs, shell scripts, CI/CD |
| **yq** | YAML/JSON processing | Fast | Easy | YAML-heavy DevOps workflows (Kubernetes, Ansible, CI configs) |
| **fx** | Interactive JSON exploration | Fast | Easy | JSON ko interactively explore karna |
| **Python** | General-purpose data processing | Fast | Moderate | Complex processing aur automation |

**Kab kaunsa?**
- Command-line par JSON processing → **jq**
- YAML zyada hai → **yq**
- JSON ko explore karke dekhna hai → **fx**
- Complex business logic, external API calls, bahut error handling → **Python**

## 3.7 Advantages vs Disadvantages

| ✅ Advantages | ❌ Disadvantages |
|---|---|
| Lightweight CLI tool | jq filter syntax seekhni padti hai |
| Specifically JSON ke liye bana hai | General-purpose programming language ka replacement nahi |
| Common JSON tasks mein fast | Complex transformations maintain karna mushkil |
| Shell scripts aur CLI tools ke saath achha | Bahut bade ya bahut complex processing ke liye dedicated application behtar |
| Filtering, transformation, arrays, aggregation support | YAML iska primary format nahi |
| DevOps aur CI/CD automation mein useful | Galat filter se unexpected results aa sakte hain |

## 3.8 Best Practices

| Practice | Kyun |
|---|---|
| **Shell-friendly output chahiye toh `-r` use karo** | Strings ko shell variables/commands mein bina quotes ke dene ke liye |
| **Filters simple aur readable rakho** | Complex filter ko pipe `\|` se stages mein todo |
| **Expected JSON structure validate karo** | Input mein wo fields hain ya nahi jo filter maanta hai |
| **Explicit filters use karo** | Sirf required fields select karo, extra data process mat karo |
| **CI/CD scripts mein errors handle karo** | jq fail ho ya unexpected value aaye toh pipeline sahi react kare |
| **jq version pin/standardize karo** | CI environments mein compatibility issues kam hote hain |
| **Sensitive values print mat karo** | Credentials, tokens, secrets CI logs mein expose na hon |
| **Production se pehle filters test karo** | Representative JSON par verify karo |

## 3.9 Recommendation

- **Command-line JSON processing** ke liye jq recommended hai (DevOps, automation, API integration, AWS CLI, CI/CD).
- Simple se moderately complex JSON kaam ke liye custom script likhne se jq behtar hai kyunki lightweight aur focused hai.
- Bahut complex logic (business logic, external APIs, extensive error handling) ke liye Python jaisi language behtar.
- CI mein standardize karne se pehle **official releases page par current version check** karo.

## 3.10 POC (repo mein planned)

Repo mein POC ka link placeholder hai (`POC_URL`). POC jin cheezon ko cover karne wala tha:

1. jq installation aur version verification
2. JSON files banana aur padhna
3. Basic jq filters
4. Field extraction
5. Nested JSON processing
6. Array processing
7. `select()` se filtering
8. Pipe se filters chain karna
9. JSON transformation
10. `-r` se raw output
11. jq with `curl`
12. jq with AWS CLI
13. CI/CD shell script mein jq

### 🆕 Extra: In 13 points ke commands (practice ke liye)

```bash
# 1. Install + version (Ubuntu)
sudo apt update && sudo apt install -y jq
jq --version

# 2-3. File banao aur pretty print karo
echo '{"id":101,"name":"Vashishtha","department":"IT"}' > employee.json
jq '.' employee.json

# 4. Field extraction
jq '.name' employee.json

# 5. Nested
echo '{"employee":{"address":{"city":"Mathura"}}}' | jq '.employee.address.city'

# 6. Array
jq '.employees[]' employees.json

# 7. select()
jq '.employees[] | select(.department == "IT")' employees.json

# 8. Pipe chain
jq '.employees[] | select(.department == "IT") | .name' employees.json

# 9. Transform (naya object banao)
jq '.employees[] | {id: .id, who: .name}' employees.json

# 10. Raw output
jq -r '.employees[].name' employees.json

# 11. curl ke saath
curl -s https://api.github.com/repos/jqlang/jq | jq -r '.full_name'

# 12. AWS CLI ke saath (aws configured ho)
aws ec2 describe-instances | jq -r '.Reservations[].Instances[].InstanceId'

# 13. CI/CD script
STATUS=$(jq -r '.status' response.json)
[ "$STATUS" = "success" ] || { echo "Validation failed"; exit 1; }
```

## 3.11 🆕 Extra: Interview mein poochhe jaane wale jq features (repo mein nahi hain)

| Feature | Example | Matlab |
|---|---|---|
| `-c` (compact) | `jq -c '.' f.json` | Ek line mein compact output |
| `-e` (exit status) | `jq -e '.status == "success"' r.json` | Result `false`/`null` ho toh non-zero exit code. CI checks ke liye bahut useful |
| `--arg` | `jq --arg d "IT" '.employees[] \| select(.department == $d)' f.json` | Shell variable ko safely jq mein pass karna |
| `-s` (slurp) | `jq -s '.' a.json b.json` | Multiple JSON inputs ko ek array banana |
| `length` | `jq '.employees \| length' f.json` | Array ka size |
| `keys` | `jq 'keys' f.json` | Object ki keys |
| `map()` | `jq '.employees \| map(.name)' f.json` | Array ke har item par transform |
| `sort_by()` | `jq '.employees \| sort_by(.name)' f.json` | Sort |
| `group_by()` | `jq '.employees \| group_by(.department)' f.json` | Grouping |
| `//` (alternative) | `jq '.missing // "default"' f.json` | Value null/false ho toh default |
| `?` | `jq '.a[]?' f.json` | Error ignore karo |
| `@csv`, `@tsv` | `jq -r '.employees[] \| [.id,.name] \| @csv' f.json` | CSV/TSV output |
| `to_entries` | `jq 'to_entries' f.json` | Object ko key/value pairs ki list banana |

## 3.12 Common errors aur fixes (jq)

| Error / Problem | Reason | Fix |
|---|---|---|
| `parse error: Invalid numeric literal` | Input valid JSON nahi hai (HTML error page, ya extra text) | Pehle `curl -s` se raw output dekho, `-f` flag ya status code check karo |
| Output mein `"value"` quotes aa rahe hain | `-r` nahi lagaya | `jq -r` use karo |
| `null` aa raha hai | Field naam galat ya path galat | `jq 'keys'` se actual keys dekho |
| `Cannot iterate over null` | `[]` aisi cheez par laga jo array nahi / missing hai | Pehle path check karo ya `.field[]?` use karo |
| `jq: command not found` | jq install nahi hai | `sudo apt install -y jq` |
| Shell variable filter ke andar kaam nahi kar raha | Single quotes mein `$VAR` expand nahi hota | `--arg name "$VAR"` use karo |

## 3.13 🎯 JQ — Interview Q&A

**Q1. jq kya hai aur kyun use karte hain?**
jq ek lightweight command-line JSON processor hai. CLI tools aur APIs ka output JSON hota hai, jq se sirf zaroori fields nikaal kar shell scripts aur CI/CD pipelines mein use karte hain.

**Q2. `jq '.'` kya karta hai?**
`.` identity filter hai, poora input return karta hai. Iska sabse common use JSON ko pretty-print karna hai.

**Q3. `-r` flag kya karta hai aur kab use karte ho?**
Raw output deta hai, yaani string ke quotes hata deta hai. Jab value ko shell variable ya kisi dusre command ko dena ho tab use karte hain.

**Q4. `jq '.items[]'` aur `jq '.items'` mein kya farak hai?**
`.items` poora array ek baar return karta hai. `.items[]` array ko iterate karke har element alag output karta hai.

**Q5. `select()` kya hai? Example do.**
Condition satisfy karne wale items ko hi aage bhejta hai. Example: `jq '.employees[] | select(.department == "IT")'`.

**Q6. Pipe `|` jq mein kaise kaam karta hai? Shell ke pipe se alag kaise hai?**
jq ke andar `|` ek filter ka output doosre filter ko input deta hai (single quotes ke andar). Shell ka pipe do alag processes jodta hai (jaise `aws ... | jq ...`). Dono ek hi command mein use ho sakte hain.

**Q7. CI/CD pipeline mein jq ka real use batao.**
API ya AWS CLI ka JSON response parse karke status/version/ID nikalna, phir `if` condition se decide karna ki pipeline aage badhe ya `exit 1` se fail ho.

**Q8. jq vs yq vs fx vs Python?**
jq JSON CLI processing ke liye, yq YAML ke liye, fx interactive exploration ke liye, aur Python complex logic ya bade scripts ke liye.

**Q9. jq ki limitations kya hain?**
Syntax seekhna padta hai, complex transformations maintain karna mushkil, YAML primary format nahi, aur bahut complex business logic ke liye general-purpose language behtar.

**Q10. CI logs mein jq use karte waqt security ka kya dhyan rakhoge?**
Secrets/tokens/credentials print nahi karunga. Sirf explicit fields select karunga aur sensitive values logs mein echo nahi karunga.

**Q11. Aap CI mein jq version kyun pin karoge?**
Alag versions mein behaviour ya features alag ho sakte hain. Version standardize karne se "mere machine par chal raha hai, CI par nahi" wali problem kam hoti hai.

**Q12. Agar jq ka filter galat ho aur pipeline phir bhi pass ho jaaye toh?**
Galat filter `null` ya khali output de sakta hai aur script use success maan sakti hai. Isliye expected structure validate karo, `jq -e` jaise exit-status based checks use karo aur filters production se pehle test karo.

**Q13. AWS CLI ke output se sirf running instances ke IDs kaise nikaloge?** (🆕 scenario)
```bash
aws ec2 describe-instances \
 | jq -r '.Reservations[].Instances[] | select(.State.Name=="running") | .InstanceId'
```

**Q14. Shell variable ko jq filter mein safely kaise doge?** (🆕)
`--arg` se: `jq --arg dept "$DEPT" '.employees[] | select(.department == $dept)' f.json`.

---
# 4. Maven

## 4.1 Maven kya hai?

**Apache Maven** ek **build automation aur dependency management tool** hai (Apache Software Foundation ka). Java applications ko **build, test, package aur deploy** karne ke liye use hota hai.

- Project ki saari info `pom.xml` mein hoti hai. **POM = Project Object Model**.
- `pom.xml` mein: project metadata, dependencies, plugins, build config, repositories, profiles, deployment config.
- CI/CD mein Maven ek **CI check** ki tarah use hota hai: source validate, dependencies resolve, tests run, package banana, aur optionally artifact ko remote repository mein publish karna.

## 4.2 Standard project structure

```text
my-java-application/
├── pom.xml
├── src/
│   ├── main/
│   │   └── java/        ← application code
│   └── test/
│       └── java/        ← test code
└── target/              ← build output (compiled classes, JAR/WAR). Git mein commit nahi karte
```

> 🔑 **Convention over configuration:** Maven predefined structure maanta hai, isliye har project ko alag se bataana nahi padta ki source kahan hai.

## 4.3 `pom.xml` ka example (repo se)

```xml
<project>
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>employee-api</artifactId>
    <version>1.0.0</version>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <version>3.5.0</version>
        </dependency>
    </dependencies>
</project>
```

### Maven Coordinates (GAV)

```text
groupId : artifactId : version
com.example : employee-api : 1.0.0
```

| Part | Matlab |
|---|---|
| `groupId` | Organisation/project group (usually reverse domain) |
| `artifactId` | Project/module ka naam |
| `version` | Version (`1.0.0`, `1.0.0-SNAPSHOT`) |

Ye coordinates hi decide karte hain ki artifact repository mein kis **path** par milega.

## 4.4 Key features (repo ki table)

| Feature | Description |
|---|---|
| **Dependency Management** | Dependencies automatically download aur manage |
| **Build Automation** | Compile, test, package |
| **Standard Project Structure** | Predictable structure |
| **POM Configuration** | `pom.xml` mein centralized config |
| **Transitive Dependencies** | Dependencies ki dependencies bhi automatically resolve |
| **Build Lifecycle** | `compile`, `test`, `package`, `install`, `deploy` jaise standard phases |
| **Plugin Ecosystem** | Compile, test, package, analysis, deployment plugins se hote hain |
| **Repository Management** | Local aur remote repositories |
| **CI/CD Integration** | Jenkins, GitHub Actions, GitLab CI se aasaani se chalta hai |
| **Reproducible Builds** | Dependency versions explicitly define kar sakte hain |

## 4.5 Maven kyun chahiye? (Why Maven)

### Maven ke bina
```text
Developer
   +-- JARs manually download karo
   +-- Classpath configure karo
   +-- Java compile karo
   +-- Tests run karo
   +-- JAR/WAR banao
   +-- Versions manually manage karo
```

### Maven ke saath
```text
Developer → pom.xml → Maven
                        +--> Resolve Dependencies
                        +--> Compile
                        +--> Test
                        +--> Package
                        +--> Install
                        +--> Deploy
```

### CI/CD mein Maven commands (repo se)

```bash
mvn clean test       # purana build saaf + sirf tests tak
mvn clean verify     # integration checks tak (package + verify)
mvn clean package    # JAR/WAR tak
```

```text
Git Push → CI Pipeline → Maven
                          +--> Dependency Resolution
                          +--> Compile
                          +--> Unit Tests
                          +--> Verification
                          v
                    Build PASS / FAIL
```

> Maven compile ya tests fail hone par CI pipeline fail honi chahiye, taaki faulty build aage na jaaye.

## 4.6 Build Lifecycle (⭐ interview ka favourite)

Maven ke **default lifecycle** ke main phases (order mein):

| # | Phase | Kya hota hai |
|---|---|---|
| 1 | `validate` | Project sahi hai aur zaroori info available hai ya nahi |
| 2 | `compile` | Source code compile (`src/main/java`) |
| 3 | `test` | Unit tests run (`src/test/java`) |
| 4 | `package` | Compiled code ko JAR/WAR mein package |
| 5 | `verify` | Integration tests / quality checks |
| 6 | `install` | Package ko **local repository** (`~/.m2/repository`) mein install |
| 7 | `deploy` | Final package ko **remote repository** mein copy |

> 🔑 **Rule:** Koi phase chalane par uske **pehle ke saare phases bhi chalte hain**. `mvn package` = validate → compile → test → package. `mvn install` = ... → package → verify → install.

**Alag lifecycle:** `clean` (purane `target/` ko delete karta hai). Isliye `mvn clean install` mein pehle clean, phir default lifecycle.

*(🆕 Extra: Maven mein teen built-in lifecycles hain: `default`, `clean`, `site`. Default lifecycle mein upar ke 7 ke beech aur bhi phases hote hain, jaise `generate-sources`, `process-resources`, `test-compile`. Interview ke liye upar ke 7 yaad rakhna kaafi hai.)*

## 4.7 Repository Workflow (sabse important section)

> 🔑 **Golden line (repo se):** **Git source code store karta hai; Maven repositories build artifacts aur dependencies store karti hain.**

```text
                 Developer
                     | git push
                     v
                Git Remote Repo (GitHub/GitLab)
                     |
                     v
                 CI Pipeline (Jenkins / GitHub Actions)
                     |
                     v
                  Maven (pom.xml)
                     |
          +----------+----------+
          |                     |
          v                     v
   Local Repository       Remote Repository
   ~/.m2/repository      Maven Central / Nexus / Artifactory
          |                     |
          +----------+----------+
                     v
              Build Artifact (JAR/WAR)
                     |
                     v
             Remote Artifact Repo  (mvn deploy)
```

### Git Repository vs Maven Repository

| | Git Repository | Maven Repository |
|---|---|---|
| Kya store karta hai | Source code, `pom.xml`, tests, config, docs | JAR, WAR, POM, metadata, checksums |
| Examples | GitHub, GitLab, Bitbucket | Maven Central, Nexus, JFrog Artifactory, Azure Artifacts |
| Local jagah | `.git/` | `~/.m2/repository/` |

> ⚠️ **"Local Maven Repository ≠ Local Git Repository"**. Ye interview mein confuse karne ke liye aksar poochha jaata hai.

## 4.8 Local Repository

Ye us machine par ek directory hai jahan Maven chal raha hai.

```text
Linux/macOS : ~/.m2/repository
Windows     : C:\Users\<username>\.m2\repository
```

Default `${user.home}/.m2/repository` hai, aur `settings.xml` se change ho sakta hai.

**Do kaam karta hai:**
1. Remote repositories se download kiye artifacts ko **cache** karta hai
2. `mvn install` se locally install kiye artifacts ko store karta hai

### Dependency resolution flow

```text
Maven ko dependency chahiye
  |
  v
~/.m2/repository check karo
  |
  +-- mil gayi  ----> local copy use karo
  |
  +-- nahi mili ----> remote repository se download
                         |
                         v
                   local repository mein store
```

Isse baar-baar download nahi hota aur agle builds fast hote hain.

### Local repository layout (coordinates → path)

```text
~/.m2/repository/
└── org/apache/commons/commons-lang3/3.18.0/
    ├── commons-lang3-3.18.0.jar
    ├── commons-lang3-3.18.0.pom
    └── ...
```

`groupId` ke dots folders ban jaate hain: `org.apache.commons` → `org/apache/commons/`.

### `mvn install`

```bash
mvn install
```
Project build karke uska artifact local repository mein rakhta hai:

```text
~/.m2/repository/com/example/employee-api/1.0.0/
    ├── employee-api-1.0.0.jar
    └── employee-api-1.0.0.pom
```
Ye isliye hai taaki **dusre local projects** is artifact ko use kar sakein.

## 4.9 Remote Repository

Dusri location par accessible repository, aam taur par HTTP/HTTPS par.

Examples: **Maven Central**, **Nexus Repository**, **JFrog Artifactory**, company ke hosted repositories.

Remote repo se **download** bhi hota hai aur (permission ke saath) **upload** bhi.

```text
Dependency download:  Maven → Local (nahi hai) → Remote → download → Local → Build
Artifact upload:      Source → Maven Build → JAR/WAR → mvn deploy → Remote Maven Repository
```

`deploy` phase build/release environment ke liye hai. Final package ko remote repo mein copy karta hai taaki baaki developers aur projects share kar sakein.

## 4.10 Local vs Remote Repository (full table)

| Parameter | Local Repository | Remote Repository |
|---|---|---|
| **Location** | Developer / CI machine | Server / cloud / network |
| **Default example** | `~/.m2/repository` | Maven Central / Nexus / Artifactory |
| **Purpose** | Cache aur local artifact storage | Shared artifact storage |
| **Accessibility** | Aam taur par ek build environment | Multiple developers / CI systems |
| **Dependency download** | Maven **pehle yahin** dekhta hai | Local mein na mile tab use hota hai |
| **Artifact sharing** | Team-wide sharing ke liye nahi | Sharing ke liye hi bana hai |
| **Typical command** | `mvn install` | `mvn deploy` |
| **Internet** | Hamesha zaroori nahi | Aam taur par chahiye (jab tak internally hosted na ho) |
| **Scope** | Machine / build environment | Organization / team / ecosystem |
| **Example artifact** | `employee-api-1.0.0.jar` | Shared company artifact |

## 4.11 `mvn install` vs `mvn deploy` (one-liner)

| | `mvn install` | `mvn deploy` |
|---|---|---|
| Kahan jaata hai | **Local** repo (`~/.m2`) | **Remote** repo (Nexus/Artifactory) |
| Kiske liye | Apni machine ke dusre projects | Poori team / CI |
| Credentials chahiye? | Nahi | Haan (`settings.xml` / CI secrets) |

## 4.12 Maven vs Gradle vs Ant vs sbt

| Tool | Description | Speed | Ease | Best Use Case |
|---|---|---|---|---|
| **Maven** | XML/POM-based build + dependency management | Medium | Easy | Enterprise Java, standardized CI/CD |
| **Gradle** | Modern build tool (Groovy/Kotlin DSL) | Fast | Medium | Large/modern projects jahan flexible builds chahiye |
| **Ant** | Purana XML-based build tool, highly configurable tasks | Medium | Medium | Legacy Java applications |
| **sbt** | Scala projects ka build tool | Fast | Medium | Scala-based applications |

## 4.13 Advantages vs Disadvantages

| ✅ Advantages | ❌ Disadvantages |
|---|---|
| Standardized project structure | XML configuration verbose ho sakti hai |
| Automatic dependency management | Bade projects mein build config complex |
| Strong plugin ecosystem | Optimized Gradle builds se kabhi slower |
| Easy CI/CD integration | Versions manage na hon toh dependency conflicts |
| Local aur remote repositories support | Lifecycle, plugins aur repositories samajhna padta hai |
| Transitive dependencies support | Bade dependency trees se complexity badhti hai |

## 4.14 Best Practices

| Practice | Description |
|---|---|
| **Dependency versions pin karo** | Explicit aur controlled versions, unpredictable versions nahi |
| **CI mein `mvn verify` use karo** | Compile + test + verification build accept karne se pehle |
| **`.m2` ko Git mein commit mat karo** | Ye machine-level cache hai |
| **Internal repository manager use karo** | Nexus/Artifactory se controlled storage aur dependency proxying |
| **SNAPSHOT aur Release alag rakho** | Development ke liye `SNAPSHOT`, stable artifacts ke liye release versions |
| **Credentials secure rakho** | `settings.xml` / CI secrets, Git mein passwords nahi |
| **Dependency management centralize karo** | Multi-module projects mein versions ek jagah |
| **CI mein Maven cache karo** | Local repo cache se build time kam |
| **Maven Wrapper use karo** | Maven version ki reproducibility (`mvnw`) |
| **Unnecessary remote repos avoid karo** | Security aur dependency risks kam |

### 🆕 Extra: `settings.xml` ka chhota example (credentials + mirror)

```xml
<settings>
  <servers>
    <server>
      <id>company-nexus</id>
      <username>${env.NEXUS_USER}</username>
      <password>${env.NEXUS_PASS}</password>
    </server>
  </servers>

  <mirrors>
    <mirror>
      <id>company-nexus</id>
      <mirrorOf>*</mirrorOf>
      <url>https://nexus.example.com/repository/maven-public/</url>
    </mirror>
  </mirrors>
</settings>
```

- **`<server>`**: repository ke credentials (password plain text mein hardcode nahi, env/CI secrets se).
- **`<mirror>`**: saari requests ko internal repository manager par redirect karta hai. Enterprise mein external internet band ho tab bhi dependencies milti hain.
- `settings.xml` ke do locations: user level `~/.m2/settings.xml`, aur global level Maven install ke `conf/` mein.

## 4.15 Recommended enterprise workflow (repo se)

```text
GitHub/GitLab
      |
      v
   Jenkins
      |
      v
     Maven
      |
      +----> Local ~/.m2/repository
      |
      +----> Internal Remote Repository
      |          +----> External dependencies ko proxy karta hai
      |          +----> Internal artifacts store karta hai
      v
    JAR/WAR
      |
      v
Deployment Environment
```

## 4.16 POC (repo mein planned)

Repo mein Maven POC ka link placeholder hai (`<POC_URL>`). POC ka topic: **Maven Build, Dependency Management, Local Repository aur Remote Repository workflow**.

### 🆕 Extra: Hands-on practice (laptop par kar sakte ho)

```bash
# Install + check
sudo apt update && sudo apt install -y maven openjdk-17-jdk
mvn -v

# Naya project (quickstart archetype)
mvn archetype:generate -DgroupId=com.example -DartifactId=employee-api \
    -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
cd employee-api

mvn clean test        # compile + tests
mvn clean package     # target/employee-api-1.0-SNAPSHOT.jar
mvn install           # ~/.m2/repository/com/example/employee-api/... mein copy
ls ~/.m2/repository/com/example/employee-api/

# Dependency tree dekho (transitive dependencies samajhne ke liye)
mvn dependency:tree
```

## 4.17 🆕 Extra: Dependency scopes (interview mein aksar poochha jaata hai)

| Scope | Kab available | Example |
|---|---|---|
| `compile` (default) | Compile, test aur runtime, teeno mein | `commons-lang3` |
| `provided` | Compile + test; runtime par container deta hai | Servlet API |
| `runtime` | Runtime + test (compile ke time nahi) | JDBC driver |
| `test` | Sirf test compile/run | JUnit |

## 4.18 🆕 Extra: SNAPSHOT vs Release

| | SNAPSHOT (`1.0.0-SNAPSHOT`) | Release (`1.0.0`) |
|---|---|---|
| Matlab | Development version, badalta rehta hai | Stable, fixed version |
| Remote repo mein | Overwrite ho sakta hai | Immutable (dobara overwrite nahi karte) |
| Use | Ongoing development | Production |

## 4.19 Common errors aur fixes (Maven)

| Problem | Reason | Fix |
|---|---|---|
| `mvn: command not found` | Maven install nahi / PATH mein nahi | Install karo, `mvn -v` check |
| `Could not resolve dependencies` / `Could not transfer artifact` | Network ya remote repo/mirror issue, ya galat coordinates | Internet/mirror check, GAV verify, `mvn -U` se force update |
| `Compilation failure` ya `release version X not supported` | JDK version aur `pom.xml` ka Java version mismatch | `java -version`, `pom.xml` mein compiler version match karo |
| Tests fail → build fail | Code/test bug | Report `target/surefire-reports/` mein dekho |
| `401 Unauthorized` on `mvn deploy` | Credentials missing/galat | `settings.xml` mein `<server>` ka `id` repo `id` se match karo, CI secrets check |
| Dependency conflict (galat version aa raha) | Transitive dependency version clash | `mvn dependency:tree`, `dependencyManagement` ya exclusion use karo |
| Corrupt jar / purani cached cheez | `~/.m2` mein kharab artifact | Us artifact ka folder delete karke dobara build |

## 4.20 🎯 Maven — Interview Q&A

**Q1. Maven kya hai aur kyun use karte hain?**
Java ka build automation aur dependency management tool. Manual JAR download, classpath, compile, test, package ke kaam ko `pom.xml` aur standard lifecycle se automate karta hai.

**Q2. POM kya hota hai?**
Project Object Model, yaani `pom.xml`. Isme project info, dependencies, plugins, build config, repositories, profiles hote hain.

**Q3. Maven coordinates kya hain?**
`groupId:artifactId:version`. Ye artifact ko uniquely identify karte hain aur repository mein uska path decide karte hain.

**Q4. Maven lifecycle ke main phases batao.**
`validate → compile → test → package → verify → install → deploy`. Koi phase chalane par uske pehle ke saare phases chalte hain.

**Q5. `mvn clean install` mein kya hota hai?**
`clean` pehle purana `target/` delete karta hai, phir default lifecycle `install` phase tak chalti hai (compile, test, package, verify, install) aur artifact local repo mein jaata hai.

**Q6. `mvn install` aur `mvn deploy` mein kya farak hai?**
`install` artifact ko local repository (`~/.m2`) mein rakhta hai. `deploy` use remote repository (Nexus/Artifactory) mein bhejta hai taaki team/CI share kar sake.

**Q7. Local aur remote repository mein kya farak hai?**
Local = us machine par cache aur local artifacts (`~/.m2/repository`). Remote = shared repository (Maven Central, Nexus, Artifactory). Maven pehle local dekhta hai, nahi mile toh remote se download karke local mein rakhta hai.

**Q8. Git repository aur Maven repository mein kya farak hai?**
Git source code aur uski history store karta hai. Maven repository JAR/WAR/POM jaise build artifacts aur dependencies store karti hai.

**Q9. Transitive dependency kya hoti hai?**
Jab tum A ko dependency banate ho aur A ko B chahiye, toh B bhi automatically resolve ho jaati hai. `mvn dependency:tree` se dekh sakte ho.

**Q10. `.m2` folder Git mein commit kyun nahi karte?**
Ye machine-level cache hai, bada hota hai aur har machine par automatically ban jaata hai.

**Q11. SNAPSHOT aur release version mein kya farak hai?**
SNAPSHOT development version hai jo badalta rehta hai. Release stable hota hai aur remote repo mein overwrite nahi hona chahiye.

**Q12. Nexus ya Artifactory kyun use karte hain jab Maven Central hai?**
Controlled artifact storage, external dependencies ka proxy/cache, internal artifacts ka private storage, aur security/compliance control.

**Q13. `settings.xml` mein kya hota hai?**
Local repository path, server credentials, mirrors, proxy aur profiles. Passwords Git mein commit nahi karte, CI secrets/env se dete hain.

**Q14. Mirror kya hota hai?**
Mirror repository requests ko kisi doosre (aam taur par internal) repository manager par redirect karta hai.

**Q15. Maven Wrapper (`mvnw`) kyun?**
Project ke saath Maven ka specific version aata hai, toh sab developers aur CI same Maven version par build karte hain (reproducibility).

**Q16. CI mein `mvn test`, `mvn verify` ya `mvn package` mein se kya chalaoge?**
Normal check ke liye `mvn clean verify` (tests aur verification dono). Sirf jaldi feedback chahiye toh `mvn clean test`. Sirf artifact chahiye toh `mvn clean package`.

**Q17. Maven build slow ho toh kya karoge?** (🆕)
CI mein `~/.m2` cache, internal repository manager (nearby mirror), parallel build (`-T 1C`), aur unnecessary dependencies/plugins hatana.

**Q18. Maven vs Gradle?**
Maven XML/convention based aur predictable. Gradle Groovy/Kotlin DSL se flexible aur aam taur par bade builds mein fast. Maven standardized enterprise CI mein popular.

---
# 5. Python Installation via Bash Script (SCRUM-11)

## 5.1 Ticket kya maangta hai?

**SCRUM-11** ek **generic Bash script** maangta hai jo support kare:

- Multiple Python versions
- Installation
- Upgrades
- Tarball-based installation
- Package-manager-based installation

Is ticket ka implementation hai: **`python-installer.sh`**.

### Requirement → Implementation

| Ticket Requirement | Implementation |
|---|---|
| Generic Bash script | `python-installer.sh` |
| Installation | `package` aur `tarball` methods |
| Multiple Python versions | `--version` input aur version-specific install |
| Upgrades | `--upgrade` flag aur version comparison |
| Tarball | Download → checksum → configure → build → `make altinstall` |
| Package manager | APT |
| Automatic method selection | `--method auto` |

> 📝 Ticket mein sirf upar ke 5 points the. **SHA256 verification, dependency checks, logging, cleanup, tests** ye "supporting engineering features" hain jo tumne apni taraf se jode (docs mein bhi yehi likha hai). Interview mein ye clearly bolo, impressive hai.

## 5.2 Script ka CLI (options)

```text
./python-installer.sh --version <version> --method <package|tarball|auto> [options]
```

| Option | Required? | Matlab |
|---|---|---|
| `--version <v>` | ✅ Haan | Python version: `3.x` ya `3.x.y` (jaise `3.12`, `3.13.7`) |
| `--method <m>` | ✅ Haan | `package`, `tarball`, ya `auto` |
| `--sha256 <hash>` | Sirf tarball build ke liye | Source archive ka SHA256 (exactly 64 hex characters) |
| `--upgrade` | ❌ Optional | Existing install ko upgrade karne ki permission |
| `--keep-build` | ❌ Optional | Build directory (`/tmp/python-build-<version>`) delete mat karo |
| `--help` | ❌ Optional | Usage dikhao |

### Example commands

```bash
# 1. APT se
./python-installer.sh --version 3.12 --method package

# 2. APT se upgrade
./python-installer.sh --version 3.12 --method package --upgrade

# 3. Source se (checksum ke saath)
./python-installer.sh --version 3.13.7 --method tarball \
    --sha256 6c9d80839cfa20024f34d9a6dd31ae2a9cd97ff5e980e969209746037a5153b2

# 4. Auto: pehle APT, nahi mila toh tarball
./python-installer.sh --version 3.13.7 --method auto \
    --sha256 6c9d80839cfa20024f34d9a6dd31ae2a9cd97ff5e980e969209746037a5153b2

# 5. Build folder debugging ke liye rakho
./python-installer.sh --version 3.13.7 --method tarball --sha256 <hash> --keep-build
```

## 5.3 Teen methods — kab kaunsa?

| Method | Source | Flexibility | Best use |
|---|---|---|---|
| 📦 **package** | Ubuntu APT repository | Medium | Version APT mein available ho |
| 📦 **tarball** | Python ka official source archive (`python.org/ftp/python/...`) | High | APT mein na ho ya specific release chahiye |
| 🤖 **auto** | APT ya source (script decide karti hai) | High | Generic automation, user ko decide nahi karna |

### `auto` ka decision logic

```text
        Requested version
               |
               v
     APT package available?   (apt-cache show python<VERSION>)
          /          \
        YES           NO
         |             |
         v             v
        APT         Tarball
```

> 🔑 **Subtle point:** `auto` mein `python${VERSION}` package naam banta hai. `--version 3.12` → `python3.12` (APT mein hai ✅). `--version 3.13.7` → `python3.13.7` (aisa APT package hota hi nahi) → isliye 3.13.7 ke liye `auto` hamesha **tarball fallback** par jaata hai. Repo ke docs mein yehi POC dikhaya hai.

## 5.4 Tarball install ka poora flow

```text
Validate input (version, method)
        |
        v
Existing install check  (/usr/local/bin/python3.X)
        |   SAME → "Nothing to install" → exit 0
        |   DOWNGRADE → error
        |   UPGRADE → --upgrade nahi diya toh error
        v
Validate SHA256 format (64 hex chars)
        |
        v
Check dependencies (commands + build libraries)
        |
        v
Download   (wget → /tmp/python-build-<version>/Python-<version>.tgz)
        |
        v
Verify checksum (sha256sum -c)   ← mismatch = STOP
        |
        v
Extract (tar -xzf)
        |
        v
./configure --prefix=/usr/local
        |
        v
make -j$(nproc)
        |
        v
sudo make altinstall
        |
        v
Verify (/usr/local/bin/python3.X --version)
        |
        v
Cleanup (build dir delete, jab tak --keep-build na ho)
```

### Tarball ka version-comparison behaviour (⭐ table yaad rakho)

Script `/usr/local/bin/python${VERSION%.*}` check karti hai (jaise `3.13.7` → `/usr/local/bin/python3.13`).

| Installed vs Target | `compare_versions` result | `--upgrade` ke bina | `--upgrade` ke saath |
|---|---|---|---|
| Binary hai aur same version | `SAME` | "Nothing to install", exit 0 | "Upgrade requested, but target already installed", exit 0 |
| Installed purana, target naya | `UPGRADE` | ❌ Error: "newer target requested. Use --upgrade." | ✅ Build + install |
| Installed naya, target purana | `DOWNGRADE` | ❌ Error: downgrade not supported | ❌ Error: downgrade not supported |
| Binary hi nahi hai | (comparison nahi hota) | Fresh install | Fresh install |

## 5.5 Package (APT) flow

```text
check_package  →  apt-cache show python<VERSION>
      |
      +--- nahi mila → "NOT available in APT" → script exit (non-zero)
      |
      v
python<VERSION> already installed?
      |
      +--- Haan, --upgrade nahi → "Nothing to install"
      +--- Haan, --upgrade       → sudo apt update + sudo apt install --only-upgrade -y python<VERSION>
      +--- Nahi                  → sudo apt update + sudo apt install -y python<VERSION>
      v
python<VERSION> --version (verify)
```

> `--upgrade` sirf **us Python package** ko upgrade karta hai, poore system ka `apt upgrade` **nahi** karta.

## 5.6 📖 `python-installer.sh` — function-by-function walkthrough

Interview mein "script explain karo" ka sabse bada sawal. Neeche har block ka matlab hai.

### (1) Safety line

```bash
#!/bin/bash
set -euo pipefail
```

| Flag | Matlab |
|---|---|
| `-e` | Koi command fail ho (non-zero) toh script turant band |
| `-u` | Undefined variable use hua toh error |
| `-o pipefail` | Pipe (`a \| b`) mein kisi bhi command ke fail hone par pura pipe fail maana jaaye |

### (2) Variables aur paths

```bash
VERSION="" METHOD="" SHA256="" UPGRADE=false KEEP_BUILD=false
SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
LOG_DIR="${SCRIPT_DIR}/logs"
LOG_FILE="${LOG_DIR}/python-installer.log"
```
- `SCRIPT_DIR` = script jis folder mein hai uska absolute path. Isse log hamesha script ke saath `logs/` mein banta hai, chahe script kahin se bhi chalao.
- `mkdir -p "$LOG_DIR"` logs folder banata hai.

### (3) Logging functions

```bash
log()   # timestamp + [LEVEL] + message → file mein append, aur screen par sirf message
info()  # log "INFO"
warn()  # log "WARN"
error() # log "ERROR" aur exit 1
```
Log ka format: `2026-08-24 10:56:10 [INFO] Python installer started`.
`error()` message log karke `exit 1` karta hai, isiliye har validation failure script ko rok deti hai.

### (4) Cleanup + `trap`

```bash
# (Simplified: sirf logic samjhane ke liye)
BUILD_DIR=""
cleanup() {
    local exit_code=$?
    if [[ -n "$BUILD_DIR" && -d "$BUILD_DIR" ]]; then
        if   [[ "$KEEP_BUILD" == false && "$exit_code" -eq 0 ]]; then  rm -rf "$BUILD_DIR"   # success: saaf
        elif [[ "$KEEP_BUILD" == true ]]; then                          # user ne rakhne ko kaha
        elif [[ "$exit_code" -ne 0 ]]; then                             # fail: debugging ke liye preserve
        fi
    fi
    exit "$exit_code"
}
trap cleanup EXIT
```
- `trap cleanup EXIT` = script kisi bhi tarah khatam ho (success, error, `exit 1`) toh `cleanup` zaroor chalega.
- Matrix:

| Result | `--keep-build` | Build dir ka kya hota hai |
|---|---|---|
| Success | nahi | **Delete** |
| Success | haan | Rakha jaata hai |
| Fail | koi bhi | **Preserve** (debugging) |

### (5) `usage()`
Help text print karke `exit 1`. (Note: `--help` bhi exit code **1** deta hai. Test script mein is baat ka comment hai.)

### (6) Validation functions

| Function | Regex / Logic | Result |
|---|---|---|
| `validate_version` | `^3\.[0-9]+(\.[0-9]+)?$` | `3.12`, `3.13.7` ✅ · `abc`, `2.7`, `3` ❌ |
| `validate_method` | `case` mein `package\|tarball\|auto` | baaki sab → "Unsupported method" |
| `validate_sha256` | Khali nahi + `^[a-fA-F0-9]{64}$` | Galat format → "Invalid SHA256 checksum format" |

### (7) Dependency checks (sirf tarball ke liye)

- `check_required_commands`: `gcc make tar wget sha256sum` `command -v` se check.
- `check_build_packages`: `build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev libffi-dev liblzma-dev tk-dev uuid-dev`.
  - Check: `dpkg-query -W -f='${Status}' <pkg> | grep -q "install ok installed"`.
  - Kuch missing ho toh poori list dikhata hai aur ready-made command deta hai: `sudo apt install -y <missing packages>`. Phir `error` se band.

> 🔑 **Ye kyun zaroori:** Missing dev libraries ke saath Python build toh ho jaata hai, par `ssl`, `sqlite3`, `ctypes` jaise modules **silently missing** reh sakte hain. Isliye pehle hi check.

### (8) `compare_versions`

```bash
if installed == target            → SAME
elif sort -V ke baad last == target → UPGRADE
else                              → DOWNGRADE
```
`sort -V` **version sort** karta hai (3.9 < 3.10 sahi se, jo normal string sort mein galat hota).

### (9) `get_installed_version`
`"$binary" --version | awk '{print $2}'`. `Python 3.13.7` se sirf `3.13.7`.

### (10) APT functions
- `check_package`: `apt-cache show python<VERSION>` success → return 0, warna return 1.
- `install_from_package`: upar 5.5 ka flow.

### (11) `install_from_tarball`
Upar 5.4 ka flow. Dhyan dene wali details:
- `BUILD_DIR="/tmp/python-build-${VERSION}"`
- Download: `wget -q --show-progress "$url" -O "$filename"` (agar file pehle se hai toh dobara download nahi)
- Empty file check: `[[ ! -s "$filename" ]]` → error
- Checksum: `echo "${SHA256}  ${filename}" | sha256sum -c -` (**do spaces** zaroori hain format mein). Fail → "The tarball will not be built."
- Extract tabhi jab `Python-<ver>/` folder pehle se nahi hai
- `./configure --prefix=/usr/local`, `make -j"$(nproc)"`, `sudo make altinstall`

### (12) `install_auto`
`check_package` → success toh `install_from_package`, warna "Falling back to tarball installation" → `install_from_tarball`.

### (13) `main`
- Koi argument nahi → `usage`.
- `while [[ $# -gt 0 ]]` + `case "$1"` se arguments parse. Value wale options mein check hota hai ki value di gayi hai ya nahi, phir `shift 2`. `--upgrade` aur `--keep-build` mein `shift` (1).
- Unknown argument → error.
- Version/method missing → error.
- Header log: "Python installer started / Target version / Method / Upgrade / Keep build".
- `case "$METHOD"` se sahi function.
- End: "Python installer finished successfully."

## 5.7 Teen bade design concepts (interview gold)

### 1️⃣ `make altinstall` vs `make install`

| | `make install` | `make altinstall` |
|---|---|---|
| Binary naam | `python3` bhi banata hai | Sirf `python3.13` (version-specific) |
| Risk | System ke `/usr/bin/python3` / default `python3` ko **override** kar sakta hai | System Python ko **nahi chhedta** |

> Ubuntu ke kai system tools system Python par depend karte hain, isiliye `altinstall` safe hai. Install location: `/usr/local/bin/python3.13`.

### 2️⃣ Idempotency
Script dobara chalane par agar target version already installed hai toh **kuch nahi badalta**. States: `SAME`, `UPGRADE`, `DOWNGRADE`. Isse rebuild (jo slow hai) aur accidental changes se bachte hain.

### 3️⃣ SHA256 integrity verification
Download hui source archive ka hash expected hash se match hona chahiye, warna build nahi hota. Isse corrupted download ya tampered archive se bachte hain (supply-chain security). Expected checksum **trusted source** (python.org) se lo.

```bash
echo "6c9d80839cfa20024f34d9a6dd31ae2a9cd97ff5e980e969209746037a5153b2  Python-3.13.7.tgz" | sha256sum -c -
# Python-3.13.7.tgz: OK
```

## 5.8 Logging

Location: `logs/python-installer.log` (script ke folder mein).

```text
2026-08-24 10:56:10 [INFO] Python installer started
2026-08-24 10:56:10 [INFO] Target version: 3.12
2026-08-24 10:56:10 [INFO] Method: package
2026-08-24 10:56:10 [INFO] python3.12 is already installed.
2026-08-24 10:56:10 [INFO] Nothing to install.
2026-08-24 10:56:10 [INFO] Python installer finished successfully.
```
Log mein: timestamp, target version, method, upgrade state, installation decision, final status.

## 5.9 Testing (SCRUM-11)

### Test environment (docs se)

| Component | Value |
|---|---|
| OS | Ubuntu 24.04.4 LTS |
| Platform | WSL2 |
| Architecture | x86_64 |
| System Python | 3.12.3 |
| Source-installed Python | 3.13.7 |
| Package manager | APT |
| Compiler | GCC 13.3.0 |

### Test case matrix (TC-01 ... TC-12)

| ID | Scenario | Command (short) | Expected |
|---|---|---|---|
| TC-01 | Shell syntax | `bash -n python-installer.sh` | Koi output nahi, exit 0 |
| TC-02 | Package method | `--version 3.12 --method package` | "already installed ... Nothing to install" |
| TC-03 | Package upgrade | `--version 3.12 --method package --upgrade` | "already the newest version" + verification |
| TC-04 | Auto → APT | `--version 3.12 --method auto` | "APT package found. Using package manager." |
| TC-05 | Auto → Tarball | `--version 3.13.7 --method auto --sha256 ...` | "NOT available in APT ... Falling back to tarball" |
| TC-06 | Existing tarball | `--version 3.13.7 --method tarball --sha256 ...` | "Version comparison: SAME ... Nothing to install" |
| TC-07 | Invalid version | `--version abc --method package` | Error + non-zero exit |
| TC-08 | Invalid method | `--version 3.12 --method xyz` | "Unsupported method" + non-zero exit |
| TC-09 | Help | `--help` | Usage text |
| TC-10 | Logging | `cat logs/python-installer.log` | Execution entries |
| TC-11 | Runtime | `/usr/local/bin/python3.13 --version` + ssl/sqlite/modules/pip | Python 3.13.7 + sab import OK |
| TC-12 | SHA256 | `sha256sum -c` | `Python-3.13.7.tgz: OK` |

### Runtime verification commands (TC-11)

```bash
/usr/local/bin/python3.13 --version
/usr/local/bin/python3.13 -c "import ssl; print('SSL:', ssl.OPENSSL_VERSION)"
/usr/local/bin/python3.13 -c "import sqlite3; print('SQLite:', sqlite3.sqlite_version)"
/usr/local/bin/python3.13 -c "import bz2, lzma, ctypes, readline; print('Core modules: OK')"
/usr/local/bin/python3.13 -m pip --version
```
Verified values (docs se): Python 3.13.7, OpenSSL 3.0.13, SQLite 3.45.1, pip 25.2.

> 🔑 **Point:** Sirf "file disk par hai" kaafi nahi. Runtime verification se confirm hota hai ki Python **actually kaam karta hai** (SSL, sqlite, core modules, pip).

### `test-installation.sh` kaise kaam karta hai

- `set -u` (sirf undefined variable check; `-e` nahi rakha taaki ek test fail hone par baaki tests chalte rahein).
- Helper functions: `print_test`, `pass`, `fail` + counters `PASS`, `FAIL`.
- Pehle check: installer file exist karti hai aur executable hai.
- Pattern har test mein:
  ```bash
  output=$("$SCRIPT" --version 3.12 --method package 2>&1)   # output + errors capture
  status=$?                                                  # exit code
  if [[ $status -eq 0 ]] && echo "$output" | grep -q "already installed"; then pass ... else fail ...
  ```
  Yani **exit code + expected output text** dono check hote hain. Negative tests mein `status -ne 0`.
- Script mein **9 automated checks** hain: syntax, package, auto→APT, existing tarball, invalid version, invalid method, help, log file, runtime 3.13.7.
- Final summary: `PASSED: n`, `FAILED: n`, aur "ALL TESTS PASSED" (exit 0) ya "SOME TESTS FAILED" (exit 1).
- **Docs ke TC-03 (upgrade), TC-05 (auto→tarball) aur TC-12 (SHA256) script mein automate nahi hain.** Docs mein bhi likha hai ki checksum POC ke time independently verify kiya gaya.

### Acceptance criteria (docs se)
Syntax pass · Package pass · Upgrade path verified · Auto→APT · Auto→tarball fallback · Existing versions detected · Invalid version/method rejected · Help available · Logs generated · Runtime verified · Valid SHA256 verified · Invalid SHA256 handling verified · Existing version ka unnecessary rebuild nahi.

## 5.10 SOP document (`@nd-readme.md`) ka saar

SOP teen installation approaches batata hai:

| Method | Description | Best use | Complexity |
|---|---|---|---|
| Package Manager | OS repositories se | Quick setup, system environments | Low |
| Tarball (Source) | Source compile | Custom builds, version control | Medium |
| Bash Automation | Script-based | CI/CD, repeatability | High |

```bash
# Package manager
sudo apt update
sudo apt install python3 python3-pip -y

# Tarball
wget https://www.python.org/ftp/python/3.12.0/Python-3.12.0.tgz
tar -xvf Python-3.12.0.tgz
cd Python-3.12.0
./configure --enable-optimizations
make -j$(nproc)
sudo make altinstall

# Version management
python3 --version
update-alternatives --config python3
```

| Task | Command |
|---|---|
| Version check | `python3 --version` |
| Versions switch | `update-alternatives` |
| Alternate binary install | `make altinstall` |

**SOP ke Best practices:** venv use karo · system Python binaries modify mat karo · repeatability ke liye automation scripts · dependency documentation maintain karo · production se pehle staging mein validate.

**SOP Troubleshooting:**

| Issue | Cause | Resolution |
|---|---|---|
| Python not found | PATH misconfiguration | Environment variables update |
| pip missing | Incomplete installation | `python3-pip` install |
| Build failure | Missing dependencies | Required libraries install |

> ℹ️ SOP ke tarball example mein `./configure --enable-optimizations` hai (PGO optimized, slow build, fast Python). `python-installer.sh` mein `./configure --prefix=/usr/local` hai, optimizations ke bina. Ye ek difference hai jo interviewer pakad sakta hai.

## 5.11 `python-manager-explained.md` — ek alag script ki explanation

Is file mein **`python_manager.sh`** ko Hinglish mein line-by-line samjhaya gaya hai. ⚠️ Ye script is branch (`main`) mein **maujood nahi** hai, sirf uski explanation hai. `python-installer.sh` isse alag aur zyada safe/robust hai.

```text
./python_manager.sh install 3.13.4 tarball
   → Arguments (ACTION, VERSION, METHOD)
   → remove_old_version()   (purana apt ya tarball version delete)
   → install_via_tarball() ya install_via_pkg_manager()
   → state file mein naya version save
```

| Pehlu | `python_manager.sh` (explained file) | `python-installer.sh` (actual deliverable) |
|---|---|---|
| Interface | Positional args: `install\|upgrade\|list` VERSION METHOD | Named flags: `--version --method --sha256 --upgrade --keep-build` |
| Methods | `pkg`, `tarball` | `package`, `tarball`, `auto` |
| Package managers | apt, dnf, yum, apk detect | Sirf APT (Ubuntu) |
| Purana version | Install se pehle **remove** karta hai | Remove nahi; compare karke SAME/UPGRADE/DOWNGRADE decide |
| State tracking | `/opt/python_manager/current_version.txt` | State file nahi, installed binary se version padhta hai |
| Install location | `/opt/python/<version>`, symlink `/usr/local/bin/python3` | `/usr/local` (`/usr/local/bin/python3.X`) |
| Checksum | ❌ Nahi | ✅ SHA256 mandatory (tarball) |
| Error handling | ❌ Koi nahi (`set -e` nahi) | ✅ `set -euo pipefail`, `trap`, validation |
| Dependency check | ❌ Nahi | ✅ Commands + build libraries |
| Logging | ❌ | ✅ `logs/python-installer.log` |
| Tests | ❌ | ✅ `tests/test-installation.sh` |
| Extra | Deadsnakes PPA add karta hai | PPA use nahi karta |

**python_manager.sh ki known limitations (doc ke hisaab se):** `sudo` script ke andar nahi · build dependencies install nahi · koi error check nahi (fail hone par bhi "installed successfully") · checksum nahi · `${VERSION%.*}` ka bug (2-part version par galat) · state file sirf version yaad rakhti hai, method nahi · loose `grep` match · `add-apt-repository` minimal Ubuntu par default nahi · symlink har baar delete.

## 5.12 🔍 `python-installer.sh` ki known quirks (code padh kar, honest notes)

Ye cheezein code mein dikhti hain. Interview mein "improvements" ke taur par bolna bahut strong lagta hai:

| # | Observation | Asar | Kaise sudhaar sakte ho |
|---|---|---|---|
| 1 | `--help` **exit code 1** deta hai | Scripts help ko failure samajh sakti hain | `--help` par `exit 0` |
| 2 | **Package method** mein `check_package` ek simple command hai; `set -e` ke karan package na mile toh script bina "ERROR:" message ke bas "NOT available" log karke exit 1 kar deti hai | Error message clear nahi | `if ! check_package; then error "..."; fi` |
| 3 | Tarball ke liye `--version 3.13` (2-part) valid hai, par `${VERSION%.*}` ka result `3` banta hai aur download URL `Python-3.13.tgz` bhi galat hota hai | Tarball ke liye 3-part version (`3.x.y`) zaroori hai | Validation tarball ke liye 3-part enforce kare |
| 4 | Package method mein 3-part version (`3.12.3`) dene par `python3.12.3` package naam banta hai jo APT mein hota hi nahi | Package method sirf `3.x` ke saath kaam karta hai | `${VERSION%.*}` use karke package naam banao |
| 5 | Tarball mein `./configure --prefix=/usr/local` hai, `--enable-optimizations` nahi (SOP mein hai) | Python thoda slower | `--enable-optimizations` add karo (build slow hoga) |
| 6 | Test script log path `"$HOME/python-installer/logs/python-installer.log"` hardcode karta hai, jabki script apne folder (`SCRIPT_DIR`) mein log banati hai | Project kisi aur folder mein ho toh log test fail | Test mein bhi `SCRIPT_DIR`-based path |
| 7 | README mein file ka naam `test-installations.sh` hai (aur "Project Structure" mein bhi), par asli file `tests/test-installation.sh` hai | Docs ke commands copy-paste karne par "file not found" | Naam align karo |
| 8 | Tests environment-dependent hain (machine par pehle se Python 3.12 aur 3.13.7 hona chahiye) | CI mein clean machine par fail honge | Docker container ya mocks |
| 9 | `sudo` script ke andar hardcoded hai | Non-sudo environments (containers) mein dikkat | Root check ya `$SUDO` variable |
| 10 | Sirf Ubuntu/APT support | RHEL/Alpine par kaam nahi | `detect_pkg_manager` jaisa abstraction |
| 11 | Downgrade supported nahi (by design) | Rollback manually | Optional `--allow-downgrade` |

## 5.13 Troubleshooting (Python installer)

| Problem | Reason | Fix |
|---|---|---|
| "Package pythonX is NOT available in APT" | Us version ka APT package nahi | `--method auto` ya `--method tarball` |
| "SHA256 verification failed" | Galat checksum ya corrupted download | Archive aur expected hash dono verify karo. **Bypass mat karo** |
| "Invalid SHA256 checksum format" | Hash 64 hex characters ka nahi | Sahi hash copy karo |
| "SHA256 checksum is required for tarball installation" | `--sha256` nahi diya | `--sha256 <hash>` do |
| "Required Python build libraries are missing" | Dev packages install nahi | Script jo `sudo apt install -y ...` command deti hai wo chalao |
| "A newer target version is requested. Use --upgrade." | Naya version request kiya par flag nahi | `--upgrade` lagao |
| "Downgrade is not supported" | Installed version target se naya hai | Intentional hai; manually handle karo |
| "Version comparison: SAME ... Nothing to install" | Already installed | Ye **expected** behaviour hai |
| `Permission denied` | Script executable nahi | `chmod +x python-installer.sh tests/test-installation.sh` |
| `ssl`/`sqlite3` module missing after build | Build se pehle dev libraries missing thi | Libraries install karke dobara build |
| Build failed | Koi bhi build error | `--keep-build` se `/tmp/python-build-<ver>` rakho aur logs dekho |

## 5.14 🎯 Python Installer — Interview Q&A

**Q1. SCRUM-11 ka project kya tha?**
Ek generic Bash script jo Python ko multiple versions mein install aur upgrade kar sake, APT package aur source tarball dono se. Maine `python-installer.sh` banayi jisme `package`, `tarball` aur `auto` methods hain, saath mein validation, SHA256, logging, cleanup aur tests.

**Q2. `package`, `tarball` aur `auto` mein kya farak hai?**
`package` APT se install, `tarball` python.org ke source se build, `auto` pehle APT check karta hai aur nahi mile toh tarball par fallback.

**Q3. Tarball install kaise hota hai (steps)?**
Validate → existing check → SHA256 format check → dependency check → download → checksum verify → extract → configure → make → `make altinstall` → verify → cleanup.

**Q4. `make install` ki jagah `make altinstall` kyun?**
`altinstall` sirf `python3.X` naam se install karta hai aur system ke default `python3` ko override nahi karta. System tools ko break hone se bachata hai.

**Q5. SHA256 verification kyun zaroori hai?**
Download corrupted ya tampered na ho. Checksum match na ho toh build rokte hain. Ye supply-chain security ka basic step hai.

**Q6. Idempotency kya hai aur tumhari script mein kaise hai?**
Script baar-baar chalane par same result mile aur extra kaam na ho. Script installed version ko target se compare karti hai (`SAME`, `UPGRADE`, `DOWNGRADE`). SAME hone par "Nothing to install" kehkar exit 0.

**Q7. `--upgrade` kya karta hai?**
Package method mein `apt install --only-upgrade` se sirf us Python package ko upgrade karta hai (poora system nahi). Tarball mein naye version ko build karne ki permission deta hai. Downgrade dono mein supported nahi.

**Q8. `set -euo pipefail` ka matlab?**
`-e` command fail par exit, `-u` undefined variable par error, `pipefail` pipe ke kisi bhi step ke fail par pipe fail.

**Q9. `trap cleanup EXIT` kya karta hai?**
Script kaise bhi khatam ho (success ya error) `cleanup` function chalta hai. Success par build directory delete, fail par debugging ke liye preserve, `--keep-build` par hamesha preserve.

**Q10. Version comparison kaise karte ho? `sort -V` kyun?**
`printf '%s\n' installed target | sort -V | tail -n1`. Agar sabse bada target hai toh UPGRADE, warna DOWNGRADE. `sort -V` version-aware hai (3.9 < 3.10), normal sort mein "3.10" "3.9" se pehle aata.

**Q11. Build dependencies kaise check karte ho?**
Pehle `command -v` se `gcc make tar wget sha256sum`, phir `dpkg-query -W -f='${Status}'` se build libraries. Missing hon toh poori list aur install command dikhate hain.

**Q12. Auto mode mein 3.13.7 ke liye tarball kyun chala?**
Auto `python3.13.7` naam ka APT package dhundta hai, jo exist hi nahi karta, isliye fallback tarball par.

**Q13. Script ke tests kaise hain?**
`tests/test-installation.sh` mein 9 automated checks (syntax, package, auto, existing tarball, invalid version, invalid method, help, log, runtime). Har test exit code aur expected output text dono verify karta hai. Docs mein 12 test cases (TC-01..TC-12) hain; upgrade, auto→tarball aur SHA256 manual/POC se verify hue.

**Q14. Positive aur negative testing mein kya farak?**
Positive: valid input par expected behaviour. Negative: invalid input (`--version abc`, `--method xyz`) reject hona aur non-zero exit.

**Q15. Production mein tum kaunsa method chunoge?**
Version APT mein ho toh `package` (stable, OS-managed). Specific/new version chahiye toh `tarball` SHA256 ke saath. Generic automation ke liye `auto`.

**Q16. System Python ko modify kyun nahi karna chahiye?**
Ubuntu ke kai system tools usi par depend karte hain. Change karne se OS functionality toot sakti hai. Isliye `altinstall` aur virtual environments (`venv`).

**Q17. Multiple Python versions ko kaise manage karte ho?**
`make altinstall` se version-specific binaries (`python3.12`, `python3.13`), `update-alternatives --config python3` se default switch, aur project-wise `venv`.

**Q18. Is script mein tum kya improve karoge?** (⭐ 5.12 se bolo)
`--help` ka exit code 0, package-missing par clear error message, tarball ke liye 3-part version enforce, `--enable-optimizations` option, root/sudo handling, multi-distro support (dnf/apk), aur CI mein tests ko containers mein chalana.

**Q19. Agar `./configure` ya `make` fail ho jaaye toh?**
`set -e` ki wajah se script ruk jaati hai, `trap` build directory preserve karta hai (`/tmp/python-build-<ver>`) aur log file mein reason hota hai. Typically missing dev library ya compiler issue hota hai.

**Q20. Log file mein kya hota hai aur kyun?**
Timestamp, level (INFO/WARN/ERROR), target version, method, upgrade/keep-build flags, decisions aur final status. Troubleshooting aur audit ke liye.

**Q21. `wget -q --show-progress ... -O file` ka matlab?**
`-q` quiet mode, `--show-progress` sirf progress bar dikhao, `-O` output file ka naam.

**Q22. `sha256sum -c -` mein dono `-` ka matlab?**
`-c` check mode (hash list se verify), aur akela `-` ka matlab input stdin se (jo `echo` pipe kar raha hai).

---
# 6. Bash Concepts Cheat Sheet

Ye wo Bash concepts hain jo `python-installer.sh` aur `test-installation.sh` mein use hue hain. Interviewer script ke kisi bhi line ke baare mein pooch sakta hai.

| Concept | Syntax | Matlab / Script mein kahan use hua |
|---|---|---|
| Shebang | `#!/bin/bash` | OS ko batata hai ki script bash se chalani hai |
| Strict mode | `set -euo pipefail` | Safe scripting (upar 5.6 mein) |
| Variable | `VERSION="3.12"` | `=` ke aas-paas space nahi |
| Variable use | `"$VERSION"` | Hamesha quotes mein (space wali values ke liye safe) |
| `local` | `local package="python${VERSION}"` | Function ke andar hi limited variable |
| Function | `info() { ... }` | Reusable block; script mein `log`, `info`, `warn`, `error`, `validate_*` |
| Positional args | `$1`, `$2`, `$#`, `$@` | `$#` arguments ki ginti, `$@` sab arguments |
| `shift` / `shift 2` | `shift 2` | Parsed arguments ko aage badhao (flag + value) |
| `[[ ... ]]` | `[[ -z "$SHA256" ]]` | Bash ka improved test (regex, `&&`, `\|\|` support) |
| String tests | `-z` khali, `-n` khali nahi | Validation mein |
| File tests | `-f` file, `-d` dir, `-x` executable, `-s` non-empty | `[[ -x "$python_binary" ]]`, `[[ ! -s "$filename" ]]` |
| Regex match | `[[ "$VERSION" =~ ^3\.[0-9]+(\.[0-9]+)?$ ]]` | `validate_version`, `validate_sha256` |
| `case` | `case "$METHOD" in package\|tarball\|auto) ;; esac` | Method validation aur argument parsing |
| Array | `commands=(gcc make tar)` | Dependency lists |
| Array loop | `for c in "${commands[@]}"; do ... done` | Har element par loop |
| Array length | `${#missing_packages[@]}` | Missing packages ki ginti |
| Array append | `missing_packages+=("$package")` | Item jodna |
| Command substitution | `x=$(command)` | `comparison=$(compare_versions ...)` |
| Exit status | `$?` | `exit_code=$?` (`cleanup` mein) |
| Exit | `exit 1` | Error par band |
| `command -v` | `command -v gcc >/dev/null 2>&1` | Command exist karti hai ya nahi |
| Redirection | `>/dev/null 2>&1` | stdout aur stderr dono chhupao |
| Append | `>> "$LOG_FILE"` | File ke end mein jodna (overwrite nahi) |
| Merge streams | `2>&1` | Error ko output ke saath capture (tests mein) |
| Pipe | `a \| b` | `printf ... \| sort -V \| tail -n1` |
| `awk` | `awk '{print $2}'` | `Python 3.13.7` se `3.13.7` |
| `sort -V` | version sort | Version comparison |
| `printf` | `printf '%s\n' a b` | Har argument alag line mein |
| `trap` | `trap cleanup EXIT` | Exit par function chalao |
| `BASH_SOURCE[0]` | script ka path | `SCRIPT_DIR` nikalne ke liye |
| `dirname`, `pwd` | | Script ka folder |
| `mkdir -p` | | Folder banao (exist kare toh error nahi, parents bhi) |
| `rm -rf` | | Recursive + force delete |
| Here-string / `echo "x" \| cmd -` | `echo "$SHA  $file" \| sha256sum -c -` | Stdin se input |
| `nproc` | `make -j"$(nproc)"` | CPU cores ke hisaab se parallel build |

### `[ ]` vs `[[ ]]`

| | `[ ]` | `[[ ]]` |
|---|---|---|
| Type | POSIX (`test` command) | Bash keyword |
| Regex `=~` | ❌ | ✅ |
| `&&` / `\|\|` andar | ❌ (`-a`, `-o` use hote hain) | ✅ |
| Quotes ki zaroorat | Zyada (word splitting) | Kam |

### Exit codes yaad rakho

| Code | Matlab |
|---|---|
| `0` | Success |
| `1` (non-zero) | Failure / error |
| `$?` | Pichli command ka exit code |

---

# 7. Big Picture (CI/CD)

## 7.1 Teeno tickets ek hi CI/CD story ka hissa hain

```text
                 Developer
                     | git push
                     v
              Git (GitHub / GitLab)
                     |
                     v
               CI Pipeline (Jenkins)
                     |
   +-----------------+-------------------+
   |                 |                   |
   v                 v                   v
Environment      Build & Test        Validation / Decisions
setup            (Maven)             (jq on API / CLI JSON)
(python-installer.sh)
   |                 |                   |
   |  Python 3.x     | JAR/WAR           | status == success?
   |  ready          | → Nexus/Artifactory| → Deploy ya Fail
   +-----------------+-------------------+
```

| Stage | Tool | Role |
|---|---|---|
| Machine/agent ko ready karna | `python-installer.sh` | Required Python version install/upgrade, repeatable aur logged |
| Java build + dependencies | Maven | `mvn clean verify`, artifact ko Nexus/Artifactory mein publish |
| JSON responses se decisions | jq | API/CLI output parse karke pipeline pass/fail |

## 7.2 🆕 Illustrative Jenkinsfile (samajhne ke liye, repo ka nahi)

```groovy
pipeline {
    agent any
    stages {
        stage('Setup Python') {
            steps {
                sh './python-installer.sh --version 3.12 --method package'
            }
        }
        stage('Build & Test') {
            steps {
                sh 'mvn -B clean verify'
            }
        }
        stage('Validate API') {
            steps {
                sh '''
                    STATUS=$(curl -s "$HEALTH_URL" | jq -r '.status')
                    [ "$STATUS" = "success" ] || { echo "Validation failed"; exit 1; }
                '''
            }
        }
    }
}
```

## 7.3 Common thread (interview mein kaam aane wali baat)

| Principle | JQ | Maven | Python installer |
|---|---|---|---|
| **Automation** | JSON data scripts mein | Build/test/package automated | Installation automated |
| **Repeatability** | Same filter = same result | `pom.xml` + pinned versions | Idempotent script |
| **CI decision-making** | `jq -r` + `if` / `exit 1` | Test fail = build fail | Non-zero exit on error |
| **Integrity / security** | Secrets log mein nahi | Credentials `settings.xml`/CI secrets | SHA256 verification |
| **Documentation** | 12-section template | 12-section template | 12-section template + tests |

---

# 8. Ubuntu (Common Stack — Operating System)

> 📚 **Source note:** Sections 8 se 19 sprint backlog ke baaki topics hain. Inke docs repo mein nahi the, isliye ye **concept-level, interview-ready** content hai (general knowledge se). SOPs hata diye hain; sirf wahi commands hain jo concept samajhne ke liye zaroori hain.

## 8.1 Ubuntu kya hai, kyun use karte hain?

**Ubuntu** ek **Debian-based Linux distribution** hai, jise **Canonical** maintain karta hai.

| Pehlu | Detail |
|---|---|
| Release cycle | Har 6 mahine mein release; har 2 saal mein **LTS** (Long Term Support), jaise 22.04, **24.04** |
| LTS | Standard support 5 saal; servers aur production ke liye recommended |
| Package system | `apt` / `dpkg` (`.deb` packages) |
| Init system | `systemd` |
| Default shell | `bash` |

**DevOps mein kyun?**
- Free aur open source, bada community aur documentation
- Cloud providers (AWS, Azure, GCP) ke official images
- Stable LTS releases, predictable security updates
- `apt` se software management aasaan
- Containers (Docker base images), CI agents, servers mein sabse common

## 8.2 Software Management (APT)

```text
APT (high-level)  →  dpkg (low-level)  →  .deb package
   |
   +-- Repositories: /etc/apt/sources.list  aur  /etc/apt/sources.list.d/
```

| Command | Kya karta hai |
|---|---|
| `sudo apt update` | Repository se **package list (index) refresh** karta hai (kuch install nahi karta) |
| `sudo apt upgrade` | Installed packages ko naye versions par upgrade |
| `sudo apt full-upgrade` | Upgrade + zaroorat par packages remove/add (dependency changes) |
| `sudo apt install <pkg>` | Install (`-y` = auto yes) |
| `sudo apt install --only-upgrade <pkg>` | Sirf ek package upgrade (python-installer.sh mein yahi use hua) |
| `sudo apt remove <pkg>` | Package hataata hai, **config files rakhta hai** |
| `sudo apt purge <pkg>` | Package + config files dono hataata hai |
| `sudo apt autoremove` | Wo dependencies hataata hai jo ab kisi ko chahiye nahi |
| `apt search <word>` / `apt show <pkg>` | Search / package ki details |
| `apt-cache policy <pkg>` | Kaunsa version available / installed, kis repo se |
| `dpkg -l` / `dpkg -L <pkg>` | Installed packages / package ki files |
| `sudo add-apt-repository ppa:...` | PPA (third-party repo) jodna |

> 🔑 **`update` vs `upgrade`:** `update` sirf list refresh karta hai. `upgrade` actual software badalta hai. Install se pehle hamesha `update` chalao.

**Snap:** Canonical ka alag packaging format (`snap install ...`), sandboxed aur self-contained.

## 8.3 Services (systemd)

**systemd** Ubuntu ka init system aur service manager hai (PID 1). Services ko **units** ke roop mein manage karta hai (`nginx.service`).

| Command | Kya karta hai |
|---|---|
| `sudo systemctl start nginx` | Service abhi start |
| `sudo systemctl stop nginx` | Abhi stop |
| `sudo systemctl restart nginx` | Stop + start |
| `sudo systemctl reload nginx` | Config reload (bina downtime, agar service support kare) |
| `sudo systemctl enable nginx` | **Boot par automatically start** hone ke liye |
| `sudo systemctl disable nginx` | Boot par auto-start band |
| `sudo systemctl enable --now nginx` | Enable + start ek saath |
| `systemctl status nginx` | Current state, PID, recent logs |
| `systemctl is-active nginx` / `is-enabled nginx` | Active hai? Boot par enabled hai? |
| `systemctl list-units --type=service` | Saari services |
| `sudo systemctl daemon-reload` | Unit file edit karne ke baad systemd ko batao |
| `journalctl -u nginx -f` | Service ke logs (follow mode) |

> 🔑 **`start` vs `enable`:** `start` abhi chalata hai. `enable` boot par chalata hai. Dono alag hain.

**Unit file location:** `/etc/systemd/system/` (custom), `/lib/systemd/system/` (package-provided).

Custom service example (jaise Gunicorn app ke liye):
```ini
[Unit]
Description=My App
After=network.target

[Service]
User=ubuntu
WorkingDirectory=/opt/myapp
ExecStart=/opt/myapp/.venv/bin/gunicorn -w 3 -b 127.0.0.1:8000 app:app
Restart=on-failure
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
```

## 8.4 Common commands (zaroori subset)

| Kaam | Commands |
|---|---|
| Navigation | `pwd`, `ls -la`, `cd` |
| Files | `cp`, `mv`, `rm -rf`, `mkdir -p`, `touch`, `cat`, `less`, `head`, `tail -f` |
| Search | `grep -r "text" .`, `find / -name "*.log"`, `which`, `whereis` |
| Permissions | `chmod 755 f`, `chown user:group f` |
| Processes | `ps aux`, `top`/`htop`, `kill <pid>`, `kill -9 <pid>` |
| Network | `ip a`, `ss -tulnp`, `curl`, `ping` |
| System | `uname -a`, `hostname`, `uptime`, `free -h`, `whoami` |
| Users | `sudo`, `useradd`, `usermod -aG sudo user`, `passwd` |

**Permissions samjho:** `rwx` = 4+2+1. `755` = owner `rwx`, group `r-x`, others `r-x`. `644` = owner `rw-`, baaki `r--`.

## 8.5 Disk aur ulimit

### Disk

| Command | Kya dikhata hai |
|---|---|
| `df -h` | Filesystems ka disk usage (human readable) |
| `du -sh /var/log` | Folder ka size |
| `du -h --max-depth=1 /var \| sort -h` | Kaunsa subfolder bada hai |
| `lsblk` | Block devices (disks, partitions) tree |
| `findmnt` / `mount` | Mount points |
| `blkid` | Partition UUIDs |
| `sudo fdisk -l` | Partition table |

- **Mount point:** wo directory jahan koi filesystem attach hota hai (jaise `/`, `/boot`, `/mnt/data`).
- **Permanent mount:** `/etc/fstab` mein entry (UUID ke saath). Galat `fstab` boot toda sakta hai, isliye `sudo mount -a` se test karo.
- **Inode full:** `df -i`. Disk free dikhe par "No space left" aaye toh inodes check karo.

### ulimit

`ulimit` **process ke resource limits** control karta hai (open files, processes, stack size).

| Command | Matlab |
|---|---|
| `ulimit -a` | Saari limits |
| `ulimit -n` | Max open files (file descriptors) |
| `ulimit -Sn` / `ulimit -Hn` | **Soft** / **Hard** limit |
| `cat /proc/<pid>/limits` | Chalte process ki actual limits |

- **Soft limit:** current effective limit (user badha sakta hai, hard tak). **Hard limit:** upper ceiling (sirf root badha sakta hai).
- **Persist karna:** `/etc/security/limits.conf` ya `/etc/security/limits.d/*.conf`:
  ```text
  ubuntu  soft  nofile  65535
  ubuntu  hard  nofile  65535
  ```
- **systemd services ke liye:** `limits.conf` kaam nahi karta, service file mein `LimitNOFILE=65535` do.
- Login session ke liye PAM (`pam_limits`) ye limits lagata hai.

## 8.6 Cron

**cron** time-based job scheduler hai.

```text
┌───────── minute (0-59)
│ ┌─────── hour (0-23)
│ │ ┌───── day of month (1-31)
│ │ │ ┌─── month (1-12)
│ │ │ │ ┌─ day of week (0-7, 0 aur 7 = Sunday)
* * * * *  command
```

| Example | Matlab |
|---|---|
| `0 2 * * * /opt/backup.sh` | Roz raat 2:00 baje |
| `*/5 * * * * /opt/check.sh` | Har 5 minute |
| `30 9 * * 1-5 cmd` | Mon-Fri subah 9:30 |
| `@reboot cmd` | Reboot par |

| Command | Kya |
|---|---|
| `crontab -e` | Apna crontab edit |
| `crontab -l` | List |
| `crontab -r` | **Saari jobs delete** (careful!) |
| `sudo crontab -u user -l` | Kisi aur user ka |

- System-wide: `/etc/crontab`, `/etc/cron.d/`, aur `/etc/cron.daily|hourly|weekly|monthly/`.
- **Logs:** `grep CRON /var/log/syslog` ya `journalctl -u cron`.
- **Best practices:** absolute paths use karo (cron ka `PATH` chhota hota hai), output redirect karo (`>> /var/log/job.log 2>&1`), script ko executable banao, pehle manually chala ke test karo.

## 8.7 Logrotate

**logrotate** log files ko automatically **rotate, compress aur delete** karta hai, taaki disk full na ho.

- Main config: `/etc/logrotate.conf`; per-app config: `/etc/logrotate.d/`.
- Ubuntu par ye aam taur par daily chalta hai (systemd timer `logrotate.timer`, ya `/etc/cron.daily/logrotate`).

```text
/var/log/myapp/*.log {
    daily
    rotate 14
    compress
    delaycompress
    missingok
    notifempty
    create 0640 ubuntu ubuntu
    postrotate
        systemctl reload myapp > /dev/null 2>&1 || true
    endscript
}
```

| Directive | Matlab |
|---|---|
| `daily` / `weekly` / `monthly` | Rotation frequency |
| `rotate 14` | Retention: 14 purani files rakho |
| `compress` / `delaycompress` | gzip / ek rotation ke baad compress |
| `missingok` | Log na ho toh error nahi |
| `notifempty` | Khali log rotate mat karo |
| `size 100M` | Size ke basis par rotate |
| `copytruncate` | Copy karke original truncate (jab app file handle band nahi karti) |
| `postrotate ... endscript` | Rotation ke baad command (jaise service reload) |

```bash
sudo logrotate -d /etc/logrotate.d/myapp   # dry-run/debug
sudo logrotate -f /etc/logrotate.d/myapp   # force rotation
```
State file: `/var/lib/logrotate/status`.

## 8.8 Sysctl

**sysctl** Linux **kernel parameters** ko runtime par dekhne aur badalne ke liye hai (performance aur security tuning).

| Command | Matlab |
|---|---|
| `sysctl -a` | Saare parameters |
| `sysctl vm.swappiness` | Ek parameter dekho |
| `sudo sysctl -w vm.swappiness=10` | **Temporary** change (reboot par chala jaata hai) |
| `sudo sysctl -p` | `/etc/sysctl.conf` se apply |
| `sudo sysctl --system` | Saari config files (`/etc/sysctl.d/*.conf` bhi) se apply |

**Persist karna:** `/etc/sysctl.d/99-custom.conf` mein likho:
```text
vm.swappiness = 10
net.ipv4.ip_forward = 1
fs.file-max = 2097152
vm.max_map_count = 262144
```
Phir `sudo sysctl --system`.

| Parameter | Use |
|---|---|
| `vm.swappiness` | Swap kitni aggressively use ho |
| `net.ipv4.ip_forward` | IP forwarding (routers, Docker/K8s) |
| `net.core.somaxconn` | Listen backlog (busy web servers) |
| `fs.file-max` | System-wide max open files |
| `vm.max_map_count` | Memory map areas (**SonarQube/Elasticsearch ke liye 262144 chahiye**) |

## 8.9 🎯 Ubuntu — Interview Q&A

**Q1. `apt update` aur `apt upgrade` mein farak?** `update` package index refresh karta hai, `upgrade` installed packages ko naye versions par laata hai.

**Q2. `remove` vs `purge`?** `remove` package hataata hai par config files rakhta hai; `purge` config bhi hataata hai.

**Q3. `systemctl start` aur `enable` mein farak?** `start` abhi chalata hai, `enable` boot par auto-start set karta hai. `enable --now` dono.

**Q4. Service ka log kaise dekhoge?** `journalctl -u <service> -f`, aur `systemctl status <service>`.

**Q5. `df` aur `du` mein farak?** `df` filesystem level par free/used space batata hai, `du` kisi directory ka size.

**Q6. Disk free dikh raha hai par "No space left on device"?** Inodes khatam ho sakte hain (`df -i`) ya deleted file ko koi process abhi bhi pakde hai (`lsof +L1`).

**Q7. Soft aur hard ulimit?** Soft effective limit hai, hard uski upper limit. Sirf root hard badha sakta hai.

**Q8. "Too many open files" aaye toh?** `ulimit -n`, `/proc/<pid>/limits` check; `limits.conf` ya systemd mein `LimitNOFILE` badhao.

**Q9. Cron job chal nahi rahi, kya check karoge?** Syntax, absolute paths, permissions/executable, environment (PATH), `grep CRON /var/log/syslog`, output redirect karke error dekho.

**Q10. Logrotate kyun zaroori hai?** Logs disk bhar sakte hain. Rotation, compression aur retention se disk control mein rehti hai.

**Q11. `sysctl -w` aur `/etc/sysctl.d` mein farak?** `-w` temporary hai; file mein likhne se reboot ke baad bhi persist hota hai.

**Q12. LTS ka matlab?** Long Term Support release (5 saal standard security updates), production ke liye.

---

# 9. Python Ecosystem (Intro, venv, Poetry, requirements.txt, Gunicorn)

> 📚 Python **installation** (script, tarball, package) section 5 mein detail se hai. Yahan baaki Python concepts hain.

## 9.1 Python Intro

| Pehlu | Detail |
|---|---|
| Creator | Guido van Rossum; pehla release 1991 |
| Naam | "Monty Python" comedy group se (saanp se nahi) |
| Type | High-level, interpreted, dynamically typed, multi-paradigm (OOP, procedural, functional) |
| Main implementation | CPython |
| Python 2 | **End of life** Jan 2020; ab Python 3 hi use hota hai |

**Features:** simple readable syntax, bahut bada standard library ("batteries included"), huge third-party ecosystem (PyPI), cross-platform, automatic memory management.

**Use cases:** automation/scripting, web backend (Django, Flask, FastAPI), data science/ML, DevOps tooling (Ansible Python mein hai), testing.

**Interview concepts:** **GIL** (Global Interpreter Lock): CPython mein ek time par ek hi thread Python bytecode chalata hai, isliye CPU-bound kaam ke liye multiprocessing. (Python 3.13 mein optional experimental free-threaded build aaya hai.)

## 9.2 Virtual Environment (venv)

**Virtual environment** ek isolated Python environment hai jisme project ki apni packages hoti hain, system Python se alag.

**Kyun?**
- Dependency conflicts se bachna (Project A ko `django 3`, Project B ko `django 5`)
- System Python ko na chhedna
- Reproducible environments

```bash
sudo apt install -y python3-venv          # Ubuntu par agar zaroorat ho
python3 -m venv .venv                     # banao
source .venv/bin/activate                 # activate (Linux/macOS)
pip install requests                      # sirf is env mein install
pip freeze > requirements.txt             # versions save
deactivate                                # bahar aao
rm -rf .venv                              # delete (bas folder hata do)
```
Windows par activate: `.venv\Scripts\activate`.

| Problem | Reason | Fix |
|---|---|---|
| `ensurepip is not available` / venv banta nahi | `python3-venv` missing | `sudo apt install python3-venv` (ya `python3.X-venv`) |
| `externally-managed-environment` error | Ubuntu 23.04+ (PEP 668) system Python mein `pip install` rokta hai | Virtual environment use karo |
| `source: not found` | `sh` mein chal rahi hai | `bash` use karo ya `. .venv/bin/activate` |
| Permission denied | Folder ka owner alag / `sudo` se banaya | Apne user se banao, `sudo pip` kabhi mat karo |
| Galat Python use ho raha | Env activate nahi | `which python` check karo |

**Best practices:** har project ke liye alag env · `.venv` ko `.gitignore` mein rakho · `requirements.txt`/lock file commit karo · env ko commit mat karo · `sudo pip` mat chalao.

## 9.3 Poetry

**Poetry** ek Python **dependency management aur packaging tool** hai. Ek tool mein virtual env + dependency resolution + lock file + build/publish.

| File | Kaam |
|---|---|
| `pyproject.toml` | Project metadata + dependencies |
| `poetry.lock` | Exact resolved versions (reproducible installs) |

```bash
poetry new myproject                 # naya project
poetry init                          # existing folder mein
poetry add requests                  # dependency add
poetry add --group dev pytest        # dev dependency
poetry install                       # lock file se install
poetry update                        # versions update
poetry remove requests
poetry run python app.py             # env ke andar command
poetry env info                      # env ki info
poetry build / poetry publish        # package banao / PyPI par bhejo
```

### Poetry vs pip vs venv

| | **venv** | **pip** | **Poetry** |
|---|---|---|---|
| Kaam | Isolated env banata hai | Packages install karta hai | Env + dependencies + lock + packaging |
| Dependency resolver | ❌ | ✅ (basic) | ✅ (strong, conflict detect) |
| Lock file | ❌ | ❌ (freeze manual) | ✅ `poetry.lock` |
| Dev/prod groups | ❌ | Alag files | ✅ groups |
| Build/publish | ❌ | ❌ | ✅ |
| Config file | — | `requirements.txt` | `pyproject.toml` |

## 9.4 requirements.txt

pip ki dependency list file. `pip install -r requirements.txt` se install.

```text
flask==3.0.3          # exact pin (best for reproducibility)
requests~=2.32        # compatible release (>=2.32, <3.0)
gunicorn>=22.0        # minimum (kam predictable)
```

| Specifier | Matlab |
|---|---|
| `==1.2.3` | Exact version |
| `>=1.2` | Minimum |
| `~=1.2` | Compatible release (`>=1.2, <2.0`) |
| `!=1.3` | Exclude |

```bash
pip install -r requirements.txt
pip freeze > requirements.txt        # sab installed (transitive bhi) pin
pip check                            # broken dependencies
```

**Best practices:** production mein versions **pin** karo · dev/prod alag (`requirements-dev.txt`) · transitive dependencies ke liye `pip-tools` (`pip-compile`) · env ke andar `pip freeze` · hashes (`--require-hashes`) high-security ke liye · regularly update + test.

**Troubleshooting:** dependency conflict → versions loosen/align; build error → system dev libs install (`python3-dev`, `build-essential`, `libpq-dev` waghera); purani cache → `pip install --no-cache-dir`.

## 9.5 Gunicorn

**Gunicorn** ("Green Unicorn") ek **Python WSGI HTTP server** hai, production mein Flask/Django apps chalane ke liye.

**Kyun?** Flask/Django ka built-in dev server production ke liye nahi hai (single-threaded, secure/stable nahi). Gunicorn **multiple worker processes** (pre-fork model) se concurrent requests handle karta hai.

```text
Client → Nginx (reverse proxy, TLS, static files) → Gunicorn (workers) → Flask/Django app
```

```bash
pip install gunicorn
gunicorn -w 4 -b 0.0.0.0:8000 app:app          # app.py mein `app` object
gunicorn -c gunicorn.conf.py app:app            # config file se
```
`app:app` = `module_name:variable_name`.

| Option | Matlab |
|---|---|
| `-w N` | Worker processes. Common starting point: `(2 × CPU cores) + 1` |
| `-b host:port` | Bind address |
| `--timeout 30` | Worker silent rahe toh kill (default 30s) |
| `-k gthread` / `gevent` | Worker class |
| `--access-logfile -` | Access log stdout par |
| `--reload` | Code change par reload (sirf development) |

- **WSGI** sync Python web apps ka standard. **ASGI** (async) ke liye `uvicorn` ya `gunicorn -k uvicorn.workers.UvicornWorker` (FastAPI).
- Production mein Gunicorn ko **systemd service** se chalao (8.3 ka example) aur **Nginx** ke peeche rakho.
- Signals: `HUP` = config reload + workers restart, `TERM` = graceful shutdown.

## 9.6 🎯 Python Ecosystem — Interview Q&A

**Q1. Virtual environment kyun?** Dependency isolation, system Python safe, reproducibility.

**Q2. Ubuntu 24.04 par `pip install` "externally-managed-environment" kyun deta hai?** PEP 668 ke karan, taaki system packages na tootein. Virtual environment use karo.

**Q3. venv aur Poetry mein farak?** venv sirf environment banata hai. Poetry environment + dependency resolution + lock file + build/publish sab karta hai.

**Q4. `poetry.lock` kyun commit karte hain?** Taaki sab developers aur CI exactly same versions install karein.

**Q5. `requirements.txt` mein `==` vs `~=`?** `==` exact pin (reproducible), `~=` compatible updates allow karta hai.

**Q6. `pip freeze` ka nuksan?** Transitive dependencies bhi pin ho jaati hain aur direct/indirect ka farak chhup jaata hai. `pip-tools`/Poetry behtar.

**Q7. Gunicorn kyun, Flask dev server kyun nahi?** Dev server production-grade nahi. Gunicorn multi-worker, stable aur monitored deployment deta hai.

**Q8. Gunicorn ke saath Nginx kyun?** TLS termination, static files, buffering slow clients, load balancing aur security.

**Q9. Kitne workers rakhoge?** Starting point `(2 × cores) + 1`, phir load testing se tune karo.

**Q10. WSGI vs ASGI?** WSGI synchronous standard, ASGI asynchronous (websockets, async frameworks).

**Q11. GIL kya hai?** CPython mein ek time par ek thread bytecode chalata hai; CPU-bound kaam ke liye multiprocessing use karo.

---
# 10. Java (Intro + pom.xml)

> 📚 **Maven** ka detail section 4 mein hai. Yahan Java intro aur `pom.xml` ki best practices hain (jo Maven section mein repeat nahi hui).

## 10.1 Java Intro

| Pehlu | Detail |
|---|---|
| Creator | James Gosling (Sun Microsystems); 1995; ab Oracle ke paas |
| Motto | **"Write Once, Run Anywhere" (WORA)** |
| Type | High-level, **compiled to bytecode**, class-based OOP, statically typed |
| Open-source build | **OpenJDK** (Temurin, Corretto jaise distributions) |
| LTS versions | 8, 11, 17, 21, 25 |

### JDK vs JRE vs JVM (⭐ favourite)

```text
JDK  = JRE + development tools (javac, jar, jdb ...)
JRE  = JVM + core libraries
JVM  = bytecode ko machine code mein chalata hai (platform-specific)
```

```text
Hello.java --javac--> Hello.class (bytecode) --JVM--> chalta hai (kisi bhi OS par)
```

**Features:** platform independent (JVM ki wajah se), automatic garbage collection, multithreading, strong typing aur memory safety, huge ecosystem (Spring Boot, Hibernate), backward compatibility.

**Use cases:** enterprise/backend applications, microservices (Spring Boot), Android (Kotlin ke saath), big data (Hadoop, Spark, Kafka), banking systems.

### Installation methods (concept)

| Method | Command / idea |
|---|---|
| APT package | `sudo apt install -y openjdk-17-jdk` |
| Tarball (manual) | JDK `.tar.gz` download → `/opt/` mein extract → `JAVA_HOME` set |
| SDKMAN | Multiple Java versions manage (`sdk install java 21...`) |

```bash
java -version                       # runtime
javac -version                      # compiler (JDK)
sudo update-alternatives --config java      # multiple versions mein switch
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export PATH=$JAVA_HOME/bin:$PATH
```
> **Generic installer script ka pattern** wahi hai jo Python script (section 5) mein hai: version validate, method choose (package/tarball), checksum verify, existing version compare, `update-alternatives`/`JAVA_HOME` set, log. Isliye Java/Go/React ke alag "bash script" tickets mein concept repeat nahi kiya.

## 10.2 pom.xml — structure aur best practices

### Main sections

| Section | Kaam |
|---|---|
| `<modelVersion>` | POM model version (`4.0.0`) |
| `<groupId> <artifactId> <version>` | Project ki identity (GAV) |
| `<packaging>` | `jar` (default), `war`, `pom` |
| `<parent>` | Parent POM se settings inherit (jaise `spring-boot-starter-parent`) |
| `<properties>` | Variables (Java version, dependency versions) |
| `<dependencies>` | Project ki dependencies |
| `<dependencyManagement>` | Versions ek jagah centralize (dependencies yahan declare karne se versions apply, add nahi hoti) |
| `<build><plugins>` | Build plugins (compiler, surefire, jar, spring-boot) |
| `<profiles>` | Environment-specific config (dev/prod) |
| `<repositories>`, `<distributionManagement>` | Download aur deploy locations |
| `<modules>` | Multi-module project ke child modules |

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.example</groupId>
  <artifactId>employee-api</artifactId>
  <version>1.0.0-SNAPSHOT</version>
  <packaging>jar</packaging>

  <properties>
    <maven.compiler.release>17</maven.compiler.release>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <commons-lang3.version>3.18.0</commons-lang3.version>
  </properties>

  <dependencies>
    <dependency>
      <groupId>org.apache.commons</groupId>
      <artifactId>commons-lang3</artifactId>
      <version>${commons-lang3.version}</version>
    </dependency>
    <dependency>
      <groupId>org.junit.jupiter</groupId>
      <artifactId>junit-jupiter</artifactId>
      <version>5.10.2</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
</project>
```

### Dependency versioning best practices

| Practice | Kyun |
|---|---|
| Versions **properties** mein rakho (`${x.version}`) | Ek jagah update, duplicate nahi |
| `LATEST`, `RELEASE` ya version **ranges** (`[1.0,2.0)`) avoid karo | Build reproducible nahi rehta |
| `<dependencyManagement>` / **BOM** use karo | Multi-module mein consistent versions |
| Sahi `<scope>` do (`test`, `provided`) | Final artifact chhota aur clean |
| Unused dependencies hatao (`mvn dependency:analyze`) | Security surface kam |
| Conflicts `mvn dependency:tree` se dekho; zaroorat par `<exclusions>` | Transitive conflicts solve |
| Plugin versions bhi pin karo | Build stable |
| Parent POM se common config share karo | DRY |
| Vulnerable dependencies regularly update (scan: OWASP dependency-check / SonarQube) | Security |
| `maven-enforcer-plugin` se rules (Java/Maven version, banned dependencies) | Policy enforcement |

## 10.3 🎯 Java — Interview Q&A

**Q1. JDK, JRE, JVM mein farak?** JVM bytecode chalata hai, JRE = JVM + libraries, JDK = JRE + compiler/tools.

**Q2. Java platform independent kaise hai?** Source bytecode mein compile hota hai, aur har platform ka JVM use chalata hai.

**Q3. `JAVA_HOME` kya hai aur kyun zaroori?** Maven, Jenkins jaise tools ko batata hai ki JDK kahan hai.

**Q4. Multiple Java versions kaise manage karoge?** `update-alternatives`, SDKMAN ya `JAVA_HOME` switch, aur Jenkins mein tool configuration.

**Q5. `dependencies` vs `dependencyManagement`?** `dependencies` mein declare ki hui cheez actual use hoti hai. `dependencyManagement` sirf versions define karta hai (add nahi karta).

**Q6. Version range ya `LATEST` kyun avoid karte hain?** Build kal alag result de sakta hai (non-reproducible), aur breaking change aa sakta hai.

**Q7. Transitive dependency conflict kaise solve karoge?** `mvn dependency:tree`, version ko `dependencyManagement` mein force karo ya `<exclusions>`.

**Q8. `packaging` ke types?** `jar`, `war`, `pom` (parent/aggregator).

---

# 11. Golang

## 11.1 Go kya hai, kyun?

| Pehlu | Detail |
|---|---|
| Creators | Google (Robert Griesemer, Rob Pike, Ken Thompson); announced 2009, Go 1.0 in 2012 |
| Type | **Compiled**, statically typed, garbage collected |
| Output | **Single static binary** (runtime install ki zaroorat nahi) |
| Concurrency | **Goroutines** aur **channels** built-in |

**Key features:**
- Fast compilation, fast execution
- Simple syntax, chhota language spec
- Built-in concurrency (goroutines halke threads jaise hote hain)
- Strong standard library (HTTP server, JSON, testing)
- Cross-compilation (`GOOS=linux GOARCH=amd64 go build`)
- Built-in tooling: `go fmt`, `go vet`, `go test`, `go mod`

**Use cases:** cloud-native aur DevOps tools (**Docker, Kubernetes, Terraform, Prometheus** Go mein bane hain), microservices/REST APIs, CLI tools.

## 11.2 Core concepts

| Concept | Matlab |
|---|---|
| **Modules** | Dependency management. `go.mod` (module path + dependencies), `go.sum` (checksums). Go 1.11 se |
| **GOROOT / GOPATH** | GOROOT = Go ka install folder. GOPATH = purana workspace model (ab modules use hote hain) |
| **Package** | Code ka unit; `package main` + `func main()` = executable |
| **Goroutine** | `go f()` se halka concurrent function |
| **Channel** | Goroutines ke beech data bhejne ka safe tareeka (`ch <- v`, `v := <-ch`) |
| **Interface** | Methods ka set; implicitly implement hota hai |
| **`defer`** | Function ke end par chalta hai (cleanup ke liye) |
| **Error handling** | Exceptions nahi; `value, err := f(); if err != nil {...}` |

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, Go")
}
```

## 11.3 Installation (concept) aur commands

| Method | Idea |
|---|---|
| Official tarball (recommended) | `go1.X.linux-amd64.tar.gz` download → `sudo tar -C /usr/local -xzf ...` → `export PATH=$PATH:/usr/local/go/bin` |
| `apt install golang-go` | Aasaan par version aksar purana |
| Multiple versions | `go install golang.org/dl/go1.xx@latest` phir `go1.xx download` |

```bash
go version
go mod init github.com/me/employee-api   # go.mod banao
go mod tidy                              # unused hatao, missing jodo
go build ./...                           # compile
go run main.go                           # chalao
go test ./... -cover                     # tests + coverage
go vet ./...                             # static checks
go fmt ./...                             # formatting
```

**CI pipeline (typical):** `go mod download` → `go vet` → `go test -cover` → `go build` → (SonarQube scan, Docker image) .

## 11.4 🎯 Golang — Interview Q&A

**Q1. Go ki khaas baat?** Simple, fast, built-in concurrency, single static binary.

**Q2. Goroutine thread se alag kaise?** Bahut halka hota hai, Go runtime schedule karta hai, hazaaron chal sakte hain.

**Q3. Channel kyun?** Goroutines ke beech safe communication ("share memory by communicating").

**Q4. `go.mod` aur `go.sum`?** `go.mod` mein module aur dependencies, `go.sum` mein unke checksums (integrity).

**Q5. Go mein error handling kaise?** Errors normal return values hote hain; `if err != nil` se check.

**Q6. `defer` kya karta hai?** Function return hone par chalta hai; file close, unlock jaise cleanup ke liye.

**Q7. Go DevOps mein popular kyun?** Single binary (deploy aasaan), cross-compile, chhota container image, fast.

**Q8. `go mod tidy` kya karta hai?** Unused dependencies hataata hai aur missing jodta hai.

---

# 12. React JS aur NPM

## 12.1 React Intro

| Pehlu | Detail |
|---|---|
| Kya hai | **JavaScript library** user interfaces banane ke liye |
| Creator | Meta (Facebook), 2013 |
| Style | **Component-based**, **declarative** |

**Key features:**
- **Components:** UI ke reusable tukde (function components)
- **JSX:** JavaScript ke andar HTML jaisa syntax
- **Virtual DOM:** React pehle memory mein virtual tree banata hai, changes ka diff nikaal ke real DOM mein sirf zaroori update karta hai
- **One-way data flow:** data parent se child (props) ki taraf
- **Hooks:** function components mein state aur lifecycle

| Concept | Matlab |
|---|---|
| **props** | Parent se child ko mila data (read-only) |
| **state** | Component ka apna badalne wala data (`useState`) |
| `useState` | State variable |
| `useEffect` | Side effects (API call, subscriptions); render ke baad |
| `useContext` | Prop drilling ke bina shared data |
| `useRef` | DOM reference / mutable value jo re-render nahi karti |
| `useMemo` / `useCallback` | Memoization (performance) |

```jsx
import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>Clicked {count}</button>;
}
```

**Tooling:** Create React App ab deprecated hai; naye projects **Vite** (`npm create vite@latest my-app -- --template react`) ya **Next.js** se.

**Build aur deploy:** `npm run build` static files (`dist/` ya `build/`) banata hai, jinhe **Nginx** ya CDN se serve karte hain. React app browser mein chalti hai, isliye production mein Node server zaroori nahi (static hosting kaafi).

**Installation (concept):** Node.js chahiye (NodeSource ya **nvm** se multiple versions: `nvm install --lts`). Generic installer script ka pattern section 5 jaisa hi hai.

## 12.2 NPM

**npm** = **Node Package Manager**, Node.js ke saath aata hai. JavaScript packages ka default package manager aur registry (npmjs.com).

| File / Folder | Kaam |
|---|---|
| `package.json` | Project metadata, dependencies, scripts |
| `package-lock.json` | Exact installed versions (reproducible) |
| `node_modules/` | Installed packages (Git mein commit nahi) |

```bash
npm init -y                      # package.json banao
npm install                      # package.json ke hisaab se install
npm install react                # dependency add
npm install -D eslint            # devDependency
npm uninstall react
npm update
npm ci                           # lock file se clean, exact install (CI ke liye)
npm run build                    # scripts section ka script
npm ls                           # dependency tree
npm outdated                     # purane packages
npm audit                        # vulnerabilities
npx create-vite                  # package ko install kiye bina chalao
```

| Cheez | Detail |
|---|---|
| `dependencies` vs `devDependencies` | Runtime ke liye vs development/build/test ke liye |
| **Semver** (`1.4.2` = major.minor.patch) | `^1.4.2` = minor+patch updates allowed. `~1.4.2` = sirf patch |
| `npm install` vs `npm ci` | `install` lock update kar sakta hai; `ci` lock ko exactly follow karta hai (fast, strict, CI ke liye) |
| Alternatives | **yarn**, **pnpm** |

| Problem | Fix |
|---|---|
| `EACCES` permission error | Global installs ke liye nvm use karo ya npm prefix badlo, `sudo npm` avoid |
| `ERESOLVE` peer dependency conflict | Versions align karo, ya `--legacy-peer-deps` (soch-samajh ke) |
| Ajeeb errors / corrupted install | `node_modules` aur lock delete karke `npm install`, ya `npm cache verify` |
| Build memory error | `NODE_OPTIONS=--max-old-space-size=4096` |

## 12.3 🎯 React + NPM — Interview Q&A

**Q1. React kya hai? Framework ya library?** Library (UI ke liye). Routing/state jaisi cheezein ecosystem se aati hain.

**Q2. Virtual DOM kya hai?** DOM ki memory-copy. State badalne par naya virtual tree purane se compare (diffing) hota hai aur real DOM mein sirf changes apply hote hain.

**Q3. Props aur state mein farak?** Props parent se aate hain (read-only), state component ka apna hai aur badalne par re-render hota hai.

**Q4. `useEffect` kab chalta hai?** Render ke baad. Dependency array se control hota hai.

**Q5. JSX kya hai?** JavaScript syntax extension jo HTML jaisa dikhta hai aur JS mein compile hota hai.

**Q6. `npm install` vs `npm ci`?** `ci` lock file se exact aur clean install karta hai; CI/CD mein recommended.

**Q7. `dependencies` vs `devDependencies`?** Runtime vs dev/build/test tools.

**Q8. `^` aur `~` mein farak?** `^` minor aur patch updates allow, `~` sirf patch.

**Q9. React app production mein kaise deploy karte ho?** `npm run build` se static files, Nginx/CDN se serve.

**Q10. `package-lock.json` kyun commit karte hain?** Sab ko same dependency versions mile.

---
# 13. Make

## 13.1 Make kya hai, kyun?

**GNU Make** ek **build automation tool** hai. `Makefile` mein likha hota hai ki kaunsi cheez kaise banti hai, aur `make` sirf wahi kaam karta hai jo zaroori ho (timestamps compare karke).

**Kyun?**
- Repeated commands ko ek naam dena (`make test`, `make build`)
- Incremental builds (sirf badli hui files recompile)
- Language-independent: C/C++ se lekar Docker, Go, Python projects tak
- Python ko source se build karte waqt bhi use hua: `./configure && make && make altinstall`

## 13.2 Makefile ka structure

```make
target: prerequisites
<TAB>recipe (shell command)
```

> ⚠️ **Recipe se pehle TAB hona zaroori hai, spaces nahi.**

```make
APP := employee-api

.PHONY: build test clean

build:
	go build -o bin/$(APP) ./...

test:
	go test ./... -cover

clean:
	rm -rf bin
```

```bash
make            # pehla target (default)
make test
make -n build   # dry-run (sirf commands dikhao)
make -j4        # parallel
```

| Concept | Matlab |
|---|---|
| **Target** | Jo banana hai (file ya action ka naam) |
| **Prerequisite** | Target ke liye pehle chahiye |
| **Recipe** | Banane ki shell commands |
| `.PHONY` | Aisa target jo file nahi, sirf action hai (jaise `test`, `clean`). Isse same naam ki file hone par bhi chalta hai |
| Variables | `NAME := value` (turant evaluate), `NAME = value` (jab use ho), use: `$(NAME)` |
| Automatic variables | `$@` = target, `$<` = pehla prerequisite, `$^` = saare prerequisites |
| Pattern rule | `%.o: %.c` = har `.c` se `.o` |
| `@` prefix | Command ko print mat karo (`@echo hi`) |
| `-` prefix | Error ignore karo |

**DevOps use:** Makefile ko project ka "command menu" banate hain: `make build`, `make test`, `make docker-build`, `make deploy`. CI mein bhi `make test` hi chalta hai, taaki local aur CI same commands use karein.

| Error | Reason / Fix |
|---|---|
| `*** missing separator` | Recipe mein TAB ki jagah spaces |
| `No rule to make target 'x'` | Target ya prerequisite file nahi mili / naam galat |
| `Nothing to be done for 'x'` | Target already up-to-date (ya `.PHONY` chahiye) |
| `make: command not found` | `sudo apt install make` (ya `build-essential`) |

## 13.3 🎯 Make — Interview Q&A

**Q1. Make kya karta hai?** Makefile ke rules se targets banata hai aur timestamp dekh kar sirf zaroori kaam karta hai.

**Q2. `.PHONY` kyun?** Taaki `clean`/`test` jaise action targets hamesha chalein, chahe usi naam ki file maujood ho.

**Q3. `=` aur `:=` mein farak?** `:=` definition ke time evaluate hota hai, `=` use hone ke time (recursive).

**Q4. `$@`, `$<`, `$^`?** Target, pehla prerequisite, saare prerequisites.

**Q5. Make ko DevOps mein kaise use karte ho?** Common commands (build/test/lint/docker) ka standard interface, local aur CI dono mein.

**Q6. Make vs Maven vs npm scripts?** Make generic aur language-independent hai; Maven Java ke liye lifecycle + dependencies deta hai; npm scripts JS ecosystem mein tasks chalate hain.

---

# 14. Migrate (Database Migrations)

> ⚠️ Backlog mein tool ka exact naam nahi likha. DevOps/Go context mein "migrate" aam taur par **golang-migrate** (`migrate` CLI) hota hai, isliye yahan wahi aur database-migration ka concept cover hai. Agar tumhare doc mein koi aur tool tha (Flyway, Alembic...), toh concept same rahega.

## 14.1 Database migration kya hai?

Database ke **schema changes** (table banana, column add karna, index) ko **versioned scripts** ki tarah code ke saath manage karna, taaki har environment (dev, staging, prod) par database ek hi tarah update ho.

**Kyun?**
- Schema ko Git mein version control karna
- Manual SQL chalane se galtiyan bachna
- Repeatable, ordered, audit-able changes
- Rollback ka plan (`down`)
- CI/CD mein automate karna

## 14.2 golang-migrate kaise kaam karta hai

**Migration files ki jodi (up + down):**
```text
db/migrations/
├── 000001_create_users.up.sql      # change lagao
├── 000001_create_users.down.sql    # change wapas lo
├── 000002_add_email_index.up.sql
└── 000002_add_email_index.down.sql
```

```sql
-- 000001_create_users.up.sql
CREATE TABLE users (id SERIAL PRIMARY KEY, name TEXT NOT NULL);

-- 000001_create_users.down.sql
DROP TABLE users;
```

**Tracking:** migrate database mein `schema_migrations` table banata hai jisme **current version** aur **dirty flag** hota hai.

```bash
# Nayi migration files banao
migrate create -ext sql -dir db/migrations -seq create_users

# Sab pending migrations lagao
migrate -path db/migrations \
        -database "postgres://user:pass@localhost:5432/mydb?sslmode=disable" up

migrate -path db/migrations -database "$DB_URL" up 1      # sirf 1 aage
migrate -path db/migrations -database "$DB_URL" down 1    # 1 peeche
migrate -path db/migrations -database "$DB_URL" goto 3    # version 3 par jao
migrate -path db/migrations -database "$DB_URL" version   # current version
migrate -path db/migrations -database "$DB_URL" force 2   # version zabardasti set (dirty fix)
```

| Concept | Matlab |
|---|---|
| **up / down** | Aage lagana / wapas lena |
| **Version** | Migration ka number (sequence ya timestamp) |
| **Dirty state** | Migration beech mein fail hui, DB half-applied. Tool aage badhne se rokta hai |
| **`force V`** | Manually fix karne ke baad version set karta hai (SQL nahi chalata) |
| **Drivers** | PostgreSQL, MySQL, SQLite, MongoDB... |
| **Sources** | Local files, GitHub, S3... |
| Library mode | Go code ke andar bhi use ho sakta hai (`migrate.New(...)`) |

**Dirty database fix:** error aaye toh pehle jo half-apply hua use manually theek karo, phir `migrate force <last_good_version>`, phir `up` dobara.

## 14.3 CI/CD mein

```text
Build → Test → Image → [Migrate up] → Deploy app
```
- Migration ek alag pipeline step ya Kubernetes **init container/Job** ke roop mein, app deploy se pehle
- Migrations **backward-compatible** rakho (pehle column add, app deploy, baad mein purana column hatao), taaki rolling deploy mein purana app bhi chale
- Ek hi migration file ko kabhi edit mat karo jo already apply ho chuki hai; nayi file banao
- Production se pehle staging par test, aur backup lo

**Alternatives:** Flyway, Liquibase (Java), Alembic (Python/SQLAlchemy), Django migrations.

## 14.4 🎯 Migrate — Interview Q&A

**Q1. DB migration tool kyun?** Schema changes ko version-controlled, repeatable aur automated banane ke liye.

**Q2. `up` aur `down` files kyun?** `up` change lagata hai, `down` rollback deta hai.

**Q3. Dirty state kya hai?** Migration beech mein fail hui; DB half-applied. Manually fix karke `force` se version set karte hain.

**Q4. Production mein migration kaise chalaoge?** Pipeline step ya init container se, backup ke baad, backward-compatible changes ke saath.

**Q5. Applied migration file edit kyun nahi karte?** Dusre environments mein already chal chuki hoti hai; history mismatch hoti hai. Nayi migration banao.

**Q6. Migrate tool kaise jaanta hai ki kya apply hua?** `schema_migrations` table ke version se.

---

# 15. Ansible (Role, Playbook, Inventory, Jinja2, CI/CD)

## 15.1 Ansible Introduction

**Ansible** ek open-source **configuration management, automation aur orchestration** tool hai (Red Hat).

| Pehlu | Detail |
|---|---|
| **Agentless** | Managed nodes par koi agent install nahi; **SSH** (Linux) se kaam |
| **Push-based** | Control node se commands push hote hain |
| **Language** | **YAML** (playbooks), Python (modules) |
| **Idempotent** | Dobara chalane par sirf zaroori changes hote hain |
| **Declarative** | "Kya chahiye" batate ho (`state: present`), "kaise" nahi |

```text
Control Node (Ansible installed)
     |  SSH
     +--> Managed Node 1 (web)
     +--> Managed Node 2 (db)
     +--> Managed Node 3 ...
```

**Kyun?** Manual server setup repeat nahi hota, consistency aur speed, infrastructure as code (Git mein), ek command se hazaaron servers.

### Core terms

| Term | Matlab |
|---|---|
| **Control node** | Jahan Ansible chalta hai |
| **Managed node** | Jinhe manage kiya jaata hai |
| **Inventory** | Servers ki list (groups ke saath) |
| **Module** | Ek kaam ki unit (`apt`, `copy`, `service`, `template`) |
| **Task** | Ek module ka call |
| **Play / Playbook** | Hosts + tasks ka YAML; playbook = plays ki list |
| **Handler** | Sirf tab chalta hai jab `notify` ho (jaise config badle toh restart) |
| **Role** | Reusable, structured automation ka package |
| **Facts** | Host ki auto-collected info (`ansible_distribution`) |
| **Vault** | Secrets ko encrypt karna |
| **Collection** | Modules/roles/plugins ka distribution unit |

```bash
ansible all -i inventory.ini -m ping                 # ad-hoc: connectivity
ansible webservers -i inventory.ini -m apt -a "name=nginx state=present" --become
```

## 15.2 Inventory

### Static inventory

INI format:
```ini
[webservers]
web1 ansible_host=10.0.1.11
web2 ansible_host=10.0.1.12

[dbservers]
db1 ansible_host=10.0.2.21

[prod:children]
webservers
dbservers

[all:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/id_rsa
```

YAML format:
```yaml
all:
  children:
    webservers:
      hosts:
        web1: { ansible_host: 10.0.1.11 }
        web2: { ansible_host: 10.0.1.12 }
    dbservers:
      hosts:
        db1: { ansible_host: 10.0.2.21 }
```

| Cheez | Detail |
|---|---|
| Groups / `:children` | Hosts ko group karna, groups ke group |
| `group_vars/<group>.yml`, `host_vars/<host>.yml` | Variables ko alag files mein |
| Special vars | `ansible_host`, `ansible_user`, `ansible_port`, `ansible_ssh_private_key_file`, `ansible_python_interpreter` |
| `ansible.cfg` | Defaults (inventory path, remote_user, etc.) |

```bash
ansible-inventory -i inventory.ini --list     # JSON
ansible-inventory -i inventory.ini --graph    # tree
ansible-playbook -i inventory.ini site.yml --limit webservers
```

### Dynamic inventory

Servers ki list **runtime par kisi source se** aati hai (jahan servers bante-bigadte rehte hain), hardcode nahi.

| Source | Kaise |
|---|---|
| **Cloud** (AWS, Azure, GCP) | **Inventory plugins**: `amazon.aws.aws_ec2`, `azure.azcollection.azure_rm`, `google.cloud.gcp_compute` |
| **Database / koi aur source** | Custom **script** ya plugin jo JSON return kare |

AWS example (`aws_ec2.yml`):
```yaml
plugin: amazon.aws.aws_ec2
regions: [ap-south-1]
filters:
  tag:Environment: prod
keyed_groups:
  - key: tags.Role
    prefix: role
```
```bash
ansible-inventory -i aws_ec2.yml --graph
ansible-playbook -i aws_ec2.yml site.yml
```

**Custom script ka contract:** `--list` par JSON de (groups + `_meta.hostvars`), `--host <name>` par ek host ke vars.
```json
{
  "webservers": { "hosts": ["10.0.1.11", "10.0.1.12"] },
  "_meta": { "hostvars": { "10.0.1.11": { "ansible_user": "ubuntu" } } }
}
```
Database se hosts nikalne wali script ye JSON print karti hai. (🔗 JSON processing ke liye jq: `ansible-inventory --list | jq '.webservers'`.)

| Static | Dynamic |
|---|---|
| Fixed servers, chhota setup | Autoscaling/cloud, servers badalte rehte hain |
| Manual update | Automatically current |
| Simple | Setup thoda complex (credentials, plugin) |

## 15.3 Playbook

```yaml
---
- name: Configure web servers
  hosts: webservers
  become: true
  vars:
    app_port: 8080

  tasks:
    - name: Install nginx
      ansible.builtin.apt:
        name: nginx
        state: present
        update_cache: true

    - name: Copy nginx config from template
      ansible.builtin.template:
        src: nginx.conf.j2
        dest: /etc/nginx/nginx.conf
      notify: Restart nginx

    - name: Ensure nginx is running and enabled
      ansible.builtin.service:
        name: nginx
        state: started
        enabled: true

  handlers:
    - name: Restart nginx
      ansible.builtin.service:
        name: nginx
        state: restarted
```

```bash
ansible-playbook -i inventory.ini site.yml
ansible-playbook site.yml --syntax-check       # sirf syntax
ansible-playbook site.yml --check --diff       # dry-run, kya badlega dikhao
ansible-playbook site.yml --limit web1 --tags nginx -e "app_port=9090" -v
ansible-playbook site.yml --ask-vault-pass
```

| Feature | Matlab |
|---|---|
| `become: true` | sudo/root privilege |
| `when:` | Condition (`when: ansible_distribution == "Ubuntu"`) |
| `loop:` | Repeat (`loop: [git, curl]`) |
| `register:` | Task ka output variable mein |
| `tags:` | Selected tasks chalao |
| `block / rescue / always` | Error handling |
| `serial:` | Rolling update (batches mein) |

**Idempotency:** `apt state=present` dobara chalane par `changed=0`. `command`/`shell` modules idempotent nahi hote, isliye `creates:`/`when:` ya proper module use karo.

**Playbook SOP ki main baatein (validation):** purpose clear ho · required inputs/variables listed · `--syntax-check` → `--check --diff` → real run · dobara run par `changed=0` (idempotency) · tasks ke `name:` descriptive · secrets Vault mein.

## 15.4 Role aur Directory Structure

**Role** playbook ko reusable aur organized banata hai. `ansible-galaxy init nginx` se structure banta hai.

```text
roles/nginx/
├── tasks/main.yml        # Role ke main tasks
├── handlers/main.yml     # Handlers (restart, reload)
├── defaults/main.yml     # Default variables (sabse LOW priority, easily override)
├── vars/main.yml         # Role variables (HIGH priority, override mushkil)
├── templates/            # Jinja2 templates (*.j2)
├── files/                # Static files (as-is copy)
├── meta/main.yml         # Role dependencies + Galaxy metadata
├── tests/                # Simple test playbook + inventory
├── library/              # Custom modules (optional)
└── README.md
```

| Directory | Purpose |
|---|---|
| `tasks/` | Role ka kaam (`main.yml` entry point) |
| `handlers/` | `notify` se trigger hone wale tasks |
| `defaults/` | User ke override ke liye default values |
| `vars/` | Internal constants (high precedence) |
| `templates/` | Variables wale config files (Jinja2) |
| `files/` | Bina badle copy hone wali files |
| `meta/` | Dependencies (`dependencies: [common]`), author, platforms |
| `tests/` | Role ko test karne ka basic playbook |

> 🔑 **`defaults` vs `vars`:** `defaults` sabse kam precedence (override karna aasaan), `vars` zyada (override mushkil). User-configurable values `defaults` mein rakho.

Playbook mein role use:
```yaml
- hosts: webservers
  become: true
  roles:
    - nginx
    - { role: app, app_port: 9090 }
```

## 15.5 Jinja2 Templating

Ansible **Jinja2** se dynamic config files banata hai. `template` module `.j2` file ko render karke target par copy karta hai.

| Syntax | Matlab |
|---|---|
| `{{ variable }}` | Value print |
| `{% if cond %} ... {% endif %}` | Condition |
| `{% for item in list %} ... {% endfor %}` | Loop |
| `{# comment #}` | Comment |
| `{{ var \| default('x') }}` | Filter: default |
| `{{ name \| upper }}`, `{{ data \| to_nice_json }}` | Filters |

`nginx.conf.j2`:
```jinja
worker_processes {{ ansible_processor_vcpus }};

server {
    listen {{ app_port | default(80) }};
    server_name {{ server_name }};
{% if enable_ssl %}
    ssl_certificate {{ ssl_cert_path }};
{% endif %}
}
```
- Facts (`ansible_*`) aur variables dono templates mein use hote hain.
- `template` (Jinja2 render) vs `copy` (as-is): variables chahiye toh `template`.

## 15.6 CI/CD Workflow (Role aur Playbook, ek hi jagah)

### CI (Continuous Integration): code merge se pehle quality

```text
Git push / Pull Request
   |
   v
1. Lint            yamllint  +  ansible-lint
2. Syntax check    ansible-playbook site.yml --syntax-check
3. Dry-run         ansible-playbook site.yml --check --diff   (test inventory par)
4. Test (roles)    Molecule (Docker container mein role chalao)
5. Idempotency     Dobara chalao → changed=0 hona chahiye
   |
   v
Pass → merge     |   Fail → PR block
```

### CD (Continuous Delivery/Deployment): servers par lagana

```text
Merge to main
   |
   v
Staging inventory par ansible-playbook  →  verify (smoke tests)
   |
   v
Approval (manual gate)
   |
   v
Production inventory par ansible-playbook  (serial: rolling, --limit, tags)
   |
   v
Notify (Slack/email)
```

| | **Role** | **Playbook** |
|---|---|---|
| CI focus | Lint, **Molecule tests**, idempotency | Lint, syntax-check, `--check --diff` |
| CD / release | Versioned release (Git tag) → **Ansible Galaxy / Git** par publish | **Inventory par deploy** (staging → prod) |
| Secrets | Role mein nahi; consumer deta hai | **Vault / Jenkins credentials** |

```groovy
pipeline {
  agent any
  stages {
    stage('Lint')   { steps { sh 'yamllint . && ansible-lint' } }
    stage('Syntax') { steps { sh 'ansible-playbook -i inventories/staging site.yml --syntax-check' } }
    stage('Check')  { steps { sh 'ansible-playbook -i inventories/staging site.yml --check --diff' } }
    stage('Deploy Staging') { steps { sh 'ansible-playbook -i inventories/staging site.yml' } }
    stage('Approval') { steps { input 'Deploy to production?' } }
    stage('Deploy Prod')    { steps { sh 'ansible-playbook -i inventories/prod site.yml' } }
  }
}
```
**Best practices:** secrets Vault/Jenkins credentials mein, Git mein nahi · versions pin (collections/roles `requirements.yml`) · small roles · idempotent tasks · `--limit`/`serial` se controlled rollout.

## 15.7 🎯 Ansible — Interview Q&A

**Q1. Ansible agentless kaise?** Managed nodes par koi agent nahi, SSH (aur Python) se modules push hote hain.

**Q2. Idempotency kya hai?** Playbook baar-baar chalane par system ek hi final state par rehta hai; sirf zaroori changes hote hain (`changed=0`).

**Q3. Playbook, play, task, module mein farak?** Playbook = plays ki file; play = hosts + tasks; task = ek module ka call; module = kaam ki unit.

**Q4. Handler kya hai?** Task jo sirf `notify` hone par (change ke baad), play ke end mein chalta hai, jaise service restart.

**Q5. `defaults` aur `vars` mein farak?** `defaults` lowest precedence (override easy), `vars` high precedence.

**Q6. `template` aur `copy` mein farak?** `template` Jinja2 variables render karta hai, `copy` file as-is copy karta hai.

**Q7. Static aur dynamic inventory?** Static fixed file; dynamic runtime par cloud/DB se hosts laata hai.

**Q8. Dynamic inventory ka script kya return karta hai?** `--list` par groups aur `_meta.hostvars` wala JSON.

**Q9. `--check` aur `--syntax-check`?** `--syntax-check` sirf YAML/syntax dekhta hai. `--check` (dry-run) batata hai kya change hoga, bina lagaye.

**Q10. Secrets kaise manage karte ho?** Ansible Vault (`ansible-vault encrypt`) ya CI credentials; plain text mein Git mein nahi.

**Q11. Role aur playbook CI mein farak?** Role par Molecule tests aur Galaxy/Git release; playbook par syntax/check mode aur inventory par staging→prod deploy.

**Q12. Rolling update kaise karoge?** `serial: 2` (batches), `--limit`, health checks, aur `max_fail_percentage`.

**Q13. Ansible vs Terraform?** Ansible configuration management (servers ke andar kya hai), Terraform infrastructure provisioning (servers/networks banana). Aksar saath use hote hain.

**Q14. `ansible.cfg` mein kya?** Defaults: inventory path, remote user, SSH settings, roles path, etc.

---
# 16. Jenkins Shared Library

## 16.1 Shared Library kya hai?

**Jenkins Shared Library** reusable pipeline code ka collection hai (Groovy), jo **alag Git repository** mein rehta hai aur **kai Jenkinsfiles** use kar sakti hain.

**Problem jo solve karta hai:** 50 projects ke Jenkinsfile mein build/test/notify ka same code copy-paste hota hai. Ek jagah badalna ho toh 50 jagah badlo. Shared library mein code ek baar likho, sab use karein.

## 16.2 Structure (vars, src, resources)

```text
shared-library-repo/
├── vars/                     # Global variables / custom pipeline steps
│   ├── notifyPipeline.groovy      → step ka naam = file ka naam
│   └── notifyPipeline.txt         → (optional) step ki documentation
├── src/                      # Groovy classes (packages ke saath)
│   └── org/company/utils/
│       └── BuildHelper.groovy
└── resources/                # Non-Groovy files (scripts, templates, JSON)
    └── scripts/check.sh
```

| Folder | Kaam | Kab use karein |
|---|---|---|
| **`vars/`** | Har `.groovy` file ek **custom step** banti hai, `call()` method ke saath. Jenkinsfile mein seedha naam se call | Simple, reusable steps (notify, build, deploy) |
| **`src/`** | Standard Groovy **classes** (`org/foo/Class.groovy`) | Complex logic, OOP, helper classes, testable code |
| **`resources/`** | Non-Groovy files, `libraryResource('path')` se padhte hain | Shell scripts, config templates, email HTML |

### `vars/` example (step)

```groovy
// vars/notifyPipeline.groovy
def call(Map config = [:]) {
    String status = config.status ?: currentBuild.currentResult
    String channel = config.channel ?: '#ci'
    echo "Notify ${channel}: ${env.JOB_NAME} #${env.BUILD_NUMBER} is ${status}"
    // yahan Slack/email step aayega
}
```

### `src/` example (class)

```groovy
// src/org/company/utils/BuildHelper.groovy
package org.company.utils

class BuildHelper implements Serializable {
    def steps                                   // pipeline ke steps (sh, echo) ka reference
    BuildHelper(steps) { this.steps = steps }

    def runTests(String cmd) {
        steps.sh cmd
    }
}
```
> `src/` classes ko pipeline steps (`sh`, `echo`) seedhe nahi milte, isliye `steps`/`script` object **pass** karna padta hai. Classes `Serializable` honi chahiye (pipeline pause/resume ke liye).

### Jenkinsfile mein use

```groovy
@Library('my-shared-lib@main') _        // library load (name@version)
import org.company.utils.BuildHelper    // src class chahiye toh

pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                script { new BuildHelper(this).runTests('mvn test') }
            }
        }
    }
    post {
        always { notifyPipeline(status: currentBuild.currentResult) }   // vars step
    }
}
```
- `@Library('name@version') _` mein `_` zaroori hai jab agli line mein `import` na ho.
- `@main` = branch, ya **tag** (`@v1.2.0`) ya commit SHA. Production mein **tag/version pin** karo.
- Dynamic load: `library 'my-shared-lib@main'`.

## 16.3 Setup

**Manage Jenkins → System → Global Pipeline Libraries**: Name, Default version, Retrieval method = Modern SCM (Git repo URL + credentials).

| Option | Matlab |
|---|---|
| **Load implicitly** | Har pipeline mein bina `@Library` ke load |
| **Allow default version to be overridden** | Jenkinsfile mein `@Library('x@branch')` se version badalne do |
| **Global library** | **Trusted**, sandbox ke bahar chalti hai (admin-controlled) |
| **Folder / project library** | **Sandboxed** (restricted), kuch methods ke liye script approval chahiye |

## 16.4 Workflow

```text
Developer → shared library repo update (PR + review + tag)
                |
Jenkinsfile (@Library('lib@v1.2.0') _)
                |
Pipeline run → Jenkins library ko Git se checkout (build ke time) → steps/classes load → chalao
```

## 16.5 Advantages / Disadvantages

| ✅ Advantages | ❌ Disadvantages |
|---|---|
| DRY: code ek jagah, reuse har jagah | Library mein bug aaye toh **sab pipelines** affect |
| Ek update se sab projects mein standard | Groovy/CPS ki limitations seekhni padti hain |
| Standardization, governance | Debug mushkil (pipeline ke andar) |
| Jenkinsfile chhote aur readable | Versioning discipline chahiye |
| Complex logic `src/` mein testable | Sandbox/script approval ka overhead |

## 16.6 Best Practices

- **Version pin** karo (tag), `main` par production mat chalao
- Steps chhote aur single-purpose; parameters `Map` mein do
- Heavy logic ke liye `src/` classes, steps ke liye `vars/`
- **Secrets** hamesha Jenkins credentials (`withCredentials`) se; library mein hardcode nahi
- `vars/*.txt` mein documentation
- Unit tests (**JenkinsPipelineUnit**)
- Library repo par **PR review** + semantic versioning
- `@NonCPS` sirf zaroorat par (jab CPS-incompatible code ho, jaise kuch collection operations); usme pipeline steps mat chalao
- Backward compatibility rakho; breaking change par naya major version

## 16.7 🎯 Shared Library — Interview Q&A

**Q1. Shared library kyun?** Duplicate pipeline code hatane aur standardization ke liye.

**Q2. `vars` aur `src` mein farak?** `vars` mein global variables/custom steps (`call()`), `src` mein Groovy classes. `resources` mein non-Groovy files.

**Q3. Library ko Jenkinsfile mein kaise load karte hain?** `@Library('name@version') _`. Dynamic ke liye `library 'name@version'`.

**Q4. `@Library('x@v1.0') _` mein `_` kyun?** Annotation ko kisi statement se attach hona hota hai; import na ho toh `_` use hota hai.

**Q5. `src` class se `sh` kaise chalate ho?** Pipeline ka `steps`/`this` object class ko pass karte ho.

**Q6. Global vs folder library?** Global trusted (sandbox ke bahar), folder-level sandboxed.

**Q7. Library version kaise manage karte ho?** Git tags, Jenkinsfile mein tag pin, semantic versioning.

**Q8. Declarative vs Scripted pipeline?** Declarative structured/limited syntax (`pipeline {}`), Scripted flexible Groovy (`node {}`). Shared libraries dono mein chalti hain.

**Q9. `@NonCPS` kya hai?** Method ko CPS transformation se bahar rakhta hai (non-serializable Groovy operations ke liye); usme pipeline steps nahi chalte.

---

# 17. SonarQube

## 17.1 Kya hai, kyun?

**SonarQube** ek **continuous code quality aur security inspection** platform hai. Source code ka **static analysis** karta hai (code chalaye bina), bugs, vulnerabilities aur code smells dhundta hai.

**Kyun?**
- Galtiyan **merge se pehle** pakadna
- Code quality ka objective measure (coverage, duplication, complexity)
- Security vulnerabilities aur hotspots
- Quality ko **gate** bana ke pipeline ko pass/fail karna
- 30+ languages support (Java, Python, JS/TS, Go, C#, ...)

## 17.2 Key concepts

| Term | Matlab |
|---|---|
| **Bug** | Code mein galti jo failure laa sakti hai |
| **Vulnerability** | Security weakness |
| **Security Hotspot** | Security-sensitive code jise **review** karna hai |
| **Code Smell** | Maintainability issue (kharab design, complex code) |
| **Coverage** | Tests kitna code cover karte hain (coverage report import hoti hai; SonarQube khud tests nahi chalata) |
| **Duplications** | Repeat hua code |
| **Technical Debt** | Issues theek karne mein lagne wala estimated time |
| **Quality Profile** | Rules ka set (language-wise) |
| **Quality Gate** | Pass/fail conditions (jaise new code par coverage ≥ 80%, koi new bug nahi) |
| **New Code / Clean as You Code** | Sirf **naye/badle** code par standard lagao, purane debt par nahi atko |
| **Ratings (A–E)** | Reliability, Security, Maintainability |

## 17.3 Architecture

```text
Developer → CI (Jenkins) → SonarScanner  --report-->  SonarQube Server
                                                         |-- Web server (UI/API)
                                                         |-- Compute Engine (report process)
                                                         |-- Search (Elasticsearch)
                                                         |
                                                         v
                                                     Database (PostgreSQL)
```

- **SonarScanner** (CLI / Maven plugin / Gradle plugin) code analyse karke report server ko bhejta hai.
- Server report process karke dashboard aur Quality Gate result deta hai.
- **Editions:** Community (free), Developer, Enterprise, Data Center (branch/PR analysis jaisi features paid editions mein).

## 17.4 Setup aur use

```bash
# Quick local server (Docker)
docker run -d --name sonarqube -p 9000:9000 sonarqube:community
# UI: http://localhost:9000  (pehli baar admin / admin, password badalna padega)

# Linux host par Elasticsearch ke liye kernel settings (sysctl, section 8.8)
sudo sysctl -w vm.max_map_count=262144
```

`sonar-project.properties` (project root):
```properties
sonar.projectKey=employee-api
sonar.projectName=Employee API
sonar.sources=src
sonar.host.url=http://sonar.example.com:9000
# Token CI credentials se do, file mein hardcode nahi:
# sonar-scanner -Dsonar.token=$SONAR_TOKEN
```

```bash
sonar-scanner -Dsonar.token=$SONAR_TOKEN          # generic
mvn clean verify sonar:sonar -Dsonar.token=$SONAR_TOKEN   # Maven
```

**Coverage import:** Java → JaCoCo XML, Python → `coverage.xml`, Go → coverprofile, JS → lcov. Pehle tests chalao + coverage report banao, phir scan.

### Jenkins integration

```groovy
stage('SonarQube Analysis') {
    steps {
        withSonarQubeEnv('MySonarServer') {          // Jenkins mein configured server
            sh 'mvn clean verify sonar:sonar'
        }
    }
}
stage('Quality Gate') {
    steps {
        timeout(time: 5, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true    // gate fail → pipeline fail
        }
    }
}
```
`waitForQualityGate` ke kaam ke liye SonarQube mein **webhook** (Jenkins URL par) configure hona chahiye.

## 17.5 Workflow

```text
Commit/PR → CI build + tests (+coverage) → SonarScanner → SonarQube analysis
        → Quality Gate PASS → merge/deploy
        → Quality Gate FAIL → pipeline fail, developer fix
```

## 17.6 Advantages / Disadvantages

| ✅ Advantages | ❌ Disadvantages |
|---|---|
| Early bug/vulnerability detection | Server aur DB maintain karna padta hai |
| Quality Gate se enforcement | False positives ho sakte hain (tuning chahiye) |
| Multi-language, CI/CD integration | Advanced features (PR/branch analysis) paid editions mein |
| Trends, technical debt, dashboards | Static analysis runtime bugs nahi pakadta |
| "Clean as You Code" legacy projects ke liye practical | Memory/CPU heavy (Elasticsearch) |

## 17.7 Best Practices

- **Quality Gate** pipeline mein enforce karo (`abortPipeline: true`)
- **New code** par focus (Clean as You Code)
- **Token** CI secrets mein, `sonar.token` ke roop mein
- Coverage report scan se pehle generate karo
- Quality Profiles ko team ke standard ke hisaab se tune karo
- Security Hotspots review karo
- Server ke liye persistent DB (PostgreSQL), backups, aur `vm.max_map_count`
- Version-controlled `sonar-project.properties`

## 17.8 🎯 SonarQube — Interview Q&A

**Q1. SonarQube kya karta hai?** Static code analysis: bugs, vulnerabilities, code smells, coverage, duplication ko measure karke Quality Gate se pass/fail deta hai.

**Q2. Quality Gate vs Quality Profile?** Profile = kaun se rules lagenge. Gate = pass/fail ki conditions (metrics ke thresholds).

**Q3. Bug, vulnerability, code smell, hotspot mein farak?** Bug = galti, vulnerability = security weakness, smell = maintainability issue, hotspot = security-sensitive code jise human review chahiye.

**Q4. Coverage SonarQube khud nikalta hai?** Nahi. Tests aur coverage tool (JaCoCo, coverage.py) chalte hain, report SonarQube ko import hoti hai.

**Q5. "Clean as You Code" kya hai?** Quality gate naye/badle code par lagao, purane debt par nahi, taaki code gradually behtar ho.

**Q6. Jenkins mein gate fail par pipeline kaise rokte ho?** `waitForQualityGate abortPipeline: true`, webhook ke saath.

**Q7. SonarQube ko authenticate kaise karte ho?** Token (`sonar.token`), CI credentials se.

**Q8. SonarQube server ko Linux par kya kernel setting chahiye?** `vm.max_map_count=262144` (Elasticsearch ke liye), aur file descriptors limit.

**Q9. SonarQube vs SonarCloud?** SonarQube self-hosted, SonarCloud SonarSource ki hosted SaaS (naam/branding badal sakti hai, official docs dekho).

---

# 18. VCS (Version Control System)

## 18.1 VCS kya hai, kyun?

**Version Control System** files ke changes ka **history** track karta hai: kisne, kab, kya badla, aur kisi bhi purane version par wapas jaane deta hai.

**Kyun?** Team collaboration, history/audit, rollback, branching (parallel kaam), backup, CI/CD trigger (code push par pipeline).

## 18.2 VCS ke types

| Type | Kaise kaam karta hai | Examples | Nuksan |
|---|---|---|---|
| **Local** | Ek hi machine par versions (copy/RCS) | RCS | Collaboration nahi |
| **Centralized (CVCS)** | Ek central server, developers wahin se check-out/commit | SVN, CVS, Perforce | Server down = kaam band, single point of failure |
| **Distributed (DVCS)** | Har developer ke paas **poori repo history** (clone) | **Git**, Mercurial | Seekhne mein thoda complex |

```text
Centralized:  Dev1 ─┐            Distributed:  Dev1 (full repo) ─┐
              Dev2 ─┼─> Server                  Dev2 (full repo) ─┼─> Remote (GitHub/GitLab)
              Dev3 ─┘                           Dev3 (full repo) ─┘
```

## 18.3 Git ke core concepts

```text
Working Directory --git add--> Staging Area (Index) --git commit--> Local Repo --git push--> Remote Repo
                                                                   <--git fetch/pull--
```

| Term | Matlab |
|---|---|
| **Repository** | Project + uski poori history |
| **Commit** | Changes ka snapshot (unique SHA ke saath) |
| **Branch** | Commits ki independent line (halka pointer) |
| **HEAD** | Abhi aap kis commit/branch par ho |
| **Remote** | Server par repo (`origin`) |
| **Tag** | Kisi commit ko naam (release, `v1.0.0`) |
| **Merge** | Do branches ko jodna |
| **Rebase** | Commits ko doosre base par dobara lagana (linear history) |
| **Stash** | Adhuri changes ko temporarily rakhna |
| **Cherry-pick** | Ek specific commit doosri branch par lena |
| **`.gitignore`** | Jo files track nahi karni |
| **Hooks** | Events par scripts (pre-commit, pre-push) |

```bash
git init / git clone <url>
git status
git add . ; git commit -m "msg"
git branch feature/x ; git switch -c feature/x
git merge feature/x
git rebase main
git fetch ; git pull ; git push -u origin feature/x
git log --oneline --graph --all
git stash / git stash pop
git tag -a v1.0.0 -m "release"
git cherry-pick <sha>
```

| Confusing pair | Farak |
|---|---|
| `git fetch` vs `git pull` | `fetch` sirf download karta hai, `pull` = fetch + merge |
| `git merge` vs `git rebase` | merge history preserve karta hai (merge commit); rebase history linear karta hai (shared branch par mat karo) |
| `git reset` vs `git revert` | `reset` history badalta hai; `revert` ek naya commit banake change undo karta hai (shared branch par safe) |
| `git clone` vs `git fork` | clone local copy; fork GitHub par apni copy |

**Merge conflict:** do branches ne same lines badli hon. Conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`) hatao, sahi version rakho, `git add`, phir commit.

**Platforms:** GitHub, GitLab, Bitbucket, Azure Repos (Git hosting + PR/MR, CI, access control).

## 18.4 Advantages / Disadvantages (Git)

| ✅ Advantages | ❌ Disadvantages |
|---|---|
| Distributed, offline kaam | Learning curve |
| Fast, lightweight branching | Bade binary files ke liye acha nahi (Git LFS chahiye) |
| Poori history, easy rollback | Galat `reset --hard`/force push se history kho sakti hai |
| Strong CI/CD aur PR ecosystem | Merge conflicts handle karne padte hain |

## 18.5 Best Practices

- Chhote, meaningful commits; clear commit messages (kya + kyun)
- `main` par seedha push nahi, **Pull Request + review**
- Branch protection rules (required reviews, passing CI)
- **Secrets commit mat karo** (agar ho gaya toh rotate karo)
- `.gitignore` shuru se (`node_modules/`, `target/`, `.venv/`)
- Shared branches par `force push` nahi
- Tags se releases, signed commits optionally
- Regularly `pull`/rebase taaki conflicts chhote rahein

## 18.6 🎯 VCS — Interview Q&A

**Q1. VCS kyun?** History, collaboration, rollback, branching.

**Q2. Centralized aur distributed VCS?** Centralized mein ek server (single point of failure); distributed mein har developer ke paas poori history (Git).

**Q3. Git aur GitHub mein farak?** Git version control tool hai; GitHub Git repositories ki hosting platform (PRs, issues, Actions).

**Q4. Staging area kya hai?** Commit se pehle ki jagah jahan tum choose karte ho ki kaunse changes agle commit mein jaayenge.

**Q5. Merge vs rebase?** Merge history preserve (merge commit); rebase linear history, par shared branch par avoid.

**Q6. Reset vs revert?** `reset` history badalta hai; `revert` naya undo commit banata hai (shared branch par safe).

**Q7. Merge conflict kaise solve karoge?** Conflict markers dekh kar sahi code rakho, `git add`, commit.

**Q8. Galti se secret commit ho gaya toh?** Secret turant rotate/revoke karo, phir history se hatao (`git filter-repo`/BFG), team ko batao.

**Q9. `git fetch` vs `git pull`?** `fetch` download, `pull` = fetch + merge.

**Q10. Detached HEAD kya hai?** HEAD kisi branch par nahi, seedha kisi commit par hai. Naye commits kho sakte hain jab tak branch na banao.

---

# 19. Branching Strategy

## 19.1 Kya hai, kyun?

**Branching strategy** team ka agreed rule hai ki branches kaise banengi, kahan merge hongi aur release kaise niklegi.

**Kyun?** Parallel kaam bina conflict ke, stable `main`, predictable releases, CI/CD ke saath alignment, hotfix ka clear raasta.

## 19.2 Popular strategies

### 1) Git Flow

```text
main      ●─────────────────●──────────●   (sirf release/production, tagged)
           \               /          /
release     \        ●────●          /      (release/x.y: final testing)
             \      /               /
develop  ●────●────●────●──────────●──      (integration branch)
          \       /  \
feature    ●─●─●─     ●─●                    (feature/*)
hotfix                          ●───────●    (main se, fix, main + develop mein merge)
```
Branches: `main`, `develop`, `feature/*`, `release/*`, `hotfix/*`.
- **Best for:** scheduled releases, multiple versions maintain, bade teams.
- **Cons:** complex, long-lived branches, merge conflicts, CD ke liye slow.

### 2) GitHub Flow

```text
main  ●────●─────────●─────●
       \   /  \     /
feature ●─●    ●───●        (short-lived branch → PR → review → merge → deploy)
```
Rules: `main` hamesha deployable · feature branch banao · PR + review + CI · merge ke baad deploy.
- **Best for:** web apps, continuous deployment, chhoti/medium teams.
- **Cons:** multiple release versions maintain karna mushkil.

### 3) Trunk-Based Development

```text
main (trunk)  ●─●─●─●─●─●─●─●    (sab chhote, frequent commits; short-lived branches < 1-2 din)
```
Feature **flags** se adhuri feature hidden rakhte hain. Strong CI, automated tests zaroori.
- **Best for:** mature CI/CD, high-performing teams, fast releases.
- **Cons:** disciplined testing aur feature flags chahiye.

### 4) GitLab Flow (environment branches)
`main` → `staging` → `production` branches; changes upstream se downstream promote hote hain.
- **Best for:** environment-based deployment ke saath.

## 19.3 Comparison

| | Git Flow | GitHub Flow | Trunk-Based | GitLab Flow |
|---|---|---|---|---|
| Complexity | High | Low | Low (par discipline high) | Medium |
| Long-lived branches | `main`, `develop` | Sirf `main` | Sirf trunk | env branches |
| Release style | Scheduled | Continuous | Continuous | Env promotion |
| Hotfix | `hotfix/*` | Normal PR | Normal commit/PR | Cherry-pick/env |
| CI/CD fit | Medium | High | **Highest** | High |
| Best for | Versioned products | Web apps | Fast-moving teams | Multi-env deploys |

## 19.4 Naming aur Merge strategies

**Branch naming:** `feature/<ticket>-<short-desc>`, `bugfix/...`, `hotfix/...`, `release/1.4.0`.
Example: `feature/SCRUM-11-python-installer`. Ticket ID se Jira ↔ Git traceability.

| Merge strategy | Kya hota hai | Kab |
|---|---|---|
| **Merge commit** | Branch history + ek merge commit | History preserve karni ho |
| **Squash and merge** | Branch ke saare commits ek commit mein | Clean `main` history |
| **Rebase and merge** | Commits `main` ke upar linear | Linear history |

**Versioning:** Semantic Versioning `MAJOR.MINOR.PATCH` (breaking.feature.fix) + Git tags.

## 19.5 Best Practices

- Branches **short-lived** rakho
- `main` **protected** (PR, review, CI pass required)
- Consistent naming + ticket ID
- Chhote PRs, jaldi merge
- Merge ke baad branch delete
- CI har PR par; `main` hamesha deployable
- Hotfix ka alag, documented raasta
- Tags se release marking

## 19.6 🎯 Branching — Interview Q&A

**Q1. Git Flow aur GitHub Flow mein farak?** Git Flow mein `develop`, `release`, `hotfix` jaisi kai long-lived branches (scheduled releases). GitHub Flow mein sirf `main` + short-lived feature branches (continuous deployment).

**Q2. Trunk-based development kya hai?** Sab developers chhote, frequent commits ek hi main branch (trunk) par; feature flags aur strong CI ke saath.

**Q3. Kaunsi strategy kab choose karoge?** Versioned/scheduled releases → Git Flow. Web app + continuous deploy → GitHub Flow. Mature CI/CD aur fast delivery → Trunk-based.

**Q4. Hotfix ka process?** Production branch se `hotfix/*` banao, fix + test, `main` mein merge aur `develop` (ya trunk) mein bhi, tag lagao.

**Q5. Squash merge kab?** Jab `main` ki history clean chahiye (ek feature = ek commit).

**Q6. Branch protection rules kya hote hain?** `main` par direct push roko, PR review, status checks (CI) pass hona zaroori.

**Q7. Long-lived feature branches ke nuksan?** Bade merge conflicts, integration late, risk zyada.

**Q8. Branch ka naam ticket ID ke saath kyun?** Traceability: Jira ticket aur code change link ho jaate hain.

---
# 20. Master Interview Q&A

## 20.1 Introduction / Project-level

**Q. Apne Sprint-0 ke kaam ke baare mein batao.**
> "Sprint-0 mein foundation DevOps tools par kaam tha. Maine teen cheezein ki: JQ ka documentation (command-line JSON processing aur CI/CD use), Maven ka documentation (build lifecycle, dependency management aur local/remote repository workflow), aur Python installation ka ticket SCRUM-11, jisme maine ek Bash script `python-installer.sh` likhi. Script APT, source tarball aur auto mode support karti hai, SHA256 verify karti hai, idempotent hai, logging aur cleanup karti hai, aur uske liye automated test suite bhi hai."

**Q. Sabse challenging part kaunsa tha?**
Template jawab (apne experience ke hisaab se customize karo): "Python installer mein tarball build aur idempotency. Existing version detect karna, SAME/UPGRADE/DOWNGRADE decide karna, aur fail hone par build directory preserve karna sahi se design karna tha. Aur `auto` mode mein samajhna tha ki `3.13.7` ke liye APT package naam match nahi hota."

**Q. Documentation itni detail mein kyun likhi?**
Taaki koi bhi naya team member us tool ko samajh sake, alternatives ka comparison dikhe (decision justify ho), best practices follow hon, aur POC se reproduce ho sake. Reviewer levels (L0/L1/L2) ke saath review process bhi tha.

**Q. Tum alternatives ka comparison kyun karte ho?**
Decision ko justify karne ke liye. Jaise JSON ke liye jq vs yq vs fx vs Python, build ke liye Maven vs Gradle vs Ant vs sbt. Ek tool ko recommend karte waqt batana padta hai ki kab doosra behtar hoga.

## 20.2 Scenario-based

**S1. CI pipeline mein Python ka specific version install karna hai, APT mein nahi hai. Kya karoge?**
`--method tarball` ya `--method auto` se python.org ka source tarball, SHA256 verify karke, `make altinstall` se `/usr/local/bin/python3.X` par install. System Python ko touch nahi karunga. Project ke liye `venv` use karunga.

**S2. Script do baar chal gayi. Kya Python dobara build hoga?**
Nahi. Script installed version ko target se compare karti hai; `SAME` hone par "Nothing to install" kehkar exit 0 (idempotent).

**S3. Checksum mismatch aa gaya.**
Build rokni hai, bypass nahi karna. Pehle check: archive sahi release hai, hash 64 hex characters ka hai aur trusted source (python.org) se liya hai. Tampered ya corrupted download ho sakta hai.

**S4. Maven build local par chal raha hai, CI par `Could not resolve dependencies` de raha hai.**
Possible: CI agent ko remote/mirror repo ka network access nahi, `settings.xml` mein mirror/credentials missing, ya dependency sirf tumhare local `~/.m2` mein thi (kisi ne `mvn install` kiya tha, remote par publish nahi hua). Fix: dependency ko internal repo mein `deploy` karo aur CI ka `settings.xml` check karo.

**S5. `mvn deploy` par `401 Unauthorized`.**
Credentials CI mein nahi hain ya `settings.xml` ke `<server><id>` aur `pom.xml` ke repository `<id>` match nahi kar rahe. Secrets CI ke secure store se do, Git mein nahi.

**S6. API ka response JSON ke bajaye HTML error page aa gaya aur jq `parse error` de raha hai.**
API ne error page diya (auth/timeout/5xx). `curl -s` se pehle HTTP status check karo (`curl -f` ya `-w '%{http_code}'`), response save karke dekho, tabhi jq lagao. Pipeline ko explicit fail karo.

**S7. Pipeline `jq -r '.status'` se `null` utha raha hai.**
Field ka naam ya path galat hai. `jq 'keys'` ya `jq '.'` se structure dekho. `jq -e` se null par non-zero exit lo taaki pipeline silently pass na ho.

**S8. Team ko ek hi Maven version par build karna hai.**
Maven Wrapper (`mvnw`) commit karo, CI mein `./mvnw` use karo.

**S9. Python build ke baad `import ssl` fail ho raha hai.**
Build ke waqt `libssl-dev` missing tha. Dependencies install karke dobara build. Script ka `check_build_packages` isi problem ko pehle hi pakadta hai.

**S10. Installed Python 3.13.7 hai aur koi `--version 3.13.5` maangta hai.**
Script `DOWNGRADE` detect karke error deti hai (downgrade supported nahi). Alag prefix ya `venv` se handle karna padega.

## 20.3 Behavioral / Process

**Q. Teen tickets mein tumhare liye sabse zyada seekhne wala kaunsa tha aur kyun?**
Template: "Python installer, kyunki wahan design decisions (idempotency, altinstall, checksum) aur testing ek saath aaye. Maine seekha ki script sirf kaam karne se zyada, **safe aur repeatable** honi chahiye."

**Q. Review process kaise tha?**
Har doc mein Author table hai, versions aur L0/L1/L2 reviewer columns. Doc review ke baad update hota hai.

**Q. Agar time hota toh kya improve karte?**
Python script ke liye 5.12 ki list (help exit code, clear error messages, multi-distro, optimizations, container-based tests). JQ/Maven ke POCs ko actual runnable examples ke saath complete karna.

## 20.4 ⚡ Rapid-fire (ek line ke jawab)

| Sawal | Jawab |
|---|---|
| jq ka full form? | Koi official full form nahi; ye ek command-line JSON processor ka naam hai |
| jq raw output flag? | `-r` |
| jq mein array iterate? | `.[]` |
| jq mein filter condition? | `select(...)` |
| jq pipe? | `\|` |
| Maven ka config file? | `pom.xml` |
| POM full form? | Project Object Model |
| Maven coordinates? | `groupId:artifactId:version` |
| Local repo default? | `~/.m2/repository` |
| Remote repo examples? | Maven Central, Nexus, Artifactory |
| Local mein install? | `mvn install` |
| Remote mein publish? | `mvn deploy` |
| Maven lifecycle order? | validate, compile, test, package, verify, install, deploy |
| `.m2` commit karte hain? | Nahi |
| Python tarball install ka safe command? | `make altinstall` |
| Python system install location (APT)? | `/usr/bin` (system), tarball: `/usr/local/bin/python3.X` |
| Installer ke methods? | package, tarball, auto |
| Installer ka log? | `logs/python-installer.log` |
| Build temp dir? | `/tmp/python-build-<version>` |
| Checksum algorithm? | SHA256 (64 hex chars) |
| Downgrade supported? | Nahi |
| `--upgrade` poore system ko upgrade karta hai? | Nahi, sirf requested Python package |
| `set -e` ka kaam? | Command fail par script exit |
| `trap ... EXIT` ka kaam? | Script khatam hone par cleanup |
| Version sort ka command? | `sort -V` |
| Ticket jisme Python installer tha? | SCRUM-11 |

## 20.5 🔗 Cross-topic / End-to-end Questions (poori sprint ko jodne wale)

**Q1. Python (Flask/Django) app ko Ubuntu server par production mein kaise deploy karoge?**
Python install (section 5/9) → project ke liye `venv` → `pip install -r requirements.txt` → **Gunicorn** se app → Gunicorn ko **systemd service** (`enable --now`, `LimitNOFILE`) → **Nginx** reverse proxy → **logrotate** se logs → cron se backups/cleanup → `sysctl`/`ulimit` tuning agar zaroori.

**Q2. Java app ka end-to-end CI/CD batao.**
Git push (branching strategy: feature → PR) → Jenkins (Jenkinsfile + **Shared Library**) → `mvn clean verify` → **SonarQube** scan + Quality Gate → artifact `mvn deploy` se Nexus/Artifactory → **Ansible** playbook se staging → approval → production.

**Q3. Go microservice ko DB ke saath kaise deploy karoge?**
`go test` + `go build` → Docker image → pipeline mein **migrate up** (init container/step) → app deploy. Migrations backward-compatible.

**Q4. React app ki pipeline?**
`npm ci` → lint/test → `npm run build` → static files Nginx/CDN par deploy; SonarQube scan optional.

**Q5. Ansible dynamic inventory ke output ko tum kaise inspect karoge?**
`ansible-inventory -i aws_ec2.yml --list | jq '.'` (JSON, isliye jq se filter).

**Q6. SonarQube server Linux par kyun start nahi ho raha?**
Aksar `vm.max_map_count` kam hai (sysctl se 262144) ya file descriptors/ulimit kam; Java version aur memory bhi check karo.

**Q7. Ek service down hai, troubleshooting steps?**
`systemctl status` → `journalctl -u <svc> -n 100` → port (`ss -tulnp`) → disk (`df -h`, `df -i`) → memory (`free -h`) → config syntax → ulimit → recent change (Git/Ansible run).

**Q8. Har language ki dependency file aur lock file kaun si hai?**

| Ecosystem | Dependency file | Lock / checksum | Install command |
|---|---|---|---|
| Python (pip) | `requirements.txt` | (freeze / pip-tools) | `pip install -r requirements.txt` |
| Python (Poetry) | `pyproject.toml` | `poetry.lock` | `poetry install` |
| Java (Maven) | `pom.xml` | (versions pinned in POM) | `mvn clean install` |
| Go | `go.mod` | `go.sum` | `go mod download` |
| JavaScript (npm) | `package.json` | `package-lock.json` | `npm ci` |

**Q9. Quality aur security shift-left kaise karoge?**
PR par lint + unit tests + SonarQube Quality Gate + dependency scan (`npm audit`, OWASP dependency-check) + branch protection, taaki problems merge se pehle pakdi jayein.

**Q10. Is sprint ka sabse important common principle?**
**Automation + Repeatability + Version control + Security**: sab kuch code mein (Git), scripts idempotent, secrets CI credentials/Vault mein, aur har change CI se validate.

---

# 21. Last-Minute Revision Cheat Sheet

## 21.1 jq

```bash
jq '.'                              # pretty print
jq '.name' f.json                   # field
jq -r '.name' f.json                # raw (bina quotes)
jq '.a.b.c' f.json                  # nested
jq '.items[]' f.json                # array iterate
jq '.items[] | .name' f.json        # pipe
jq '.items[] | select(.x=="IT")' f.json   # filter
jq -e '.status=="success"' r.json   # exit code se check
jq --arg v "$VAR" '.[] | select(.x==$v)' f.json   # shell var
aws ec2 describe-instances | jq -r '.Reservations[].Instances[].InstanceId'
```

## 21.2 Maven

```bash
mvn -v
mvn clean test        # tests tak
mvn clean verify      # verification tak (CI ke liye recommended)
mvn clean package     # JAR/WAR
mvn install           # local repo (~/.m2)
mvn deploy            # remote repo
mvn dependency:tree   # dependency tree
mvn -U ...            # snapshots/dependencies force update
```

```text
Lifecycle: validate → compile → test → package → verify → install → deploy
Local  : ~/.m2/repository   (cache + mvn install)
Remote : Maven Central / Nexus / Artifactory   (mvn deploy)
Git stores source; Maven repo stores artifacts
```

## 21.2b Maven ek line mein
**POM** = config · **GAV** = identity · **Lifecycle** = steps · **Local repo** = cache · **Remote repo** = sharing · **install** = local · **deploy** = remote.

## 21.3 Python installer

```bash
chmod +x python-installer.sh tests/test-installation.sh
bash -n python-installer.sh                               # syntax check
./tests/test-installation.sh                              # tests

./python-installer.sh --version 3.12 --method package
./python-installer.sh --version 3.12 --method package --upgrade
./python-installer.sh --version 3.13.7 --method tarball --sha256 <64-hex>
./python-installer.sh --version 3.13.7 --method auto    --sha256 <64-hex>
./python-installer.sh --version 3.13.7 --method tarball --sha256 <64-hex> --keep-build

cat logs/python-installer.log
/usr/local/bin/python3.13 --version
echo "<sha>  Python-3.13.7.tgz" | sha256sum -c -
```

```text
Tarball: Validate → Existing? → SHA format → Deps → Download → Verify SHA → Extract
         → configure --prefix=/usr/local → make -j$(nproc) → sudo make altinstall → Verify → Cleanup
Auto   : APT package milta hai? → Haan: APT | Nahi: Tarball
States : SAME (skip) | UPGRADE (--upgrade chahiye) | DOWNGRADE (error)
Flags  : --version --method --sha256 --upgrade --keep-build --help
```

## 21.4 Top 12 baatein jo interview se pehle ek baar zaroor padho

1. jq CI/CD platform nahi, JSON processing component hai.
2. `-r` shell comparisons ke liye zaroori hai.
3. Maven: **Git ≠ Maven repository**.
4. `install` = local, `deploy` = remote.
5. Dependency resolution: pehle local, phir remote, phir local mein cache.
6. Lifecycle mein ek phase chalane par uske pehle ke saare phases chalte hain.
7. Installer: `altinstall` system Python ko safe rakhta hai.
8. Installer: SHA256 mismatch = build STOP.
9. Installer: idempotent (SAME = Nothing to install), downgrade unsupported.
10. `set -euo pipefail` + `trap cleanup EXIT` = safe script.
11. Auto mode: `python3.13.7` APT naam nahi hai → tarball fallback.
12. Tests: exit code **aur** output text dono check hote hain.

## 21.5 Naye topics ka quick cheat sheet

```bash
# ---- Ubuntu ----
sudo apt update && sudo apt install -y <pkg>        # install
sudo systemctl enable --now <svc> ; systemctl status <svc> ; journalctl -u <svc> -f
df -h ; du -sh * ; df -i ; lsblk ; ulimit -n ; cat /proc/<pid>/limits
crontab -e ; crontab -l ; grep CRON /var/log/syslog
sudo logrotate -d /etc/logrotate.d/<app>            # dry-run
sudo sysctl -w vm.max_map_count=262144 ; sudo sysctl --system

# ---- Python ----
python3 -m venv .venv && source .venv/bin/activate ; pip freeze > requirements.txt ; deactivate
poetry add <pkg> ; poetry install ; poetry run <cmd>
gunicorn -w 4 -b 0.0.0.0:8000 app:app

# ---- Java / Go / Node ----
java -version ; sudo update-alternatives --config java ; mvn dependency:tree
go mod init <mod> ; go mod tidy ; go test ./... -cover ; go build ./...
npm ci ; npm run build ; npm audit

# ---- Make / Migrate ----
make <target> ; make -n <target>
migrate -path db/migrations -database "$DB_URL" up|down 1|version|force <v>

# ---- Ansible ----
ansible all -i inv -m ping
ansible-playbook -i inv site.yml --syntax-check | --check --diff | --limit web1 | --tags x
ansible-inventory -i inv --graph ; ansible-galaxy init <role> ; ansible-vault encrypt <file>

# ---- Git ----
git switch -c feature/SCRUM-11-x ; git add . ; git commit -m "..." ; git push -u origin HEAD
git fetch ; git rebase main ; git log --oneline --graph --all
```

```text
Shared Library : vars/ (steps, call())  src/ (classes)  resources/ (files)  |  @Library('lib@v1') _
SonarQube      : Scanner → Server → Quality Gate | waitForQualityGate abortPipeline: true | vm.max_map_count
Ansible Role   : tasks handlers defaults(low) vars(high) templates files meta tests
Branching      : Git Flow (develop/release/hotfix) | GitHub Flow (main + PR) | Trunk-based (flags)
VCS            : Local → Centralized (SVN) → Distributed (Git) ; fetch=download, pull=fetch+merge
```

---

# 22. Repo ki Gaps / Placeholders (Honest Notes)

Interview se pehle ye jaan lo, taaki koi pooche toh sahi jawab ho:

| # | Cheez | Detail |
|---|---|---|
| 1 | JQ POC | `POC_URL` placeholder hai. POC planned scope hai, link nahi |
| 2 | Maven POC | `<POC_URL>` placeholder hai |
| 3 | Maven doc mein contact | `<Name>` / `<email>` placeholders |
| 4 | Reviewers | JQ doc mein L0/L1/L2 `TBD`; Python docs mein reviewers `—` ya team names |
| 5 | JQ aur Maven ticket IDs | Docs mein explicit nahi (sirf SCRUM-11 hai) |
| 6 | `python-manager-explained.md` | `python_manager.sh` ki explanation hai par wo script file repo mein nahi hai |
| 7 | Test file naam mismatch | Docs mein `test-installations.sh`, asli file `test-installation.sh` |
| 8 | Test log path | Test script `$HOME/python-installer/logs/...` dekhti hai, script `SCRIPT_DIR/logs` mein likhti hai |
| 9 | Branches | Jo ZIP mujhe mila usme sirf **`main`** branch ka content tha. Agar doosri branches mein alag content hai toh unka hissa is guide mein nahi hai |
| 10 | Poori sprint ke baaki topics | Sections 8 se 19 (Ubuntu, Python ecosystem, Java/pom.xml, Go, React/npm, Make, Migrate, Ansible, Shared Library, SonarQube, VCS, Branching) repo ke docs se nahi, **general knowledge** se bane hain, kyunki ye tickets teammates ke the |
| 11 | Ansible Playbook CI | Tumhare naam wala ticket, par repo ki `main` branch mein iska doc nahi tha. Section 15.6 general workflow hai, tumhare doc se match nahi karega |
| 12 | "Migrate" tool | Backlog mein exact tool naam nahi; golang-migrate maana gaya hai |
| 13 | "Setup: API's" | OT-Microservice ke local setup ki instructions Jira comment mein hain, is guide mein nahi |
| 14 | SOP tickets | Dropped (user ki request), unke zaroori commands concept sections mein merge hain |
| 15 | Version-specific facts | Java LTS list, React/CRA status jaise facts time ke saath badalte hain; interview se pehle official docs se ek baar verify kar lo |

---

<p align="center">

**📘 Sprint-0 • JQ • Maven • Python Installation (SCRUM-11) • Interview Ready**

</p>
