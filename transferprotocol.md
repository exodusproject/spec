A transfer protocol based on HTTP.
I propose we use a text based protocol (possibly with binary alternative) with each message in two parts.
* First is the header.
  * First line of the header consists of an `action verb`, a `descriptor` of the resource being handled, and a `protocol identifier`.
  * Following lines are headers, where some can be mandatory and some optional.
  * The header is ended by a blank line (I.e. double newline characters).
* The second part is an optional body.
  * The body should contain the (non-meta) data relevant to the used `action verb`.
  * The body can also contain the entire resource in question, is it is relevant to transfer that.

This message format is intentionally compatible with HTTP. This is to ease serving public (I.e. no authentication requirement) resources to be served as hypertext where applicable. Any Exodus node can in that way serve as a lightweight static webserver.

Because Exodus is a peer2peer protocol, and not client-server like HTTP, there is no distinction between request and response messages. If necessary there could be designated `action verb`s for replying to specific `action verb`s, e.g. `get` and `get-response`. Or this could be covered by a `push` action, where a node can then decide if it wants to store the resource being delivered, depending on whether it was requested, or other factors.

Example message
```
PUSH /blogs/why-exodus-is-awesome EXODUS/0.1
Authentication: [authentication method]; [signed proof]

{
... Resource ...
}
```
