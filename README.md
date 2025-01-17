# eWeLink API library

Ewelink SDK to control your eWelink smart devices. 

[![Build Status](https://github.com/pavelbazika/ewelink/workflows/Test/badge.svg)](https://github.com/pavelbazika/ewelink/actions?query=workflow%3ATest)
[![Reviewdog](https://github.com/pavelbazika/ewelink/workflows/reviewdog/badge.svg)](https://github.com/pavelbazika/ewelink/actions?query=workflow%3Areviewdog)
[![Go Report Card](https://goreportcard.com/badge/github.com/pavelbazika/ewelink)](https://goreportcard.com/report/github.com/pavelbazika/ewelink)
[![GoDoc](https://godoc.org/github.com/pavelbazika/ewelink?status.svg)](https://godoc.org/github.com/pavelbazika/ewelink)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/cabd5fbbcde543ec959fb4a3581600ed)](https://app.codacy.com/gh/NicklasWallgren/ewelink?utm_source=github.com&utm_medium=referral&utm_content=NicklasWallgren/ewelink&utm_campaign=Badge_Grade)

Check out the API Documentation http://godoc.org/github.com/pavelbazika/ewelink

# Installation
The library can be installed through `go get` 
```bash
go get github.com/pavelbazika/ewelink
```

# Supported versions
We support the two major Go versions, which are 1.15 and 1.16 at the moment.

# Features
- Retrieve devices
- Turn on/off devices
- Get power consumption [TODO]

# Examples 

## Initiate power state request
```go
import (
    "context"
    "fmt"
    "github.com/pavelbazika/ewelink"
)

instance := ewelink.New()

// authenticate using email
session, err := instance.AuthenticateWithEmail(
	context.Background(), ewelink.NewConfiguration("REGION"), "EMAIL", "PASSWORD")

// retrieve the list of registered devices
devices, err := instance.GetDevices(context.Background(), session)

// turn on the outlet(s) of the first device
response, err := instance.SetDevicePowerState(context.Background(), session, &devices.Devicelist[0], true)

fmt.Println(response)
fmt.Println(err)
```

## Custom AppId and AppSecret
You can provide your own AppId and AppSecret, which can be retrieved from https://dev.ewelink.cc.

```go
ewelink.NewConfiguration("REGION", ewelink.WithAppID("APP_ID"), ewelink.WithAppSecret("APP_SECRET"))
```

## Unit tests
```bash
go test -v -race ./...
```

### Code Guide
We use GitHub Actions to make sure the codebase is consistent (`golangci-lint run`) and continuously tested (`go test -v -race $(go list ./... | grep -v vendor)`). We try to keep comments at a maximum of 120 characters of length and code at 120.


## Contributing
If you find any problems or have suggestions about this library, please submit an issue. Moreover, any pull request, code review and feedback are welcome.
