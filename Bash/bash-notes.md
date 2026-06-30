# Bash Scripting Notes

## Concepts covered
- Variables (no spaces around =)
- Loops (for, nested loops)
- Arrays (ERROR_PATTERNS=("ERROR" "FATAL" "CRITICAL"))
- Conditionals (if/then/fi with [ ] test)
- Command substitution $(command)
- File redirection (> overwrite, >> append)

## Key learnings
- Variable assignment: NO spaces around =
- ./script.sh needed to run (current dir not in $PATH)
- chmod +x to make executable
- mv command both renames AND moves files
- find = locate files, grep = search content inside files

## Script built
analyse-logs.sh - Log analyzer that:
- Finds log files modified in last 24hrs
- Searches for ERROR/FATAL/CRITICAL patterns
- Counts occurrences
- Generates report file
- Alerts if error count exceeds threshold
