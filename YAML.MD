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