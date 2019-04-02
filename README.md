![alt text](https://i.imgur.com/V0IxO5Tl.png "SingularityNET Daemon")

<img src="https://i.imgur.com/V0IxO5T.png" width="400">

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

<img src="/img/daemon_diagram.png" width="400">

With this improvement, payment channels inside MPE have the following favorable
properties:
* The channel between sender and recipient can persist indefinitely. The sender can extend
the expiration time and add funds to the channel. The recipient can claim the amount
signed over to him at any time.
* The system is comfortably functional even when the Ethereum network is overloaded
with confirmation time of several hours or even more, for the following reasons:
  * Neither the sender nor recipient needs any confirmation from the blockchain. Alice can continue to add funds, and Bob can continue to claim them in the channel, with no confirmation from the blockchain. For example, after Bob claims his funds, he can inform Alice that the nonce of the channel has changed, and she can start to send messages with the new nonce. It is easy to demonstrate that this is safe for both the sender and the recipient. There is only one condition: the recipient should make sure that the transaction is mined before the expiry time of the channel.
  * There is no race condition between claiming (from the recipient side) and extending/adding funds (from the sender side). The parties can use these functions at any time, and the final result will not depend on the order in which these transactions are mined.
When a user wants to call a given service, they must open a channel, add funds to it, and set an
expiry date that allows sufficient time for the service to fulfill its function. Each channel is
unique to a combination of client identity (sender), service identity (recipient), and daemon
group identity. This allows daemons in the same group to share payment information via etdc,
reducing the overall number of channels and simplifying life on the client side. Clients can be
end users interacting with the platform via the Marketplace DApp or applications making calls
directly or through the SDK's generated code.
