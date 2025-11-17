# XSS Learning Project --> Secure Input Handling

This project is a simple Node.js + Express application created to
demonstrate **Cross-Site Scripting (XSS)** vulnerabilities and how to
prevent them using proper sanitization. It includes a comment/discussion
section --- the perfect playground to test and understand real XSS
attacks.

---

## Features

- Comment/discussion page
- Demonstration of XSS vulnerabilities
- Sanitized user input using the `xss` library
- Stores comments in MongoDB
- Switch easily between **vulnerable** and **secure** mode
- Beginner-friendly structure for learning web security

---

## Tech Stack

- **Node.js** -- Server runtime
- **Express.js** -- Backend framework
- **MongoDB** -- For storing comments
- **EJS** -- Templating engine

## Installation & Setup

### 1️⃣ Clone the repository

```bash
git clone https://github.com/Altamash-khn/CSRF.git
cd CSRF
```

### 2️⃣ Install dependencies

```bash
npm install
```

---

## 🟢 IMPORTANT: Start MongoDB Before Running

This project **requires an active MongoDB server** on:

    mongodb://localhost:27017

#### macOS:

```bash
brew services start mongodb-community
```

#### Windows:

```bash
net start MongoDB
```

#### Linux:

```bash
sudo systemctl start mongod
```

---

## Start the Application

```bash
node app.js
```

Visit:

    http://localhost:3000

---

## Testing XSS (Vulnerable Mode)

To intentionally test XSS attacks, disable sanitization.

### 1. Disable sanitization in `routes/discussion.js`

Replace:

```js
text: xss(req.body.comment),
```

With (INSECURE):

```js
text: req.body.comment,
```

---

### 2. Remove escaping in EJS (`views/discussion.ejs`)

Replace:

```ejs
<%= comment.text %>
```

With unescaped output (INSECURE):

```ejs
<%- comment.text %>
```

---

## Try an XSS Attack

Enter this as a comment:

```html
<script>
  alert("XSS Attack Activated!");
</script>
```

- Sanitization ON → harmless
- Sanitization OFF → script executes

---

## How Sanitization Works

```js
const xss = require("xss");

const comment = {
  text: xss(req.body.comment),
};
```

This escapes malicious scripts and HTML before rendering.

---

## Contributing

- Add more XSS demos
- Improve UI
- Add more security examples

PRs are welcome!
