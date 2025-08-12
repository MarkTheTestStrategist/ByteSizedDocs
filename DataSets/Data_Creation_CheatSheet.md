# 🧪 Test Data Creation Cheatsheet for QA/Testers

## 🔍 Understand Your Test Data Needs First

Before creating anything, ask:

* What environment is this for? (Dev, Test, UAT, Pre-prod?)
* What systems are involved (APIs, UI, DB, third-party integrations)?
* What type of data is needed? (Valid, invalid, edge cases, empty, large volume, etc.)
* Does it need to be persistent or disposable?
* Is the data *read-only*, *editable*, or *created* during the test?

---

### 🧰 Key Test Data Creation Methods

#### 1. **Manual Data Creation (UI/API)**

Use the system’s interface or exposed APIs to set up known data.

* ✅ Great for: Exploratory or ad-hoc testing.
* ⚠️ Risk: Time-consuming and error-prone.

#### 2. **Scripting via Automation**

Use scripting languages or frameworks (e.g., Postman, Python, JS, PowerShell) to generate test data via API endpoints or direct DB inserts.

* 🎯 Ideal for: Regression, performance, and integration testing.
* 💡 Tip: Parameterise inputs for wide coverage and reusability.

#### 3. **Factory Pattern / Builders**

Use factory methods (common in unit testing frameworks) to generate data objects.

* 📦 Tools: FactoryBoy (Python), DataFactory (C#), Java Faker + Lombok builders.
* 📋 Ideal for: Test automation, mocking services, unit tests.

#### 4. **Cloning/Copying Existing Production Data**

Copy anonymised slices of real data into lower environments.

* 🔐 Be sure to: Mask PII/PCI/GDPR-sensitive data.
* 🔄 Automate refresh cycles using scheduled jobs or pipelines.

#### 5. **Data Seeding / Fixtures**

Seed databases with pre-structured data via SQL scripts or seeders.

* 📑 Ideal for: Integration and system testing.
* 🛠️ Tip: Use transactions to roll back test runs where needed.

#### 6. **Synthetic Test Data Generation**

Use tools to auto-generate structured randomised data.

* 🧪 Tools: [Mockaroo](https://mockaroo.com), [Faker](https://github.com/faker-js/faker), [Test Data Generator](https://generatedata.com/), DataGenerator (IntelliJ plugin).
* 👍 Good for: Load testing, edge cases, GDPR-safe data.

#### 7. **Stateful Test Accounts**

Maintain a small set of curated accounts that are reset to a known state regularly.

* 🧽 Reset via: APIs, SQL, or admin tools.
* 📘 Document each account’s purpose clearly for team use.

---

### 🛡️ Best Practices for Test Data

* **Tag test data clearly**
  Use a naming convention or metadata (e.g. "QA\_", "TEST\_", "AUTOMATION\_") to identify it.

* **Clean up after your tests**
  Use teardown steps in automation or after-test scripts to prevent environment pollution.

* **Use environment-specific data**
  Avoid hard-coding values that only work in one environment.

* **Avoid using stale data**
  Build a data freshness check or regenerate as needed.

* **Automate where you can**
  Use CI pipelines to auto-seed environments or refresh nightly.

* **Log test data creation**
  Helps with traceability and debugging. Log or store reference IDs if needed.

---

### 🧩 Examples of Test Data Types to Consider

| Type            | Examples                                           |
| --------------- | -------------------------------------------------- |
| **Positive**    | Valid user accounts, correct payment details       |
| **Negative**    | Wrong password, invalid email, bad JSON            |
| **Edge Cases**  | Max length inputs, zero values, large files        |
| **Boundary**    | Exactly 0, 1, max-1, max+1 items or values         |
| **Randomised**  | Dynamic email, random strings, timestamped IDs     |
| **Interlinked** | User with orders, account with roles, dependencies |

---

### 📎 Suggested Tool Stack (for Automation/Scripting)

* **API**: Postman, REST-assured, Python requests
* **UI**: Playwright, Selenium, Cypress
* **Database**: DBeaver, SQL scripts, Flyway
* **Mocking/Seeding**: Faker, Mockaroo, TestContainers, FactoryBot
* **CI/CD Integration**: GitHub Actions, Jenkins, Azure Pipelines
