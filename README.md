# go-mvg

A simple and unofficial Go client for the MVG REST API, built using `oapi-codegen`. Copy and paste the snippet below to get started:

```golang
package main

import (
	"context"
	"fmt"
	"net/http"

	"github.com/everystreet/go-mvg/api/fib/v2"
)

func main() {
	client, err := fib.NewClientWithResponses("https://www.mvg.de/api/fib/v2")
	if err != nil {
		panic(err)
	}

	resp, err := client.GetDeparturesWithResponse(context.Background(), &fib.GetDeparturesParams{
		GlobalId:        "de:09162:50", // Sendlinger Tor
		Limit:           ptr(50),
		OffsetInMinutes: ptr(0),
		TransportTypes:  ptr([]fib.TransportType{fib.UBAHN, fib.TRAM, fib.BUS, fib.REGIONALBUS, fib.SBAHN, fib.SCHIFF}),
	})
	if err != nil {
		panic(err)
	} else if resp.StatusCode() != http.StatusOK {
		panic(resp.Status())
	}

	fmt.Println(resp.JSON200)
}

func ptr[T any](v T) *T {
	return &v
}
```
