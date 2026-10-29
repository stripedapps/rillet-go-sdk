# Rillet Go SDK

Go client library for the [Rillet Accounting API](https://api.rillet.com). Covers contracts, invoices, bills, payments, journal entries, customers, customer families, vendors, approval workflows, cash matching, close checklists, reports, webhooks, and more.

This client is generated from the Rillet OpenAPI spec using [OpenAPI Generator](https://openapi-generator.tech). Do not edit the generated files directly — regenerate from the spec instead.

- API version: v4.0
- Package version: 1.0.0
- Generator version: 7.13.0

## Regenerating

The spec source is Rillet's public docs hub:
`https://docs.api.rillet.com/openapi/rillet-accounting-api.json`

Download it over the vendored `openapi.json`, then regenerate with OpenAPI
Generator 7.13.0 (run via Docker so no local Java is required):

```sh
curl -sL -H "Accept: application/json" \
  -o openapi.json \
  "https://docs.api.rillet.com/openapi/rillet-accounting-api.json"

docker run --rm -v "$PWD":/local openapitools/openapi-generator-cli:v7.13.0 generate \
  -i /local/openapi.json -g go -o /local \
  --git-user-id stripedapps --git-repo-id rillet-go-sdk \
  --additional-properties=packageName=openapi,enumClassPrefix=true,generateInterfaces=true

go mod tidy
go build ./...
```

The `--additional-properties` are required to keep the output stable:
`enumClassPrefix=true` preserves prefixed enum constants (e.g. `INVOICESTATUS_UNPAID`),
and `generateInterfaces=true` keeps the per-service `…API` interface types.
`.openapi-generator-ignore` protects `README.md`, `docs/`, and `test/` from being
overwritten.

After a regeneration, update the "API version" line above to match `info.version` in `openapi.json`.

## Installation

```sh
go get github.com/stripedapps/rillet-go-sdk
```

Import in your code:

```go
import openapi "github.com/stripedapps/rillet-go-sdk"
```

## Quick start

```go
package main

import (
	"context"
	"fmt"
	"log"

	openapi "github.com/stripedapps/rillet-go-sdk"
)

func main() {
	cfg := openapi.NewConfiguration()
	cfg.AddDefaultHeader("X-Rillet-API-Version", "4")
	client := openapi.NewAPIClient(cfg)

	ctx := context.WithValue(context.Background(), openapi.ContextAccessToken, "YOUR_BEARER_TOKEN")

	customers, _, err := client.CustomersAPI.ListAllCustomers(ctx).Execute()
	if err != nil {
		log.Fatal(err)
	}
	fmt.Printf("%d customers\n", len(customers.GetCustomers()))
}
```

To use a proxy, set the environment variable `HTTP_PROXY`:

```go
os.Setenv("HTTP_PROXY", "http://proxy_name:proxy_port")
```

## API version header

The SDK matches API v4, and the client does not send a version on its own. Set the `X-Rillet-API-Version` header to `4` on the configuration, as the Quick start does. Without the header, Rillet picks the version for you. Its [docs](https://docs.api.rillet.com/docs/getting-started.md) describe version 1 as the default, with a switch to the latest version on August 1st, 2026. An explicit header keeps responses matching the v4 models in this SDK, whichever default applies.

## Configuration of Server URL

`NewConfiguration()` lists two servers, both from the OpenAPI spec:

| Index | URL | Use |
|---|---|---|
| 0 | `https://api.rillet.com` | Production (default) |
| 1 | `https://sandbox.api.rillet.com` | Sandbox |

### Select Server Configuration

To use the sandbox, set the context value `openapi.ContextServerIndex` (type `int`) to `1`.

```go
ctx := context.WithValue(context.Background(), openapi.ContextAccessToken, "YOUR_SANDBOX_TOKEN")
ctx = context.WithValue(ctx, openapi.ContextServerIndex, 1)
```

### URLs Configuration per Operation

An operation picks its own server with `openapi.ContextOperationServerIndices`. The key is `"{ServiceName}.{OperationName}"`, matching the Go method, for example `CustomersAPIService.ListAllCustomers`.

```go
ctx := context.WithValue(context.Background(), openapi.ContextOperationServerIndices, map[string]int{
	"CustomersAPIService.ListAllCustomers": 1,
})
```

The spec defines no server variables, so `openapi.ContextServerVariables` and `openapi.ContextOperationServerVariables` have no effect.

## Documentation For Authorization

Authentication schemes defined for the API:

### bearerAuth

- **Type**: HTTP Bearer token authentication

Example

```go
auth := context.WithValue(context.Background(), openapi.ContextAccessToken, "BEARER_TOKEN_STRING")
customers, _, err := client.CustomersAPI.ListAllCustomers(auth).Execute()
```

## Documentation for Utility Methods

Due to the fact that model structure members are all pointers, this package contains
a number of utility functions to easily obtain pointers to values of basic types.
Each of these functions takes a value of the given basic type and returns a pointer to it:

* `PtrBool`
* `PtrInt`
* `PtrInt32`
* `PtrInt64`
* `PtrFloat32`
* `PtrFloat64`
* `PtrString`
* `PtrTime`

## Author

Mateo ([@mateomaple](https://github.com/mateomaple))
