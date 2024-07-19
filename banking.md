idempotency
blue-green deployment
feature flag
security
do not crash
high availability is critical (own data center?)
multi tenant
disaster recovery
atomic transactions
a LOT of logs
auditing table
metrics
reliability
antifraud
double entry

        credit book account
       /
entry -
       \
        debit book account

balance: the sum of all credits and debits for one book-account
a customer's balance sheet is a cumulative funcion of their entire history

double entry: the rulebook
we have to relate business events like a new purchase, a new payment, to a series of entries that maps to our domain model
all credit implies in a debit
all debit implies in a credit
challenges of double entry:
  - ordering matters (movements are not commulative)
  - late arriving events (e.g. payment was made 3 days ago)
  - fixing invariants
    - create a combinatory of events or data loss to with a random initial state to test all possibilities
  - write throughput
generative test or property based test

write throughput - sacaling bottlenecks
- database limits required throttling writes
- batch job latency impacting customer experience
solutions
- need to partition the workload
- customer data spread across services
- safe to partition the user base
- interactions between customers are minimal, so you can have the things above and deal with things concurrently

option #1: partition service databases
- write into a single database, if reaches certain limite we crate another shard
- every query and request will need to route to the correct database

problems
- complexity in code (specially with microsservices)
- does not address non-db bottlenecks
- risks intermingling data infrastructure code with business logic

option #2: scalability units
- each service group has your own shard. Like **multi tenants**

problems
- we still need to route to the right shard when certain events happens
  - ex.: global section that is not sharded and mantain mappings to externaly known notifiers to customer's respectively shard (with an id, for example)
  - you have to create this mapping on the very beggining, when the customer loggs in
  - using hiperlinks that will point to the right service

falt tolerance patterns
- deadletters
  - producer
  - consumer
  - motician
  - topic
  - deadletter-topic
  * this is very good because data loss is unacceptable

- circuit breakers
  - messaging
  - consuming messages
  - outbound faild and a circuit breaker trips
  - stop consuming messages

ETL + Analytical Environment
- Hello erlang
- have assertions of facts
  - when you have something that use to be a fact (like limit change), you have to log this
- translate a risk analysis in a credit limit
- we need to think about these data, contribution margins, interchange, personal, customer non interest expenses because of regulators
- machine learning models

that are a lot of interactions between bounded contexts, we need to decouple them

we need idempotency keys to make sure that a thing will happen more than one time, nubank uses procedures of datomic for it, acid transactions for that, correlation_id

when to use dynamodb?
database practices for financial applications
a data have to be linked with its owner, correlation_id

data backup strategies
risk manegement
crisis management
circuit breaker

Maybe the KYC should be done inside the fintech. We have to study about the baas KYC to decide wether they politics matches our policies: “Aside from the regulatory considerations, there's the brand management and the customer journey”.

Outsourcing compliance only makes sense in the short term.

## Leaving baas

Key issues are improving compliance management, gaining autonomy, developing innovative products, adding customer value, and better managing their margins.

You should leave a BaaS when your product core is accounts and payments. Or when you have something between 500k~1kk payments per year.

## Fraud prevention

https://www.unit21.ai/blog/neobank-fraud

Heightened fraud attacks are the new normal with data breaches and identity theft on the rise.

Bad actors love digital banks because is fast and anonymous.

Digital banks with high rates of fraud and failures saw losses to their revenue, reputation and customer base.

The priority is to balancing growth with security measures.

Data-driven decisions are now a crucial part of fraud mitigation as a way to detect fraud and reduce false-positive rates.

Customized, personalized user experiences can help neobanks track fraud using the customer’s profile and transaction history.

### Fraud prevention will only work if you know what to look for.

| Type of fraud   | What it is    |
|--------------- | --------------- |
| Identity Theft | A form of fraud that occurs when criminals use stolen information to access banking services. Virtual onboarding makes neobanks a more appealing target of fraud, as users don’t have to open accounts in person.   |
| New Account Fraud or Account Opening Fraud  | Occurs when a fraudster successfully opens a bank account with the intention of committing fraud and/or taking advantage of the FI (eg. abusing a signup bonus promotion). Neobanks are susceptible to this since accounts can be opened from any device, rather than in person. |
| Account Takeover (ATO) fraud | A form of identity theft where stolen information is used to gain access to an existing bank account. Neobanks are easy targets of account takeover fraud due to the perceived anonymity of using their platforms. |
| Social Engineering or Authorized Push Payment (APP) scam | The act of using aggressive and deceptive actions to make someone “willingly” hand their money or financial information to a criminal. This is another instance where neobanks are targeted due to the anonymity of using these digital services.  |
| Phishing Scams | 	A form of social engineering where a fraudster pretends to be a reputable company or person to trick victims into revealing financial information. This information can then be used to access the victim’s neobanking account (ATO fraud) or open a new account with their information (new account fraud). |
| Chargeback Fraud | Occurs when a bad actor makes an illicit attempt to dispute a transaction and receive a refund. As digital credit providers, neobanks are likely to face these transaction risks. |
| Fraud Rings | An organized circle of criminals that work together to defraud people and FIs. Fraud rings might use neobanks to access and transfer funds while remaining undetected. |
| Romance Fraud | A form of first-party fraud where a fraudster tricks an individual into sending them money by convincing them that they’ve formed a genuine relationship. Neobanks might notice uncharacteristic withdrawals or transfers from the victim when this type of fraud is happening. |
| Funds Transfer Fraud (FTF) or Wire Transfer Fraud | Occurs when bad actors use malicious means (such as an emulator or social engineering) to transfer illicit funds undetected. The perceived anonymity and convenience attached to neobanks makes them an ideal target for these types of illicit transactions. |
| Loan application fraud | The act of applying for a financial loan using stolen or synthetic information. Fraudsters will apply for a loan with a neobank, in hopes of increasing their chances of approval, then disappear before paying it back. |

https://www.unit21.ai/blog/first-party-fraud-what-it-is-and-how-to-prevent-it
https://www.unit21.ai/fraud-aml-dictionary/account-takeover-fraud

### Why digital banks struggle with fraud prevention?

1. Increase in opportunities for online fraud
2. Difficulty managing regulatory requirements
    - While compliance measures might seem tedious, these regulations were implemented as guidelines to improve security.
3. Cost cuts hurt risk and compliance teams
4. Desire to speed up customer onboarding
5. Loss of monetary resources due to fraud

https://www.unit21.ai/videos/how-to-perform-frictionless-fraud-prevention-at-onboarding
https://www.unit21.ai/products/case-management

### Fraud prevention best practices

Know what to avoid doing: https://www.unit21.ai/blog/worst-anti-fraud-practices

https://www.unit21.ai/blog/fraud-detection-prevention-for-financial-organizations

invest in compliance early on
reduce the overarching cost of fraud
https://www.unit21.ai/solutions/fraud-detection
https://www.unit21.ai/blog/reduce-fraud-false-positives

strenghten your KYC process
establish workflows that utilize advanced identity verification methods
commit to meeting regulatory requirements

## Real cases

- Fake paypal signups for bonuses
    - Solution: check for ip address and geolocation.
- Zelle for Social Engineering
    - Solution: Track the money being sent from new devices compared to the typical devices. 
- Romance fraud
    - Solution: look for entities with a spike of incoming transactions compared to the amount we expect them to get in a one-month period to identify criminals

https://www.unit21.ai/products/onboarding-orchestration
https://www.unit21.ai/videos/future-fraud-trends
https://www.unit21.ai/videos/emerging-areas-of-fraud
https://sofieblakstad.medium.com/lets-build-a-bank-service-architecture-410dca881291

infrastructure breaches must be inaceptable. Everything needs a certificate.

how to help your user to deal with security:

- Implement two factor or multi-factor authentication features
- end-to-end encryptation sensitive data
- test your code, your security and always audit everything
 


https://github.com/plausible/analytics/blob/master/lib/plausible/auth/email_activation_code.ex

