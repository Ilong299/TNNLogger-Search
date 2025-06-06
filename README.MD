# TNNLogger Search Tutorial

This document outlines how to effectively use the search functionality within TNNLogger.

## How to Search

The TNNLogger search command generally follows this format:

`/tnnlogger-search [parameter]:[value] [parameter]:[value] ...`

You can combine multiple parameters in a single search query to refine your results.

## Available Parameters

Here's a detailed list of the available search parameters:

### `sender`

* **Description:** Filters messages based on the username of the sender.
* **Value Type:** String. Supports:
    * Exact matches.
    * Wildcards (`*`) for partial matches.
    * Comma-separated values for multiple senders (OR logic).
* **Examples:**
    * `sender:JohnDoe` - Finds messages sent by "JohnDoe".
    * `sender:*admin*` - Finds messages sent by any user whose name contains "admin".
    * `sender:User1,User2` - Finds messages sent by "User1" OR "User2".
    * `sender:*i*,*e*` - Finds messages sent by users whose names contain "i" OR "e".

### `content`

* **Description:** Filters messages based on the text content within the message.
* **Value Type:** String. Supports:
    * Exact phrase matches.
    * Wildcards (`*`) for partial matches.
* **Examples:**
    * `content:hello world` - Finds messages containing the exact phrase "hello world".
    * `content:*error occurred*` - Finds messages where "error occurred" is present anywhere in the content.

### `isCommand`

* **Description:** Filters messages to include only commands or exclude them.
* **Value Type:** `true` or `false`.
* **Examples:**
    * `isCommand:true` - Displays only messages that were recognized as commands.
    * `isCommand:false` - Displays only messages that were not recognized as commands.

### `UUID`

* **Description:** Filters messages by their unique identifier (UUID).
* **Value Type:** String (a valid UUID).
* **Example:**
    * `UUID:a1b2c3d4-e5f6-7890-1234-567890abcdef` - Finds a specific message by its UUID.

### `sentdate`

* **Description:** Filters messages by the date they were sent.
* **Value Type:** Date string. Supports:
    * Specific dates (e.g., `DD.MM.YYYY`).
    * Wildcards (`*`) for day, month, or year.
* **Examples:**
    * `sentdate:03.03.2023` - Finds messages sent on March 3rd, 2023.
    * `sentdate:04.*.202*` - Finds messages sent on the 4th day of any month in any year starting with '202' (e.g., 2020, 2021, etc.).
    * `sentdate:*.01.2024` - Finds messages sent in January 2024.

### `senttimehours`

* **Description:** Filters messages by the hour they were sent (24-hour format).
* **Value Type:** Integer (0-23). Supports:
    * Single hours.
    * Ranges using a hyphen (`-`).
    * Comma-separated values for multiple specific hours or ranges (OR logic).
* **Examples:**
    * `senttimehours:10` - Finds messages sent at 10 AM.
    * `senttimehours:11-13` - Finds messages sent between 11 AM and 1 PM (inclusive).
    * `senttimehours:9,17` - Finds messages sent at 9 AM or 5 PM.
    * `senttimehours:11-13,15` - Finds messages sent between 11 AM and 1 PM, OR at 3 PM.

### `senttimemins`

* **Description:** Filters messages by the minute they were sent.
* **Value Type:** Integer (0-59). Supports:
    * Single minutes.
    * Ranges using a hyphen (`-`).
    * Comma-separated values for multiple specific minutes or ranges (OR logic).
* **Examples:**
    * `senttimemins:30` - Finds messages sent at the 30th minute of an hour.
    * `senttimemins:0-15` - Finds messages sent within the first 15 minutes of an hour.
    * `senttimemins:0,15,30,45` - Finds messages sent at the 0, 15, 30, or 45th minute of an hour.

---

## Output Control Parameters

TNNLogger provides additional parameters to control the display and storage of search results. These are appended to your search query.

### `loglevel`

* **Description:** Controls the verbosity of logging for files processed during a search.
* **Value Type:** `false`, `true`, `true-console`, or `absolute`.
* **Examples:**
    * `loglevel:false` - No logs about the checked files will be displayed.
    * `loglevel:true` - Logs of the checked files will be shown to the sender.
    * `loglevel:true-console` - Logs of the checked files will be displayed in the console.
    * `loglevel:absolute` - Logs will be displayed to both the sender and the console.

### `searchres`

* **Description:** Dictates where the search results are outputted.
* **Value Type:** `file(filename.extension)`, `inchat`, or `both`.
* **Examples:**
    * `searchres:file(results.txt)` - Results will be saved to `results.txt`.
    * `searchres:file()` - Results will be saved to a file with a default name.
    * `searchres:inchat` - Results will be displayed directly in the chat or interface.
    * `searchres:both` - Results will be saved to a file and displayed in the chat.

### `searchreshow`

* **Description:** Controls how many search results are displayed.
* **Value Type:** `all` or `limit(intLimit)`.
* **Examples:**
    * `searchreshow:all` - All search results will be displayed.
    * `searchreshow:limit(50)` - Only the first 50 results will be shown.
    * `searchreshow:limit()` - Shows results with the default limit of 20. If `searchres` is `inchat` and results exceed the limit, they will be paginated.

---

## Combined Search Examples

Here are some practical examples demonstrating how to combine multiple parameters, including output controls:

* **Find commands sent by specific users between 11 AM and 1 PM, showing logs in console and results in chat:**
    `/tnnlogger-search isCommand:true senttimehours:11-13 sender:UserA,UserB loglevel:true-console searchres:inchat`

* **Find messages containing "error" sent on any day in March 2023, saving all results to a file:**
    `/tnnlogger-search content:*error* sentdate:*.03.2023 searchres:file(error_logs_march_2023.txt) searchreshow:all`

* **Find messages sent by users whose names contain "i" or "e", between 11 AM and 1 PM, showing logs to sender and limiting results to 10 in chat:**
    `/tnnlogger-search senttimehours:11-13 sender:*i*,*e* loglevel:true searchres:inchat searchreshow:limit(10)`

* **Find any message sent at exactly 10:00 AM on March 3rd, 2023, displaying all logs and sending results to both file and chat:**
    `/tnnlogger-search sentdate:03.03.2023 senttimehours:10 senttimemins:0 loglevel:absolute searchres:both searchreshow:all`

---

For further assistance, feel free to reach out: ilon@ilongeniy.me
