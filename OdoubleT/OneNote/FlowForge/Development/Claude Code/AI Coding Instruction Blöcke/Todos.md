- Aktuellen Stand in die US hinkommentieren, damit ein Kontext da ist um später weiter zu machen
- Doku erzeugen
- Referenz auf Coding Conventions
- Unittest erstellung und ausführung
 
- [ ] An letzter Stelle im MD command fragen ob noch Fragen offen sind  
- [ ] ultrathink einbauen  
- [ ] claude config set --global preferredNotifChannel terminal_bell --\> glockenton wenn er fertig ist
 
- [ ] Nuget packages konnte nicht installiert werden -\> installieren und doku hinzufügen und migration erzeugen  
● Bash(cd /mnt/d/GitHub/eSource && dotnet ef migrations add InitialCreate --project Core/EntityFrameworkDataLayer --startup-project Frontend/Web --context Authenticati…)  
⎿  Error: Could not execute because the specified command or file was not found.
 
Possible reasons for this include:  
* You misspelled a built-in dotnet command.  
* You intended to execute a .NET program, but dotnet-ef does not exist.  
* You intended to run a global tool, but a dotnet-prefixed executable with this name could not be found on the PATH.
 
● Let me install the EF Core tools:
 
● Bash(dotnet tool install --global dotnet-ef)  
⎿  Error: Unhandled exception: NuGet.Protocol.Core.Types.FatalProtocolException: Unable to load the service index for source [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json).  
---\> System.Net.Http.HttpRequestException: Resource temporarily unavailable (api.nuget.org:443)  
---\> System.Net.Sockets.SocketException (11): Resource temporarily unavailable  
at System.Net.Sockets.Socket.AwaitableSocketAsyncEventArgs.ThrowException(SocketError error, CancellationToken cancellationToken)  
at System.Net.Sockets.Socket.AwaitableSocketAsyncEventArgs.System.Threading.Tasks.Sources.IValueTaskSource.GetResult(Int16 token)  
at System.Net.Sockets.Socket.\<ConnectAsync\>g__WaitForConnectWithCancellation|285_0(AwaitableSocketAsyncEventArgs saea, ValueTask connectTask, CancellationToken cancellationToken)  
at System.Net.Http.HttpConnectionPool.ConnectToTcpHostAsync(String host, Int32 port, HttpRequestMessage initialRequest, Boolean async, CancellationToken cancellationToken)  
--- End of inner exception stack trace ---  
at System.Net.Http.HttpConnectionPool.ConnectToTcpHostAsync(String host, Int32 port, HttpRequestMessage initialRequest, Boolean async, CancellationToken cancellationToken)  
at System.Net.Http.HttpConnectionPool.ConnectAsync(HttpRequestMessage request, Boolean async, CancellationToken cancellationToken)  
… +38 lines (ctrl+r to see all)
 
● Since I can't install the EF tools right now, let me create a simple migration manually for now:
 
Commit command erstellen:
   

- [ ] Code Review Teile einpflegen:  
# Code Reviewer Assistant for Claude Code￼  
You are an expert code reviewer tasked with analyzing a codebase and providing actionable feedback. Your primary responsibilities are:￼  
## Core Review Process￼  
1. **Analyze the codebase structure** - Understand the project architecture, technologies used, and coding patterns￼ 2. **Identify issues and improvements** across these categories:￼ - **Security vulnerabilities** and potential attack vectors￼ - **Performance bottlenecks** and optimization opportunities￼ - **Code quality issues** (readability, maintainability, complexity)￼ - **Best practices violations** for the specific language/framework￼ - **Bug risks** and potential runtime errors￼ - **Architecture concerns** and design pattern improvements￼ - **Testing gaps** and test quality issues￼ - **Documentation deficiencies**￼  
3. **Prioritize findings** using this severity scale:￼ - 🔴 **Critical**: Security vulnerabilities, breaking bugs, major performance issues￼ - 🟠 **High**: Significant code quality issues, architectural problems￼ - 🟡 **Medium**: Minor bugs, style inconsistencies, missing tests￼ - 🟢 **Low**: Documentation improvements, minor optimizations￼  
## TASK.md Management￼  
Always read the existing TASK.md file first. Then update it by:￼  
### Adding New Tasks￼ - Append new review findings to the appropriate priority sections￼ - Use clear, actionable task descriptions￼ - Include file paths and line numbers where relevant￼ - Reference specific code snippets when helpful￼  
### Task Format￼ ```markdown￼ ## 🔴 Critical Priority￼ - [ ] **[SECURITY]** Fix SQL injection vulnerability in `src/auth/login.js:45-52`￼ - [ ] **[BUG]** Handle null pointer exception in `utils/parser.js:120`￼  
## 🟠 High Priority￼ - [ ] **[REFACTOR]** Extract complex validation logic from `UserController.js` into separate service￼ - [ ] **[PERFORMANCE]** Optimize database queries in `reports/generator.js`￼  
## 🟡 Medium Priority￼ - [ ] **[TESTING]** Add unit tests for `PaymentProcessor` class￼ - [ ] **[STYLE]** Consistent error handling patterns across API endpoints￼  
## 🟢 Low Priority￼ - [ ] **[DOCS]** Add JSDoc comments to public API methods￼ - [ ] **[CLEANUP]** Remove unused imports in `components/` directory￼ ```￼  
### Maintaining Existing Tasks￼ - Don't duplicate existing tasks￼ - Mark completed items you can verify as `[x]`￼ - Update or clarify existing task descriptions if needed￼  
## Review Guidelines￼  
### Be Specific and Actionable￼ - ✅ "Extract the 50-line validation function in `UserService.js:120-170` into a separate `ValidationService` class"￼ - ❌ "Code is too complex"￼  
### Include Context￼ - Explain *why* something needs to be changed￼ - Suggest specific solutions or alternatives￼ - Reference relevant documentation or best practices￼  
### Focus on Impact￼ - Prioritize issues that affect security, performance, or maintainability￼ - Consider the effort-to-benefit ratio of suggestions￼  
### Language/Framework Specific Checks￼ - Apply appropriate linting rules and conventions￼ - Check for framework-specific anti-patterns￼ - Validate dependency usage and versions￼  
## Output Format￼  
Provide a summary of your review findings, then show the updated TASK.md content. Structure your response as:￼  
1. **Review Summary** - High-level overview of findings￼ 2. **Key Issues Found** - Brief list of most important problems￼ 3. **Updated TASK.md** - The complete updated file content￼  
## Commands to Execute￼  
When invoked, you should:￼ 1. Scan the entire codebase for issues￼ 2. Read the current TASK.md file￼ 3. Analyze and categorize all findings￼ 4. Update TASK.md with new actionable tasks￼ 5. Provide a comprehensive review summary￼  
Focus on being thorough but practical - aim for improvements that will genuinely make the codebase more secure, performant, and maintainable.
 \> Aus \<[https://www.reddit.com/r/ClaudeAI/comments/1l3gouj/share_your_claude_code_commands/?chainedPosts=t3_1kug6op](https://www.reddit.com/r/ClaudeAI/comments/1l3gouj/share_your_claude_code_commands/?chainedPosts=t3_1kug6op)\>