# OpenProject MCP Server

Model Context Protocol (MCP) server for OpenProject API integration. Enables AI assistants to interact with OpenProject work packages, projects, and time tracking.

## Installation

### Global Installation (Recommended)

```bash
npm install -g @sparkbird/openproject-mcp
```

### Local Installation

```bash
npm install @sparkbird/openproject-mcp
```

## Configuration

### Get OpenProject API Key

1. Log into your OpenProject instance
2. Go to **My Account** → **Access tokens**
3. Create a new API token
4. Copy the token

### Add to Kiro MCP Config

Add to `.kiro/settings/mcp.json`:

```json
{
  "mcpServers": {
    "openproject": {
      "command": "npx",
      "args": ["-y", "@sparkbird/openproject-mcp"],
      "env": {
        "OPENPROJECT_URL": "https://your-openproject-instance.com",
        "OPENPROJECT_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

Or if installed globally:

```json
{
  "mcpServers": {
    "openproject": {
      "command": "openproject-mcp",
      "env": {
        "OPENPROJECT_URL": "https://your-openproject-instance.com",
        "OPENPROJECT_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

## Available Tools

| Tool | Description |
|------|-------------|
| `list_projects` | List all projects |
| `get_work_package` | Get work package details by ID |
| `list_work_packages` | List work packages with filters |
| `get_children` | Get child work packages of a parent |
| `list_statuses` | List all available statuses |
| `list_types` | List all work package types (Feature, Task, Bug, etc.) |
| `get_user` | Get user information |
| `create_work_package` | Create a new work package |
| `update_work_package` | Update an existing work package |
| `log_time` | Log time entry for a work package |
| `list_attachments` | List attachments of a work package |
| `get_attachment` | Fetch an attachment; returns the image inline for image files, metadata + URL otherwise |
| `upload_attachment` | Upload a file (local path or base64) to a work package |
| `raw_api_call` | Make a raw API call to any endpoint |

## Usage Examples

### List Children of a Feature

```javascript
get_children({ parentId: 211 })
```

### Create a New Task

```javascript
create_work_package({
  subject: "Implement token budget management",
  parentId: 538,
  assigneeId: 10,
  startDate: "2026-01-15",
  dueDate: "2026-01-15"
})
```

### List Tasks Assigned to Me

```javascript
list_work_packages({ assigneeId: "me" })
```

### Update Work Package Status

```javascript
update_work_package({
  id: 123,
  statusId: 12,  // Status ID from list_statuses
  estimatedTime: "PT2H"  // 2 hours in ISO 8601 format
})
```

### Log Time

```javascript
log_time({
  workPackageId: 123,
  hours: 2.5,
  comment: "Implemented feature X",
  spentOn: "2026-01-23"
})
```

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `OPENPROJECT_URL` | Yes | Your OpenProject instance URL |
| `OPENPROJECT_API_KEY` | Yes | API key from OpenProject |

## Requirements

- Node.js >= 18.0.0
- OpenProject instance with API access

## License

MIT. Fork of [cyborgx0x/mcp-openproject](https://github.com/cyborgx0x/mcp-openproject) (MIT, © original authors), extended with attachment/image support.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request.

## Links

- [OpenProject API Documentation](https://www.openproject.org/docs/api/)
- [Model Context Protocol](https://modelcontextprotocol.io/)
