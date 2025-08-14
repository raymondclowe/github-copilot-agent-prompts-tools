# MCP Server Tools Available

This file lists all MCP (Model Context Protocol) server tools available to the GitHub Copilot agent.

## GitHub MCP Server

The GitHub MCP Server provides comprehensive access to GitHub repositories, issues, pull requests, workflows, and more.

### Repository Content

#### github-mcp-server-get_file_contents
**Description:** Get the contents of a file or directory from a GitHub repository

**Parameters:**
- `owner` (required): Repository owner (username or organization)
- `repo` (required): Repository name
- `path` (optional): Path to file/directory (directories must end with a slash '/'), defaults to "/"
- `ref` (optional): Accepts optional git refs such as `refs/tags/{tag}`, `refs/heads/{branch}` or `refs/pull/{pr_number}/head`
- `sha` (optional): Accepts optional commit SHA. If specified, it will be used instead of ref

#### github-mcp-server-search_code
**Description:** Fast and precise code search across ALL GitHub repositories using GitHub's native search engine. Best for finding exact symbols, functions, classes, or specific code patterns.

**Parameters:**
- `query` (required): Search query using GitHub's powerful code search syntax. Examples: 'content:Skill language:Java org:github', 'NOT is:archived language:Python OR language:go', 'repo:github/github-mcp-server'. Supports exact matching, language filters, path filters, and more.
- `sort` (optional): Sort field ('indexed' only)
- `order` (optional): Sort order for results ('asc' or 'desc')
- `page` (optional): Page number for pagination (min 1)
- `perPage` (optional): Results per page for pagination (min 1, max 100)

#### github-mcp-server-search_repositories
**Description:** Find GitHub repositories by name, description, readme, topics, or other metadata. Perfect for discovering projects, finding examples, or locating specific repositories across GitHub.

**Parameters:**
- `query` (required): Repository search query. Examples: 'machine learning in:name stars:>1000 language:python', 'topic:react', 'user:facebook'. Supports advanced search syntax for precise filtering.
- `page` (optional): Page number for pagination (min 1)
- `perPage` (optional): Results per page for pagination (min 1, max 100)

### Commits and Branches

#### github-mcp-server-get_commit
**Description:** Get details for a commit from a GitHub repository

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `sha` (required): Commit SHA, branch name, or tag name
- `page` (optional): Page number for pagination (min 1)
- `perPage` (optional): Results per page for pagination (min 1, max 100)

#### github-mcp-server-list_commits
**Description:** Get list of commits of a branch in a GitHub repository. Returns at least 30 results per page by default, but can return more if specified using the perPage parameter (up to 100).

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `sha` (optional): Commit SHA, branch or tag name to list commits of. If not provided, uses the default branch of the repository. If a commit SHA is provided, will list commits up to that SHA.
- `author` (optional): Author username or email address to filter commits by
- `page` (optional): Page number for pagination (min 1)
- `perPage` (optional): Results per page for pagination (min 1, max 100)

#### github-mcp-server-list_branches
**Description:** List branches in a GitHub repository

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `page` (optional): Page number for pagination (min 1)
- `perPage` (optional): Results per page for pagination (min 1, max 100)

### Tags

#### github-mcp-server-get_tag
**Description:** Get details about a specific git tag in a GitHub repository

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `tag` (required): Tag name

#### github-mcp-server-list_tags
**Description:** List git tags in a GitHub repository

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `page` (optional): Page number for pagination (min 1)
- `perPage` (optional): Results per page for pagination (min 1, max 100)

### Issues

#### github-mcp-server-get_issue
**Description:** Get details of a specific issue in a GitHub repository.

**Parameters:**
- `owner` (required): The owner of the repository
- `repo` (required): The name of the repository
- `issue_number` (required): The number of the issue

#### github-mcp-server-get_issue_comments
**Description:** Get comments for a specific issue in a GitHub repository.

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `issue_number` (required): Issue number
- `page` (optional): Page number for pagination (min 1)
- `perPage` (optional): Results per page for pagination (min 1, max 100)

#### github-mcp-server-list_issues
**Description:** List issues in a GitHub repository. For pagination, use the 'endCursor' from the previous response's 'pageInfo' in the 'after' parameter.

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `state` (optional): Filter by state, by default both open and closed issues are returned when not provided ('OPEN' or 'CLOSED')
- `labels` (optional): Filter by labels
- `since` (optional): Filter by date (ISO 8601 timestamp)
- `orderBy` (optional): Order issues by field. If provided, the 'direction' also needs to be provided. ('CREATED_AT' or 'UPDATED_AT')
- `direction` (optional): Order direction. If provided, the 'orderBy' also needs to be provided. ('ASC' or 'DESC')
- `after` (optional): Cursor for pagination. Use the endCursor from the previous page's PageInfo for GraphQL APIs.
- `perPage` (optional): Results per page for pagination (min 1, max 100)

#### github-mcp-server-search_issues
**Description:** Search for issues in GitHub repositories using issues search syntax already scoped to is:issue

**Parameters:**
- `query` (required): Search query using GitHub issues search syntax
- `owner` (optional): Optional repository owner. If provided with repo, only issues for this repository are listed.
- `repo` (optional): Optional repository name. If provided with owner, only issues for this repository are listed.
- `sort` (optional): Sort field by number of matches of categories, defaults to best match ('comments', 'reactions', 'reactions-+1', 'reactions--1', 'reactions-smile', 'reactions-thinking_face', 'reactions-heart', 'reactions-tada', 'interactions', 'created', 'updated')
- `order` (optional): Sort order ('asc' or 'desc')
- `page` (optional): Page number for pagination (min 1)
- `perPage` (optional): Results per page for pagination (min 1, max 100)

#### github-mcp-server-list_sub_issues
**Description:** List sub-issues for a specific issue in a GitHub repository.

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `issue_number` (required): Issue number
- `page` (optional): Page number for pagination (default: 1)
- `per_page` (optional): Number of results per page (max 100, default: 30)

### Pull Requests

#### github-mcp-server-get_pull_request
**Description:** Get details of a specific pull request in a GitHub repository.

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `pullNumber` (required): Pull request number

#### github-mcp-server-get_pull_request_comments
**Description:** Get comments for a specific pull request.

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `pullNumber` (required): Pull request number

#### github-mcp-server-get_pull_request_diff
**Description:** Get the diff of a pull request.

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `pullNumber` (required): Pull request number

#### github-mcp-server-get_pull_request_files
**Description:** Get the files changed in a specific pull request.

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `pullNumber` (required): Pull request number
- `page` (optional): Page number for pagination (min 1)
- `perPage` (optional): Results per page for pagination (min 1, max 100)

#### github-mcp-server-get_pull_request_reviews
**Description:** Get reviews for a specific pull request.

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `pullNumber` (required): Pull request number

#### github-mcp-server-get_pull_request_status
**Description:** Get the status of a specific pull request.

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `pullNumber` (required): Pull request number

#### github-mcp-server-list_pull_requests
**Description:** List pull requests in a GitHub repository. If the user specifies an author, then DO NOT use this tool and use the search_pull_requests tool instead.

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `state` (optional): Filter by state ('open', 'closed', 'all')
- `head` (optional): Filter by head user/org and branch
- `base` (optional): Filter by base branch
- `sort` (optional): Sort by ('created', 'updated', 'popularity', 'long-running')
- `direction` (optional): Sort direction ('asc' or 'desc')
- `page` (optional): Page number for pagination (min 1)
- `perPage` (optional): Results per page for pagination (min 1, max 100)

#### github-mcp-server-search_pull_requests
**Description:** Search for pull requests in GitHub repositories using issues search syntax already scoped to is:pr

**Parameters:**
- `query` (required): Search query using GitHub pull request search syntax
- `owner` (optional): Optional repository owner. If provided with repo, only pull requests for this repository are listed.
- `repo` (optional): Optional repository name. If provided with owner, only pull requests for this repository are listed.
- `sort` (optional): Sort field by number of matches of categories, defaults to best match ('comments', 'reactions', 'reactions-+1', 'reactions--1', 'reactions-smile', 'reactions-thinking_face', 'reactions-heart', 'reactions-tada', 'interactions', 'created', 'updated')
- `order` (optional): Sort order ('asc' or 'desc')
- `page` (optional): Page number for pagination (min 1)
- `perPage` (optional): Results per page for pagination (min 1, max 100)

### Workflows and Actions

#### github-mcp-server-list_workflows
**Description:** List workflows in a repository

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `page` (optional): Page number for pagination (min 1)
- `perPage` (optional): Results per page for pagination (min 1, max 100)

#### github-mcp-server-get_workflow_run
**Description:** Get details of a specific workflow run

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `run_id` (required): The unique identifier of the workflow run

#### github-mcp-server-list_workflow_runs
**Description:** List workflow runs for a specific workflow

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `workflow_id` (required): The workflow ID or workflow file name
- `actor` (optional): Returns someone's workflow runs. Use the login for the user who created the workflow run.
- `branch` (optional): Returns workflow runs associated with a branch. Use the name of the branch.
- `event` (optional): Returns workflow runs for a specific event type
- `status` (optional): Returns workflow runs with the check run status ('queued', 'in_progress', 'completed', 'requested', 'waiting')
- `page` (optional): Page number for pagination (min 1)
- `perPage` (optional): Results per page for pagination (min 1, max 100)

#### github-mcp-server-list_workflow_jobs
**Description:** List jobs for a specific workflow run

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `run_id` (required): The unique identifier of the workflow run
- `filter` (optional): Filters jobs by their completed_at timestamp ('latest' or 'all')
- `page` (optional): Page number for pagination (min 1)
- `perPage` (optional): Results per page for pagination (min 1, max 100)

#### github-mcp-server-get_job_logs
**Description:** Download logs for a specific workflow job or efficiently get all failed job logs for a workflow run

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `job_id` (optional): The unique identifier of the workflow job (required for single job logs)
- `run_id` (optional): Workflow run ID (required when using failed_only)
- `failed_only` (optional): When true, gets logs for all failed jobs in run_id
- `return_content` (optional): Returns actual log content instead of URLs
- `tail_lines` (optional): Number of lines to return from the end of the log (default: 500)

#### github-mcp-server-get_workflow_run_logs
**Description:** Download logs for a specific workflow run (EXPENSIVE: downloads ALL logs as ZIP. Consider using get_job_logs with failed_only=true for debugging failed jobs)

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `run_id` (required): The unique identifier of the workflow run

#### github-mcp-server-get_workflow_run_usage
**Description:** Get usage metrics for a workflow run

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `run_id` (required): The unique identifier of the workflow run

#### github-mcp-server-list_workflow_run_artifacts
**Description:** List artifacts for a workflow run

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `run_id` (required): The unique identifier of the workflow run
- `page` (optional): Page number for pagination (min 1)
- `perPage` (optional): Results per page for pagination (min 1, max 100)

#### github-mcp-server-download_workflow_run_artifact
**Description:** Get download URL for a workflow run artifact

**Parameters:**
- `owner` (required): Repository owner
- `repo` (required): Repository name
- `artifact_id` (required): The unique identifier of the artifact

### Security and Scanning

#### github-mcp-server-list_code_scanning_alerts
**Description:** List code scanning alerts in a GitHub repository.

**Parameters:**
- `owner` (required): The owner of the repository.
- `repo` (required): The name of the repository.
- `state` (optional): Filter code scanning alerts by state. Defaults to open ('open', 'closed', 'dismissed', 'fixed')
- `ref` (optional): The Git reference for the results you want to list.
- `severity` (optional): Filter code scanning alerts by severity ('critical', 'high', 'medium', 'low', 'warning', 'note', 'error')
- `tool_name` (optional): The name of the tool used for code scanning.

#### github-mcp-server-get_code_scanning_alert
**Description:** Get details of a specific code scanning alert in a GitHub repository.

**Parameters:**
- `owner` (required): The owner of the repository.
- `repo` (required): The name of the repository.
- `alertNumber` (required): The number of the alert.

#### github-mcp-server-list_secret_scanning_alerts
**Description:** List secret scanning alerts in a GitHub repository.

**Parameters:**
- `owner` (required): The owner of the repository.
- `repo` (required): The name of the repository.
- `state` (optional): Filter by state ('open' or 'resolved')
- `secret_type` (optional): A comma-separated list of secret types to return. All default secret patterns are returned. To return generic patterns, pass the token name(s) in the parameter.
- `resolution` (optional): Filter by resolution ('false_positive', 'wont_fix', 'revoked', 'pattern_edited', 'pattern_deleted', 'used_in_tests')

#### github-mcp-server-get_secret_scanning_alert
**Description:** Get details of a specific secret scanning alert in a GitHub repository.

**Parameters:**
- `owner` (required): The owner of the repository.
- `repo` (required): The name of the repository.
- `alertNumber` (required): The number of the alert.

### Users

#### github-mcp-server-search_users
**Description:** Find GitHub users by username, real name, or other profile information. Useful for locating developers, contributors, or team members.

**Parameters:**
- `query` (required): User search query. Examples: 'john smith', 'location:seattle', 'followers:>100'. Search is automatically scoped to type:user.
- `sort` (optional): Sort users by number of followers or repositories, or when the person joined GitHub. ('followers', 'repositories', 'joined')
- `order` (optional): Sort order ('asc' or 'desc')
- `page` (optional): Page number for pagination (min 1)
- `perPage` (optional): Results per page for pagination (min 1, max 100)

---

## Playwright Browser MCP Server

The Playwright Browser MCP Server provides browser automation capabilities for web testing and interaction.

### Browser Management

#### playwright-browser_close
**Description:** Close the page

**Parameters:** None

#### playwright-browser_resize
**Description:** Resize the browser window

**Parameters:**
- `width` (required): Width of the browser window
- `height` (required): Height of the browser window

#### playwright-browser_install
**Description:** Install the browser specified in the config. Call this if you get an error about the browser not being installed.

**Parameters:** None

### Navigation

#### playwright-browser_navigate
**Description:** Navigate to a URL

**Parameters:**
- `url` (required): The URL to navigate to

#### playwright-browser_navigate_back
**Description:** Go back to the previous page

**Parameters:** None

#### playwright-browser_navigate_forward
**Description:** Go forward to the next page

**Parameters:** None

### Page Interaction

#### playwright-browser_click
**Description:** Perform click on a web page

**Parameters:**
- `element` (required): Human-readable element description used to obtain permission to interact with the element
- `ref` (required): Exact target element reference from the page snapshot
- `button` (optional): Button to click, defaults to left ('left', 'right', 'middle')
- `doubleClick` (optional): Whether to perform a double click instead of a single click

#### playwright-browser_type
**Description:** Type text into editable element

**Parameters:**
- `element` (required): Human-readable element description used to obtain permission to interact with the element
- `ref` (required): Exact target element reference from the page snapshot
- `text` (required): Text to type into the element
- `slowly` (optional): Whether to type one character at a time. Useful for triggering key handlers in the page. By default entire text is filled in at once.
- `submit` (optional): Whether to submit entered text (press Enter after)

#### playwright-browser_press_key
**Description:** Press a key on the keyboard

**Parameters:**
- `key` (required): Name of the key to press or a character to generate, such as `ArrowLeft` or `a`

#### playwright-browser_hover
**Description:** Hover over element on page

**Parameters:**
- `element` (required): Human-readable element description used to obtain permission to interact with the element
- `ref` (required): Exact target element reference from the page snapshot

#### playwright-browser_drag
**Description:** Perform drag and drop between two elements

**Parameters:**
- `startElement` (required): Human-readable source element description used to obtain the permission to interact with the element
- `startRef` (required): Exact source element reference from the page snapshot
- `endElement` (required): Human-readable target element description used to obtain the permission to interact with the element
- `endRef` (required): Exact target element reference from the page snapshot

#### playwright-browser_select_option
**Description:** Select an option in a dropdown

**Parameters:**
- `element` (required): Human-readable element description used to obtain permission to interact with the element
- `ref` (required): Exact target element reference from the page snapshot
- `values` (required): Array of values to select in the dropdown. This can be a single value or multiple values.

### Page Content and Information

#### playwright-browser_take_screenshot
**Description:** Take a screenshot of the current page. You can't perform actions based on the screenshot, use browser_snapshot for actions.

**Parameters:**
- `filename` (optional): File name to save the screenshot to. Defaults to `page-{timestamp}.{png|jpeg}` if not specified.
- `type` (optional): Image format for the screenshot. Default is png. ('png' or 'jpeg')
- `fullPage` (optional): When true, takes a screenshot of the full scrollable page, instead of the currently visible viewport. Cannot be used with element screenshots.
- `element` (optional): Human-readable element description used to obtain permission to screenshot the element. If not provided, the screenshot will be taken of viewport. If element is provided, ref must be provided too.
- `ref` (optional): Exact target element reference from the page snapshot. If not provided, the screenshot will be taken of viewport. If ref is provided, element must be provided too.

#### playwright-browser_snapshot
**Description:** Capture accessibility snapshot of the current page, this is better than screenshot

**Parameters:** None

#### playwright-browser_evaluate
**Description:** Evaluate JavaScript expression on page or element

**Parameters:**
- `function` (required): () => { /* code */ } or (element) => { /* code */ } when element is provided
- `element` (optional): Human-readable element description used to obtain permission to interact with the element
- `ref` (optional): Exact target element reference from the page snapshot

### File Operations

#### playwright-browser_file_upload
**Description:** Upload one or multiple files

**Parameters:**
- `paths` (required): The absolute paths to the files to upload. Can be a single file or multiple files.

### Tab Management

#### playwright-browser_tab_list
**Description:** List browser tabs

**Parameters:** None

#### playwright-browser_tab_new
**Description:** Open a new tab

**Parameters:**
- `url` (optional): The URL to navigate to in the new tab. If not provided, the new tab will be blank.

#### playwright-browser_tab_select
**Description:** Select a tab by index

**Parameters:**
- `index` (required): The index of the tab to select

#### playwright-browser_tab_close
**Description:** Close a tab

**Parameters:**
- `index` (optional): The index of the tab to close. Closes current tab if not provided.

### Monitoring and Debugging

#### playwright-browser_console_messages
**Description:** Returns all console messages

**Parameters:** None

#### playwright-browser_network_requests
**Description:** Returns all network requests since loading the page

**Parameters:** None

#### playwright-browser_handle_dialog
**Description:** Handle a dialog

**Parameters:**
- `accept` (required): Whether to accept the dialog.
- `promptText` (optional): The text of the prompt in case of a prompt dialog.

#### playwright-browser_wait_for
**Description:** Wait for text to appear or disappear or a specified time to pass

**Parameters:**
- `text` (optional): The text to wait for
- `textGone` (optional): The text to wait for to disappear
- `time` (optional): The time to wait in seconds