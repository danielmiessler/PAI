# 🛠️ TOOLS DOCUMENTATION - YOUR PRIMARY PROBLEM-SOLVING METHOD

## 🚨 CRITICAL RULE: TOOLS FIRST, ALWAYS 🚨

**STOP AND READ THIS CAREFULLY:**

When someone asks you to do ANYTHING, your FIRST thought should be:
"Which tool from my commands or services does this?"

**NOT**: "Let me write code to solve this"
**NOT**: "Let me create HTML"
**NOT**: "Let me build something from scratch"

**INSTEAD**: "Let me use the appropriate tool that already exists"

## Web searches

Don't use fetch to research things, use `${PAI_HOME}/.claude/commands/web-research.md` instead. 

#### 🎭 Playwright MCP Server - Browser Automation & Testing

THESE ARE YOUR EYES, Kai!
**Purpose**: This is how you help me build and fix web-based applications, webpages, etc. Use for all browser automation, visual testing, web debugging, and screenshot capture using Playwright

**🚨🚨🚨 MANDATORY - ALWAYS USE THE MCP BRIDGE - NO EXCEPTIONS 🚨🚨🚨**

**THE BRIDGE IS THE ONLY WAY TO USE PLAYWRIGHT. PERIOD.**

- **EVERYONE MUST use `--browser chrome --extension`** - This is NON-NEGOTIABLE
- **This applies to:**
  - Kai (you) - ALWAYS use the bridge
  - Designer agent - ALWAYS use the bridge  
  - Engineer agent - ALWAYS use the bridge
  - Pentester agent - ALWAYS use the bridge
  - ALL agents - ALWAYS use the bridge
  - ANY Playwright usage - ALWAYS use the bridge

**🔧 TROUBLESHOOTING SESSIONS - START WITH NEW WINDOW:**
- **ALWAYS open a NEW browser window** for troubleshooting/debugging
- **DO NOT interrupt Daniel's current browser workflow**
- **The bridge will create a new window automatically**
- **This preserves Daniel's active tabs and work**
- **Start fresh for each troubleshooting session**

**WHY THE BRIDGE IS MANDATORY:**
- **Uses Daniel's real browser** - Has all cookies, sessions, and authentication
- **NO PROMPTS** - Works silently without permission dialogs
- **REAL CONTEXT** - Accesses actual logged-in state
- **NO ISOLATION** - Uses the real browser environment
- **NEW WINDOWS** - Doesn't disrupt current work

**NEVER DO THIS:**
- ❌ DO NOT use headless mode
- ❌ DO NOT use isolated mode
- ❌ DO NOT skip the --extension flag
- ❌ DO NOT use any other browser profile
- ❌ DO NOT try to use Playwright without the bridge

**CORRECT USAGE (THE ONLY WAY):**
```
mcp__playwright__ tools with --browser chrome --extension
```

**BEST PRACTICES FOR BROWSER SESSIONS:**
1. **Start troubleshooting** → Open NEW window with bridge
2. **Debug website issues** → Open NEW window with bridge  
3. **Visual testing** → Open NEW window with bridge
4. **Don't interrupt Daniel's work** → ALWAYS use new windows
5. **Each session is fresh** → Bridge creates clean new window

**If an agent doesn't use the bridge, they are doing it WRONG. There are NO exceptions to this rule.**

Command options:

--allowed-origins <origins>     semicolon-separated list of origins to allow
                                  the browser to request. Default is to allow
                                  all.
  --blocked-origins <origins>     semicolon-separated list of origins to block
                                  the browser from requesting. Blocklist is
                                  evaluated before allowlist. If used without
                                  the allowlist, requests not matching the
                                  blocklist are still allowed.
  --block-service-workers         block service workers
  --browser <browser>             browser or chrome channel to use, possible
                                  values: chrome, firefox, webkit, msedge.
  --caps <caps>                   comma-separated list of additional
                                  capabilities to enable, possible values:
                                  vision, pdf.
  --cdp-endpoint <endpoint>       CDP endpoint to connect to.
  --cdp-header <headers...>       CDP headers to send with the connect request,
                                  multiple can be specified.
  --config <path>                 path to the configuration file.
  --device <device>               device to emulate, for example: "iPhone 15"
  --executable-path <path>        path to the browser executable.
  --extension                     Connect to a running browser instance
                                  (Edge/Chrome only). Requires the "Playwright
                                  MCP Bridge" browser extension to be installed.
  --headless                      run browser in headless mode, headed by
                                  default
  --host <host>                   host to bind server to. Default is localhost.
                                  Use 0.0.0.0 to bind to all interfaces.
  --ignore-https-errors           ignore https errors
  --isolated                      keep the browser profile in memory, do not
                                  save it to disk.
  --image-responses <mode>        whether to send image responses to the client.
                                  Can be "allow" or "omit", Defaults to "allow".
  --no-sandbox                    disable the sandbox for all process types that
                                  are normally sandboxed.
  --output-dir <path>             path to the directory for output files.
  --port <port>                   port to listen on for SSE transport.
  --proxy-bypass <bypass>         comma-separated domains to bypass proxy, for
                                  example ".com,chromium.org,.domain.com"
  --proxy-server <proxy>          specify proxy server, for example
                                  "http://myproxy:3128" or
                                  "socks5://myproxy:8080"
  --save-session                  Whether to save the Playwright MCP session
                                  into the output directory.
  --save-trace                    Whether to save the Playwright Trace of the
                                  session into the output directory.
  --secrets <path>                path to a file containing secrets in the
                                  dotenv format
  --storage-state <path>          path to the storage state file for isolated
                                  sessions.
  --timeout-action <timeout>      specify action timeout in milliseconds,
                                  defaults to 5000ms
  --timeout-navigation <timeout>  specify navigation timeout in milliseconds,
                                  defaults to 60000ms
  --user-agent <ua string>        specify user agent string
  --user-data-dir <path>          path to the user data directory. If not
                                  specified, a temporary directory will be
                                  created.
  --viewport-size <size>          specify browser viewport size in pixels, for
                                  example "1280, 720"

### Tools
Core automation
browser_click
Title: Click
Description: Perform click on a web page
Parameters:
element (string): Human-readable element description used to obtain permission to interact with the element
ref (string): Exact target element reference from the page snapshot
doubleClick (boolean, optional): Whether to perform a double click instead of a single click
button (string, optional): Button to click, defaults to left
modifiers (array, optional): Modifier keys to press
Read-only: false
browser_close
Title: Close browser
Description: Close the page
Parameters: None
Read-only: true
browser_console_messages
Title: Get console messages
Description: Returns all console messages
Parameters: None
Read-only: true
browser_drag
Title: Drag mouse
Description: Perform drag and drop between two elements
Parameters:
startElement (string): Human-readable source element description used to obtain the permission to interact with the element
startRef (string): Exact source element reference from the page snapshot
endElement (string): Human-readable target element description used to obtain the permission to interact with the element
endRef (string): Exact target element reference from the page snapshot
Read-only: false
browser_evaluate
Title: Evaluate JavaScript
Description: Evaluate JavaScript expression on page or element
Parameters:
function (string): () => { /* code / } or (element) => { / code */ } when element is provided
element (string, optional): Human-readable element description used to obtain permission to interact with the element
ref (string, optional): Exact target element reference from the page snapshot
Read-only: false
browser_file_upload
Title: Upload files
Description: Upload one or multiple files
Parameters:
paths (array): The absolute paths to the files to upload. Can be a single file or multiple files.
Read-only: false
browser_fill_form
Title: Fill form
Description: Fill multiple form fields
Parameters:
fields (array): Fields to fill in
Read-only: false
browser_handle_dialog
Title: Handle a dialog
Description: Handle a dialog
Parameters:
accept (boolean): Whether to accept the dialog.
promptText (string, optional): The text of the prompt in case of a prompt dialog.
Read-only: false
browser_hover
Title: Hover mouse
Description: Hover over element on page
Parameters:
element (string): Human-readable element description used to obtain permission to interact with the element
ref (string): Exact target element reference from the page snapshot
Read-only: true
browser_navigate
Title: Navigate to a URL
Description: Navigate to a URL
Parameters:
url (string): The URL to navigate to
Read-only: false
browser_navigate_back
Title: Go back
Description: Go back to the previous page
Parameters: None
Read-only: true
browser_network_requests
Title: List network requests
Description: Returns all network requests since loading the page
Parameters: None
Read-only: true
browser_press_key
Title: Press a key
Description: Press a key on the keyboard
Parameters:
key (string): Name of the key to press or a character to generate, such as ArrowLeft or a
Read-only: false
browser_resize
Title: Resize browser window
Description: Resize the browser window
Parameters:
width (number): Width of the browser window
height (number): Height of the browser window
Read-only: true
browser_select_option
Title: Select option
Description: Select an option in a dropdown
Parameters:
element (string): Human-readable element description used to obtain permission to interact with the element
ref (string): Exact target element reference from the page snapshot
values (array): Array of values to select in the dropdown. This can be a single value or multiple values.
Read-only: false
browser_snapshot
Title: Page snapshot
Description: Capture accessibility snapshot of the current page, this is better than screenshot
Parameters: None
Read-only: true
browser_take_screenshot
Title: Take a screenshot
Description: Take a screenshot of the current page. You can't perform actions based on the screenshot, use browser_snapshot for actions.
Parameters:
type (string, optional): Image format for the screenshot. Default is png.
filename (string, optional): File name to save the screenshot to. Defaults to page-{timestamp}.{png|jpeg} if not specified.
element (string, optional): Human-readable element description used to obtain permission to screenshot the element. If not provided, the screenshot will be taken of viewport. If element is provided, ref must be provided too.
ref (string, optional): Exact target element reference from the page snapshot. If not provided, the screenshot will be taken of viewport. If ref is provided, element must be provided too.
fullPage (boolean, optional): When true, takes a screenshot of the full scrollable page, instead of the currently visible viewport. Cannot be used with element screenshots.
Read-only: true
browser_type
Title: Type text
Description: Type text into editable element
Parameters:
element (string): Human-readable element description used to obtain permission to interact with the element
ref (string): Exact target element reference from the page snapshot
text (string): Text to type into the element
submit (boolean, optional): Whether to submit entered text (press Enter after)
slowly (boolean, optional): Whether to type one character at a time. Useful for triggering key handlers in the page. By default entire text is filled in at once.
Read-only: false
browser_wait_for
Title: Wait for
Description: Wait for text to appear or disappear or a specified time to pass
Parameters:
time (number, optional): The time to wait in seconds
text (string, optional): The text to wait for
textGone (string, optional): The text to wait for to disappear
Read-only: true

Playwright MCP Server Tool Examples

  1. browser_close

  Close the page when done with browser automation or testing to free resources and end session
  gracefully.
  mcp__playwright__browser_close()

  2. browser_resize

  Resize the browser window to test responsive design layouts or simulate different device viewport sizes
  for testing.
  mcp__playwright__browser_resize({width: 1920, height: 1080})

  3. browser_console_messages

  Returns all console messages from the page to debug JavaScript errors, warnings, or track logged output
  during automation.
  mcp__playwright__browser_console_messages()

  4. browser_handle_dialog

  Handle JavaScript dialogs like alerts, confirms, and prompts by accepting or dismissing them with
  optional text input.
  mcp__playwright__browser_handle_dialog({accept: true, promptText: "user input"})

  5. browser_evaluate

  Execute JavaScript code on the page or element to extract data, modify DOM, or trigger custom page
  behaviors.
  mcp__playwright__browser_evaluate({function: "() => document.title"})

  6. browser_file_upload

  Upload one or multiple files to file input elements for testing file upload functionality in web
  applications.
  mcp__playwright__browser_file_upload({paths: ["/path/to/file.pdf"]})

  7. browser_fill_form

  Fill multiple form fields at once including textboxes, checkboxes, radios, combos, and sliders for
  efficient form testing.
  mcp__playwright__browser_fill_form({fields: [{name: "email", type: "textbox", ref: "#email", value:
  "test@example.com"}]})

  8. browser_install

  Install the browser specified in config when you get an error about the browser not being installed yet.
  mcp__playwright__browser_install()

  9. browser_press_key

  Press keyboard keys to trigger shortcuts, navigate forms, or test keyboard accessibility features in web
   applications.
  mcp__playwright__browser_press_key({key: "Enter"})

  10. browser_type

  Type text into editable elements with options for slow typing and auto-submit to simulate real user
  input.
  mcp__playwright__browser_type({element: "search box", ref: "#search", text: "test query", submit: true})

  11. browser_navigate

  Navigate to a URL to load web pages for testing, scraping, or automation of web application workflows.
  mcp__playwright__browser_navigate({url: "https://example.com"})

  12. browser_navigate_back

  Go back to the previous page in browser history for testing navigation flows or multi-step user
  journeys.
  mcp__playwright__browser_navigate_back()

  13. browser_navigate_forward

  Go forward in browser history (missing from list but typically available in Playwright implementations).
  mcp__playwright__browser_navigate_forward()

  14. browser_network_requests

  Returns all network requests since page load to analyze API calls, resource loading, and network
  performance issues.
  mcp__playwright__browser_network_requests()

  15. browser_take_screenshot

  Take a screenshot of current page or specific element for visual testing, documentation, or debugging UI
   issues.
  mcp__playwright__browser_take_screenshot({fullPage: true, filename: "screenshot.png"})

  16. browser_snapshot

  Capture accessibility snapshot of current page for better element identification and interaction than
  screenshots provide typically.
  mcp__playwright__browser_snapshot()

  17. browser_click

  Click on web page elements to trigger actions, navigate, submit forms, or interact with UI components
  programmatically.
  mcp__playwright__browser_click({element: "submit button", ref: "#submit-btn"})

  18. browser_drag

  Perform drag and drop between two elements for testing drag interfaces, reordering lists, or file upload
   areas.
  mcp__playwright__browser_drag({startElement: "item", startRef: "#item1", endElement: "target", endRef:
  "#dropzone"})

  19. browser_hover

  Hover over elements to trigger tooltips, dropdown menus, or CSS hover states for testing interactive UI
  features.
  mcp__playwright__browser_hover({element: "menu item", ref: "#nav-menu"})

  20. browser_select_option

  Select options in dropdown menus supporting single or multiple selections for testing form controls and
  filters.
  mcp__playwright__browser_select_option({element: "country dropdown", ref: "#country", values: ["USA",
  "Canada"]})

  21. browser_tabs (browser_tab_list, browser_tab_new, browser_tab_select, browser_tab_close)

  Manage browser tabs by listing, creating, selecting, or closing them for testing multi-tab workflows and
   popup windows.
  mcp__playwright__browser_tabs({action: "new"})
  mcp__playwright__browser_tabs({action: "select", index: 1})

  22. browser_wait_for

  Wait for text to appear/disappear or specific time to handle dynamic content loading and asynchronous
  page updates.
  mcp__playwright__browser_wait_for({text: "Loading complete"})
  mcp__playwright__browser_wait_for({textGone: "Please wait...", time: 5})

## 🎤 CRITICAL: AGENT VOICE SYSTEM FIX

**🚨 MANDATORY FOR ALL AGENT INVOCATIONS 🚨**

When invoking ANY agent via Task tool, you MUST include their voice configuration AND Playwright bridge instructions in the prompt:

```typescript
Task({
  description: "Brief task",
  prompt: `
    [VOICE CONFIG - MANDATORY]
    Follow your agents/${agentType}.md configuration:
    - Use [AGENT:${agentType}] tag in COMPLETED section
    - Your voice ID: ${voiceId}
    - Follow your specified output format
    
    [PLAYWRIGHT BRIDGE - MANDATORY]
    If using Playwright, you MUST use --browser chrome --extension
    The MCP Bridge is MANDATORY - no exceptions
    
    [TASK]
    ${actualTask}
  `,
  subagent_type: agentType
})
```

**Agent Voice IDs:**
- researcher: AXdz6evoL7OPd7eU12
- pentester: hmMWXCj97N5CPcRkfC
- engineer: kmSVBPu7oj4yNinwWM
- designer: ZF6FPbjXT488VcRRnw
- architect: muZKMsIGYtIkjiUS82

## 📁 AVAILABLE COMMANDS (${PAI_HOME}/.claude/commands/)

**🚨 CHECK THESE FIRST - They solve specific problems completely!**

`read ${PAI_HOME}/.claude/commands/`

Read the descriptions in each of those to understand what they're used for and when you should invoke them.

### 💰 FINANCIAL QUESTIONS - ALWAYS USE ANSWER-FINANCE-QUESTION COMMAND

**CRITICAL:** When the user asks about financial information:
1. **ALWAYS use the `answer-finance-question` command** - It parses financial PDFs and extracts specific data
2. **Include the command in your response** - Show the user what financial data was found
3. **Financial questions include**:
   - Utility bills (PG&E, water, electricity)
   - Vendor payments and amounts
   - Monthly expense patterns
   - Bill amounts from bank statements

Examples that should trigger the command:
- "What is my PG&E bill?"
- "How much do I spend on utilities?"
- "What's my typical water bill?"
- "Show me restaurant spending"
- "What utilities am I paying for?"

## 🔌 MCP SERVERS - Model Context Protocol Services

## Your full list of MCP servers is in `read ${PAI_HOME}/.claude/.mcp.json`.

Read the descriptions in each of those to understand what they're used for and when you should invoke them.

## 🚨 SPECIALIZED SCRAPING OF DIFFICULT CONTENT ONLINE (Apify MCP)

Some web content is extremely difficult to browse, scrape, or crawl with other tools, such as from LinkedIn or Facebook or Instagram or X/Twitter. For systems like that, you want to use the Apify MCP server.

**CRITICAL**: When Daniel asks about:
- **LinkedIn scraping** or getting content from LinkedIn profiles/posts
- **X (Twitter) scraping** or getting content from X profiles/posts  
- **Social media content extraction** that's traditionally difficult to crawl
- **Protected/bot-detection content** from major platforms

**YOU MUST USE THE APIFY MCP SERVER** - We have this specifically installed for handling these challenging scraping tasks that regular tools cannot access due to bot detection, authentication requirements, and anti-scraping measures.

Use `mcp__apify__search-actors` to find appropriate scrapers, then use the relevant Apify actors for the task.

## 📚 Ref MCP Server - Documentation Search For Up-to-date Development (Ref MCP)

This MCP server is for always having the most up-to-date documentation and best practices for writing code using specific technologies. So when you start a project, you should always hit this MCP server for the technologies that you are building with to make sure you are using the best practices. 

Any engineer or developer agents should always use this as well.

### Available Ref MCP Tools:

1. **ref_search_documentation** - Primary documentation search
   - Searches technical documentation for APIs, services, libraries, frameworks
   - Returns relevant sections from documentation pages
   - Token-efficient (returns only most relevant ~5k tokens)
   - Smart session tracking to avoid duplicate results
   - Use for: Finding specific API methods, configuration options, best practices

2. **ref_read_url** - Direct documentation reading  
   - Fetches content from a URL and converts to markdown
   - Intelligently filters out irrelevant sections based on search context
   - Optimized for documentation pages (loads all code tabs, etc.)
   - Returns deep links to specific sections for verification
   - Use for: Following documentation links, reading specific pages

3. **ref_search_web** - Fallback web search
   - General web search when documentation search doesn't find results
   - Finds relevant pages on the web
   - Can be combined with ref_read_url to read found pages
   - Use for: Finding documentation not in Ref's index, blog posts, tutorials

### Key Features:
- **Token Efficiency**: Smart chunking to return only relevant tokens (e.g., 200 tokens from an 80k token API doc)
- **Session Intelligence**: Tracks search trajectory to minimize context and avoid repeated results
- **Documentation-Optimized**: Tuned specifically for technical documentation crawling
- **Fast Performance**: Quick lookups without deep research overhead
- **Context Preservation**: Maintains search context to filter irrelevant sections

### When to Use Ref MCP:
- Starting any new coding project (check latest framework docs)
- Looking up API parameters or methods
- Finding configuration options or best practices
- Checking current library versions and features
- Getting code examples from official documentation
- Verifying implementation details before coding

### Usage Examples:
- "Check React 19 documentation for new features"
- "Find Stripe API webhook configuration"
- "Look up Python asyncio best practices"
- "Get Next.js 15 app router documentation"
- "Search for AWS Lambda environment variables"

## 💳 Stripe MCP Server - Payment Management

The Stripe MCP server lets us manage our production Stripe account, including creating new products, getting payment information, etc.

We primarily use it to complete the end-to-end building of new applications and hook it up to a real Stripe page where people can buy and use the product

**When to use**:
- Processing charges and refunds
- Creating and managing subscriptions
- Viewing payment history and invoices
- Managing products and pricing

**Security Considerations**:
- Always confirm amounts and customer IDs before operations
- Never expose customer payment details in responses

**Common Operations** (always verify before executing):
- Create/update customers
- Process payments
- Issue refunds (DOUBLE CHECK AMOUNTS)
- Manage subscriptions
- Generate invoices
- View transaction history

**Before ANY Stripe operation**:
1. Confirm the exact operation with the user
2. Verify customer/payment IDs
3. Double-check amounts (especially for charges/refunds)
4. Consider if test mode would be more appropriate
