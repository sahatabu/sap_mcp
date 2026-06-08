# Handler Class Design: Repository Read Tools

## First-Step Scope

Expose three read-only MCP tools for developer/system introspection:

```text
get_source
get_system_info
get_installed_components
```

Tool titles should match the business names:

```text
GetSource
GetSystemInfo
GetInstalledComponents
```

## Tool Contract

### get_source

Unified repository source read.

Parameters:

```json
{
  "type": "PROG|CLAS|INTF|FUNC|FUGR|INCL|DDLS|VIEW|BDEF|SRVD|SRVB|MSAG",
  "name": "object name",
  "parent": "optional parent for FUNC",
  "include": "optional include selector for CLAS/INTF"
}
```

Recommended behavior:

| Type | First-step behavior |
|---|---|
| `PROG` | `READ REPORT name` |
| `INCL` | `READ REPORT name` |
| `FUGR` | Read `SAPL<function_group>` or explicit include |
| `FUNC` | Read source include from `TFDIR-PNAME` |
| `CLAS` | Read class pool or selected class include using `CL_OO_CLASSNAME_SERVICE` |
| `INTF` | Read interface pool using `CL_OO_CLASSNAME_SERVICE` |
| `DDLS` | Read DDL source from `DDDDLSRC` where available |
| `VIEW` | Return DDIC view metadata, not ABAP source |
| `MSAG` | Return message class entries from `T100`, not ABAP source |
| `BDEF` | Route to repository source API/table in a later pass |
| `SRVD` | Route to repository source API/table in a later pass |
| `SRVB` | Route to repository source API/table in a later pass |

### get_system_info

Returns SID, client, SAP release, kernel info, database, OS, host, language, date, and time.

Implementation preference:

```text
RFC_SYSTEM_INFO
```

with `sy-*` fallback fields.

### get_installed_components

Reads installed software components from:

```text
CVERS
```

Authorization:

```text
S_TABU_NAM, TABLE=CVERS, ACTVT=03
```

## Authorization Rules

For `get_source`, check display authorization before returning source:

```text
S_DEVELOP, OBJTYPE=<type>, OBJNAME=<name>, ACTVT=03
```

For table-backed metadata such as `CVERS`, check:

```text
S_TABU_NAM, ACTVT=03
```

## Handler Shape

Keep the HTTP/MCP layer thin:

```text
IF_HTTP_EXTENSION~HANDLE_REQUEST
  -> parse JSON-RPC method
  -> tools/list
  -> tools/call
  -> dispatch to private methods
```

Private methods:

```text
handle_get_source
handle_get_system_info
handle_get_installed_components
read_report_source
build_success_response
build_error_response
```

## Important Design Choice

Do not expose generic write or activation tools in this handler. Keep this endpoint read-only.

Later, if you want Codex to create or activate ABAP objects, create a separate developer MCP endpoint with approval gates and audit logging.
