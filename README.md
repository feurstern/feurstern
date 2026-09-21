<div align="center">

<img width="100%" alt="Muhammad Rio Kurniawan — Software Engineer, Rust and Go backend and network systems" src="https://github.com/user-attachments/assets/2bfa4f95-90dd-420a-b963-721708030f66" style="border-radius: 15px;" />

<br>

<img alt="Software Engineer — Rust, Go, Systems & Network Infrastructure" src="https://readme-typing-svg.demolab.com?font=Poppins&weight=600&size=28&duration=4000&pause=1000&color=8B61C0&center=true&random=false&width=620&lines=Muhammad+Rio+Kurniawan;Software+Engineer+%E2%80%94+Rust+%C2%B7+Go+%C2%B7+Systems">

<p>
  <img alt="GitHub followers" src="https://img.shields.io/github/followers/feurstern?style=for-the-badge&color=8B61C0">
  <img alt="GitHub stars" src="https://img.shields.io/github/stars/feurstern?style=for-the-badge&color=F8D866">
  <img alt="Profile views" src="https://komarev.com/ghpvc/?username=feurstern&color=F85D7F&style=for-the-badge">
  <a href="https://wakatime.com/@76205aa1-14ff-4941-b8f2-8ad9881b5ad4"><img alt="Wakatime" src="https://wakatime.com/badge/user/76205aa1-14ff-4941-b8f2-8ad9881b5ad4.svg?style=for-the-badge"></a>
</p>

</div>

<summary><b>📊 GitHub activity & stats</b></summary>

<div align="center">
  <img src="https://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=feurstern&theme=tokyonight" width="49%" />
  <img src="https://streak-stats.demolab.com/?user=feurstern&theme=tokyonight&hide_border=false" width="49%" />
</div>
<br>
<div align="center">
  <img src="https://github-profile-summary-cards.vercel.app/api/cards/most-commit-language?username=feurstern&theme=tokyonight" width="49%" />
  <img src="https://github-profile-summary-cards.vercel.app/api/cards/repos-per-language?username=feurstern&theme=tokyonight" width="49%" />
</div>
<br>
<div align="center">
  <img alt="Activity graph" src="https://github-readme-activity-graph.vercel.app/graph/?username=feurstern&bg_color=1F222E&color=F8D866&line=F85D7F&point=FFFFFF&hide_border=true" width="100%" />
</div>


# Muhammad Rio Kurniawan — Software Engineer (Rust · Go · Systems & Network Infrastructure)

**Muhammad Rio Kurniawan** — known as **Rio**, and as **`feurstern`** on GitHub — is a software engineer based in Indonesia who builds **backend services, network infrastructure tooling, and low-level systems software**. He currently works as a **Software Engineer at Mediatech Core (D-Net × Xirka)**, an Indonesian internet service provider, where he designs and builds the software that manages and monitors network infrastructure: virtual private servers, Linux servers, DNS, and the internal ERP and provisioning systems that run on top of them.

His working languages are **Rust and Go** for services and systems work, **TypeScript/Vue and Next.js** on the front end, and **PostgreSQL** for data. He has roughly **seven years** of professional experience spanning game development, full-stack web engineering for Indonesian government institutions, and — most recently — network and infrastructure engineering.

---

## At a glance

|                   |                                                                                                                                    |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **Full name**     | Muhammad Rio Kurniawan                                                                                                             |
| **Also known as** | Rio · M Rio K · `feurstern`                                                                                                        |
| **Role**          | Software Engineer — backend, systems, network infrastructure                                                                       |
| **Currently at**  | Mediatech Core (D-Net × Xirka), Indonesia — ISP / network software                                                                 |
| **Core stack**    | Rust · Go · TypeScript · PostgreSQL · Linux · Docker                                                                               |
| **Specialisms**   | eBPF/XDP packet filtering · REST & gRPC services · DDoS mitigation · ERP and monitoring platforms · VPS and Proxmox infrastructure |
| **Also works in** | Vue 3 / Quasar · Next.js · Laravel · PHP · C# (Unity) · Python                                                                     |
| **Education**     | B.Sc. Computer Engineering (Pranata Indonesia, 2021) · Full Stack Web Development certificate, University of Helsinki (2024)       |
| **Languages**     | English · Indonesian · Japanese · German · Korean                                                                                  |
| **Open to**       | Backend, systems, platform and infrastructure engineering roles                                                                    |

---

## What I work on

**Network and systems software.** My most recent work sits close to the kernel: packet classification, rate limiting, and DDoS mitigation on Linux using **Rust compiled to eBPF and attached with XDP**, so hostile traffic is discarded inside the NIC driver's receive path before the kernel ever allocates a socket buffer for it. Day to day at an ISP this also means VPS provisioning, Proxmox virtualisation, DNS and DNSSEC, Nginx, and Debian/Arch server administration.

**Backend services.** I build HTTP and gRPC services in **Rust (Axum, Actix, Tokio)** and **Go (Echo, Fiber, Gin)**, backed by **PostgreSQL** with versioned migrations. I care about layered architecture — transport, service, repository and domain kept separate — dependency injection, and the kind of test suite that can actually tell you something went wrong.

**Full-stack delivery for large organisations.** Before infrastructure I spent several years shipping web platforms for Indonesian government bodies and private clients: corruption-prevention monitoring for the **KPK (Corruption Eradication Commission)**, document automation for the **Ministry of Defence**, personnel systems for the **Indonesian Army**, and an MSME e-commerce marketplace built from scratch. Vue 3/Quasar, Next.js, Laravel, CodeIgniter, Docker.

**Teaching.** I have taught programming and English for several years — privately, at Timedoor Academy, and through non-profits including Gerakan Suka Baca, International Humanity Foundation and Loobit. It is the reason I write documentation the way I do.

---

## Selected projects

### Vanguard — kernel-level DDoS mitigation

**Rust · eBPF · XDP · aya · Linux** · [source](https://github.com/feurstern/vanguard_nsdaf)

Edge DDoS mitigation for Linux. A single XDP program classifies every arriving frame and returns one verdict — malformed headers, allowlist, blocklist with in-data-plane TTL expiry, bogon sources, fragments, invalid TCP flag combinations, per-port rules, per-source token buckets, and an interface-wide backstop limiter. Ships as one standalone binary with the eBPF bytecode embedded, so the loader and the program can never drift out of version step.

It defaults to **monitor mode**: it classifies and counts exactly as enforcing mode does, then passes the packet anyway, so you can measure how much legitimate traffic a policy would have cost you before arming it. Rules live in BPF maps pinned under `/sys/fs/bpf`, so a rule change takes effect on the next packet with no reload, and the blocklist survives a control-plane restart.

Tested in three layers: **40 behavioural tests** that run the real compiled bytecode in the kernel through `BPF_PROG_TEST_RUN`, an integration script that pushes live traffic through a `veth` pair inside a network namespace, and a `pktgen` load harness that measures receive-softirq CPU against unfiltered and `nftables` baselines.

### C6SIR Command Centre — cross-domain threat correlation

**Rust · Python · TypeScript · tokio · Axum · tonic/gRPC · NATS JetStream · Kafka · PostgreSQL + PostGIS · ONNX** · _(internal, not public)_

A command centre that fuses feeds from four Indonesian agencies so a hybrid cyber-physical attack surfaces as one correlated threat instead of four unrelated tickets. Twelve Rust crates, roughly 24,000 lines: CCTV analytics (RTSP → YOLO → zone geometry), anomaly detection over feature windows with robust z-scores and an ONNX autoencoder, six fusion rules, and a DMZ outbox relay. The scoring is designed so that a purely cyber detection cannot reach the critical band on its own — a property enforced by a test rather than asserted in a comment.

### X-MINER — industrial IoT for electro-refining

**Rust · Axum · Vue/Quasar · ESP32 · MQTT · PostgreSQL · Docker** · _(internal, not public)_

Thirty sensor nodes monitoring current, voltage, temperature and power across an electrolysis cell row in a metal refinery, chained through matrix buses to a data concentrator, with real-time dashboards and alarms for overcurrent, undercurrent, overvoltage and overtemperature.

### E-Koorsup & MCP — corruption-prevention monitoring, KPK

**PHP (Laravel, Phalcon) · Vue 2/3 · Quasar · PostgreSQL · Redis · Docker** · [jaga.id](https://jaga.id/) · [bima.kpk.go.id](https://bima.kpk.go.id/)

Platforms used to monitor corruption-prevention progress across Indonesian local governments over eight intervention areas — planning and budgeting, procurement, licensing, internal audit, civil-service management, tax optimisation, asset management and village finances. Included ETL pipelines into a data warehouse, case dashboards, audit trails and access-rights schemes.

### Ladara — MSME e-commerce marketplace

**Laravel · Inertia · Next.js · TypeScript · PostgreSQL · Meilisearch · Midtrans · Docker · Ansible** · [staging.ladara.id](https://staging.ladara.id/)

Built from scratch, including the architecture: backend envelope, database schema, API design, payment-gateway integration, and the CI/CD pipeline from local to staging to production.

### Go microservices

**Go · Echo · Fiber · GORM · PostgreSQL · Docker** · [source](https://github.com/feurstern/go-backend-engineering)

A collection of service implementations — e-commerce API, ERP backend with JWT auth and PDF generation, book management — built around a consistent `cmd`/`pkg` layout with handlers, models, routes and config kept apart.

### Axum microservice reference

**Rust · Axum · Diesel · PostgreSQL** · [source](https://github.com/feurstern/axum-microservice)

A small, clean reference service: `api` / `services` / `models` / `db` / `config` layering, versioned Diesel migrations with down-migrations for users, roles and permissions, and CI on every push.

---

## Technical skills

**Languages** — Rust · Go · TypeScript · JavaScript · PHP · Python · C# · C++ · C · SQL

**Backend & services** — Axum · Actix · Tokio · Echo · Fiber · Gin · Laravel · CodeIgniter · Phalcon · Node.js · REST · gRPC/tonic

**Frontend** — Vue 3 (Composition & Options API) · Quasar · Next.js · React · React Native · Pinia · Redux · Tailwind · Bootstrap

**Data** — PostgreSQL · PostGIS · MySQL · MongoDB · Redis · Diesel · sqlx · GORM · ETL pipelines

**Messaging & streaming** — NATS JetStream · Apache Kafka · RabbitMQ · MQTT

**Systems & networking** — eBPF · XDP · aya · Linux (Debian, Arch) · Nginx · DNS & DNSSEC · packet analysis · systemd

**Infrastructure** — Docker · Proxmox · Ansible · AWS (S3, Lambda) · CI/CD · VPS provisioning

**Machine learning** — Python · PyTorch · ONNX · R · scikit-learn (applied: anomaly detection, object detection)

**Game development** — Unity · C# · Godot · Phaser · Photoshop · Illustrator · Premiere

<details>
<summary><b>Icon wall</b></summary>

<div align="center">

### 🎮 Game Design & Multimedia

<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/illustrator/illustrator-plain.svg" width="45" height="45" title="Illustrator" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/photoshop/photoshop-plain.svg" width="45" height="45" title="Photoshop" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/premierepro/premierepro-plain.svg" width="45" height="45" title="Premiere Pro" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/unity/unity-original.svg" width="45" height="45" title="Unity" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/cplusplus/cplusplus-original.svg" width="45" height="45" title="C++" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/csharp/csharp-original.svg" width="45" height="45" title="C#" />&nbsp;
<img src="https://upload.wikimedia.org/wikipedia/commons/5/5f/FFmpeg_Logo_new.svg" width="112" height="30" title="FFmpeg" />

### 🐧 Linux & OS

<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/archlinux/archlinux-original.svg" width="45" height="45" title="Arch Linux" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/debian/debian-original.svg" width="45" height="45" title="Debian" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/linux/linux-original.svg" width="45" height="45" title="Linux" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/bash/bash-original.svg" width="45" height="45" title="Bash" />

### 🌐 Frontend

<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/css3/css3-original.svg" width="45" height="45" title="CSS3" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/html5/html5-original.svg" width="45" height="45" title="HTML5" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/javascript/javascript-original.svg" width="45" height="45" title="JavaScript" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/typescript/typescript-original.svg" width="45" height="45" title="TypeScript" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/tailwindcss/tailwindcss-original.svg" width="45" height="45" title="Tailwind CSS" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/bootstrap/bootstrap-original.svg" width="45" height="45" title="Bootstrap" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/react/react-original.svg" width="45" height="45" title="React" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/nodejs/nodejs-original.svg" width="45" height="45" title="Node.js" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/nextjs/nextjs-original.svg" width="45" height="45" title="Next.js" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/quasar/quasar-original.svg" width="45" height="45" title="Quasar" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/vuejs/vuejs-original.svg" width="45" height="45" title="Vue.js" />

### ⚙️ Backend

<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/rust/rust-original.svg" width="45" height="45" title="Rust" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/go/go-original.svg" width="45" height="45" title="Go" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/laravel/laravel-original.svg" width="45" height="45" title="Laravel" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/php/php-original.svg" width="45" height="45" title="PHP" />

### 📡 Messaging & Streaming

<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/apachekafka/apachekafka-original.svg" width="45" height="45" title="Apache Kafka" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/nats/nats-original.svg" width="45" height="45" title="NATS / JetStream" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/grpc/grpc-plain.svg" width="45" height="45" title="gRPC" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/rabbitmq/rabbitmq-original.svg" width="45" height="45" title="RabbitMQ" />

### 🗄️ Databases

<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/postgresql/postgresql-original.svg" width="45" height="45" title="PostgreSQL" />&nbsp;
<img src="https://postgis.net/brand.svg" width="45" height="45" title="PostGIS" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/mysql/mysql-original.svg" width="45" height="45" title="MySQL" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/mongodb/mongodb-original.svg" width="45" height="45" title="MongoDB" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/redis/redis-original.svg" width="45" height="45" title="Redis" />

### ☁️ Infrastructure

<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/docker/docker-original.svg" width="45" height="45" title="Docker" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/nginx/nginx-original.svg" width="45" height="45" title="Nginx" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/proxmox/proxmox-original.svg" width="45" height="45" title="Proxmox" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/ansible/ansible-original.svg" width="45" height="45" title="Ansible" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/git/git-original.svg" width="45" height="45" title="Git" />

### 🧠 Machine Learning

<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/python/python-original.svg" width="45" height="45" title="Python" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/pytorch/pytorch-original.svg" width="45" height="45" title="PyTorch" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/tensorflow/tensorflow-original.svg" width="45" height="45" title="TensorFlow" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/r/r-original.svg" width="45" height="45" title="R" />

</div>

</details>

---

## Background

**Software Engineer**, Mediatech Core (D-Net × Xirka) — Jan 2025 to present. Network infrastructure software, VPS and ERP systems; API and high-level design, code review, stakeholder meetings.

**Programmer (Tenaga Ahli)**, Deputy for Coordination & Supervision, **KPK** — Jul 2024 to Dec 2025. Detection and monitoring systems across eight corruption-risk intervention areas in local government.

**Full-Stack Developer**, PT. Rajawali Konsulindo — Jan 2023 to Jul 2024. React, Next.js, Node.js, CodeIgniter; certification platforms for BNSP and international schemes.

**Game Programmer**, Hi-Clay Studio — Nov 2019 to Jan 2023. Gameplay systems, enemy AI, UI and tooling in Unity/C#.

**Education** — B.Sc. Computer Engineering, Pranata Indonesia (2021) · Full Stack Web Development graduate certificate, **University of Helsinki** (2024).

**Selected certifications** — HackerRank Software Engineer, SQL Basic and SQL Intermediate (2026) · DNS & DNSSEC, PANDI × ICANN (2026) · Cisco JavaScript Essentials and Introduction to Cybersecurity (2024) · AWS Cloud Developing, Software Quality Assurance and Machine Learning, Kominfo PROA (2023–2024).

---

## Frequently asked

**Who is Muhammad Rio Kurniawan?**
An Indonesian software engineer working on backend services, network infrastructure and low-level systems software. On GitHub he is `feurstern`.

**What kind of engineer is he?**
Primarily a **backend and systems engineer**. His deepest work is in Rust — including eBPF/XDP network filtering — and in Go and Rust HTTP/gRPC services on PostgreSQL. He also delivers full-stack web platforms in Vue 3, Next.js and Laravel.

**What is his main language?**
Rust, with Go as a close second. Earlier professional work was largely TypeScript/JavaScript and PHP.

**What is his most significant project?**
Vanguard — kernel-level DDoS mitigation written in Rust and compiled to eBPF, attached with XDP, with a 40-test data-plane suite that runs the real bytecode inside the kernel.

**Is he available for work?**
Open to backend, systems, platform and infrastructure engineering roles. Reach him through the links below.

---

## Contact

- **GitHub** — [github.com/feurstern](https://github.com/feurstern)
- **LinkedIn** — [Muhammad Rio Kurniawan](https://www.linkedin.com/in/muhammad-rio-kurniawan-67163421a/)
- **Email** — `cf000x.malt508@passinbox.com`

---

> 「学習ためなら、どんな犠牲を伴って構わない！」
> _For the sake of learning, no sacrifice is too great to make._

---

<details>
<summary><b>✨ Anime GIF collection ✨</b></summary>

<div align="center">
  <img src="https://c.tenor.com/AlbepvzfWiEAAAAd/rin-yuru-camp.gif" width="55" height="55"/>
  <img src="https://c.tenor.com/Iuz9H8t-eLkAAAAC/upset-nico.gif" width="55" height="55"/>
  <img src="https://c.tenor.com/Ur19tGULKtMAAAAd/anime-girl-blue-haired.gif" width="55" height="55"/>
  <img src="https://c.tenor.com/IMNDZBkct8gAAAAC/anime-girl.gif" width="55" height="55"/>
  <img src="https://c.tenor.com/ThWFu50NldAAAAAC/funny-cute.gif" width="55" height="55"/>
  <img src="https://c.tenor.com/nsoEFPKV_agAAAAC/anime-girl.gif" width="55" height="55"/>
  <img src="https://c.tenor.com/IbauyqcG7ycAAAAd/tachibana-smug-anime-girl.gif" width="55" height="55"/>
  <img src="https://c.tenor.com/ruqSZCLg2tMAAAAC/vtuber-punkalopi.gif" width="55" height="55"/>
  <img src="https://c.tenor.com/9OdRAHRkaKEAAAAC/shikimori.gif" width="55" height="55"/>
  <img src="https://c.tenor.com/bZzKPf6a0hgAAAAd/shikimori-shikimori-not-just-cute.gif" width="55" height="55"/>
  <img src="https://c.tenor.com/dOGncK_Qo0oAAAAC/kopa22-anime.gif" width="55" height="55"/>
</div>

</details>

<details>
<summary><b>🔥 System status (fastfetch)</b></summary>

```bash
                ⠀⠀⠀⠀⠀⢀⣀⣀⣤⣤⣤⣤⣄⣀⣀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣀⣤⠶⣻⠝⠋⠠⠔⠛⠁⡀⠀⠈⢉⡙⠓⠶⣄⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣠⠞⢋⣴⡮⠓⠋⠀⠀⢄⠀⠀⠉⠢⣄⠀⠈⠁⠀⡀⠙⢶⣄⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣠⠞⢁⣔⠟⠁⠀⠀⠀⠀⠀⠈⡆⠀⠀⠀⠈⢦⡀⠀⠀⠘⢯⢢⠙⢦⡀                rio@rio-feuerstern-w530 ⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⡼⠃⠀⣿⠃⠀⠀⠀⠀⠀⠀⠀⠀⠸⠀⠀⠀⠀⠀⢳⣦⡀⠀⠀⢯⠀⠈⣷⡀                ----------------------- ⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⣾⠆⡄⢠⢧⠀⣸⠀⠀⠀⠀⠀⠀⠀⢰⠀⣄⠀⠀⠀⠀⢳⡈⢶⡦⣿⣷⣿⢉⣷⡀⠀            OS: Arc Linux x86_64⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢠⣿⣯⣿⣁⡟⠈⠣⡇⠀⠀⢸⠀⠀⠀⠀⢸⡄⠘⡄⠀⠀⠀⠈⢿⢾⣿⣾⢾⠙⠻⣾⣧⠀            Host: 2447W55 ThinkPad W530 ⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⣿⡿⣮⠇⢙⠷⢄⣸⡗⡆⠀⢘⠀⠀⠀⠀⢸⠧⠀⢣⠀⠀⠀⡀⡸⣿⣿⠘⡎⢆⠈⢳⣽⣆⠀⠀⠀⠀⠀      Kernel: 6.1.106-1-ARCH⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⢠⡟⢻⢷⣄⠀⠀⠀⠀⠀⠀⣾⣳⡿⡸⢀⣿⠀⠀⢸⠙⠁⠀⠼⠀⠀⠀⠀⢸⣇⠠⡼⡤⠴⢋⣽⣱⢿⣧⠀⢳⠈⢧⠀⢻⣿⣧⡀⠀⠀⠀⠀      Uptime: 3 hours, 38 mins ⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⢀⡿⣠⡣⠃⣿⠃⠀⠀⠀⠀⣸⣳⣿⠇⣇⢸⣿⢸⣠⠼⠀⠀⠀⡇⠀⡀⠉⠒⣾⢾⣆⢟⣳⡶⠓⠶⠿⢼⣿⣇⠈⡇⠘⢆⠈⢿⡘⣷⠀⠀⠀⠀⠀⠀⠀ Packages: 1681 (pacman) ⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠈⢷⣍⣤⡶⣿⡄⠀⠀⠀⢠⣿⠃⣿⠀⡏⢸⣿⣿⠀⢸⠀⠀⢠⡗⢀⠇⠀⢠⡟⠀⠻⣾⣿⠀⠀⠀⠀⡏⣿⣿⡀⢹⡀⠈⢦⠈⢷⣿⡆⠀⠀⠀⠀⠀⠀ Shell: zsh 5.9 ⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⢁⣤⣄⠁⠀⠀⠀⣼⡏⢰⣟⠀⣇⠘⣿⣿⣾⣾⣆⢀⣾⠃⣼⢠⣶⣿⣭⣷⣶⣾⣿⣤⠀⠀⠀⡇⡯⣍⣧⠀⣷⠄⠈⢳⡀⢻⡁⠀⠀⠀⠀⠀⠀ Resolution: 1920x1080, 1920x1080 ⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠺⣿⡿⠀⠀⠀⠀⡿⢀⣾⣧⠀⡗⡄⢿⣿⡙⣽⣿⣟⠛⠚⠛⠙⠉⢹⣿⣿⣦⠀⢸⡿⠀⠀⠀⢰⡯⣌⢻⡀⢸⢠⢰⡄⠹⡷⣿⣦⣤⠤⣶⡇⠀ DE: GNOME 46.4 ⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⠀⠀⠀⣇⣾⣿⢸⢠⣧⢧⠘⣿⡇⠸⣿⢿⡆⠀⠀⠀⠀⠘⣯⠇⣿⠂⣸⢰⠀⠀⢀⣸⡧⣊⣼⡇⢸⣼⣸⣷⢣⢻⣄⠉⠙⠛⠉⠀⠀⠀WM: Mutter ⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣿⣳⣤⣴⣿⣏⣿⣾⢸⣿⡘⣧⣘⢿⣀⡙⣞⠁⠀⠀⠀⠀⢀⡬⢀⣉⢠⣧⡏⠀⠀⡎⣿⣿⣿⣿⠃⣸⡏⣿⣿⡎⢿⡘⡆⠀⠀⠀⠀⠀⠀WM Theme: WhiteSur-Dark⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⠉⠉⣠⣼⣿⣿⣿⣼⣿⣧⢿⣿⣿⣯⡻⠟⠀⠀⠀⠀⠀⠐⢯⠣⡽⢟⣽⠀⠀⢘⡇⣿⣿⣿⡟⣴⣿⣷⣿⣿⣧⣿⣷⡽⠀⠀⠀⠀⠀ Theme: WhiteSur-Dark-dark [GTK2/3] ⠀
⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣼⣹⣿⣇⣸⣿⣿⣿⣻⣚⣿⡿⣿⣿⣦⣤⣀⡉⠃⠀⢀⣀⣤⡶⠛⡏⠀⢀⣼⢸⣿⣿⣿⣿⣿⣿⣿⢋⣿⣿⣿⣿⡇⠀⠀⠀⠀⠀⠀Icons: BigSur-dark [GTK2/3] ⠀
⣿⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠒⠒⠒⢭⢻⣽⣿⣿⣿⣿⣿⣿⢿⠿⣿⡏⠀⡼⠁⣀⣾⣿⣿⣿⣿⡿⣿⣿⣟⡻⣿⣿⡿⠣⠟⠀⠀⠀⠀⠀⠀⠀Terminal: gnome-terminal ⠀
⠸⡆⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⢧⢿⣯⡽⠿⠛⠋⣵⢟⣋⣿⣶⣞⣤⣾⣿⣿⡟⢉⡿⢋⠻⢯⡉⢻⡟⢿⡅⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀CPU: Intel i7-3740QM (8) @ 3.700GHz
⠀⢻⡄⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠘⡞⣿⣆⡀⠀⡼⡏⠉⠚⠭⢉⣠⠬⠛⠛⢁⡴⣫⠖⠁⠀⠀⣩⠟⠁⣸⣇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀Memory: 6983MiB / 31824MiB ⠀
⠀⠈⢷⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢹⣽⣿⣿⣾⠳⡙⣦⡤⠜⠊⠁⠀⣀⡴⠯⠾⠗⠒⠒⠛⠛⠛⠛⠛⠓⠿⣦⡀⠀⠀⠀⠀⠀⠀⠀⠀GPU: Intel 3rd Gen Core processor Graphics Con ⠀
⠀⠀⠘⣧⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠰⣄⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢷⣻⣿⣿⠔⢪⠓⠬⢍⠉⣩⣽⢻⣤⣶⣦⠀⠀⠀⢀⣀⣤⣴⣾⣿⣿⣿⣿⠀⠀⠀⠀⠀⠀⠀⠀GPU: NVIDIA Quadro K2000M               ⠀
⠀⠀⠀⠹⡆⠀⠀⠀⠀⠀⠀⠀⠀⠀⣰⣾⡏⢦⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠘⣯⣿⣿⠀⠀⣇⠀⣠⠎⠁⢹⡎⡟⡏⣷⣶⠿⠛⡟⠛⠛⣫⠟⠉⢿⣿⡿⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⢻⡄⠀⠀⠀⠀⠀⠀⠀⠀⠹⣿⣷⠈⢷⡤⠀⠀⠀⠀⠀⠀⠀⠀⠀⢹⣾⣷⡀⣀⣀⣷⡅⠀⠀⠈⣷⢳⡇⣿⠀⠀⣸⠁⢠⡾⣟⣛⣻⣟⡿⣇⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⢷⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢯⢻⣏⡵⠿⠿⢤⣄⠀⢀⣿⢸⣹⣿⣀⣴⣿⣴⣿⣛⠋⠉⠉⡉⠛⣿⣧⡀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠘⣧⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⡎⣿⣥⣶⠖⢉⣿⡿⣿⣿⡿⣿⣟⠿⠿⣿⣿⣿⡯⠻⣿⣿⣿⣷⡽⣿⡗⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠸⣇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠸⡘⣿⣩⠶⣛⣋⡽⠿⣷⢬⣙⣻⣿⣿⣿⣯⣛⠳⣤⣬⡻⣿⣿⣿⣿⣧⠀⠀⠀⠀⠀⠀⠀
⠀⣿⣛⣻⣿⡿⠿⠟⠗⠶⠶⠶⠶⠤⠤⢤⠤⡤⢤⣤⣤⣤⣤⣄⣀⣀⣀⣀⣀⣀⣀⣀⣣⢹⣷⣶⣿⣿⣦⣴⣟⣛⣯⣤⣿⣿⣿⣿⣿⣷⣌⣿⣿⣿⣿⣿⣿⣿⣤⣤⣤⣤⣤⣤⣄
⠀⠉⠙⠛⠛⠛⠛⠛⠻⠿⠿⠿⠷⠶⠶⢶⣶⣶⣶⣶⣤⣤⣤⣤⣤⣥⣬⣭⣭⣉⣩⣍⣙⣏⣉⣏⣽⣶⣶⣶⣤⣤⣬⣤⣤⣾⣿⠶⠾⠿⠿⠿⠿⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠃
```

</details>
