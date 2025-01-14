# Antifraud Service

1. Clone the `.env.example` file and rename to `.env`. Then change the variable values if neccessary.
2. Exec `npm run install` for install dependencies.
3. Exec `npm run dev` for development.
4. Exec `npm run build` and then `npm run start` for production.
5. Exec `npm run lint` to apply linter.

# Services

## Validate transaction

```mermaid
sequenceDiagram
    Kafka->>+[Infraestructure] ValidateTransaction: {consumerMessage, producer}
    [Infraestructure] ValidateTransaction->>+[Domain] TransactionValidator: validate(amount)
    [Domain] TransactionValidator->>-[Infraestructure] ValidateTransaction: status
    [Infraestructure] ValidateTransaction->>+[Infraestructure] ValidationResource: new({ transactionId, amount, status })
    [Infraestructure] ValidationResource->>-[Infraestructure] ValidateTransaction: resource
    [Infraestructure] ValidateTransaction->>-kafka: send(resource)
```
