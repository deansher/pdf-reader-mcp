# 📚 PDF Reader MCP

[![npm version](https://img.shields.io/npm/v/@sylphlab/pdf-reader-mcp.svg)](https://www.npmjs.com/package/@sylphlab/pdf-reader-mcp)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Welcome to the **PDF Reader MCP** repository! This is an [MCP (Model Context Protocol)](https://modelcontextprotocol.io/) server built with Node.js and TypeScript. It allows LLM clients like Claude and other MCP-compatible AI assistants to read PDF files from local storage or URLs. With this tool, AI agents can extract text, metadata, and page counts from PDF documents, enhancing their ability to work with PDF content.

## 🚀 Features

- **MCP Server Implementation**: Built with the official MCP SDK to provide a standardized interface for AI assistants
- **Text Extraction**: Extract plain text from PDF documents (full documents or specific pages)
- **Metadata Retrieval**: Access metadata such as author, title, and creation date
- **Page Count**: Get the total number of pages in a PDF
- **Multi-source Support**: Process multiple PDF files in a single request
- **URL Support**: Read PDFs from both local files and URLs

## 🔧 Installation

### Prerequisites

- **Node.js**: Make sure you have Node.js installed (version 22.0.0 or higher as specified in package.json)
  - Verify your installation by running `node --version` in your terminal
  - If not installed, download from [nodejs.org](https://nodejs.org/)

### Option 1: Install from NPM (Recommended)

The easiest way to get started is to install the package globally from NPM:

```bash
npm install -g @sylphlab/pdf-reader-mcp
```

After installation, the `pdf-reader-mcp` command will be available in your terminal.

### Option 2: Build from Source

Alternatively, you can build from source:

1. Clone the repository:
   ```bash
   git clone https://github.com/sylphlab/pdf-reader-mcp.git
   ```

2. Navigate to the project directory:
   ```bash
   cd pdf-reader-mcp
   ```

3. Install dependencies:
   ```bash
   npm install
   # Or if you prefer pnpm:
   pnpm install
   ```

4. Build the project:
   ```bash
   npm run build
   # Or:
   pnpm run build
   ```

5. Run the server:
   ```bash
   node dist/index.js
   ```

## 🌐 Setting Up with Claude Clients

This MCP server can be used with different Claude clients. Follow the instructions below for your preferred platform.

### Setting Up with Claude Desktop

Claude Desktop is a standalone application that supports MCP servers on Windows and macOS.

#### Detailed Setup Instructions

1. **Install Claude Desktop** 
   - Download from [claude.ai/download](https://claude.ai/download) if you haven't already
   - Available for Windows and macOS (Linux not currently supported)

2. **Access Claude's Configuration**
   - Open Claude Desktop
   - Click on the Claude menu in your system menu bar or taskbar (not in the app window)
   - Select "Settings..."
   - Click on "Developer" in the left sidebar
   - Click "Edit Config"

3. **Edit Configuration File**
   This will open the configuration file located at:
   - **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
   - **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

4. **Add PDF Reader MCP Configuration**
   Add or modify the configuration to include the PDF Reader MCP:

   ```json
   {
     "mcpServers": {
       "pdf-reader": {
         "command": "pdf-reader-mcp"
       }
     }
   }
   ```

   If you have other MCP servers already configured, add this as an additional entry in the `mcpServers` object.

5. **Specify Directories (Optional but Recommended)**
   If you want to limit PDF access to specific directories, use the following format:

   ```json
   {
     "mcpServers": {
       "pdf-reader": {
         "command": "pdf-reader-mcp",
         "args": [
           "--allowed-dirs",
           "/path/to/pdf/directory1",
           "/path/to/pdf/directory2"
         ]
       }
     }
   }
   ```

   Replace the paths with actual directories where your PDFs are stored.

6. **Restart Claude Desktop**
   - Close Claude Desktop completely
   - Restart the application

7. **Verify Installation**
   - After restart, you should see a hammer icon (🔨) in the input box
   - Click it to see available tools, which should include the PDF reader tool

### Setting Up with Claude Code (CLI)

Claude Code is a CLI tool that also supports MCP servers.

#### Detailed Setup Instructions

1. **Install Claude Code** if you haven't already:
   ```bash
   npm install -g @anthropic-ai/claude-code
   ```

2. **Add the PDF Reader MCP Server**:
   ```bash
   # Add to the current project (default scope)
   claude mcp add pdf-reader pdf-reader-mcp
   ```

3. **Add with Directory Restrictions (Optional)**: 
   ```bash
   claude mcp add pdf-reader pdf-reader-mcp --allowed-dirs /path/to/pdf/directory1 /path/to/pdf/directory2
   ```

4. **Verify Installation**:
   ```bash
   claude mcp list
   ```

5. **Use the PDF Reader in Claude Code**:
   ```bash
   claude
   ```
   
   Then, in the Claude Code session, you can ask about PDFs:
   ```
   > read the content from /path/to/document.pdf
   ```

#### Understanding MCP Server Scopes in Claude Code

Claude Code supports different scopes for MCP server configurations, giving you flexibility in how you manage servers across projects and teams.

1. **Available Scopes**:

   - **Local scope** (default): Stored in your project-specific user settings
   - **User scope**: Available across all your projects
   - **Project scope**: Shared with your team via a `.mcp.json` file

2. **Using Different Scopes**:

   ```bash
   # Add to local scope (default)
   claude mcp add pdf-reader pdf-reader-mcp
   
   # Add to user scope (available across all your projects)
   claude mcp add -s user pdf-reader pdf-reader-mcp
   
   # Add to project scope (shared with team via .mcp.json)
   claude mcp add -s project pdf-reader pdf-reader-mcp
   ```

3. **Pros and Cons of Different Scopes**:

   **User Scope (`-s user`):**
   - ✅ **Pros**:
     - Available in all your projects without re-adding
     - Persists even when switching between different codebases
     - No need to configure for each new project
     - Keeps your personal configuration preferences private
   
   - ❌ **Cons**:
     - Not shared with team members automatically
     - May cause confusion when collaborating if teammates don't have the same setup
     - Configuration stays in your user settings, not with the project

   **Project Scope (`-s project`):**
   - ✅ **Pros**:
     - Automatically shared with team members via version control
     - Configuration travels with the project
     - Ensures consistent MCP server setup across team
     - New team members automatically get the same configuration
   
   - ❌ **Cons**:
     - Requires committing `.mcp.json` to version control
     - May include paths that don't work across different environments
     - All team members need to approve the server when first used

   **Local Scope (default):**
   - ✅ **Pros**:
     - Simple project-specific configuration
     - Doesn't affect other projects
     - Private to your user settings for the specific project
   
   - ❌ **Cons**:
     - Need to reconfigure for each project
     - Not shared with team automatically
     - Configuration doesn't persist across different machines

4. **Recommended Approach**:
   - Use **user scope** for personal tools you want available everywhere
   - Use **project scope** for team-shared tools that should be available to everyone working on the project
   - Use **local scope** for project-specific configurations you don't want to share

5. **Managing Scope-specific Configurations**:
   ```bash
   # List servers in a specific scope
   claude mcp list -s user
   
   # Remove server from a specific scope
   claude mcp remove -s user pdf-reader
   ```

### Troubleshooting Claude Integration

If the PDF Reader MCP doesn't appear in Claude:

1. **Check Configuration Syntax**
   - Ensure your JSON is valid with proper syntax
   - All keys and strings should be enclosed in double quotes

2. **Verify Node Installation**
   - Run `node --version` to verify Node.js is installed and in your PATH
   - Make sure your Node version is 22.0.0 or higher

3. **Check MCP Installation**
   - Verify the package was installed globally by running `pdf-reader-mcp --version`
   - If not found, try reinstalling with `npm install -g @sylphlab/pdf-reader-mcp`

4. **Check Claude Logs**
   - For Claude Desktop, look for error messages in Claude's log files:
     - **macOS**: `~/Library/Logs/Claude/mcp*.log`
     - **Windows**: `%APPDATA%\Claude\logs\mcp*.log`
   - For Claude Code, run with verbose output: `claude --verbose`
   
5. **Test Manual Execution**
   - Try running `pdf-reader-mcp` directly in your terminal to see if it works

## 🌐 Using with Claude.ai Web

Currently, Claude.ai web interface doesn't support MCP servers directly. This functionality is only available in the desktop applications and Claude Code CLI.

## 🌐 Using with Other MCP Clients

For other MCP clients, refer to your client's documentation on how to connect MCP servers. The server uses stdio transport and follows the MCP specification.

## 🧪 Standalone Testing

You can test the server locally using the MCP Inspector tool:

```bash
npm run inspector
# Or:
pnpm run inspector
```

This opens an interactive testing interface where you can explore the available tools and test them.

## 📝 Available Tools

The server provides the following MCP tool:

### `read_pdf`

Reads content and metadata from one or more PDFs (local or from URL).

**Arguments**:
```typescript
{
  "sources": [
    {
      "path": "path/to/local.pdf",  // Local path (relative to where server is run)
      // OR
      "url": "https://example.com/document.pdf",  // URL to PDF
      "pages": "1-3,5,7-"  // Optional: specific pages to extract (string or number[])
    }
    // Can include multiple sources in one request
  ],
  "include_full_text": true,  // Optional: include full text of document (default: false)
  "include_metadata": true,   // Optional: include metadata (default: true)
  "include_page_count": true  // Optional: include total page count (default: true)
}
```

**Response**:
```json
{
  "results": [
    {
      "source": "path/to/local.pdf",
      "success": true,
      "data": {
        "num_pages": 10,
        "info": {
          "PDFFormatVersion": "1.7",
          "IsLinearized": false,
          "IsAcroFormPresent": false,
          "Author": "John Doe",
          "Title": "Sample Document"
        },
        "metadata": { /* Additional metadata */ },
        "full_text": "Extracted text content...",
        // OR if specific pages were requested:
        "page_texts": [
          { "page": 1, "text": "Page 1 content..." },
          { "page": 2, "text": "Page 2 content..." }
        ]
      }
    }
  ]
}
```

## 🛠️ Technologies Used

- **Model Context Protocol (MCP)**: An open protocol for connecting LLMs with external data sources and tools
- **Node.js**: JavaScript runtime environment
- **TypeScript**: Typed superset of JavaScript
- **pdf.js**: Mozilla's PDF rendering library
- **Zod**: TypeScript-first schema validation library

## 🛡️ Security

The server includes path validation to prevent directory traversal attacks. However, you should be careful about which directories you run the server from, as it can access files relative to its working directory.

For enhanced security:
1. Use the `--allowed-dirs` argument to explicitly specify which directories can be accessed
2. Run the server with minimal permissions needed
3. Be cautious about allowing access to sensitive documents

## 📊 Contribution

We welcome contributions! If you would like to contribute to this project, please follow these steps:

1. Fork the repository
2. Create a new branch:
   ```bash
   git checkout -b feature/YourFeature
   ```
3. Make your changes and commit them
4. Push to the branch:
   ```bash
   git push origin feature/YourFeature
   ```
5. Open a pull request

## 📅 Roadmap

- Support for encrypted PDFs
- Image extraction capabilities
- OCR for scanned documents
- Performance optimizations for large PDFs

## 📞 Contact

For any inquiries or support, feel free to reach out via the [GitHub issues page](https://github.com/sylphlab/pdf-reader-mcp/issues).

## 🎉 Acknowledgments

- The [Model Context Protocol](https://modelcontextprotocol.io/) team for creating the specification
- Mozilla for the [pdf.js](https://github.com/mozilla/pdf.js/) library

---

Thank you for your interest in **PDF Reader MCP**! Happy coding!