#

# Git Hooks with Husky: Why and How We Use It

## How to Set Up the Project

1. **Clone the Repository**

```bash
   git clone https://github.com/Shaybush/blocks-user-pre-commit.git
   cd blocks-user-pre-commit
```

2. **Install Dependencies**

```bash
   pnpm i
```

3. **Try to change file in secret folder and commit**

## Why Did I Choose Husky?

Managing Git hooks directly through `.git/hooks` has limitations, especially in a team-based workflow. Here’s why we chose **Husky**:

1. **Version-Controlled Hooks**:

   - Git's native hooks (`.git/hooks/pre-commit`) are not tracked by Git, meaning every team member would need to manually set them up.
   - With Husky, hooks are stored in the `.husky/` directory, which **is tracked by Git**. This ensures that all team members automatically get the same hooks after cloning the repository.

2. **Cross-Team Consistency**:

   - Husky automatically ensures all team members follow the same pre-commit checks (e.g., linting, testing, formatting).
   - Developers only need to run `pnpm install`, and Husky will handle the setup for them.

3. **Ease of Setup**:

   - Husky provides a simple way to manage and configure Git hooks using commands like `npx husky init`.
   - It avoids the manual process of creating, managing, and making hooks executable.

4. **Integration with Other Tools**:

   - Husky works seamlessly with tools like `lint-staged` and `commitlint`, helping us enforce consistent coding standards.

5. **Cross-Platform Compatibility**:
   - Husky resolves issues with executable permissions (`chmod +x`) across different operating systems, ensuring smooth setup on Windows, macOS, and Linux.

## What Happens Automatically?

1. When you clone the repository and run `pnpm install`, the `prepare` script in `package.json` automatically:

   - Installs Husky.
   - Sets up the `.husky/` directory and hooks.
   - Ensures hooks are ready to run without extra steps.

2. The `pre-commit` hook is already configured to:
   - Retrieve the Git username making the commit.
   - Print the username before the commit proceeds.

---

### Second: Automating `chmod +x` to Avoid Manual Setup

Husky already automates permissions for hooks, but if you still encounter the need for `chmod +x`, you can take the following steps to ensure the hooks are always executable **automatically**:

#### 1. **Add a `prepare` Script in `package.json`**

The `prepare` script in `package.json` ensures Husky installs hooks correctly during `pnpm install`. Here’s how it looks:

```json
"scripts": {
  "prepare": "husky install"
}
```

## More Issues could happend

Sometimes, hooks might not work if the hooks path isn’t set explicitly.

You can configure this in the repository with:

```bash
    git config core.hooksPath .husky
```
