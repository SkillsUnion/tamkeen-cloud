# **Step-by-Step Guide: Creating a GitHub Actions Workflow**

## **Step 1: Create a GitHub Repository**
1. Go to [github.com](https://github.com).
2. Click **New** to create a new repository.
3. Fill in:
   - Repository name: `my-node-app` (or any name)
   - Choose **Public** or **Private**
   - Check **Initialize this repository with a README**
4. Click **Create repository**.

---

## **Step 2: Add a Sample Node.js Project**
You can do this locally, or directly from GitHub’s UI.

If using your terminal:

```bash
git clone https://github.com/your-username/my-node-app.git
cd my-node-app
npm init -y
npm install jest
```

Create a file named `sum.js`:
```js
function sum(a, b) {
  return a + b;
}
module.exports = sum;
```

Create a test in `sum.test.js`:
```js
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```

Update `package.json` to use Jest:
```json
"scripts": {
  "test": "jest"
}
```

Push your code to GitHub:

```bash
git add .
git commit -m "Add sample Node.js app with test"
git push origin main
```

---

## **Step 3: Create a GitHub Actions Workflow**
1. In your repository, go to `Actions` tab.
2. Click **Set up a workflow yourself** (or click "New workflow").
3. Create a new file named:

```plaintext
.github/workflows/node-ci.yml
```

4. Paste the following workflow:

```yaml
name: Node.js CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test
```

5. Commit and push the file.

---

## **Step 4: Observe the Workflow Execution**
1. Navigate to the **Actions** tab.
2. You will see your `Node.js CI` workflow running on the latest push.
3. Click on it to view detailed logs for each step (install, test, etc.).

---

## **Step 5: (Optional) Add a Status Badge to README**
Add the following to your `README.md`:

```md
![Node.js CI](https://github.com/your-username/my-node-app/actions/workflows/node-ci.yml/badge.svg)
```

Replace `your-username/my-node-app` with your actual repository path.

---

## Summary

You’ve created a basic **CI workflow** that:
- Runs when code is pushed or a pull request is created.
- Installs Node.js, installs dependencies, and runs unit tests.
- Can be extended later with deployment steps, linting, or more test environments.