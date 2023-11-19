gRPC relies on HTTP2.

Comunication with protocol buffers.

We can do something called *server streaming*: You send one request, but you receive a lot of responses (that can be large and divided in pieces, justifying the many responses).

With *client streaming* we can make a stream of requests.

With bidirectional streaming we have both.

You can cancel requests.

## What is protocol buffers?

Protocol buffers are a Google's language-neutral, pratform-neutral, extensible mechanism for serialize structured data - think in XML, but smaller, faster and simpler.

It uses a less bandwith. The payload is smaller.

Uses binary data.
