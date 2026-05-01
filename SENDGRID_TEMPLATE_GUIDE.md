# CarbonOpus: SendGrid Template Design Guide

This document is a hand-off guide for the design and creation of CarbonOpus email templates in SendGrid. 

## 🎨 Brand & Aesthetic Guidelines
CarbonOpus is a modern, Web3 social music platform. The emails should reflect the app's UI:
*   **Theme:** Dark mode by default (deep blacks/grays like `#09090b` or `#000000`).
*   **Accents:** Neon Green (`#4ade80`) for financial/success actions, and Neon Purple (`#a855f7`) for social/brand elements.
*   **Typography:** Clean sans-serif (e.g., Inter, Helvetica) for body text. Use **Monospace** (e.g., JetBrains Mono, Courier New) for numbers, IDs, prices, and technical data.
*   **Tone:** Professional, empowering, and slightly futuristic.

---

## 🛠 Instructions for the Email Designer
1. Log into SendGrid and go to **Email API > Dynamic Templates**.
2. Click **Create a Dynamic Template** for each item in the list below.
3. Name it clearly (e.g., `CarbonOpus - Purchase Receipt`).
4. Add a Version and build the email using the Design Editor or Code Editor.
5. **CRITICAL:** You must include the exact Handlebars tags (e.g., `{{name}}`) in your text where dynamic data needs to appear.
6. Once a template is saved, copy the **Template ID** (it looks like `d-1234567890abcdef...`) and update the `src/config/emailConfig.ts` file, or hand the list of IDs back to the development team.

---

## 📋 Required Templates & Variables

Here is the comprehensive list of templates to build, the placeholder ID currently in the codebase, and the exact variables that the backend will inject into the email.

### 1. Fan Welcome Email
*   **Codebase Key:** `WELCOME_FAN`
*   **Current ID:** `d-placeholder-welcome-fan`
*   **Description:** Sent immediately when a user creates an account. Focus on discovery, finding music, and setting up their profile.
*   **Required Variables:**
    *   `{{name}}` - The user's display name.

### 2. Artist Welcome Email
*   **Codebase Key:** `WELCOME_ARTIST`
*   **Current ID:** `d-placeholder-welcome-artist`
*   **Description:** Specialized welcome for creators. Focus on uploading tracks, setting prices, and launching their Creator Coin.
*   **Required Variables:**
    *   `{{name}}` - The artist's display name.

### 3. Purchase Receipt (For Buyers)
*   **Codebase Key:** `PURCHASE_RECEIPT`
*   **Current ID:** `d-placeholder-purchase-receipt`
*   **Description:** The transactional receipt sent when a user buys a track.
*   **Required Variables:**
    *   `{{name}}` - The buyer's name.
    *   `{{orderId}}` - The unique transaction/order ID.
    *   `{{total}}` - The total cost (in USDC/USD).
    *   `{{itemCount}}` - Number of tracks purchased.

### 4. New Sale Alert (For Artists)
*   **Codebase Key:** `NEW_SALE_ALERT`
*   **Current ID:** `d-placeholder-new-sale-alert`
*   **Description:** Notification sent to an artist when someone buys their track.
*   **Required Variables:**
    *   `{{artistName}}` - The artist's name.
    *   `{{buyerName}}` - The name of the fan who purchased.
    *   `{{trackTitle}}` - The title of the track sold.

### 5. AI Credit Purchase Receipt
*   **Codebase Key:** `AI_CREDIT_RECEIPT`
*   **Current ID:** `d-placeholder-ai-credit-receipt`
*   **Description:** Receipt for purchasing AI credits for post/image generation.
*   **Required Variables:**
    *   `{{name}}` - The buyer's name.
    *   `{{orderId}}` - The unique order ID.
    *   `{{packagePrice}}` - How much they paid.
    *   `{{creditsAdded}}` - How many credits were added to their account.

### 6. Social Mention Alert
*   **Codebase Key:** `SOCIAL_MENTION`
*   **Current ID:** `d-placeholder-social-mention`
*   **Description:** Sent when a user is `@mentioned` in a post.
*   **Required Variables:**
    *   `{{mentionedName}}` - The user who was tagged.
    *   `{{authorName}}` - The person who wrote the post.
    *   `{{postId}}` - Used to generate a link back to the exact post.

### 7. New Follower Digest (Daily)
*   **Codebase Key:** `NEW_FOLLOWER_DIGEST`
*   **Current ID:** `d-placeholder-new-follower-digest`
*   **Description:** Sent once a day grouping all new followers together to prevent spam.
*   **Required Variables:**
    *   `{{profileName}}` - The user receiving the digest.
    *   `{{followerCount}}` - Total new followers today (e.g., "5").
    *   `{{recentFollowers}}` - A formatted string (e.g., "Alice, Bob, and 3 others").
    *   `{{profileUrl}}` - Link back to their profile.

### 8. System: Audio Verified
*   **Codebase Key:** `AUDIO_VERIFIED`
*   **Current ID:** `d-placeholder-audio-verified`
*   **Description:** Sent when a track passes moderation/DMCA checks and is live on the marketplace.
*   **Required Variables:**
    *   *(To be determined, typically `{{name}}` and `{{trackTitle}}`)*

### 9. System: Audio Flagged
*   **Codebase Key:** `AUDIO_FLAGGED`
*   **Current ID:** `d-placeholder-audio-flagged`
*   **Description:** Sent if a track is taken down due to a DMCA claim or moderation issue.
*   **Required Variables:**
    *   *(To be determined, typically `{{name}}` and `{{trackTitle}}`)*

### 10. General Marketing / Newsletter
*   **Codebase Key:** `NEWSLETTER`
*   **Current ID:** `d-placeholder-newsletter`
*   **Description:** A generic wrapper template used by admins to send platform announcements.
*   **Required Variables:**
    *   `{{name}}` - The user's name.
    *   `{{subject}}` - The email subject line.
    *   `{{bodyContent}}` - The main HTML/Text payload of the email.
    *   `{{previewText}}` - The hidden pre-header text.
    *   `{{ctaText}}` - Text for the primary button.
    *   `{{ctaUrl}}` - Link for the primary button.

---

## 🚀 Post-Design Handoff
When all templates are designed, copy the 10 resulting `d-...` IDs and replace the placeholder strings in `functions/src/config/emailConfig.ts`.