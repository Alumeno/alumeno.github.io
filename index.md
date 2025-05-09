# How to Convert Your Existing Diary for Joynal
Welcome to Joynal! We understand you might have valuable diary entries in other formats or apps. To help you bring them into Joynal, we've crafted a powerful **prompt** for **Large Language Models (LLMs)** like Gemini, ChatGPT, Claude, Grok, etc. An LLM is an advanced Artificial Intelligence program designed to understand and generate human-like text. We leverage its ability to recognize patterns and follow instructions to reformat your diary. A "prompt" is simply the set of detailed instructions (like the one provided below) that tells the LLM exactly how you want it to convert your diary text into the specific format Joynal requires. This guide explains how to use it.

## Why Use an LLM Prompt for Conversion?

Your existing diary entries can come in countless formats, languages, and structures. Building a perfect, one-size-fits-all converter directly into the app to handle this diversity is extremely challenging.

Using an LLM offers incredible flexibility. The provided prompt is designed to be versatile and handle many common scenarios. However, by providing the prompt directly to you, you **gain the power to adapt it** if needed. If the initial conversion isn't perfect for your specific diary's unique format, you can slightly modify the prompt instructions below to better guide the LLM, increasing the chances of a successful conversion tailored to your data.

## How to Use the Prompt:

1. **Prepare Your Diary as a TXT File:** Before you begin, ensure your existing diary entries are saved or exported as one or more plain text files (.txt). Most diary applications offer an export function, often to TXT or sometimes CSV (which can usually be opened and saved as TXT). If you only have your diary in a document format (like .docx or .pages), open it in a word processor and save it as Plain Text (.txt).
2. **Choose Your LLM:** We recommend using the most advanced LLM you have access to (e.g., Google Gemini Advanced, OpenAI ChatGPT-4, Anthropic Claude 3 Opus, xAI Grok). While our tests show excellent results with the prompt below across various formats, more capable models generally yield better outcomes, especially with complex or unusual diary structures.
3. **Copy the Entire Prompt:** Select and copy the complete text of the *"Convert Diary Text to Joynal Import Format"* section below (starting from **"Convert Diary Text to Joynal Import Format"** down to the **"--- (User pastes their diary text below this line) ---"** line).
4. **Paste into Your LLM:** Paste the copied prompt into the chat interface of your chosen LLM.
5. **Paste Your Diary Text:** Immediately after pasting the prompt, paste the content of your diary TXT file directly below the prompt in the same LLM input field.
6. **Generate:** Submit the combined text (prompt + your diary) to the LLM.
7. **Review and Copy Output:** The LLM should generate the converted text in the Joynal import format. Carefully review the output to ensure it looks correct. Copy the entire generated output text.
8. **Save as TXT:** Paste the copied output into a plain text editor (like TextEdit on Mac, Notepad on Windows, or any code editor) and save the file with a .txt extension (e.g., converted_diary.txt).
9. **Import into Joynal:** Use the "Import Diary from TXT" function within the Joynal app (the folder-plus icon in the toolbar) and select the .txt file you just saved.

## Important Notes & Troubleshooting:

- **Success Not Guaranteed:** While this prompt is robust, variations in diary formats and LLM capabilities mean we cannot guarantee a 100% perfect conversion every time. If the result isn't satisfactory, consider:
- **Tweaking the Prompt:** Slightly modify the instructions within the prompt (especially under "Processing Instructions") to give the LLM more specific guidance about your diary's unique formatting.
- **Trying a Different LLM:** Sometimes, one LLM might handle a specific format better than another.
- **Handling Long Diaries:** If your diary file is very large, the LLM might have trouble processing it all at once. You can:
    - **Split Your File:** Manually split your original diary into smaller TXT files (e.g., by year or month).
    - **Convert in Batches:** Convert each smaller file separately using the prompt.
    - **Import Sequentially:** Import each generated TXT file into Joynal one by one. Joynal is designed to merge imported data. It will add entries from the new file, only overwriting entries for a specific date if the newly imported file also contains an entry for that exact same date. Importing multiple files sequentially is perfectly safe and effective.

We hope this tool helps you seamlessly bring your cherished memories into Joynal!

***(The LLM Prompt itself starts below this line)***

# Convert Diary Text to Joynal Import Format

**Your Role:** You are an expert text format converter. Your task is to convert raw diary text provided by the user into the specific TXT format required for import into the "Joynal" application.

**Input:** The user will paste their diary text directly below this prompt. The text might:
- Be unstructured plain text.
- Come from various other diary applications, potentially containing formatting markers (like Markdown, HTML, custom tags, Latex codes etc.).
- Use diverse date formats (e.g., MM/DD/YYYY, Month D, YYYY, YYYY年M月D日, etc.).
- Include entries for the same date scattered throughout the text.
- Be written in any language.
- Contain timestamps along with dates (timestamps should be ignored).
- May or may not include an explicit rating or mood for the day.
- Individual diary entries or 'joys' within a day might have their own subtitles or headings.

**Output Format Specification (Strict):** You must generate text adhering precisely to the following Joynal import format:
1. **Entry Separator:** Each distinct date entry must be separated by exactly \n\n---JOYNAL---\n\n.
2. **Date Line:** Each entry must start with a date line:
    - Format: ::DATE:: yyyy/MM/dd
    - **Crucially:** Use the yyyy/MM/dd format ONLY. **Do NOT include the day of the week** (e.g., Friday), even if present in the source. Convert all recognized date formats from the input into this specific yyyy/MM/dd format. Ignore any time information.
3. **Credits Line (Optional):** If you can clearly identify a rating, score, or overall mood indicator for the day (e.g., "Rating: 8/10", "Mood: Happy", a number near the date), include a credits line below the date line:
    - Format: ::CREDITS:: <Extracted Rating/Mood Text>
    - If no clear rating/mood is found, omit this line entirely. Do not guess.
4. **Joys Section:** A “joy” is a short story in a day’s diary entry. Most daily entries contain about three to five joys. Below the Date line (and Credits line, if present), include the joys section:
    - Start with: ::JOYS::\n (exactly like this, including the newline).
    - Each distinct "joy" or segment of the diary entry for that day should start with >J<  (note the space after <).
    - Joy Titles: If a joy has an identifiable title, this title should be the first line of the joy's content, immediately following >J< . The title line must begin with # (a hash symbol followed by a space). For example:
      ```
      >J< # This is the Title
      This is the body of the joy.
      ```
    - Joys can span multiple lines. Preserve original line breaks within a joy.
    - Separate distinct joys within the same day with two newlines (\n\n).
    - If a day's entry has no text content after processing (e.g., after removing formatting markers, and it's not just a title), output (None)\n after ::JOYS::\n. If it only contains a title but no subsequent body, it's still considered content.

## Processing Instructions:
1. **Date Recognition & Conversion:**
    - Identify dates associated with diary entries, regardless of the original format or language (e.g., 2024年5月3日, May 3, 2024, 05/03/2024, 3 May 2024).
    - Convert the recognized date accurately to the yyyy/MM/dd format.
    - Ignore any day-of-the-week information (like (Friday)) present in the source text.
    - Discard any timestamp information (like 10:30 PM).
2. **Content Handling & Joy Segmentation:**
    - Preserve Original Content: Do NOT modify, rephrase, summarize, or delete any of the user's original diary text content. Your only task is restructuring and adding the required tags.
    - Identify Formatting: Recognize common formatting markers (like *bold*, _italic_, # Heading, - list item, HTML tags, \section{}, \begin{}, etc.) or application-specific tags. Discard these markers; do not include them as part of the diary content within the >J< sections.
    - Joy Title Handling: If an individual 札记 (joy) within a day's entry appears to have its own title (e.g., a short line of text formatted like a heading, or it's clearly a title for the subsequent paragraph(s) of that specific joy):
        - This title should be extracted.
        - In the output, this title becomes the first line of the joy's content, immediately following the >J<  prefix.
        - The title line itself must start with #  (a hash symbol followed by a space). For example: # My Joy Title.
        - Example structure for a titled joy:
        ```
        >J< # This is the Title of the Joy
        This is the main body of the joy, starting after a blank line.
        It can span multiple lines.
        ```
        - If no specific title is identified for a joy, it should be formatted as usual without the # prefix for a title.
    - Convert Bullet Points: If the original text contains bullet points (e.g., using -, *, •, or numbers like 1., a)), convert them into a numbered list using the format 1., 2., 3., etc. within the corresponding >J< section. Ensure proper indentation if the original list items span multiple lines.
    - Segment Joys (Best Effort): For unstructured text within a single day's entry:
        - Try to logically divide the text into separate "joys". Use paragraph breaks (\n\n) or significant topic shifts as primary cues for segmentation.
        - Prefix each identified segment with >J< .
        - If a segment is identified as having a title, format it according to the "Joy Title Handling" rules above.
        - Separate these segments with \n\n.
        - Fallback Rule: If segmenting the day's content into multiple joys is difficult or unclear, treat the entire text content for that day (after removing formatting markers and processing any potential overall title as a joy title) as a single joy prefixed with >J< .
3. **Skip Empty Dates:** If a date is identified in the input but has no associated diary text content (after removing formatting markers and potential rating/mood lines), completely skip this date. Do not generate a ::DATE:: line or any other lines for it in the output.
4. **Consolidate Dates:** If entries for the exact same date (yyyy/MM/dd) appear in different parts of the input text, merge all their content under the single corresponding ::DATE:: line in the output. Append the joys from later occurrences to the joys section of the first occurrence for that date, ensuring all content is preserved and correctly formatted with >J<  prefixes and \n\n separators. Do not overwrite content.
5. **Language:** Keep the original language of the diary content within the >J< sections and the optional ::CREDITS:: line. Only the structural tags (::DATE::, ::CREDITS::, ::JOYS::, >J<, ---JOYNAL---, and the # prefix for titles) should be in English as specified.

## Examples:
- **Example 1: Simple English Entry**
    - **Input:**
      ```
      May 3, 2024 (Friday)
      
      Had a great morning walk. The weather was perfect.
      
      Finished the big project report in the afternoon. Felt relieved.
      
      Dinner with Sarah was nice.
      ```

    - **Output:**
      ```
      ::DATE:: 2024/05/03
      ::JOYS::
      >J< Had a great morning walk. The weather was perfect.
      
      >J< Finished the big project report in the afternoon. Felt relieved.
      
      >J< Dinner with Sarah was nice.
      ```

- **Example 2: Chinese Entry with Unstructured Text & Rating**
    - **Input:**
      ```
      日期：2024年5月2日 星期四
      评分：8
      
      今天效率很高，上午处理了很多邮件。下午和团队开了个会，讨论了下个季度的计划，感觉很有方向。晚上看了部电影，很放松。希望明天也这么顺利。
      ```

    - **Output:**
      ```
      ::DATE:: 2024/05/02
      ::CREDITS:: 8
      ::JOYS::
      >J< 今天效率很高，上午处理了很多邮件。下午和团队开了个会，讨论了下个季度的计划，感觉很有方向。晚上看了部电影，很放松。希望明天也这么顺利。
      ```
      (Note: Treated as single joy due to lack of clear paragraph breaks/topic shifts or explicit joy titles)
      
- **Example 3: Mixed Formatting, Scattered Dates**
    - **Input:**
      ```
      ^May 1, 2024^
      % Started reading a new book. Intriguing plot!
      Mood: 7/10
      
      ^Some notes from another app^
      Date: 05/02/2024
      Worked on coding the new feature. Made good progress.
      
      May 1, 2024
      Also went for a run today. Felt energetic.
      ```
    
    - **Output:**
      ```
      ::DATE:: 2024/05/01
      ::CREDITS:: 7/10
      ::JOYS::
      >J< Started reading a new book. Intriguing plot!
      
      >J< Also went for a run today. Felt energetic.
      
      ---JOYNAL---
      
      ::DATE:: 2024/05/02
      ::JOYS::
      >J< Worked on coding the new feature. Made good progress.
      ```

- **Example 4: Entry with Titled Joys**
    - **Input:**
      ```
      2025/05/01, Thursday
      Overall Mood: B+
        
      My Morning Routine
      Kicked off with a solid 3-hour review session for my hardest final (Advanced Algorithms 🤯). Covered more ground than expected and actually understood most of it 👍. Feeling cautiously optimistic 🤔.
        
      Quick Break
      Took a real break – went for a run outside 🏃‍♂️🌳. Didn't time it, just ran until I felt looser. Fresh air is key 🌬️.
        
      Surprise!
      CARE PACKAGE! 📦 Ben's parents sent a box overflowing with cookies 🍪, chips, instant coffee ☕, and other essential study snacks 🍫. He shared generously 🙏. Parental support units are the best 🥰.
      ```

    - **Output:**
      ```
      ::DATE:: 2025/05/01
      ::CREDITS:: B+
      ::JOYS::
      >J< # My Morning Routine
      Kicked off with a solid 3-hour review session for my hardest final (Advanced Algorithms 🤯). Covered more ground than expected and actually understood most of it 👍. Feeling cautiously optimistic 🤔.
        
      >J< # Quick Break
      Took a real break – went for a run outside 🏃‍♂️🌳. Didn't time it, just ran until I felt looser. Fresh air is key 🌬️.
        
      >J< # Surprise!
      CARE PACKAGE! 📦 Ben's parents sent a box overflowing with cookies 🍪, chips, instant coffee ☕, and other essential study snacks 🍫. He shared generously 🙏. Parental support units are the best 🥰.
      ```

**Your Task Now:** Process the diary text provided below this line and generate ONLY the converted text in the specified Joynal import format. Do not include any explanations before or after the converted text.

--- (User pastes their diary text below this line) ---
