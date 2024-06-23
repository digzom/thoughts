# Implementing Zero Trust Architecture

What this really means? Basically: if the attacker is already in your network, how can you limit the damage they can do?

## We all know about this

- WAF
- Policies
- Credential validation (authentication)
- Check if it is allowed to call that method (authorization)
- If it is ok, forward to the app

## We need to do similar checks for service-to-service communication

- Any service have to be certified (SPIFFE)
    - This extends to frontend - backend - database relation

## Always assume that the attacker is in the network

- Trust isn't based on network perimeter, or simple headers
- least priviledge
- context-based (something that would be strange, like changing location rapdly)
- git identities for **devices** and users
- In the case of a bank, you should know, at least in the beginning, that your customer will be in a certain geolocation. You should validate the device identity.
    - How to validate a device?

## Identity based segmentation

Zero Trust Segmentation.

- Tamper-proof, cryptographically verifiable identities
- Identities based on service, user and device
- NOT on network parameters suck as IP Adrees, subnets or headers of http requests

## Basic Identity Based Segmentation implementation at runtime

1. Enctryption in transit
2. Service identity & Authentication
3. Service-to-service authorization and logs
4. End User identity & Authentication
5. End user-to-resource authorization

Doing this, you have ZTA for your runtime system.

Now, we can answer the question "what happens when the attacker is in the network?". They would have to steal a lot of credentials. Request credentials, user and device credentials.

You need telemetry.

## What's a service mesh?

A ngnix besides each service. Force all network traffic into and out of the application to that proxy.

- Per-request polity and controls
- Encryption in transit
- Load balancy, service discovery
- Operational telemetry

### Mesh Capabilities

- Service discovery
- Resiliency
    - Retry, outlier detection, **circuit beaking**, timeouts, etc (what is etc?)
- Load balance
    - Cliente sid3e
- Fine-grained traffic control
    - L7, not L4. Route by headers, destination or source.
- Policy on requests
    - Authentication, rate limiting, arbitraty policy based on L7 metadata
- Workload identity (L7)
- Service-to-service authorization
- Metrics, logs, and tracing

All of these are about consistency across the apps, centralized control and ease of change.

Istio and Envoy.

## Key ideas

We talk about proxies and stuff but your authentication can be handle by a authentication provider or SSO. (how to create a secure authentication provider for my application?)

The mesh can become a Security Kernel for a distributed system.

Multitenancy mentioned. With Envoy as PEP we can move security concerns out of the application and into the mesh. NIST SP 800-204B.

## Service Mesh enables cross-curring change

- centralized control (policies)
    - Yes, it is more complex, more hard.

## Realizing Identity Based Segmentation with a Service Mesh

1. Encryption in transit
    - mTLS
2. Service Identity & Authentication
    - SPIFFE identities for workloads in the mesh
3. Service-to-Service Authorization
    - Built-in policies good starting point, mature implementations should leverage dedicated authz infra for richer policy and decisions - e.g. next generation acces control (NGAC)
4. End User identity & Authentication
    - Defer to trusted identity provider or IDaaS
5. End user-to-resource authorization
    - Integrate with existing system via OIDC or leverage dedicated authz infra - e.g. NGAC


Multi-tier policies. Network oriented policies have to exist, yet.
