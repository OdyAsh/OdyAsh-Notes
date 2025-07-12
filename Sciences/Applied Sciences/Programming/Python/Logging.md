
# Loguru

## Debugging Notes

### `KeyError: val`

If you encounter a `KeyError`  when logging using loguru, then you probably have this setup:

```python
# NOTE: It will get removed, as loguru doesn't support the following corner case:
#   * You log a message which contains a dict-like string (e.g., "this -> {'hi':1}")
#   * So it will raise (KeyError: "'hi'")
# # Define a formatter function that handles the file path formatting
def _formatter(record):
    """Format a log record with custom styling and layout.

    Example of a loguru record:
    {
        'elapsed': datetime.timedelta(microseconds=127166),
        'exception': None,
        'extra': {'name': 'module_name'},
        'file': {'name': 'file.py', 'path': 'path/to/file.py'},
        'function': '<module>' if module-level code, else 'function name',
        'level': {'name': 'DEBUG', 'no': 10, 'icon': '🐞'},
        'line': 42,
        'message': 'Example log message',
        'module': 'file',
        'name': 'module_name',
        'process': {'id': 12345, 'name': 'MainProcess'},
        'thread': {'id': 67890, 'name': 'MainThread'},
        'time': datetime(2025, 4, 29, 8, 7, 42, 126258, tzinfo=timezone)
    }
    """
    r_time = record["time"]
    r_level = record["level"]
    r_name = record["name"]
    r_file = record["file"]
    r_line = record["line"]
    r_function = record["function"]
    r_message = record["message"]

    # Format the time with green color
    time_str = f"<green>{r_time.strftime('%Y-%m-%d %H:%M:%S')}</green>"

    # Format the level with its own color
    level_str = f"<level>{r_level.name: <4}</level>"

    # Format the module/file name
    if get_settings().DEPLOYMENT_TYPE == "local":
        # file_details = r_file.path if r_level.no >= 40 else r_file.name  # 40 == ERROR
        file_details = r_file.name
        location_str = f"<cyan>{file_details}</cyan>:<cyan>{r_line}</cyan>"
    else:
        # Format like: ansari_whatsapp.presenters.whatsapp_presenter:156
        location_str = f"<cyan>{r_name}</cyan>:<cyan>{r_line}</cyan>"

    # Format the function name with blue color
    if r_function == "<module>":
        # Escape angle brackets for module-level code
        function_str = "<blue>[\\<module-code>]</blue>"
    else:
        function_str = f"<blue>[{r_function}()]</blue>"

    # Format the message with level color
    r_message = repr(r_message)
    # VVV THIS WILL RAISE KeyError IF IT CONTAINS A DICT-LIKE STRING VVV
    message_str = f"<level>{r_message}</level>"

    # Return the complete formatted string
    return f"{time_str} | {level_str} | {location_str} {function_str} | {message_str}\n"

# ... rest of code ... Then:

# Add console handler with custom format
logger.add(
	sys.stderr,
	format=_formatter # <<< THIS WILL CAUSE ERROR
	level=logging_level,
	colorize=True,
	backtrace=False,
	diagnose=True,
)

```

Solution:
* Don't use a custom formatter :(
* Use a custom formatter, but make sure strings containing dict-like strings (e.g. "this -> {'hi':1}") are NEVER logged
	* Not practical
* make `coloorize=False` (I think)
	* Not practical as well
* Ditch Loguru, and resort to logging + rich :( 