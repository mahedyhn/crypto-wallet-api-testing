<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Orbitron&size=32&duration=3000&pause=1000&color=F7A800&center=true&vCenter=true&width=700&lines=🪙+Cryptocurrency+Wallet+API;API+Testing+with+Postman+%26+Newman" alt="Typing SVG" />

<br/>

![Made with Postman](https://img.shields.io/badge/Made%20with-Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)
![Newman](https://img.shields.io/badge/Newman-CLI%20Runner-00B4E6?style=for-the-badge&logo=postman&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-Tests-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![REST API](https://img.shields.io/badge/REST-API%20Testing-4CAF50?style=for-the-badge&logo=swagger&logoColor=white)

<br/>

> **A professional end-to-end API testing suite for a Cryptocurrency Wallet platform — built with Postman, automated via Newman CLI, and validated with 48 assertions across 7 critical endpoints.**

<br/>

---

</div>

## 📊 Test Execution Summary

<div align="center">

| 🔢 Metric | 📈 Value |
|:---:|:---:|
| 🔁 **Total Iterations** | `1` |
| 📨 **Total Requests** | `7` |
| ✅ **Total Assertions** | `48` |
| ❌ **Failed Tests** | `4` |
| ⏭️ **Skipped Tests** | `0` |
| 📊 **Pass Rate** | `~91.7%` |

</div>

<br/>

---

## 🏗️ Project Structure

```
📁 Cryptocurrency_Testing/
│
├── 📄 Cryptocurrency_testing_postman_collection.json   ← Postman Collection
├── 📄 Cryptocurrency_Environment_postman_environment.json ← Environment Variables
├── 📄 Cryptocurrency_testing_report.html               ← Newman HTML Report
└── 📄 README.md                                        ← You are here!
```

---

## 🌐 API Base URL

```
https://crypto-wallet-server.mock.beeceptor.com
```

> Mock server hosted on **Beeceptor** — simulates a real Cryptocurrency Wallet backend.

---

## 🔗 Endpoints Tested

| # | 🛣️ Endpoint | 🔧 Method | 📌 Description |
|---|---|---|---|
| 1 | `/api/v1/register` | `POST` | Register a new user account |
| 2 | `/api/v1/login` | `POST` | Login with credentials |
| 3 | `/api/v1/wallet/balance` | `GET` | Retrieve wallet balance |
| 4 | `/api/v1/transactions` | `POST` | Send crypto transaction |
| 5 | `/api/v1/transaction_fee` | `POST` | Calculate transaction fees |
| 6 | `/api/v1/exchange_rates` | `GET` | Fetch live exchange rates |
| 7 | `/api/v1/transactions/history` | `GET` | View transaction history |

---

## 🧪 Detailed Test Scenarios

### 1️⃣ Register User — `POST /api/v1/register`

> Auto-generates dynamic user credentials using Postman's built-in dynamic variables.

**Pre-request Script (Dynamic Data Generation):**
```javascript
// Generate random credentials dynamically
var userName = pm.variables.replaceIn("{{$randomUserName}}");
pm.environment.set('uname', userName);

var password = pm.variables.replaceIn("{{$randomPassword}}");
pm.environment.set('pw', password);

var email = pm.variables.replaceIn("{{$randomEmail}}");
pm.environment.set('email', email);
```

**Request Body:**
```json
{
  "username": "{{uname}}",
  "password": "{{pw}}",
  "email": "{{email}}"
}
```

**✅ Assertions (11 Tests):**
- Status code is `201 Created`
- Response time is below `2000ms`
- Response size is below `2000 bytes`
- Response format is `JSON`
- `username` field exists in response
- `password` field exists in response
- `email` field exists in response
- Email is a `string` type
- Email contains `@` symbol (format validation)
- Username is a `string` type
- Username matches expected value

---

### 2️⃣ Login User — `POST /api/v1/login`

**Request Body:**
```json
{
  "username": "{{uname}}",
  "password": "{{pw}}"
}
```

**✅ Assertions (5 Tests):**
- Status code is `200 OK`
- Response time is below `2000ms`
- Response size is below `2000 bytes`
- Response format is `JSON`
- `username` property exists in response

---

### 3️⃣ Retrieve Wallet Balance — `GET /api/v1/wallet/balance`

**✅ Assertions (4 Tests):**
- Status code is `200 OK`
- Response time is below `2000ms`
- Response size is below `2000 bytes`
- Response format is `JSON`

---

### 4️⃣ Send Transaction — `POST /api/v1/transactions`

> Randomizes recipient address, amount, and cryptocurrency type on every run.

**Pre-request Script:**
```javascript
// Random recipient wallet address
var recipient_address = pm.variables.replaceIn("{{$randomUUID}}");
pm.environment.set('raddress', recipient_address);

// Random amount
var amount = pm.variables.replaceIn("{{$randomInt}}");
pm.environment.set('amount', amount);

// Random cryptocurrency from pool
const cryptos = ["BTC", "ETH", "SOL", "ADA", "DOT"];
const currency = cryptos[Math.floor(Math.random() * cryptos.length)];
pm.environment.set("currency", currency);
```

**Request Body:**
```json
{
  "recipient_address": "{{raddress}}",
  "amount": {{amount}},
  "currency": "{{currency}}"
}
```

**✅ Assertions (14 Tests):**
- Status code is `200 OK`
- Response time is below `2000ms`
- Response size is below `2000 bytes`
- Response format is `JSON`
- `id` field exists in response
- `to_address` field exists in response
- `type` field exists in response
- Transaction `type` is `"debit"`
- `amount` field exists in response
- `amount` is a `number` type
- `currency` field exists in response
- `currency` is `"ETH"` (validated)
- `timestamp` field exists in response

---

### 5️⃣ Calculate Transaction Fees — `POST /api/v1/transaction_fee`

**Request Body:**
```json
{
  "amount": 2.5,
  "currency": "BTC",
  "recipient_address": "0x1234567890ABCDEF"
}
```

**✅ Assertions (6 Tests):**
- Status code is `200 OK`
- Response time is below `2000ms`
- Response size is below `2000 bytes`
- Response format is `JSON`
- `fee` field exists in response
- `currency` field exists in response

---

### 6️⃣ Currency Exchange Rates — `GET /api/v1/exchange_rates`

**✅ Assertions (4 Tests):**
- Status code is `200 OK`
- Response time is below `200ms` *(stricter threshold)*
- Response size is below `2000 bytes`
- Response format is `JSON`

---

## 🔐 Environment Variables

| Variable | Type | Description |
|---|---|---|
| `base_url` | `default` | `https://crypto-wallet-server.mock.beeceptor.com` |
| `uname` | `dynamic` | Randomly generated username |
| `pw` | `dynamic` | Randomly generated password |
| `email` | `dynamic` | Randomly generated email |
| `raddress` | `dynamic` | Random UUID as recipient wallet address |
| `amount` | `dynamic` | Random integer transaction amount |
| `currency` | `dynamic` | Random crypto: BTC, ETH, SOL, ADA, or DOT |
| `randomCrypto` | `dynamic` | Reserved for future use |

---

## 🚀 How to Run

### ▶️ Option 1: Run in Postman

1. **Import Collection:**
   - Open Postman → `Import` → Upload `Cryptocurrency_testing_postman_collection.json`

2. **Import Environment:**
   - Open Postman → `Environments` → `Import` → Upload `Cryptocurrency_Environment_postman_environment.json`

3. **Set Environment:**
   - Select `Cryptocurrency_Environment` from the environment dropdown

4. **Run Collection:**
   - Click `Run collection` → Configure iterations → Click `Run`

---

### ▶️ Option 2: Run via Newman CLI

**Install Newman & HTML Reporter:**
```bash
npm install -g newman
npm install -g newman-reporter-htmlextra
```

**Execute the collection:**
```bash
newman run Cryptocurrency_testing_postman_collection.json \
  -e Cryptocurrency_Environment_postman_environment.json \
  -r htmlextra \
  --reporter-htmlextra-export ./reports/test-report.html
```

**Open the report:**
```bash
open ./reports/test-report.html
```

---

## 🪙 Supported Cryptocurrencies

<div align="center">

| Symbol | Currency |
|:---:|:---:|
| ₿ `BTC` | Bitcoin |
| Ξ `ETH` | Ethereum |
| ◎ `SOL` | Solana |
| ₳ `ADA` | Cardano |
| ⬡ `DOT` | Polkadot |

</div>

---

## 🛠️ Tech Stack

<div align="center">

| Tool | Purpose |
|:---:|:---:|
| ![Postman](https://img.shields.io/badge/Postman-FF6C37?style=flat-square&logo=postman&logoColor=white) | API Client & Test Authoring |
| ![Newman](https://img.shields.io/badge/Newman-CLI-00B4E6?style=flat-square&logo=postman&logoColor=white) | Command-line Collection Runner |
| ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black) | Test Scripting Language |
| ![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white) | Newman Runtime |
| ![Beeceptor](https://img.shields.io/badge/Beeceptor-Mock%20Server-8B5CF6?style=flat-square) | Mock API Server |

</div>

---

## 📌 Key Testing Highlights

- ✅ **Dynamic Data Generation** — Every test run uses freshly generated usernames, emails, passwords, wallet addresses, and amounts via Postman dynamic variables
- ✅ **Multi-Currency Support** — Transactions tested randomly across `BTC`, `ETH`, `SOL`, `ADA`, `DOT`
- ✅ **Response Validation** — Status codes, response times, sizes, body formats, and field-level assertions all covered
- ✅ **Environment-driven** — All sensitive and dynamic values managed through environment variables — no hardcoding
- ✅ **Automated Reporting** — Full HTML report generated via Newman with pass/fail breakdown per request

---

<div align="center">

---

**Made with ❤️ | API Testing | Postman × Newman**

*Cryptocurrency Wallet API — Test Suite v1.0.0*

</div>
