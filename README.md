# App Service Builder / HTTP MCP server

A stateless JSON-response MCP endpoint with a bounded read-only text tool.

Development/test only. Do not deploy production workloads.
This example was exercised on Stage, not globally release-qualified.
Use only the target approved by your preview contact. Public CLI distribution,
public region availability, and general release remain pending.

## Local setup

Requires Node.js 24 and npm. From the extracted app root:

```sh
npm ci --ignore-scripts
npm test
export APP_API_TOKEN="$(node -e "console.log(require('node:crypto').randomBytes(32).toString('hex'))")"
npm start
```

Open http://localhost:8080/ and request http://localhost:8080/health.
Health: HTTP 200 with `OK`. In a second terminal with the same token, `node client.mjs` initializes, lists `text_length`, and calls it with `Hello`; expected result is 5.
Run local servers only on a trusted/isolated development network.
Stop with Ctrl+C. Do not run several samples on port 8080 simultaneously.

Use the MCP guide in the supplied offline HTML guide for protocol/configuration, app-token security, remote `MCP_URL`, and exact Origin validation. This is a stateless read-only HTTP endpoint, not managed tool discovery or multi-user OAuth. The included client performs direct HTTP protocol requests to the official SDK-backed server.

## Deploy your copy

This ZIP extracts directly into an app source root, without an enclosing folder.
Keep every included file, including the root builder.yaml.
Review source/dependencies, commit and push to your own authorized GitHub repository.
If you put it at repository root, use the supplied Portal creation flow.
For a subtree, set the actual app root with approved Builder CLI or ARM; Portal
creation does not edit an app root and Source Control preserves the existing root.
Component paths resolve inside the selected root.

Follow Portal, Builder CLI, or ARM quickstarts in the supplied
app-service-builder-customer-guide.html. That HTML is not inside this ZIP.
Obtain the approved Portal origin, tenant/subscription/resource group, location,
provider access, and client routing from your contact first.
Do not invent a CLI installation URL or use production endpoints.
Wait for deployment success, then verify the returned application URL.

For configured secrets/settings, use Portal Variables or the ARM contract.
Save only does not modify a running version; build/deploy a new version to
capture desired values. Retained versions use historical values.
Do not put credentials in source, logs, frontend output, or greeting fields.
Builder managed identity, Connectors, Triggers, and canvas installation are
not ready for this trial. No identity-dependent setup is required by this sample.

## Cleanup

Stop local servers and unset/revoke dedicated test credentials where applicable.
Delete only the Builder test app using the supplied Portal or approved CLI.
Wait for deletion completion. App deletion leaves the GitHub repository and
separately provisioned databases, storage, and model services intact.
Those services have their own cost/lifecycle.
