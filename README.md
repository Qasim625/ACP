# 🔍 User Fetcher

A lightweight Node.js script that fetches user data from a public API, filters users by company catchphrase, and formats the results for display.

![Node.js](https://img.shields.io/badge/Node.js-14%2B-339933?logo=node.js&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-ES2017%2B-F7DF1E?logo=javascript&logoColor=black)
![License](https://img.shields.io/badge/License-MIT-blue.svg)
![API](https://img.shields.io/badge/API-JSONPlaceholder-orange)
![Status](https://img.shields.io/badge/status-active-success)

## Overview

This script calls the [JSONPlaceholder](https://jsonplaceholder.typicode.com) `/users` endpoint, filters the results to users whose company catchphrase mentions **"group"** or **"service"**, and prints a clean, formatted summary of each match.

## Features

- ⚡ Async/await-based fetch with error handling
- 🔎 Case-insensitive keyword filtering on `company.catchPhrase`
- 🧩 Object destructuring for clean data extraction
- 🖨️ Human-readable console output

## Requirements

- Node.js **v18+** (for native `fetch` support), or Node **v14+** with a `fetch` polyfill (e.g. `node-fetch`)

## Installation

```bash
git clone https://github.com/your-username/user-fetcher.git
cd user-fetcher
```

No dependencies to install — the script uses only built-in `fetch`.

> **Using an older Node version?** Install a polyfill first:
> ```bash
> npm install node-fetch
> ```
> and add `const fetch = require("node-fetch");` at the top of the file.

## Usage

Run the script directly with Node:

```bash
node fetchUsers.js
```

### Example Output

```
[
  'User: Ervin Howell | Email: Shanna@melissa.tv | City: Wisokyburgh',
  'User: Clementine Bauch | Email: Nathan@yesenia.net | City: McKenziehaven'
]
```

## How It Works

| Step | Description |
|------|-------------|
| 1️⃣ Fetch | Retrieves the full user list from the API |
| 2️⃣ Parse | Converts the response into JSON |
| 3️⃣ Filter | Keeps only users whose `company.catchPhrase` includes "group" or "service" |
| 4️⃣ Format | Destructures each user and builds a readable summary string |
| 5️⃣ Output | Logs the formatted list to the console |

## Code

```javascript
const API_URL = "https://jsonplaceholder.typicode.com/users";

async function fetchUsers() {
    try {
        const response = await fetch(API_URL);
        const users = await response.json();

        const filteredUsers = users.filter(user =>
            user.company.catchPhrase.toLowerCase().includes("group") ||
            user.company.catchPhrase.toLowerCase().includes("service")
        );

        const formattedUsers = filteredUsers.map(
            ({ name, email, address: { city } }) =>
                `User: ${name} | Email: ${email} | City: ${city}`
        );

        console.log(formattedUsers);
    } catch (error) {
        console.error("Error fetching users:", error);
    }
}

fetchUsers();
```

## Error Handling

Network failures, non-JSON responses, or unexpected API shapes are caught and logged via `console.error`, so the script fails gracefully instead of crashing.

## License

This project is licensed under the [MIT License](LICENSE).

## Contributing

Pull requests are welcome! For major changes, please open an issue first to discuss what you'd like to change.
