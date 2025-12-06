# Tools

This directory contains utility tools to assist with maintaining the repository.

## Readme_Generator.html

A standalone HTML tool that converts the source JSON data into the formatted Markdown table used in the main project README.

### Usage

1. Open `Readme_Generator.html` in any modern web browser.
2. Open `../Data/Verified_Accounts_Data.json` in a text editor and copy its contents.
3. Paste the JSON into the **"1. JSON Input"** box in the browser tool.
4. Click **Generate Markdown**.
5. Click **Copy** to grab the output.
6. Replace the content in the root `README.md` with the generated text.

### Features
*   **No Install Required:** Runs entirely in the browser using a CDN for styling.
*   **Automatic Formatting:** Handles the specific indentation arrows (`↳`), directional arrows (`🠊`), and archive superscripts (`[A]`).
*   **Smart Syntax:** Automatically applies backticks to domains and URLs based on the heuristics defined in the data schema.
*   **Validation:** Includes basic JSON error checking to prevent broken formatting.