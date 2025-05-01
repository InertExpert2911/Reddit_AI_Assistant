# Reddit AI Assistant

## Description

This tool helps users find relevant discussions on Reddit based on keywords and subreddits, analyzes post context (including top comments), and uses AI (Google Gemini) to generate comment suggestions and placement advice tailored to the user's expertise and desired tone. It aims to assist users in crafting valuable and context-aware comments for meaningful engagement.

The application is built using Python and provides an interactive web interface using Gradio, designed to run within a Kaggle notebook environment.

## Features

* **Reddit Post Search:** Find posts across specified subreddits based on keywords, negative keywords, and filters (score, comments, time). Supports boolean operators (AND, OR, NOT) and phrase searching in keywords.
* **Subreddit Validation:** Checks if target subreddits exist and are accessible, providing feedback and typo suggestions if a subreddit is not found.
* **Subreddit Recommendation:** Suggests relevant subreddits based on input keywords.
* **AI Comment Suggestions:** Generates 4-5 comment ideas using Google Gemini, considering:
    * The original post content (full text preview).
    * The context of the top 10 comments.
    * The user's specified area of expertise.
    * A user-selectable comment tone (Casual, Formal, Friendly, etc.).
* **AI Placement Advice:** Provides recommendations on whether to post as a new top-level comment or reply to a specific existing comment, along with reasoning.
* **Post Preview:** Displays the title, author, and full text (for self-posts) or link URL of the selected Reddit post.
* **Top Comments Display:** Shows the fetched top 10 comments for user context.
* **In-UI Comment Editor:** Provides a dedicated text box to refine AI suggestions or write comments before manually posting on Reddit.
* **Interactive UI:** Built with Gradio for easy interaction within a notebook environment. Includes loading indicators and help tooltips.

## Setup Instructions

To run this tool, you need API credentials for both Reddit and Google Gemini.

**1. Get Google Gemini API Key:**

* Go to [Google AI Studio](https://aistudio.google.com/).
* Sign in with your Google account.
* Create a new API key (look for "Get API key" or similar).
* **Copy the key immediately and keep it safe.**

**2. Get Reddit API Credentials:**

* You need a Reddit account.
* Log in to Reddit on the web.
* Go to your Reddit app preferences: [https://www.reddit.com/prefs/apps](https://www.reddit.com/prefs/apps)
* Scroll down and click **"are you a developer? create an app..."** or **"create another app..."**.
* Fill out the form:
    * **Name:** Give your app a unique name (e.g., `MyRedditHelperApp`).
    * **App Type:** Select **`script`**.
    * **Description:** (Optional)
    * **About URL:** (Optional)
    * **Redirect URI:** Use `http://localhost:8080` (it won't be used for this script type but is often required).
* Click **"create app"**.
* Note down the following (keep them secret!):
    * **Client ID:** The string of characters under your app name (e.g., `aBcDeFgHiJkLmN`).
    * **Client Secret:** The longer string next to `secret`.
    * **User Agent:** Create a descriptive string including your Reddit username (e.g., `MyRedditHelperApp/1.0 by u/YourUsername`). Reddit requires this for API requests.

**3. Set Up Secrets in Kaggle:**

* Open the notebook in Kaggle.
* Go to **"Add-ons"** > **"Secrets"**.
* Add the following secrets, making sure the **Label** matches exactly:
    * `GOOGLE_API_KEY`: Paste your Gemini API key here.
    * `REDDIT_CLIENT_ID`: Paste your Reddit app's Client ID.
    * `REDDIT_CLIENT_SECRET`: Paste your Reddit app's Client Secret.
    * `REDDIT_USER_AGENT`: Enter the User Agent string you created.
    * *(Note: If you were using the version with direct posting, you would also add `REDDIT_USERNAME` and `REDDIT_PASSWORD` here, but the current version doesn't require them).*

## How to Run (in Kaggle)

1.  **Upload Notebook:** Upload the `.ipynb` notebook file containing the code cells to your Kaggle account.
2.  **Add Secrets:** Follow the steps above to add your API keys and Reddit credentials as Kaggle secrets.
3.  **Run Cells Sequentially:** Execute the notebook cells one by one, in order:
    * **Cell 1 (Installations):** Installs required libraries (`gradio`, `praw`, etc.).
    * **Cell 2 (Imports & Secrets):** Loads libraries and attempts to load secrets. Check output for success.
    * **Cell 3 (API Initialization):** Connects to Reddit and Google Gemini using the secrets. Check output for success.
    * **Cell 4 (Find Posts Function):** Defines the main search logic.
    * **Cell 4.5 (Recommend Function):** Defines the subreddit recommendation logic.
    * **Cell 5 (Suggestions Function):** Defines the AI suggestion logic.
    * **Cell 6 (Gradio UI & Launch):** Defines the UI layout and starts the Gradio web server.
4.  **Access the UI:** Once Cell 6 runs successfully, it will print a public URL ending in `.gradio.live`. Click this link to open the interactive UI in a new browser tab.
5.  **Keep Cell Running:** The Gradio UI will only be accessible while the final cell (Cell 6) is actively running in your Kaggle session.

## Usage

1.  **Find Posts:** In the "1. Find Posts & Subreddits" tab, enter keywords (using AND/OR/NOT/phrases), optional negative keywords, and target subreddits. Adjust filters if needed. Click "Find Posts & Validate Subreddits". The table will populate with results, and the status area will show validation feedback.
2.  **Recommend Subreddits:** Enter keywords and click "Recommend Subreddits based on Keywords" to get suggestions.
3.  **Select Post:** Click directly on the URL or ID cell in the results table. This will automatically copy the identifier to the input field in the next tab.
4.  **Get Suggestions:** Go to the "2. Get Suggestions & Edit Comment" tab. Verify the Post URL/ID, enter your area of expertise, and select a desired AI tone. Click "Get Preview, Suggestions & Advice".
5.  **Review:** Examine the Post Preview, Top Comments context, AI Suggestions, and Placement Advice.
6.  **Edit:** Use the "Copy Suggestion to Editor Below" button or manually copy/paste a suggestion into the "Final Comment Editor". **Edit the comment thoroughly** to add your unique value, ensure accuracy, and match your voice.
7.  **Post Manually:** Copy your final edited comment from the editor box and paste it directly into the comment box on the Reddit website/app.

## Dependencies

Ensure the following Python libraries are installed (handled by Cell 1):

* `gradio`
* `praw`
* `google-generativeai`
* `pandas`

## Disclaimer

* This tool uses the official APIs of Reddit and Google Gemini. Please adhere to their respective terms of service.
* Automated posting to Reddit is against their ToS and can lead to account suspension. This tool is designed to *assist* in crafting comments, which should **always be reviewed, edited, and posted manually** by the user.
* Use this tool responsibly and focus on adding genuine value to Reddit communities. Avoid spammy or low-effort commenting.