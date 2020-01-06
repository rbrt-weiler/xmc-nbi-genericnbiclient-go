# XMC NBI GenericNbiClient (Go)

GenericNbiClient sends a query to the GraphQL-based API provided by the Northbound Interface (NBI) of [Extreme Management Center](https://www.extremenetworks.com/product/extreme-management-center/) (XMC; formerly known as NetSight) and prints the raw JSON response to stdout.

## Branches

This project uses two defined branches:

  * `master` is the primary development branch. Code within `master` may be broken at any time.
  * `stable` is reserved for code that compiles without errors and is tested. Track `stable` if you just want to use the software.

Other branches, for example for developing specific features, may be created and deleted at any time.

## Compiling

Use `go run GenericNbiClient.go` to run the tool directly or `go build GenericNbiClient.go` to compile a binary. Prebuilt binaries may be available as artifacts from the GitLab CI/CD [pipeline for tagged releases](https://gitlab.com/rbrt-weiler/xmc-nbi-genericnbiclient-go/pipelines?scope=tags).

Tested with [go1.13](https://golang.org/doc/go1.13).

## Usage

`GenericNbiClient -h`:

<pre>
Available options:
  -clientid string
        Client ID for OAuth2
  -clientsecret string
        Client Secret for OAuth2
  -host string
        XMC Hostname / IP
  -httptimeout uint
        Timeout for HTTP(S) connections (default 5)
  -insecurehttps
        Do not validate HTTPS certificates
  -nohttps
        Use HTTP instead of HTTPS
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

OAuth2 will be preferred over username/password.

All options that take a value can be set via environment variables:
  XMCHOST          -->  -host
  XMCPORT          -->  -port
  XMCNOHTTPS       -->  -nohttps
  XMCINSECURE      -->  -insecurehttps
  XMCTIMEOUT       -->  -httptimeout
  XMCCLIENTID      -->  -clientid
  XMCCLIENTSECRET  -->  -clientsecret
  XMCUSERNAME      -->  -username
  XMCPASSWORD      -->  -password
  XMCQUERY         -->  -query
</pre>

## Authentication

GenericNbiClient supports two methods of authentication: HTTP Basic Auth and OAuth2.

  * HTTP Basic Auth: To use HTTP Basic Auth, provide the parameters `username` and `password`. GenericNbiClient will transmit the supplied credentials with each API request as part of the HTTP request header.
  * OAuth2: To use OAuth2, provide the parameters `clientid` and `clientsecret`. GenericNbiClient will attempt to obtain a OAuth2 token from XMC with the supplied credentials and, if successful, submit only that token with each API request as part of the HTTP header.

As all interactions between GenericNbiClient and XMC are secured with HTTPS by default both methods should be safe for transmission over networks. It is strongly recommended to use OAuth2 though. Should the credentials ever be compromised, for example when using them on the CLI on a shared workstation, remediation will be much easier with OAuth2. When using unencrypted HTTP transfer (`nohttps`), Basic Auth should never be used.

In order to use OAuth2 you will need to create a Client API Access client. To create such a client, visit the _Administration_ -> _Client API Access_ tab within XMC and click on _Add_. Make sure to note the returned credentials, as they will never be shown again.

## Authorization

Any user or API client who wants to access the Northbound Interface needs the appropriate access rights. In general, checking the full _Northbound API_ section within rights management will suffice. Depending on the use case, it may be feasible to go into detail and restrict the rights to the bare minimum required.

For regular users (HTTP Basic Auth) the rights are managed via _Authorization Groups_ found in the _Administration_ -> _Users_ tab within XMC. For API clients (OAuth2) the rights are defined when creating an API client and can later be adjusted in the same tab.

## Source

The original project is [hosted at GitLab](https://gitlab.com/rbrt-weiler/xmc-nbi-genericnbiclient-go), with a [copy over at GitHub](https://github.com/rbrt-weiler/xmc-nbi-genericnbiclient-go) for the folks over there. Additionally, there is a project at GitLab which [collects all available clients](https://gitlab.com/rbrt-weiler/xmc-nbi-clients).
