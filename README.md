# Rillet Go SDK

Go client library for the [Rillet Accounting API](https://api.rillet.com). Covers contracts, invoices, bills, payments, journal entries, customers, vendors, reports, webhooks, and more.

This client is generated from the Rillet OpenAPI spec using [OpenAPI Generator](https://openapi-generator.tech). Do not edit the generated files directly — regenerate from the spec instead.

- API version: v3.0
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
	client := openapi.NewAPIClient(cfg)

	ctx := context.WithValue(context.Background(), openapi.ContextAccessToken, "YOUR_BEARER_TOKEN")

	customers, _, err := client.CustomersAPI.ListAllCustomers(ctx).Execute()
	if err != nil {
		log.Fatal(err)
	}
	fmt.Printf("%d customers\n", len(customers.GetData()))
}
```

To use a proxy, set the environment variable `HTTP_PROXY`:

```go
os.Setenv("HTTP_PROXY", "http://proxy_name:proxy_port")
```

## Configuration of Server URL

Default configuration comes with `Servers` field that contains server objects as defined in the OpenAPI specification.

### Select Server Configuration

For using other server than the one defined on index 0 set context value `openapi.ContextServerIndex` of type `int`.

```go
ctx := context.WithValue(context.Background(), openapi.ContextServerIndex, 1)
```

### Templated Server URL

Templated server URL is formatted using default variables from configuration or from context value `openapi.ContextServerVariables` of type `map[string]string`.

```go
ctx := context.WithValue(context.Background(), openapi.ContextServerVariables, map[string]string{
	"basePath": "v2",
})
```

Note, enum values are always validated and all unused variables are silently ignored.

### URLs Configuration per Operation

Each operation can use different server URL defined using `OperationServers` map in the `Configuration`.
An operation is uniquely identified by `"{classname}Service.{nickname}"` string.
Similar rules for overriding default operation server index and variables applies by using `openapi.ContextOperationServerIndices` and `openapi.ContextOperationServerVariables` context maps.

```go
ctx := context.WithValue(context.Background(), openapi.ContextOperationServerIndices, map[string]int{
	"{classname}Service.{nickname}": 2,
})
ctx = context.WithValue(context.Background(), openapi.ContextOperationServerVariables, map[string]map[string]string{
	"{classname}Service.{nickname}": {
		"port": "8443",
	},
})
```

## Documentation For Authorization


Authentication schemes defined for the API:
### bearerAuth

- **Type**: HTTP Bearer token authentication

Example

```go
auth := context.WithValue(context.Background(), openapi.ContextAccessToken, "BEARER_TOKEN_STRING")
r, err := client.Service.Operation(auth, args)
```


## Documentation for Utility Methods

Due to the fact that model structure members are all pointers, this package contains
a number of utility functions to easily obtain pointers to values of basic types.
Each of these functions takes a value of the given basic type and returns a pointer to it:

* `PtrBool`
* `PtrInt`
* `PtrInt32`
* `PtrInt64`
* `PtrFloat`
* `PtrFloat32`
* `PtrFloat64`
* `PtrString`
* `PtrTime`

## Author

Mateo ([@mateomaple](https://github.com/mateomaple))

