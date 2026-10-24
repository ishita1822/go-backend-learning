# Lesson 3: Constructor Functions in Go

Go commonly uses `New...` functions to initialise structs and provide dependencies. They are ordinary functions, not special language constructors.

```go
type PaymentGateway interface {
    Pay(amount int)
}

type PaymentService struct {
    gateway PaymentGateway
}

func NewPaymentService(gateway PaymentGateway) *PaymentService {
    return &PaymentService{
        gateway: gateway,
    }
}

func (p PaymentService) Pay(amount int) {
    p.gateway.Pay(amount)
}
```

Any concrete type implementing `PaymentGateway` can be supplied to `NewPaymentService`.

## Why use a constructor?

- Makes required dependencies explicit.
- Centralises initialisation.
- Can validate configuration or return an error if setup fails.
- Helps prevent callers from accidentally forgetting required setup.

## Key distinction

A constructor function is one way to perform Dependency Injection. DI is the broader principle; a `New...` function is one implementation technique.
