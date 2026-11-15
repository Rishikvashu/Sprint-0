# 📘 Sprint-0 Tickets — Complete Study Guide & Interview Prep

> **Ek hi file se poora Sprint-0 study.** Is guide mein repo ke teeno tickets ke saare concepts hain: **JQ**, **Maven** aur **Python Installation (Bash script, SCRUM-11)**. Har topic ke saath commands, diagrams, common errors aur **interview Q&A** diye gaye hain.
>
> Source: repo `Rishikvashu/sprint-0-tickets` (branch `main`). Jo cheezein repo ke docs/code se aayi hain woh as-it-is hain. Jo cheezein main ne interview ke liye **extra** jodi hain woh `🆕 Extra` tag ke saath hain, taaki tum sahi bata sako ki "repo mein kya kiya" aur "mujhe aur kya aata hai".

---

## 📑 Table of Contents

1. [Repo ka Map aur Ticket Mapping](#1-repo-ka-map-aur-ticket-mapping)
2. [Interview Mein Kaise Bolna Hai (60-second Pitch)](#2-interview-mein-kaise-bolna-hai-60-second-pitch)
3. [PART A — JQ](#3-part-a--jq)
4. [PART B — Maven](#4-part-b--maven)
5. [PART C — Python Installation via Bash Script (SCRUM-11)](#5-part-c--python-installation-via-bash-script-scrum-11)
6. [PART D — Bash Concepts Cheat Sheet](#6-part-d--bash-concepts-cheat-sheet)
7. [PART E — Teeno Tickets Ko Jodne Wali Big Picture (CI/CD)](#7-part-e--big-picture-cicd)
8. [PART F — Master Interview Q&A (Mixed, Scenario, Rapid-fire)](#8-part-f--master-interview-qa)
9. [Last-Minute Revision Cheat Sheet](#9-last-minute-revision-cheat-sheet)
10. [Repo ki Gaps / Placeholders (Honest Notes)](#10-repo-ki-gaps--placeholders-honest-notes)

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

# 3. PART A — JQ

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
# 4. PART B — Maven

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
# 5. PART C — Python Installation via Bash Script (SCRUM-11)

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
# 6. PART D — Bash Concepts Cheat Sheet

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

# 7. PART E — Big Picture (CI/CD)

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

# 8. PART F — Master Interview Q&A

## 8.1 Introduction / Project-level

**Q. Apne Sprint-0 ke kaam ke baare mein batao.**
> "Sprint-0 mein foundation DevOps tools par kaam tha. Maine teen cheezein ki: JQ ka documentation (command-line JSON processing aur CI/CD use), Maven ka documentation (build lifecycle, dependency management aur local/remote repository workflow), aur Python installation ka ticket SCRUM-11, jisme maine ek Bash script `python-installer.sh` likhi. Script APT, source tarball aur auto mode support karti hai, SHA256 verify karti hai, idempotent hai, logging aur cleanup karti hai, aur uske liye automated test suite bhi hai."

**Q. Sabse challenging part kaunsa tha?**
Template jawab (apne experience ke hisaab se customize karo): "Python installer mein tarball build aur idempotency. Existing version detect karna, SAME/UPGRADE/DOWNGRADE decide karna, aur fail hone par build directory preserve karna sahi se design karna tha. Aur `auto` mode mein samajhna tha ki `3.13.7` ke liye APT package naam match nahi hota."

**Q. Documentation itni detail mein kyun likhi?**
Taaki koi bhi naya team member us tool ko samajh sake, alternatives ka comparison dikhe (decision justify ho), best practices follow hon, aur POC se reproduce ho sake. Reviewer levels (L0/L1/L2) ke saath review process bhi tha.

**Q. Tum alternatives ka comparison kyun karte ho?**
Decision ko justify karne ke liye. Jaise JSON ke liye jq vs yq vs fx vs Python, build ke liye Maven vs Gradle vs Ant vs sbt. Ek tool ko recommend karte waqt batana padta hai ki kab doosra behtar hoga.

## 8.2 Scenario-based

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

## 8.3 Behavioral / Process

**Q. Teen tickets mein tumhare liye sabse zyada seekhne wala kaunsa tha aur kyun?**
Template: "Python installer, kyunki wahan design decisions (idempotency, altinstall, checksum) aur testing ek saath aaye. Maine seekha ki script sirf kaam karne se zyada, **safe aur repeatable** honi chahiye."

**Q. Review process kaise tha?**
Har doc mein Author table hai, versions aur L0/L1/L2 reviewer columns. Doc review ke baad update hota hai.

**Q. Agar time hota toh kya improve karte?**
Python script ke liye 5.12 ki list (help exit code, clear error messages, multi-distro, optimizations, container-based tests). JQ/Maven ke POCs ko actual runnable examples ke saath complete karna.

## 8.4 ⚡ Rapid-fire (ek line ke jawab)

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

---

# 9. Last-Minute Revision Cheat Sheet

## 9.1 jq

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

## 9.2 Maven

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

## 9.2b Maven ek line mein
**POM** = config · **GAV** = identity · **Lifecycle** = steps · **Local repo** = cache · **Remote repo** = sharing · **install** = local · **deploy** = remote.

## 9.3 Python installer

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

## 9.4 Top 12 baatein jo interview se pehle ek baar zaroor padho

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

---

# 10. Repo ki Gaps / Placeholders (Honest Notes)

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

---

<p align="center">

**📘 Sprint-0 • JQ • Maven • Python Installation (SCRUM-11) • Interview Ready**

</p>
