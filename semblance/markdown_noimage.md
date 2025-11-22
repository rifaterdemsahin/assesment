# ⚠️ Markdown Image Preview Issues: The "Why" and "How to Fix"

## The Problem
You might notice that images using absolute local paths (e.g., `![Img](file:///Users/name/project/image.png)`) do not display in markdown previewers like **Antigravity**, **VS Code**, or **Obsidian**.

## The Reason: Security Sandboxing 🔒
Markdown previewers run in a sandboxed environment (often a webview). For security reasons, modern webviews **block access to local files** via absolute paths (`file:///`). This prevents a malicious markdown file from scanning your hard drive and reading sensitive files (like SSH keys or config files) just by you opening a preview.

## The Fixes 🛠️

### Option 1: Use Relative Paths (Recommended) ✅
Most previewers allow reading files that are **relative** to the current markdown file. This keeps the scope within the project.

*   **Bad (Absolute):**
    ```markdown
    ![Thumbnail](file:///Users/rifaterdemsahin/projects/assesment/imaginary/thumbnail.png)
    ```
*   **Good (Relative):**
    Assuming this file is in `semblance/` and images are in `imaginary/`:
    ```markdown
    ![Thumbnail](../imaginary/thumbnail.png)
    ```

### Option 2: Host the Images ☁️
Upload the images to a cloud provider (GitHub, Imgur, AWS S3) and use the public URL. This works everywhere.

*   **Example:**
    ```markdown
    ![Thumbnail](https://raw.githubusercontent.com/username/repo/main/imaginary/thumbnail.png)
    ```

### Option 3: Trust the Workspace (IDE Specific) 🤝
In VS Code or similar IDEs, you can sometimes explicitly "Trust" the workspace. This *may* relax the security settings to allow local file reading, but it's less portable than using relative paths.
