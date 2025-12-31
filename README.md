# Ai Bot

This document details the features and operational logic of the Ai Bot, a multi-purpose tool powered by Google's Gemini models.

## I. AI & Chatbot Capabilities

The bot's core functionality revolves around its integration with Google's Gemini AI models, providing advanced conversational and analytical abilities.

*   **Conversational AI**: The bot responds to direct mentions or to all messages within a designated "chatbot channel." It uses the `gemini-2.5-flash` model for general chat to ensure speed and availability.

*   **Contextual Memory**: In chatbot channels, the bot fetches the last 10 messages to build a conversation history. This allows it to understand context, remember previous parts of the conversation, and provide more relevant follow-up responses.

*   **Custom Personas**: Administrators can define a unique personality for the AI on a per-server basis using the `/personality` command. This instruction is injected into the AI's memory, forcing it to adopt a specific tone, character, or set of rules for all its responses within that server.

*   **Multi-Modal Analysis**: The `/ask` command and general chat support image attachments. The bot can analyze the content of images (JPEG, PNG, GIF, etc.) and answer questions about them.

*   **Advanced Model Access**: Authorized users can access the more powerful `gemini-2.5-pro` model via the `/ask` command for more complex reasoning and generation tasks.

*   **Content Summarization**: The `/summarize` command can process either a block of text or a URL. For URLs, it fetches the webpage content, strips all HTML and script tags, and sends the clean text to the AI for a concise summary.

*   **Safety Controls**: Server administrators can adjust the AI's content safety level using `/setsafety`, choosing from `none`, `low`, `medium`, or `high` to control the strictness of the content filter.

## II. Developer Toolkit

A comprehensive suite of over 50 commands designed to assist with the entire software development lifecycle, organized into three logical groups.

### Code Group (`/code`)
Commands for direct code generation, analysis, and manipulation.
*   **Generation**: `generate`, `algorithm`, `designpattern`, `boilerplate`, `codechallenge`.
*   **Analysis & Review**: `explain`, `debug`, `complexity`, `optimize`, `securityscan`, `codereview`.
*   **Documentation**: `document`, `docstring`, `visualize` (creates Mermaid.js diagrams).
*   **Conversion**: `convert` (translates between languages), `refactor`.
*   **Testing**: `unittest`, `testdata`.

### Project Group (`/project`)
Commands for project setup, management, and documentation.
*   **Scaffolding**: `readme`, `gitignore`, `structure`, `makefile`, `config`, `envexample`.
*   **DevOps & Deployment**: `dockerfile`, `cicd`, `deploy`, `shell` (generates shell scripts).
*   **Planning & Management**: `commit` (generates conventional commit messages), `userstory`, `releasenotes`, `changelog`, `roadmap`, `breakdown`, `prdescription`.
*   **Naming & Presentation**: `nameit`, `presentation`, `colorpalette`.

### Data Group (`/data`)
Commands for handling data structures, APIs, and databases.
*   **Database**: `sql` (generates queries), `dbschema` (designs table structures).
*   **API**: `apirequest`, `apidesign`, `apidoc` (generates OpenAPI/Swagger specs), `endpoint`.
*   **Data Manipulation**: `regex`, `formatconvert`, `localize` (translates JSON language files).
*   **Web**: `scraper` (generates a Python web scraper).

## III. Server Administration & Moderation

A robust set of tools for server management, logging, and automation, with all settings stored persistently in a database.

### Logging Systems
*   **Message Logger**: Tracks message edits and deletions in a designated webhook channel. It captures the original content, author, and channel information.
*   **Voice Logger**: Monitors and logs voice channel activity, including when users join, leave, or switch channels.

### Automated Moderation & Management
*   **New Account Restriction**: Automatically assigns a "Restricted" role to newly joined members whose accounts are younger than a configurable age (e.g., 7 days). This role's permissions can be configured to limit access for new accounts.
*   **Auto-Clean**: A background task that periodically purges messages from a configured channel that are older than a set time limit, while preserving pinned messages.
*   **Sticky Messages**: A system to maintain a specific message at the bottom of a channel. The bot automatically reposts the message whenever a new message is sent.
*   **Message Migration**: A utility to copy a large number of messages from a source channel to a destination channel. It uses webhooks to impersonate the original authors, preserving their names and avatars for a seamless transfer.
*   **Ban Transfer**: A tool to iterate through the entire ban list of one server and apply those same bans to another server, useful for synchronizing moderation actions across communities.

### Community & Engagement Tools
*   **Announcements**: Allows administrators to create and send rich, webhook-based announcements that impersonate the server's name and icon.
*   **Polls**: Creates interactive polls with buttons for voting. The bot tracks votes and updates the button labels with the current count.
*   **Global Suggestion System**: Users can submit suggestions via `/suggest`. These are sent to a central, owner-configured channel for review. Admins can approve or deny suggestions, which updates the original suggestion message with the new status and reason.

## IV. Utility & Fun Features

A wide range of commands for entertainment, information lookup, and general utility.

### Information & System
*   **System Info (`/info`)**: Displays a detailed embed with bot statistics (version, uptime, server/user count), system resource usage (CPU, RAM), and project information.
*   **HTML Channel Export (`/exporthtml`)**: Generates a self-contained HTML file of a channel's message history, replicating the Discord UI. The file includes client-side JavaScript for searching and filtering messages.
*   **Invite Lookup (`/invitelookup`)**: Fetches and displays detailed information about a Discord invite link, including server features, member counts, and boost status.

### User Tools
*   **AFK System**: Users can set an AFK status with a custom message. The bot will automatically reply when the AFK user is mentioned, subject to a configurable cooldown. It can also optionally prepend `[AFK]` to the user's nickname.
*   **File Upload (`/ez`)**: Integrates with the `e-z.gg` file hosting service, allowing users to upload files using their personal API key (stored securely in the bot's database).
*   **VirusTotal Scan (`/vtscan`)**: Uploads a file to the VirusTotal API and polls for a report, displaying the detection ratio and threat level.
*   **Secret Cipher (`/cipher`)**: Encrypts and decrypts text using a custom reversible algorithm, allowing users to hide messages.

### Media & Image Manipulation
*   **Social Media Downloaders**:
    *   `/downloadtiktok`: Downloads a TikTok video without the watermark.
    *   `/twitter`: Downloads videos, GIFs, or images from a Twitter/X link using the `fxtwitter` API.
*   **Image Generation**:
    *   `/caption`: Adds a white caption bar to the top of an image or GIF, processing each frame of an animation.
    *   `/quote`: Creates a fake "Discord message" image from a specified user and text.
    *   `/mcachievement`: Generates a custom Minecraft achievement image.
*   **Text Manipulation (`/text`)**: A group of commands to style text with markdown, convert it to fancy Unicode fonts, or apply transformations like `reverse`, `zalgo`, and `OwOify`.

### Game Integrations
*   **Valorant (`/valorant`)**: A full suite of commands to look up data on agents, weapons, maps, sprays, and more, using a cached connection to the `valorant-api.com` API.
*   **Roblox (`/robloxuser`)**: Retrieves a user's profile, avatar, join date, and created games from Roblox's public APIs.
*   **Rockstar (`/rockstar`)**: Scrapes the Social Club to display user profiles and GTA V character stats.

### Fun & Miscellaneous
*   **Troll Commands**: Includes `/trollnitro` for sending a harmless fake Nitro link and `/troll move` for repeatedly moving a user between voice channels.
*   **Cat Commands (`/cat`)**: Fetches random cat images or GIFs.
*   **Simple Games**: `/coinflip` and `/8ball`.