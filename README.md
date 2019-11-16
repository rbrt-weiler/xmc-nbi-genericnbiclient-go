# XMC NBI GenericNbiClient (Go)

GenericNbiClient sends a query to the GraphQL-based API provided by the Northbound Interface (NBI) of [Extreme Management Center (XMC)](https://www.extremenetworks.com/product/extreme-management-center/) and prints the raw JSON response to stdout.

## Branches

This project uses two defined branches:

  * `master` is the primary development branch. Code within `master` may be broken at any time.
  * `stable` is reserved for code that compiles without errors and is tested. Track `stable` if you just want to use the software.

Other branches, for example for developing specific features, may be created and deleted at any time.

## Compiling

Use `go run GenericNbiClient.go` to run the tool directly or `go build GenericNbiClient.go` to compile a binary.

Tested with go1.11 and go1.13.

## Usage

`GenericNbiClient -h`:

<pre>
  -host string
        XMC Hostname / IP
  -httptimeout uint
        Timeout for HTTP(S) connections (default 5)
  -insecurehttps
        Do not validate HTTPS certificates
  -password string
        Password for HTTP auth
  -port uint
        HTTP port where XMC is listening (default 8443)
  -query string
        GraphQL query to send to XMC (default "query { network { devices { up ip sysName nickName } } }")
  -username string
        Username for HTTP auth (default "admin")
  -version
        Print version information and exit
</pre>

## Source

The original project is [hosted at GitLab](https://gitlab.com/rbrt-weiler/xmc-nbi-genericnbiclient-go), with a [copy over at GitHub](https://github.com/rbrt-weiler/xmc-nbi-genericnbiclient-go) for the folks over there. Additionally, there is a project at GitLab which [collects all available clients](https://gitlab.com/rbrt-weiler/xmc-nbi-clients).
