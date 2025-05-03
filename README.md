# Reddit AI Assistant 🤖

[![License: MIT](https://img.shields.io/badge/License-MIT-white.svg)](https://opensource.org/licenses/MIT)
[![Python Version](https://img.shields.io/badge/Python-3.x-blue.svg)](https://www.python.org/)
[![Made with Gradio](https://img.shields.io/badge/Made%20with-Gradio-orange)](https://www.gradio.app/)
[![Uses PRAW](https://img.shields.io/badge/Uses-PRAW-cyan)](https://praw.readthedocs.io/en/stable/)
[![Uses Gemini API](https://img.shields.io/badge/Uses-Gemini%20API-green)](https://ai.google.dev/)
[![Open In Kaggle](https://img.shields.io/badge/Open%20In-Kaggle-blue?logo=kaggle)](https://www.kaggle.com/code/tharunreddy2911/reddit-ai-assistant)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/16ahVmgEEH6UZDCoii827nrIoWBgBzXcb?usp=sharing)
[![Made with Jupyter](https://img.shields.io/badge/Made%20with-Jupyter-orange?logo=jupyter)](https://jupyter.org/)

### Disclaimer
* **API Usage & Reddit Rules:** This agent connects to official Reddit and Google APIs. Please use them responsibly and adhere to their respective Terms of Service.
* **Automation Risk:** Using scripts to automatically post comments can violate Reddit's rules against bots/spam and **may lead to account suspension.** This agent is intended to *assist in drafting* comments.
* **Manual Review is Crucial:** **Always manually review, significantly edit for value and originality, and post comments yourself.** Focus on contributing genuine insights and engaging constructively. Avoid spam or low-effort content to maintain a healthy Reddit community.

## Table of Contents 📑
* [Access the Notebooks](#access-the-notebooks-)
* [Overview](#overview-)
* [Core Features](#core-features-)
* [Detailed Setup Guide](#detailed-setup-guide-)
* [Execution Instructions](#execution-instructions-)
* [How to Use the Workflow](#how-to-use-the-workflow-)
* [Possible Use Cases](#possible-use-cases-)
* [Contributing](#contributing-)

## Access the Notebooks 🚀

* **[Kaggle: Reddit AI Assistant](https://www.kaggle.com/code/tharunreddy2911/reddit-ai-assistant)**
* **[Colab: Reddit AI Assistant](https://colab.research.google.com/drive/16ahVmgEEH6UZDCoii827nrIoWBgBzXcb?usp=sharing)**

## Overview 💡

The Reddit AI Assistant is a Python agent built to help you find relevant discussions on Reddit and generate smart, context-aware comment suggestions using Google's Gemini Models. It runs in notebook environments (like Kaggle, Colab, or your local machine) and provides a user-friendly interface with Gradio.

Think of it as your helper to streamline finding engagement opportunities and drafting thoughtful comments based on the post, ongoing discussion, and your own expertise.

## Core Features ✨

* **🎯 Smart Search:** Find Reddit posts with advanced keyword/filter options (keywords, negative keywords, subreddits, upvotes, comments, time).
* **✍️ AI Comment Suggestions:** Get AI-generated comment ideas based on post content, top comments, your expertise, and desired tone.
* **🗺️ AI Comment Placement Advice:** Receive AI recommendations on whether to reply directly or post a new top-level comment, with justifications.
* **👀 Quick Context Display:** Easily view the post's title, author, full text/URL, and top comments within the interface.
* **✅ Subreddit Validation & Recommendation:** Verify target subreddits exist and get suggestions for relevant communities based on keywords.

## Detailed Setup Guide 🛠️

You'll need API credentials for Reddit and Google Gemini.

**1. Google Gemini API Key:**
* Go to [Google AI Studio](https://aistudio.google.com/).
* Sign in and generate a new API key ("Get API key").
* Copy the key and store it securely.

**2. Reddit API Credentials:**
* Log into your Reddit account on the web.
* Go to Reddit app preferences: [https://www.reddit.com/prefs/apps](https://www.reddit.com/prefs/apps).
* Click "are you a developer? create an app...".
* Fill it out:
    * **Name:** Unique name (e.g., `MyRedditHelper`).
    * **Type:** Select **`script`**.
    * **Redirect URI:** Use `http://localhost:8080` (it's needed, but not really used for this script type).
* Create the app and securely record:
    * **Client ID** (the short code under the app name).
    * **Client Secret** (the long code next to `secret`).
* **Define a User Agent:** A unique string identifying your script, including your Reddit username (e.g., `MyRedditagent/1.0 by u/YourUsername`).

**3. Securely Store Your Keys (Choose Your Method):**

**Never paste secrets directly into the code!** Use the method for your environment:

* **[Kaggle](https://www.kaggle.com/):**
    * In your Kaggle notebook, use the **"Add-ons" > "Secrets"** menu.
    * Add secrets with these exact labels: `GOOGLE_API_KEY`, `REDDIT_CLIENT_ID`, `REDDIT_CLIENT_SECRET`, `REDDIT_USER_AGENT`.
    * Ensure the notebook has access selected for these secrets.
* **[Google Colab](https://colab.research.google.com/):**
    * Use the **"Secrets" tab** in the left sidebar.
    * Add secrets with the exact labels: `GOOGLE_API_KEY`, `REDDIT_CLIENT_ID`, `REDDIT_CLIENT_SECRET`, `REDDIT_USER_AGENT`.
    * Ensure "Notebook access" is enabled for each secret.
* **Local Environment (Your Computer):**
    * **Option 1: Environment Variables (Recommended):** Set system environment variables for `GOOGLE_API_KEY`, `REDDIT_CLIENT_ID`, etc. *This is recommended because it keeps secrets separate from your code files and works well with many deployment platforms.*
    * **Option 2: `.env` File:**
        * The `python-dotenv` library (installed in Cell 1) allows loading secrets from a file.
        * Create a file named exactly `.env` in your project's root directory.
        * Add key-value pairs like: `GOOGLE_API_KEY="your_key"`
        * The script (Cell 2) will automatically load variables from this file if it exists.
        * **If using Git, add `.env` to your `.gitignore` file! Don't commit secrets!**

## Execution Instructions 🏃

1.  **Prepare Notebook:** Ensure the `.ipynb` file containing the code cells (Cells 1-6) is in your chosen environment (Kaggle, Colab, local Jupyter).
2.  **Configure Secrets:** Set up the required API keys and credentials using the method appropriate for your environment (see Step 3 above).
3.  **Run Cells Sequentially:** Execute the notebook cells in order (Cell 1 through 6).
    * **Verify Cell 2 & 3 Output:** Confirm that secrets loaded successfully and that the API clients initialized without errors. Check the printed output messages carefully.
4.  **Launch UI:** Cell 6 will start the Gradio application and provide a URL. Access this URL in your web browser.
5.  **Maintain Session:** The Gradio interface is only active while the notebook cell executing `iface.launch()` (Cell 6) remains running.

## How to Use the Workflow 📝

1.  **Find Posts (Tab 1):** Enter keywords, negative keywords (optional), and target subreddits. Adjust filters if desired. Click "Find Posts & Validate Subreddits". Review the results table and subreddit status messages.
2.  **Recommend Subs (Tab 1):** Optionally, use the "Recommend Subreddits..." button based on your keywords.
3.  **Select Post (Tab 1):** Click the URL or ID in the results table. It will auto-populate the corresponding field in Tab 2.
4.  **Get Suggestions (Tab 2):** Confirm the Post ID/URL, enter your expertise, and choose an AI tone. Click "Get Preview, Suggestions & Advice".
5.  **Review (Tab 2):** Examine the post preview, top comments context, AI-generated suggestions, and the placement advice.
6.  **Edit (Tab 2):** Use the "⬇️ Copy Suggestion..." button or manually copy text into the "Final Comment Editor". **Critically review and edit the text** to add your unique perspective, ensure accuracy, and match your voice.
7.  **Post Manually:** Copy your final, polished comment from the editor. Go to the actual Reddit post/thread in your browser or app and submit it.

## Possible Use Cases 🧭

This agent can be helpful for various individuals and teams:

* **📈 Marketers & Brand Managers:** Monitor brand mentions, industry keywords, or competitor discussions. Find relevant conversations to engage with potential customers or address feedback (remembering to add genuine value, not just promote).
* **🔍 Researchers & Analysts:** Quickly find discussions related to specific topics, products, or trends across various subreddits for market research or sentiment analysis.
* **🧑‍💻 Developers & Support Teams:** Identify users discussing issues with software or products, allowing for proactive support or feedback gathering.
* **🎓 Experts & Educators:** Find questions or discussions in your area of expertise where you can share knowledge and build authority.
* **✍️ Content Creators & Bloggers:** Discover trending topics, common questions, or pain points within a niche to inspire new content ideas.
* **🤝 Community Managers:** Keep track of conversations in specific communities or related to certain themes to better understand member interests and concerns.
* **🙋 Hobbyists & Enthusiasts:** Easily find and participate in discussions related to your hobbies or interests across different subreddits.

*(Remember the disclaimer: Always prioritize manual review, significant editing, and genuine contribution over automated posting.)*

## Contributing 🤝

Contributions are welcome!

----

### Have fun being an awesome, insightful Redditor! 😄
