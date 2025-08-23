Contributing to Obsidian Web Clipper Templates

Thank you for your interest in contributing to the Obsidian Web Clipper Templates repository! This is a community-driven collection of templates for the official Obsidian Web Clipper browser extension. Templates allow users to customize how web content is clipped and formatted into Markdown notes in their Obsidian vaults. Since the repository is still under construction, your contributions will help build a valuable resource for the Obsidian community.

Contributions can include new templates for specific websites (e.g., YouTube, Reddit, IMDB), general-purpose templates, improvements to existing ones, or updates to documentation. For example, templates can extract specific elements like YouTube video transcripts, article metadata, or social media posts.

Prerequisites

If needed, ensure you have the following setup:

Required Tools

Obsidian App: Download and install Obsidian from obsidian.md. You'll need at least one vault configured to test clippings.

Obsidian Web Clipper Browser Extension: Install the official extension from the browser store:

Chrome/Edge/Brave/Arc/Vivaldi/Orion: Available via the Chrome Web Store.

Firefox: Available via Firefox Add-ons.

Safari: Available via the App Store (for macOS/iOS/iPadOS).

Links and installation details are available on the Obsidian Web Clipper page.

Browser: The extension works on Chromium-based browsers (e.g., Chrome, Edge), Firefox, and Safari.

Required Plugins

No Obsidian community plugins are strictly required to use or test basic templates, as clippings are saved as standard Markdown files.

Recommended Plugins for Advanced Features:

Local Images: If your template involves embedding images (e.g., thumbnails from YouTube), this plugin can download and save images locally to your vault for offline access and permanence.

Dataview or Templater: Useful if your templates include dynamic elements (e.g., queries or frontmatter) that you want to process in Obsidian after clipping.

Advanced URI: For templates that might link to deep Obsidian features, though not essential for most cases.

Optional LLM Integration: Some templates may benefit from post-processing with Large Language Models (LLMs) for tasks like summarizing clipped content or generating additional metadata (e.g., summarizing a YouTube transcript). This requires plugins like Obsidian AI or Text Generator, which integrate with APIs like OpenAI or Hugging Face. Note that LLM usage is optional, depends on user setup, and requires an active API key and plugin configuration.

Special Requirements

Vault Configuration: The clipper requires access to your Obsidian vault(s). In the extension settings, add your vault paths and ensure Obsidian is running when clipping.

Template Testing Environment: Templates use variables extracted from web pages (e.g., via meta tags, Schema.org data, or CSS selectors). Test on live websites to ensure compatibility. For YouTube-specific templates, test features like transcript extraction by enabling the transcript option on a video page (e.g., click "Open Transcript" in the YouTube video player to verify the transcript is accessible and correctly extracted).

Privacy and Data Handling: Templates may extract page metadata (e.g., title, author, published date, YouTube transcripts). Ensure your templates respect user privacy and do not include sensitive data extraction without clear documentation.

File Format: All templates must be valid JSON files. Invalid JSON will fail to import into the clipper.

Compatibility: Templates should work with the latest version of the Web Clipper. Check the official documentation for updates on supported variables and features.

No External Dependencies: Templates should not rely on external scripts or APIs (e.g., no direct LLM calls within the template); they use built-in clipper functionality for extraction. LLMs, if used, are for post-processing in Obsidian via plugins.

How to Contribute

Follow these steps to submit your contribution:

Fork the Repository:

Go to https://github.com/obsidian-community/web-clipper-templates.

Click "Fork" to create your own copy.

Clone Your Fork:

Clone the repository to your local machine:

git clone https://github.com/YOUR-USERNAME/web-clipper-templates.git

Navigate to the directory:

cd web-clipper-templates

Create a Branch:

Create a new branch for your changes:

git checkout -b feature/your-template-name

Add or Edit Templates:

Place new templates in the /templates directory.

Naming Conventions: Use descriptive, lowercase names with hyphens for readability and consistency (e.g., youtube-with-transcript.json). Avoid special characters or spaces; stick to alphanumeric characters and hyphens.

Update the README.md if your template requires specific instructions or snippets. Include usage instructions in the template's documentation (e.g., in the README or as comments in the JSON if applicable) to guide users on how to apply or customize it.

Commit Your Changes:

Stage and commit:

git add .
git commit -m "Add new template for [site name]"

Push to Your Fork:

Push the branch:

git push origin feature/your-template-name

Submit a Pull Request (PR):

Go to your fork on GitHub and click "Pull request".

Provide a clear title (e.g., "Add YouTube transcript template") and description, including:

What the template does (e.g., extracts YouTube video title, URL, and transcript).

Supported websites (e.g., URL patterns like *youtube.com/watch*).

Any special notes (e.g., requires enabling "Open Transcript" on YouTube videos for transcript extraction).

Screenshots or examples of clipped output.

Usage instructions: Explain how users can import and use the template, including any prerequisites (e.g., enabling transcript on YouTube).

Adjustment guidelines: Describe how users can modify the template (e.g., customizing variables, selectors, or adding LLM-based summarization via plugins).

Reference any related issues or discussions (e.g., Issue #3 for YouTube transcript templates).

Review and Merge:

Your PR will be reviewed by maintainers. Be responsive to feedback.

Once approved, it will be merged into the main branch.

Template Format and Guidelines

Templates are JSON objects that define how content is extracted and formatted. Users import them into the Web Clipper settings by copying the JSON content.

Basic Structure

A typical template JSON, including an example for YouTube with transcript extraction, looks like this:

{
  "name": "YouTube with Transcript",
  "noteName": "{{title}} - {{date:YYYY-MM-DD}}",
  "noteLocation": "Clippings/YouTube",
  "vault": "YourVaultName",  // Optional: default vault
  "content": "---\nTitle: {{title}}\nURL: {{url}}\nPublished: {{published}}\n---\n\n## Video Details\n{{content}}\n\n## Transcript\n{{transcript}}\n\n## Optional Summary\n{{#if plugin:ObsidianAI}}{{ai:summary:transcript}}{{/if}}",
  "triggers": [
    {
      "urlPattern": "*youtube.com/watch*",
      "schemaType": "VideoObject"  // Optional: Schema.org type for YouTube videos
    }
  ],
  "variables": [
    {
      "name": "transcript",
      "selector": ".ytd-transcript-body-renderer",  // CSS selector for YouTube transcript
      "filter": "trim"  // Remove excess whitespace
    }
  ]
}

Key Fields

name: Human-readable name for the template (displayed in the clipper UI).

noteName: Format for the note filename. Supports variables and date formats (e.g., {{date:YYYY-MM-DD}}).

noteLocation: Folder path in the vault (e.g., Clippings or dynamic like {{category}}).

content: The Markdown template string. Use variables for dynamic insertion. Optionally include conditional logic for plugins (e.g., {{#if plugin:ObsidianAI}} for LLM-based summarization).

triggers: Array of rules for auto-applying the template (URL patterns, Schema.org types).

variables: Custom extractions using CSS selectors, meta tags, or Schema.org paths (e.g., .ytd-transcript-body-renderer for YouTube transcripts).

Supported Variables

Common variables include:

{{title}}: Page title.

{{url}}: Full URL.

{{domain}}: Domain name.

{{content}}: Main content (e.g., video description for YouTube).

{{highlights}}: User-highlighted text.

{{author}}, {{published}}: From meta tags or Schema.org.

{{date}}: Current date (customizable format).

{{schema:author:name}}: Schema.org examples.

{{transcript}}: Custom variable for YouTube transcript (requires "Open Transcript" enabled on the video page).

Custom: Defined via selectors (e.g., .ytd-transcript-body-renderer for YouTube).

For a full list, refer to the Obsidian Web Clipper variables documentation.

Guidelines for Templates

Keep it Simple: Start with basic extraction; add complexity (e.g., transcript extraction) only if needed.

Test Thoroughly: Verify on multiple pages and browsers. For YouTube templates, test with the transcript enabled (click "Open Transcript" in the video player) and without to ensure fallback behavior.

Document: In your PR, explain variables used, triggers, and example output. Include usage instructions (e.g., "Enable 'Open Transcript' on YouTube videos for transcript extraction") and adjustment guidelines (e.g., modifying selectors for site updates or adding LLM summarization via plugins like Obsidian AI).

Avoid Over-Specificity: Use flexible selectors to handle site changes (e.g., YouTubeâ€™s DOM updates).

Include Snippets if Needed: If the template requires Obsidian snippets (e.g., CSS or JS), add them in a /snippets directory and note in the description.

LLM Integration: If suggesting LLM post-processing (e.g., summarizing YouTube transcripts), clearly document the required plugin (e.g., Obsidian AI or Text Generator), setup steps (e.g., API key configuration), and note that itâ€™s optional and user-dependent.

Testing Your Template

Copy the JSON content.

Open the Web Clipper extension settings (gear icon).

Create a new template and paste the JSON.

Visit a target website (e.g., a YouTube video page with "Open Transcript" enabled for transcript templates), clip the page, and select your template.

Check the resulting note in Obsidian for correctness.

If using LLM features, ensure the relevant plugin (e.g., Obsidian AI) is installed and configured, then test the output (e.g., summary of a clipped transcript).

If issues arise, debug using the clipper's preview feature or browser console logs.

Code of Conduct

We follow the Obsidian Community Code of Conduct. Be respectful, inclusive, and collaborative. Report issues in the Obsidian Discord (#web-clipper channel) or GitHub issues.

Questions?

Join the Obsidian Discord for discussions, especially the #web-clipper channel for template-specific ideas.

Open an issue on the repository for questions or to propose new template ideas (e.g., Issue #3 for YouTube transcript templates).

Happy clipping and contributing! ðŸš€
