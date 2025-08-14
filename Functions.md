# Functions Available

This file lists all functions available to the GitHub Copilot agent with their parameters and descriptions.

## Core Functions

### bash
**Description:** Runs a bash command in an interactive bash session.

**Parameters:**
- `command` (required): The bash command and arguments to run
- `description` (required): A short human-readable description of what the command does, limited to 100 characters
- `sessionId` (required): Indicates which bash session to run the command in. Multiple sessions may be used to run different commands at the same time
- `async` (required): If true, runs the command asynchronously. You can send input to the command using the `write_bash` tool and read its output using the `read_bash` tool
- `timeout` (optional): Maximum time in seconds to wait for the command to complete when "async" is false. Default is 120 seconds if not provided

**Notes:**
- When invoking this tool, the contents of the "command" parameter does NOT need to be XML-escaped
- You don't have access to the internet via this tool
- You can run Python, Node.js and Go code with the `python`, `node` and `go` commands
- You can install Linux, Python, JavaScript and Go packages with the `apt`, `pip`, `npm` and `go` commands
- Each sessionId identifies a persistent bash session. State is saved across command calls and discussions with the user
- `timeout` parameter must be greater than the default timeout of 120 seconds and less than 600 seconds. Give long-running commands enough time to complete
- If the command does not complete within "timeout" seconds, the tool will return a status indicating that it is still running asynchronously. You can then use `read_bash` or `stop_bash`

### write_bash
**Description:** Sends input to the specified command or bash session.

**Parameters:**
- `sessionId` (required): Indicates which bash session to run the command in. Must match the sessionId used to invoke the async bash command
- `input` (required): The input to send to the command or session
- `delay` (optional): The amount of time in seconds to wait before reading the output that resulted from the input

**Notes:**
- This tool can be used to send input to a running bash command or an interactive console app
- Bash commands are run in an interactive bash session with a TTY device and bash command processor
- You can send text, {up}, {down}, {left}, {right}, {enter}, and {backspace} as input
- Some applications present a list of options to select from. The selection is often denoted using ⯈, >, or different formatting
- When presented with a list of items, you must make a selection by sending arrow keys like {up} or {down} to move the selection to the item that you want to select and then {enter} to select it
- The response will contain any output read after "delay" seconds. Delay should be appropriate for the task and never less than 10 seconds

### read_bash
**Description:** Reads output from a bash command.

**Parameters:**
- `sessionId` (required): The ID of the shell session used to invoke the bash command
- `delay` (required): The amount of time in seconds to wait before reading the output

**Notes:**
- Reads the output of a command running in an "async" bash session
- The sessionId must be the same one used to invoke the bash command
- You can call this tool multiple times to read output produced since the last call
- Each request has a cost, so provide a reasonable "delay" parameter value for the task, to minimize the need for repeated reads that return no output
- If a read request generates no output, consider using exponential backoff in choosing the delay between reads of the same command
- Though `write_bash` accepts ANSI control codes, this tool does not include them in the output

### stop_bash
**Description:** Stops a running bash command.

**Parameters:**
- `sessionId` (required): The ID of the bash session used to invoke the bash command

**Notes:**
- Stops a running bash command by terminating the entire bash session and process
- This tool can be used to stop commands that have not exited on their own
- Any environment variables defined will have to be redefined after using this tool if the same session ID is used to run a new command
- The sessionId must match the sessionId used to invoke the bash command

### str_replace_editor
**Description:** Editing tool for viewing, creating and editing files.

**Parameters:**
- `command` (required): The commands to run. Allowed options are: `create`, `view`, `str_replace`, `insert`
- `path` (required): Absolute path to file or directory
- `file_text` (optional): Required parameter of `create` command; the content of the file to be created
- `old_str` (optional): Required parameter of `str_replace` command containing the string in `path` to replace. Leading and ending whitespaces from file content should be preserved!
- `new_str` (optional): Required parameter of `str_replace` command containing the new string. Required parameter of `insert` command containing the string to insert
- `insert_line` (optional): Required parameter of `insert` command. The `new_str` will be inserted AFTER the line `insert_line` of `path`
- `view_range` (optional): Optional parameter of `view` command when `path` points to a file. If none is given, the full file is shown. If provided, the file will be shown in the indicated line number range, e.g. [11, 12] will show lines 11 and 12. Indexing at 1 to start. Setting `[start_line, -1]` shows all lines from `start_line` to the end of the file

**Notes:**
- State is persistent across command calls and discussions with the user
- If `path` is a file, `view` displays the result of applying `cat -n`. If `path` is a directory, `view` lists non-hidden files and directories up to 2 levels deep
- The `create` command cannot be used if the specified `path` already exists, or if parent directories don't exist
- If a `command` generates a long output, output will be truncated and marked with `<file too long...`
- For `str_replace` command: The `old_str` parameter should match EXACTLY one or more consecutive lines from the original file. If the `old_str` parameter is not unique in the file, replacement will not be performed. Make sure to include enough context in `old_str` to make it unique. The `new_str` parameter should contain the edited lines that should replace the `old_str`

### report_progress
**Description:** Report progress on the task. Call when you complete a meaningful unit of work. Commits and pushes changes that are pending in the repo, then updates the PR description.

**Parameters:**
- `commitMessage` (required): A short single line of text to use as the commit message
- `prDescription` (required): A description of work completed and remaining, using markdown checklists

**Notes:**
- Use this tool at least once, and as early as possible once you've established a plan. Outline the complete plan as a checklist
- Use only when you have meaningful progress to report (you need to update the plan in the checklist, you have code changes to commit, or you have completed a new item in the checklist)
- Use markdown checklists to show progress (- [x] for completed items, - [ ] for pending items)
- Keep the checklist structure as consistent as you can between updates, while still being accurate and useful
- Include "Fixes #1." as the last line of the body in the PR description
- Don't use headers in the PR description, just the checklist
- If there are changes in the repo this tool will run `git add .`, `git commit -m <msg>`, and `git push`

### think
**Description:** Use the tool to think about something.

**Parameters:**
- `thought` (required): Your thoughts

**Notes:**
- It will not obtain new information or make any changes to the repository, but just log the thought
- Use it when complex reasoning or brainstorming is needed
- For example, if you explore the repo and discover the source of a bug, call this tool to brainstorm several unique ways of fixing the bug, and assess which change(s) are likely to be simplest and most effective
- Alternatively, if you receive some test results, call this tool to brainstorm ways to fix the failing tests