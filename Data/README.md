# Data Documentation

This directory contains `Verified_Accounts_Data.json`, which serves as the **source of truth** for the "Verified Open Source GitHub Accounts" list. 

Instead of manually editing the main README table, all data updates should be made in the JSON file. This separates the data from the presentation layer.

## File Structure

The JSON file follows this high-level structure:

```json
{
  "companies": [
    {
      "name": "Company Name",
      "accounts": [
        {
          "name": "Account Name",
          "github_url": "...",
          "verified_domain": "...",
          "proof_steps": [ ... ]
        }
      ]
    }
  ]
}
```

## Schema Definitions

### 1. Account Object
Represents a single row in the final Markdown table.

| Field | Type | Description |
|---|---|---|
| `name` | String | The display name of the GitHub organization or account. |
| `github_url` | String | The URL to the GitHub account. |
| `verified_domain` | String or Null | The domain shown on the GitHub profile with a green checkmark. If the account is not verified by GitHub, set to `null`. |
| `proof_steps` | Array | A list of steps establishing the "Chain of Custody" proving ownership. |

---

### 2. Proof Steps
Each object in the `proof_steps` array represents a line of text in the "Proof of Association" column.

#### Common Properties (All Types)
| Field | Type | Description |
|---|---|---|
| `type` | String | Defines the formatting logic (see "Step Types" below). |
| `archive_url` | String or Null | The Wayback Machine or Archive.is link. Adds a `[A]` superscript to the line. |

#### Step Types

**A. `Base`**
*   **Usage:** The starting point of verification, usually a top-level domain or a known property.
    * Could also be used for a text-only / non-link instructional step.
*   **Fields:**
    *   `text`: The content to display (e.g., "opensource.google").
    *   `url`: (Optional) Make the text a hyperlink.

**B. `StandaloneHyperlink`**
*   **Usage:** A text link, often a blog post, documentation page, or policy document.
*   **Fields:**
    *   `text`: The anchor text (e.g., "Official Announcement").
    *   `url`: The destination URL.

**C. `LinksTo` / `RedirectsTo`**
*   **Usage:** Represents a directional relationship. The generator renders these with an arrow (`🠊`).
    *   *LinksTo:* "Source A links to Target B".
    *   *RedirectsTo:* "Source A HTTP redirects to Target B".
*   **Fields:**
    *   `prefix_text`: (Optional) Text appearing *before* the arrow (e.g., `"Follow Us" button`).
    *   `text`: The target text appearing *after* the arrow.
    *   `url`: (Optional) If the target text needs to be a hyperlink.

---

## Formatting Rules

The HTML generator applies specific formatting heuristics to the JSON data.

### 1. Automatic Code Blocks
The generator tries to detect domains and file paths automatically. 
*   **Rule:** If a `text` field contains **no spaces** AND contains a **dot** (e.g., `developer.chrome.com`), it is automatically wrapped in backticks (`` ` ``).

### 2. Manual Backticks
If you need to force a code block (e.g., for a string with spaces or no dots) or strictly control the output, you can include backticks directly in the JSON string.
*   **Example:** `"prefix_text": "`sigs.kubernetes.io`"`
*   **Note:** Do **not** escape backticks (do not use `\` `). Standard JSON string rules apply.

### 3. Empty Columns
If `verified_domain` is `null`, the generator ensures the Markdown table cell renders correctly as an empty cell.

---

## Example Entry

```json
{
  "name": "GoogleChromeLabs",
  "github_url": "https://github.com/GoogleChromeLabs",
  "verified_domain": null,
  "proof_steps": [
    {
      "type": "Base",
      "text": "developer.chrome.com",
      "url": null
    },
    {
      "type": "StandaloneHyperlink",
      "text": "Blog post",
      "url": "https://developer.chrome.com/blog/...",
      "archive_url": "https://web.archive.org/..."
    },
    {
      "type": "LinksTo",
      "prefix_text": "\"JSON API Endpoints\"",
      "text": "github.com/GoogleChromeLabs",
      "url": null
    }
  ]
}
```

## Generating the README

To update the main `README.md`:
1. Edit `Verified_Accounts_Data.json`.
2. Open the HTML Generator tool in your browser.
3. Paste the JSON content.
4. Click **Generate Markdown**.
5. Copy the output and replace the content in the root `README.md`.