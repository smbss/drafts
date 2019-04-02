![alt text](https://i.imgur.com/V0IxO5Tl.png "SingularityNET Daemon")

<img src="https://i.imgur.com/V0IxO5Tl.png" width="400">

The daemon is the adapter that a service can use to interface with the SingularityNET platform.
In software architecture lingo, the daemon is a [sidecar proxy](https://docs.microsoft.com/en-us/azure/architecture/patterns/sidecar), —a process deployed next to a core application (the AI service, in this case) to abstract away some architectural concerns such
as logging and configuration as well as entire platform aspects, such as the interaction with smart
contracts or even the decision to use the Ethereum blockchain.
The two key abstraction responsibilities of the daemon are payments and request translation.
In order to authorize payments, the daemon interacts with the Multi-Party Escrow contract.
Before invoking a service through SingularityNET, a consumer must have
1. funded the Multi-Party Escrow contract (see section on payments below) and
2. opened a payment channel with the recipient as specified by the service definition
With each invocation the daemon checks that
1. the signature is authentic,
2. the payment channel has sufficient funds, and
3. the payment channel expiry is beyond a specified threshold (to ensure that the developer
can claim the accrued funds).

After these successful checks, the request is proxied to the service. The daemon also keeps track
of payment states of different clients.

<img src="https://i.imgur.com/V0IxO5T.png" width="400">

Once the daemon has validated requests, it translates them into the format expected by the AI
service. The daemon exposes a [gRPC](https://grpc.io/), so all requests are based on gRPC and [protocol buffers](https://developers.google.com/protocol-buffers/), but it can translate requests to a few different formats, as expected by the service: in addition to
gRPC/Protobuf, JSON-RPC and process fork–based services (executables to be executed on a
per-call basis with the input parameters on standard input) are supported. This translation enables
one consistent protocol to be used to communicate with any service on SingularityNET. The
daemon and CLI also use gRPC and Protobuf for communication.
One can deploy multiple instances of an AI service. Each instance will have its own sidecar
daemon, and all daemons will be registered as endpoints in the Registry. When multiple
instances exist, they can be put into one or more instance groups (a typical reason for doing so
would be to group instances in the same data center or cloud region). Daemons in the same group
coordinate to share payment status information through [etcd](https://coreos.com/etcd/).
The daemon provides some additional deployment- and administration-oriented features:
* SSL termination. This can be done either with a certificate and keyfile supplied by the service developer or with automatic certificates provided by [Let’s Encrypt](https://letsencrypt.org).
* Logging to files, with log rotation and pluggable log hooks. Currently an email hook is
provided, and an easy-to-use API is available for other hooks.
* Metrics, monitoring, and alerts. The daemon collects metrics about request calls, which service owners can use to optimize their resource usage. It also monitors daemon and service events, providing configurable alerts via email or web services.
* Rate limiting to prevent DoS attacks and to allow service owners to scale at their own
speed and ability. The daemon uses the [token bucket](https://en.wikipedia.org/wiki/Token_bucket) algorithm.
* Heartbeat. A pull-based heartbeat service is provided, following the [gRPC health
checking protocol](https://github.com/grpc/grpc/blob/master/doc/health-checking.md). The daemon will check that the heartbeat of the service is configured; this is used by monitoring services as well as the Marketplace DApp.
