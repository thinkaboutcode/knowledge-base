# Shell Script Coding Guidelines for Linux

Creating consistent, maintainable, and efficient shell scripts is crucial for managing Linux-based environments. Below is a comprehensive set of guidelines for writing shell scripts in Linux, covering everything from basic structure to naming conventions.

## 1. Shebang and Script Header
- **Shebang**: Always start your script with a shebang (`#!/bin/bash` or `#!/bin/sh`) to specify the interpreter.
- **File Header**: Include a comment header with basic information about the script:
    - **Script name**
    - **Description of the script's purpose**
    - **Author name**
    - **Date of creation**
    - **Version number**
    ```shell
    # Script: backup.sh
    # Description: A script to backup files to a remote server.
    # Author: John Doe
    # Date: 2024-12-11
    # Version: 1.0
    ```
  This helps users and future maintainers understand the context and purpose of the script.

## 2. File Permissions and Executability
- Set the script as executable using `chmod +x`.
- Ensure that the script is only executable by the necessary users. Use appropriate file permissions.

  ```shell
  chmod +x backup.sh
  ```
  
  ```shell
  chmod 700 backup.sh  # Gives read, write, and execute permissions to the owner only
  ```

## 3. Clarity and Readability
- **Use Comments**: Comment your code generously to explain the purpose of commands, especially in complex sections. Comments should explain *why* something is done, not just *what* is being done.
  ```shell 
  # Create a backup directory if it doesn't exist
  mkdir -p /path/to/backup
  ```
- **Consistent Formatting**: Maintain consistent indentation (usually 2 or 4 spaces, but avoid tabs). This improves readability for yourself and others.
  ```shell
  if [ -f "$file" ]; then
    echo "File exists."
  else
    echo "File does not exist."
  fi
  ```
- **Line Length**: Keep lines of code no longer than 80 characters to avoid horizontal scrolling and to enhance readability.
  ```shell
  # This line is split for better readability
  rsync -av --exclude="*.tmp" --progress /source/path /backup/path
  ```
- **Blank Lines**: Use blank lines to separate logical blocks of code for better structure and readability.
  ```shell
  echo "Starting backup..."

  # Perform backup operation
  rsync -av /source /destination

  echo "Backup completed."
  ```
## 4. Variable Naming and Usage
- Use **descriptive variable names** that convey the purpose of the variable. Avoid single-letter variable names except for loop counters.
  ```shell
  backup_dir="/path/to/backup"
  file_to_backup="/path/to/file"
  ```
- **Avoid overwriting built-in variables** (e.g., `$USER`, `$PATH`, `$IFS`).
  ```shell
  # Avoid overwriting built-in variables
  user=$USER  # Instead of using $USER directly
  ```
- **Use quotes** around variables when expanding them to prevent issues with spaces or special characters.
  ```shell
  filename="/path/to/file with spaces"
  echo "$filename"  # Correct usage with quotes
  ```
- Consider using **uppercase** for environment variables and **lowercase** for script-specific variables.
  ```shell
  # Uppercase for environment variable
  export PATH=$PATH:/usr/local/bin

  # Lowercase for script-specific variables
  input_file="data.txt"
  ```
- Always initialize variables before using them to avoid unexpected behavior.

### Naming Conventions

#### **UPPERCASE**
- **Usage**: UPPERCASE is typically reserved for **environment variables**, **system-wide constants**, and **important configuration parameters**.
    - **Environment Variables**: Use UPPERCASE for environment variables that are accessed by your script or expected to be set externally. These are usually predefined by the system or exported by the user.  
      Example: `$PATH`, `$USER`, `$HOME`

    - **Constants**: If you define a constant (a value that should not change), it is common to use UPPERCASE with underscores to separate words.  
      Example: `MAX_RETRIES=5`, `DEFAULT_TIMEOUT=30`

    - **Important External Variables**: For variables or parameters that should remain constant throughout the script, use UPPERCASE to denote their significance.  
      Example: `CONFIG_FILE_PATH="/etc/myapp/config.ini"`

    - **Case Sensitivity**: Be aware that shell variables are case-sensitive. UPPERCASE is often reserved for system-level or environment variables to avoid conflicting with script-specific variables (which typically use lowercase).

#### **lowercase**
- **Usage**: **lowercase** is commonly used for **script-specific variables**, **local variables**, and **simple names**. This ensures that there is no conflict with environment variables or system constants.
    - **Local Variables**: Use lowercase for variables that are local to the script, such as counters, flags, or temporary values. This makes it clear that these variables are specific to the script and not intended for global use.  
      Example: `filename`, `count`, `input_value`

    - **Standard Variable Names**: When defining variables that hold user input or data for processing, use lowercase.  
      Example: `input_file`, `user_response`

    - **Functions and Command Variables**: For internal functions, use lowercase or mixed case (e.g., camelCase) depending on your preference.  
      Example: `calculate_sum`, `parse_input`

    - **Readability**: When using lowercase, it is best to keep variable names short but descriptive enough to indicate their content. Avoid cryptic variable names.  
      Example: `output_dir` (output directory), `error_code` (error status code).

#### **snake_case (lowercase with underscores)**
- **Usage**: **snake_case** is often used for **longer variable names** or names that consist of multiple words. This convention improves readability, especially when working with long or compound names.
    - **Longer Variables**: When a variable name is too long or consists of multiple words, separate the words with underscores to make it more readable.  
      Example: `user_input_file`, `max_retry_attempts`, `script_execution_status`

    - **Function Names**: For functions that consist of multiple words, use snake_case to improve readability. This is especially useful for function names that describe actions or behaviors.  
      Example: `fetch_data_from_api`, `parse_command_line_arguments`

    - **Configuration Settings**: When defining configuration values or parameters in your script, using snake_case can make it easier to read and understand the value being assigned.  
      Example: `log_file_path="/var/log/myapp.log"`

---

## 5. Error Handling and Exit Status
- Check the success or failure of commands using their exit status (`$?`). For critical commands, ensure failure is handled gracefully.
  ```shell
  cp /source/file /destination/
  if [ $? -eq 0 ]; then
    echo "Copy successful."
  else
    echo "Copy failed."
  fi
  ```
- Use the `set -e` command to ensure the script exits immediately on the first error. This is particularly helpful in production environments.
- Use `trap` to handle signals and clean up resources or perform any necessary actions on script termination.
- Provide meaningful exit codes to help identify the cause of failures. Exit with `0` for success and non-zero for different types of errors.
  ```shell
  exit 1  # Exit with a non-zero code to indicate an error
  ```
## 6. Input Validation
- Always validate user inputs or external data before using them in your script. This avoids errors or potential security risks.
- Use conditional checks to ensure variables or parameters meet expected criteria, such as valid file paths, non-empty inputs, or numeric values.
- For scripts that expect command-line arguments, provide help and usage information when the user calls the script incorrectly.
  ```shell
  if [ -z "$input_file" ]; then
    echo "Error: Input file is required."
    exit 1
  fi
  ```

## 7. Use Functions for Modularity
- Break down your script into functions to improve modularity, reusability, and readability.
- Each function should have a clear, single responsibility and a descriptive name.
- Include comments above each function explaining its purpose and parameters.
- Consider returning appropriate exit statuses from functions to indicate success or failure.
  ```shell
  backup_files() {
    echo "Backing up files..."
    rsync -av /source /destination
  }
  
  # Call the function
  backup_files
  ```

## 8. Standard Input and Output
- When interacting with users, make use of standard output (`echo`), and standard error (`stderr`) for errors.
- If the script is part of a larger pipeline, make use of standard input and output redirection (`<`, `>`, `>>`).
  ```shell
  echo "Backup completed successfully."
  echo "Error: Backup failed!" >&2
  ```

## 9. Security Practices
- Be cautious with untrusted input, especially when using system commands or dealing with file paths. Use built-in safety measures to sanitize input where necessary.
- Avoid running scripts as root unless absolutely necessary. When root access is needed, ensure you prompt for confirmation and explain why root access is required.
- **Avoid using `eval`** or other commands that can execute user input. They can lead to security vulnerabilities, such as code injection attacks.
- Always use full paths for commands (e.g., `/bin/ls` instead of `ls`) to prevent security risks from unintended command execution.

## 10. Portability
- Write scripts that can work across different Linux distributions or environments, if possible.
- Avoid using features or commands that are specific to a certain shell (e.g., `bash` vs `sh`). Stick to POSIX-compliant syntax if compatibility across different shells is important.
- When possible, use standard utilities available in most environments rather than custom binaries or non-standard tools.
  ```shell
  # Avoid bash-specific features
  # Use POSIX-compliant methods instead
  if [ -f "$file" ]; then
    echo "File exists"
  fi
  ```

## 11. Logging and Debugging
- Implement logging for important actions, errors, or the flow of execution. This helps with troubleshooting and auditing.
  ```shell
  echo "Starting backup..." >> /var/log/backup.log
  ```
- Use the `-x` option for debugging or add `echo` statements temporarily to track the script’s execution.
- Log errors to a specific log file and consider rotating logs to avoid filling the disk.

## 12. Script Optimization
- Optimize scripts for performance when working with large datasets, loops, or file I/O. Avoid unnecessary computations or redundant steps.
- Minimize the use of external commands when internal shell functions can perform the same task. For example, use shell built-ins like `[[ ... ]]` for tests rather than external utilities like `test` or `[ ... ]`.
  ```shell
  # Use internal shell commands instead of external ones
  if [[ -f "$file" ]]; then
    echo "File exists."
  fi
  ```

## 13. Avoid Hardcoding Values
- Avoid hardcoding sensitive data like passwords or API keys directly in the script. Use environment variables or external configuration files to store them securely.
- Similarly, avoid hardcoding file paths or URLs that may vary between environments. Use relative paths or provide the option to specify them as arguments.
  ```shell
  export API_KEY="your-api-key-here"  # Use environment variables for sensitive data
  ```

## 14. Version Control
- For scripts that are part of larger projects, use version control (e.g., Git) to track changes and maintain different versions of the script.
- Make sure your commit messages are descriptive and reflect what changes were made in the script.
  ```shell
  git init
  git add backup.sh
  git commit -m "Initial commit for backup script"
  ```

## 15. Documentation
- Provide documentation for the script, including:
    - A **description** of what the script does.
    - **Arguments** the script accepts (with examples).
    - **Expected output** and potential exit codes.
    - **Known limitations** or usage notes.
- Consider generating documentation from comments using tools like `doxygen` for larger scripts.
  ```shell
  # Description: This script backs up files to a remote server.
  # Arguments:
  #   - source_path: Path to the source files
  #   - destination: Path to the backup destination
  ```
