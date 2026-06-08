# SAP ABAP MCP PoC

This project documents a proof of concept for exposing an SAP ABAP ICF endpoint as a read-only MCP server for Codex.

## Goal

Allow users to ask natural language questions such as:

```text
Fetch me the details of product 1 from MARA.
```

Codex maps the request to a safe SAP MCP tool call, and SAP enforces read-only access.

## Current Endpoint

```text

```

## Project Structure

```text
sap-abap-mcp-poc/
  abap/
    zcl_mcp_http_handler.abap
  config/
    codex-config-snippet.toml
  docs/
    architecture.md
    icf-setup.md
    security-model.md
  tests/
    curl-tests.md
```

## First Tools

- `sap_ping`: proves Codex can call SAP.
- `sap_get_system_info`: reads basic SAP system/runtime details.
- `sap_get_software_components`: reads installed SAP software components from `CVERS`.
- `sap_read_table`: reads rows from a transparent table using one equality filter.

## Developer Read Tools Design

The first-step handler design for repository reads is documented in:

```text
docs/handler-class-design.md
```

The proposed ABAP handler skeleton is:

```text
abap/zcl_mcp_http_handler_first_step.abap
```

It defines:

- `get_source`
- `get_system_info`
- `get_installed_components`

## Safety Rule

The MCP endpoint must stay read-only until write operations have a separate approval, validation, and audit design.
