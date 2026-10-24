# Dependency Inversion Principle (DIP)

## Interview Definition

The Dependency Inversion Principle states that high-level modules
should not depend on low-level modules. Both should depend on
abstractions.

Abstractions should not depend on details. Details should depend
on abstractions.

## Simple Explanation

Business logic should not be tightly tied to a specific technical
implementation, such as PostgreSQL or DynamoDB.

## Example in Go

\```go
type OrderRepository interface {
    SaveOrder(order string) error
}

type OrderService struct {
    repo OrderRepository
}

func NewOrderService(repo OrderRepository) *OrderService {
    return &OrderService{
        repo: repo,
    }
}

func (s *OrderService) CreateOrder(order string) error {
    return s.repo.SaveOrder(order)
}
\```

OrderService depends on the OrderRepository interface instead
of a concrete PostgreSQL repository.

Any compatible repository can be provided:

\```go
service := NewOrderService(&PostgresRepository{})
\```

A DynamoDB repository could also be provided if it implements
the required SaveOrder method with the matching signature.

Go uses implicit interface implementation, so no explicit
implements declaration or inheritance is required.

## DIP vs Dependency Injection

- DIP is a design principle: depend on abstractions.
- Dependency Injection (DI) is a technique: provide dependencies
  from outside a component.

A constructor that accepts an interface is one common way to
inject a dependency.

## Benefits

- Reduces coupling to concrete implementations.
- Makes testing with alternative implementations easier.
- Allows implementation details to change with less impact on
  business logic.

## Interview Takeaway

Does the business logic depend on a concrete technology or on
the capability it needs?