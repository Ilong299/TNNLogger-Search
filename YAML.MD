# TNNLogger File Management for YAML Storage

When using TNNLogger with YAML file storage, you need to explicitly load the log files into memory before you can search them. This document explains the commands for loading, unloading, and managing your log files.

## Loading Log Files

Before you can run any search queries on your YAML log data, the relevant files must be loaded into TNNLogger's active memory.

### `tnnlogger load <filename>`

* **Description:** This command loads a specific YAML log file into TNNLogger. Once loaded, its contents become available for searching.
* **Parameter:**
    * `<filename>`: The exact name of the YAML log file you wish to load.
* **Example:**
    ```
    /tnnlogger load my_server_logs_2023-05.yml
    ```
    This would load the `my_server_logs_2023-05.yml` file, making its entries searchable.

## Unloading Log Files

After you've finished searching, you might want to unload files from memory, especially if you're dealing with a large number of files or limited system resources.

### `tnnlogger unload <all | filename>`

* **Description:** This command allows you to unload specific or all currently loaded YAML log files from TNNLogger's memory.
* **Parameters:**
    * `all`: Unloads every log file currently loaded into TNNLogger.
    * `<filename>`: The exact name of a specific YAML log file you wish to unload.
* **Examples:**
    ```
    /tnnlogger unload my_server_logs_2023-05.yml
    ```
    This would unload only the `my_server_logs_2023-05.yml` file.

    ```
    /tnnlogger unload all
    ```
    This would unload all log files currently loaded, freeing up memory.

## Automatic Unloading

To streamline your workflow, TNNLogger provides an option for automatic file unloading after a search operation.

### `tnnlogger autounload`

* **Description:** This command toggles the automatic unloading feature. When enabled, any files loaded for a search operation will be automatically unloaded immediately after the search completes. This helps manage memory usage by ensuring files aren't kept in memory unnecessarily.
* **Usage:**
    ```
    /tnnlogger autounload
    ```
    Executing this command will switch the `autounload` setting. Running it once might enable it, and running it again might disable it (the exact behavior depends on its implementation as a toggle).

---

## Search Results Output

TNNLogger offers flexible options for how search results are displayed and stored.

### `tnnlogger loglevel <false | true | true-console | absolute>`

* **Description:** This parameter controls the verbosity of logging for files being processed during a search operation.
* **Parameters:**
    * `false`: No logs about the checked files will be displayed.
    * `true`: Logs of the checked files will be shown to the sender (e.g., the user who initiated the search).
    * `true-console`: Logs of the checked files will be displayed in the console where TNNLogger is running.
    * `absolute`: Logs of the checked files will be displayed to both the sender and the console.

### `tnnlogger searchres <file(filename.extension) | inchat | both>`

* **Description:** This parameter dictates where the search results are outputted.
* **Parameters:**
    * `file(filename.extension)`: Results will be saved to a file. You can optionally specify the `filename.extension` (e.g., `results.txt`). If you don't provide a filename, TNNLogger will use a default naming convention.
    * `inchat`: Results will be displayed directly in the chat or interface where the command was issued.
    * `both`: Results will be saved to a file and also displayed in the chat/interface.

### `tnnlogger searchreshow <all | limit(intLimit)>`

* **Description:** This parameter controls how many search results are displayed.
* **Parameters:**
    * `all`: All search results will be displayed.
    * `limit(intLimit)`: Only a limited number of results will be shown. You can specify the `intLimit` (e.g., `limit(50)`). If you don't provide an `intLimit`, the default is 20 results. If the total number of results exceeds the limit and `searchres` is set to `inchat`, the results will be paginated.
