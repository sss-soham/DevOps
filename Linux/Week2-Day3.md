Week 2 Day 3 — Text Processing in Linux (grep, sed, awk)

Linux provides powerful command-line tools for processing text and logs.
These tools are heavily used in DevOps for log analysis, automation, and configuration management.

The three most important tools are:

grep → searching text

sed → editing/modifying text

awk → processing structured text and columns

1. grep — Search Text Patterns

grep stands for Global Regular Expression Print.

It searches for a pattern in files and prints matching lines.

Basic Syntax
grep "pattern" filename

Example:

grep "error" logs.txt

This prints all lines containing the word error.

Common grep Options
Case-Insensitive Search
grep -i error file.txt

Matches Error, ERROR, error.

Show Line Numbers
grep -n error file.txt

Output example:

5:error occurred
12:error connecting
Count Matches
grep -c error file.txt

Shows how many lines match.

Recursive Search in Folder
grep -r "error" /var/log

Searches inside all files within the directory.

Invert Match (Exclude Pattern)
grep -v error file.txt

Shows lines not containing the word error.

Combine with Other Commands

Example:

cat logs.txt | grep error

Used frequently in log debugging.

2. sed — Stream Editor

sed is used to edit and transform text automatically.

It processes text line-by-line.

Commonly used for find and replace operations.

Basic Syntax
sed 's/old/new/' file.txt

Explanation:

s = substitute
old = text to replace
new = replacement text
Replace First Occurrence
sed 's/error/warning/' file.txt

Only replaces the first match in each line.

Replace All Occurrences
sed 's/error/warning/g' file.txt

g = global replacement.

Modify File Directly

By default sed only prints the result.

To modify the file permanently:

sed -i 's/error/warning/g' file.txt
Delete Lines

Delete line number 2:

sed '2d' file.txt

Delete lines containing a pattern:

sed '/error/d' file.txt
Create Backup While Editing
sed -i.bak 's/error/fixed/g' file.txt

Creates backup:

file.txt.bak
3. awk — Text Processing Tool

awk is used to process structured text and extract columns.

Very powerful for parsing logs, reports, and data.

Basic Syntax
awk '{print $1}' file.txt

$1 = first column.

Example file:

John 25 DevOps
Alice 30 Developer
Bob 28 Tester

Command:

awk '{print $1}' file.txt

Output:

John
Alice
Bob
Print Multiple Columns
awk '{print $1,$3}' file.txt

Output:

John DevOps
Alice Developer
Bob Tester
Pattern Matching
awk '/error/ {print $0}' logs.txt

Prints lines containing error.

Field Separator

Sometimes fields are separated by : or ,.

Example:

awk -F ":" '{print $1}' /etc/passwd

This prints usernames.

Difference Between grep, sed, awk
Tool	Purpose
grep	Search text
sed	Modify text
awk	Process structured data
DevOps Use Cases
grep

Search logs for errors
grep error /var/log/syslog
sed
Modify configuration files automatically
sed -i 's/8080/9090/g' config.conf
awk
Extract specific data from logs

awk '{print $1,$5}' access.log
cat logs.txt | grep error | awk '{print $1,$2}'
Steps:

grep finds error lines
awk extracts columns

What I Practiced

Searching logs using grep

Extracting fields using awk

Combining commands in pipelines

Key Learning


These commands are essential for DevOps engineers working with servers and logs.Text processing tools help automate log analysis and system troubleshooting.

Editing text using sed

Output shows filtered data


Example Combining All Three




