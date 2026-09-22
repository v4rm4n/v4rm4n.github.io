# Grep

| Flag |  Purpose | Example |
| - | - | - |
| -E |  Enables Extended Regex (lets you use \|, +, ?, (), {}) | `grep -E "pattern"` |
| -i |  Case-insensitive (matches upper and lower case) | `grep -i "error"` |
| -r / -R | Recursive (searches directories and subdirectories) | `grep -rn "pattern" /var/log/` |
| -n |  Shows line numbers where matches were found | `grep -n "failed"` |
| -o |  Prints ONLY the matching text, not the whole line | `grep -oE "IP_PATTERN"` |
| -v |  Inverts match (excludes matching lines) | `grep -v "Simple Boot"` |

1. Scan files for specific words:

    ```bash
    grep -Ei "password|flag|credential|key" /var/log/syslog /var/log/auth.log 2>/dev/null wrerrrrrrrrrrrrrrrrrrrrrrr
    ```

2. Search for IP Addresses

    ```bash
    grep -Eo '([0-9]{1,3}\.){3}[0-9]{1,3}' /var/log/auth.log
    ```

3. Search for Specific Hex / HTB Flag Patterns

    ```bash
    grep -E "HTB\{[A-Za-z0-9_!@#$%^&*()-+]+\}" /var/log/syslog
    ```

4. Search for Base64 Encoded Strings

    ```bash
    grep -E "[A-Za-z0-9+/]{40,}={0,2}" /var/log/apache2/access.log
    ```

5. Combining Patterns with Anchors

    - Start of line (^): Match lines beginning with a specific word (e.g., lines starting with Sep 21):
    
    ```bash
    grep -E "^Sep 21" /var/log/syslog
    ```

    - End of line ($): Match lines ending with a specific pattern:

    ```bash
    grep -E "FAILED$" /var/log/auth.log
    ```