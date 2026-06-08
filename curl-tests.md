# Curl Tests

## Initialize

```bash
curl -X POST "https://vhupnds5ci.sap.uipath.com:44300/sap/bc/mcp?sap-client=100" \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2025-11-25","capabilities":{},"clientInfo":{"name":"curl","version":"1.0"}}}'
```

## List Tools

```bash
curl -X POST "https://vhupnds5ci.sap.uipath.com:44300/sap/bc/mcp?sap-client=100" \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":2,"method":"tools/list","params":{}}'
```

## Ping

```bash
curl -X POST "https://vhupnds5ci.sap.uipath.com:44300/sap/bc/mcp?sap-client=100" \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":3,"method":"tools/call","params":{"name":"sap_ping","arguments":{}}}'
```

## System Info

```bash
curl -X POST "https://vhupnds5ci.sap.uipath.com:44300/sap/bc/mcp?sap-client=100" \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":4,"method":"tools/call","params":{"name":"sap_get_system_info","arguments":{}}}'
```

## Software Components

```bash
curl -X POST "https://vhupnds5ci.sap.uipath.com:44300/sap/bc/mcp?sap-client=100" \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":5,"method":"tools/call","params":{"name":"sap_get_software_components","arguments":{}}}'
```

## Read Table

```bash
curl -X POST "https://vhupnds5ci.sap.uipath.com:44300/sap/bc/mcp?sap-client=100" \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":6,"method":"tools/call","params":{"name":"sap_read_table","arguments":{"table":"MARA","field":"MATNR","value":"1","maxRows":5}}}'
```

## GetSource: Program

```bash
curl -X POST "https://vhupnds5ci.sap.uipath.com:44300/sap/bc/mcp?sap-client=100" \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":7,"method":"tools/call","params":{"name":"get_source","arguments":{"type":"PROG","name":"ZMY_PROGRAM"}}}'
```

## GetSource: Class Public Section

```bash
curl -X POST "https://vhupnds5ci.sap.uipath.com:44300/sap/bc/mcp?sap-client=100" \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":8,"method":"tools/call","params":{"name":"get_source","arguments":{"type":"CLAS","name":"ZCL_MY_CLASS","include":"PUBLIC"}}}'
```

## GetSystemInfo

```bash
curl -X POST "https://vhupnds5ci.sap.uipath.com:44300/sap/bc/mcp?sap-client=100" \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":9,"method":"tools/call","params":{"name":"get_system_info","arguments":{}}}'
```

## GetInstalledComponents

```bash
curl -X POST "https://vhupnds5ci.sap.uipath.com:44300/sap/bc/mcp?sap-client=100" \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":10,"method":"tools/call","params":{"name":"get_installed_components","arguments":{}}}'
```
