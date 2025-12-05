# Contributing to This Repo

The goal of this repository is to document **verified** "Chain of Custody" links between Big Tech companies and their GitHub accounts.

## Documentation
Before contributing, please review the specific documentation for the tools and data structure used in this project:

* **[Data/README.md](Data/README.md)**: Explains the JSON schema, the different types of "proof steps" (e.g., `LinksTo`, `RedirectsTo`), and data formatting rules.
* **[Tools/README.md](Tools/README.md)**: Instructions on how to use the HTML generator tool.

---

## Important: Do Not Edit README.md Directly

The main `README.md` is auto-generated. Any manual changes made to it will be overwritten.
**Always verify and edit the data in `Data/Verified_Repos_Data.json`.**

---

## How to Contribute

### 1. Find a Verified Account
We only accept accounts where ownership can be proven via a **Chain of Custody**.
* **Good Proof:** A link from an official company website (e.g., `google.com` linking to the repo), a verified DNS entry, or an official blog post.
* **Bad Proof:** "It looks official" or "The logo is correct" (anyone can upload a logo).

If there's another form of proof that doesn't fit the current JSON structure, feel free to create an issue thread to ask. I could add additional types if necessary.

### 2. Update the Data
1.  Open `Data/Verified_Repos_Data.json`.
2.  Find the company block (or add a new one if necessary).
3.  Add the account details.
    * If the account has a "Verified" badge from GitHub (green checkmark), set `"verified_domain"` to that domain.
    * If not, you **must** provide `proof_steps` showing the link from an official source to the GitHub account.

### 3. Generate the README
Once the JSON is updated, you must regenerate the main README to reflect changes.
1.  Open `Tools/Readme_Generator.html` in your web browser.
2.  Paste the content of your updated `Data/Verified_Repos_Data.json` into the input box.
3.  Click **Generate Markdown**.
4.  Copy the output and overwrite the content of `README.md` in the root of this repo.

### 4. Submit Pull Request
* Commit both the updated `Data/Verified_Repos_Data.json` and the regenerated `README.md`.
* In your PR description, please include a link to the proof if it isn't obvious in the JSON data.

---

## 💡 Tips

### Prevent Link Rot with Archives
Company blogs and documentation pages often move or disappear.
* **Best Practice:** Whenever you add a URL as proof, try to create a snapshot on [The Wayback Machine](https://web.archive.org/) or [Archive.today](https://archive.today/).
* **Add it to JSON:** Include the snapshot URL in the `archive_url` field. This ensures the proof remains valid even if the original page goes down.

### Linking Directly to Text
In most browsers you can select some text, right click, and choose "Copy Link to Highlight". This is optional, but might be helpful if a hyperlink is particularly hard to find on a page.

### Using Backticks
The generator will try to add backticks to display a naked domain as code, but sometimes it needs help.
* **Auto-detection:** Domains like `google.com` are usually automatically wrapped in code blocks if it's the only text.
* **Manual Override:** If you need to verify a specific string like a command or a domain inside a sentence, you can manually add backticks in the JSON string (e.g., `` "prefix_text": "`sigs.kubernetes.io`" ``).

### Strategies for Finding Proof Steps

* Use Google to search for references to the github account, such as searching: `site:amazon.com "github.com/AmazonAppDev"`
* The same can be done if an account has a verified domain other than the company's main domain, such as: `site:amazon.com "amazonlinux.com"`
* There are browser extensions that can list all hyperlinks on a page, making it easy to find where a link on a page is
  * I like this one: [Link Diver](https://github.com/google/link-diver/releases) . But it requires manually installing and the browser must support manifest v2.