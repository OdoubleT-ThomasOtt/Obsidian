**Benötigte MCP Funktionalitäten:**

- MS SQL Server Management (Schema Änderungen und Datenzugriff)
- Telerik Dokuzugriff (ich habe ein JS config scnippet von Telerik erhalten)
- Zugriff auf aktuelle Dokumentationen (etwas wie Context7)
 
- Sequential Thinking MCP ([servers/src/sequentialthinking at main · modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers/tree/main/src/sequentialthinking)) - immer in md file erwähnen
- Memorybank ([alioshr/memory-bank-mcp: A Model Context Protocol (MCP) server implementation for remote memory bank management, inspired by Cline Memory Bank.](https://github.com/alioshr/memory-bank-mcp))
- Website Suche [Tavily MCP Server - Tavily Docs](https://docs.tavily.com/documentation/mcp) oder fetch mcp tool [servers/src/fetch at main · modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers/tree/main/src/fetch)
 
|   |   |   |
|---|---|---|
|MCP|Purpose|Comment|
|Context 7|Damit kann das LLM Dokumentationen nutzen|[All Libraries \| Context7 Documentation](https://context7.com/libraries)|
 
**Playwright:**

1. configure playwright in claude

claude mcp add -s project playwright

3. Install in linux:

npm install playwright  
npx playwright install chrome
  
**Context7 (**[upstash/context7: Context7 MCP Server -- Up-to-date code documentation for LLMs and AI code editors](https://github.com/upstash/context7) **/** [Context7 - Up-to-date documentation for LLMs and AI code editors](https://context7.com/)**):**

1. configure context7 in claude
2. claude mcp add context7 -s project -- npx -y @upstash/context7-mcp
 
**Serena:**

1. Uvx mit warp installieren
2. Mcp in cmp.json hinzufügen "serena": {

"type": "stdio",  
"command": "uvx",  
"args": [  
"--from",  
"git+https://github.com/oraios/serena",  
"serena",  
"start-mcp-server",  
"--context",  
"ide-assistant",  
"--project",  
"/home/thomasott/RiderProjects/eSource/"  
]  
}