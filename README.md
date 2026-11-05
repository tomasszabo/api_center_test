# Azure API Center sample catalog

Sample assets for exploring [Git synchronization with Azure API Center](https://learn.microsoft.com/en-gb/azure/api-center/synchronize-assets-git?tabs=portal).
There are two examples of each asset type. No REST backend, agent runtime, or fictional MCP server is deployed by this repository.

## Assets

| Type | Sample | Definition |
| --- | --- | --- |
| REST API | Northstar Orders | [OpenAPI 3.0.3](catalog/rest/orders/openapi.yaml) |
| REST API | Pine Valley Trails | [OpenAPI 3.0.3](catalog/rest/trails/openapi.yaml) |
| Skill | Order status | [SKILL.md](catalog/skills/order-status/SKILL.md) |
| Skill | Documentation search | [SKILL.md](catalog/skills/docs-search/SKILL.md) |
| Agent | Northstar Order Assistant | [Agent definition](catalog/agents/order-assistant/agent.md) |
| Agent | Microsoft Documentation Assistant | [Agent definition](catalog/agents/docs-assistant/agent.md) |
| MCP server | Microsoft Learn (public endpoint) | [server.json](catalog/mcp/microsoft-learn/server.json) |
| MCP server | Pine Valley Trail Guide (fictional) | [server.json](catalog/mcp/trail-guide/server.json) |

The order assistant references the order-status skill and Orders API. The documentation assistant references the docs-search skill and Microsoft Learn server.

All `example.com` addresses and business records are fictional fixtures. Do not expect those endpoints to respond. The Microsoft Learn MCP endpoint, `https://learn.microsoft.com/api/mcp`, is real and public; see its [official documentation](https://github.com/MicrosoftDocs/mcp). Its descriptor's name and version identify this sample catalog entry, not an official Microsoft registry publication or upstream release.

## Connect the repository to API Center

1. Create or select an Azure API Center instance in the Azure portal.
2. Open **Integrations**, select **From Git repository**, and provide the repository URL. To limit discovery to the assets, use a branch/subfolder URL such as `https://github.com/tomasszabo/api_center_test/tree/main/catalog`; replace `main` if using a different branch.
3. For a private repository, follow the guide to store a read-access personal access token in Azure Key Vault and grant the API Center managed identity **Key Vault Secrets User** access. Never commit a token to this repository.
4. Configure asset types and inclusion patterns in the integration. The following patterns are relative to the selected `catalog` folder:

   | Asset type | Inclusion pattern |
   | --- | --- |
   | Skill | `skills/**/SKILL.md` |
   | MCP server | `mcp/**/server.json` |
   | Agent | `agents/**/agent.md` |
   | REST API (if available in your integration) | `rest/**/openapi.yaml` |

   If selecting the repository root instead, prefix each pattern with `catalog/`. Match filename case exactly: the guide's default `**/skill.md` differs from the Agent Skills standard's `SKILL.md`.
5. Set the environment title, identifier, type, and target lifecycle as requested in the portal, then create the integration.
6. Review the integration's synchronization status and the resulting inventory. Git synchronization is periodic, not necessarily immediate. Future committed changes are discovered by the configured integration.

Discovery mappings belong to the Azure integration; this repository does not require a root synchronization manifest.

### Format and integration limits

- REST definitions use OpenAPI 3.0.3 and include response fixtures. The Git synchronization guide does not specify a complete REST ingestion contract. If REST discovery is unavailable, register each definition manually using API Center's **Register an API** workflow and import its OpenAPI file.
- Skills use YAML frontmatter with `name` and `description`, following the [Agent Skills specification](https://agentskills.io/specification).
- Agents are descriptive Markdown definitions. API Center supports Markdown agent definitions for registration, but the Git guide does not document a complete agent parsing contract. Verify discovery in your instance; if unsupported, register an agent manually and upload its definition. These are not A2A JSON agent cards.
- MCP descriptors use the [MCP registry server schema](https://static.modelcontextprotocol.io/schemas/2025-12-11/server.schema.json) with `streamable-http` remote endpoints. Verify the schema version supported by your integration. Do not replace these descriptors with client configuration files containing `mcpServers` or `servers`.
- Cataloging an asset does not deploy it, configure an agent's tools, or guarantee endpoint availability. Configure Microsoft Learn in your MCP client separately if you want to use the documentation-search example.

## Validation

This asset-only repository has no application, build process, or existing test framework. Before importing edits, validate OpenAPI definitions in your preferred OpenAPI validator, MCP descriptors against their declared JSON schema, and skill frontmatter against the Agent Skills specification. Check relative links after moving files.