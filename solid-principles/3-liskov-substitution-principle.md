# Liskov Substitution Principle (LSP)

## Interview Definition

The Liskov Substitution Principle states that objects of a
superclass should be replaceable with objects of its subclasses
without altering the correctness of the program.

## Applying LSP in Go

Go does not use class inheritance in the usual Java-style way.
We apply the same behavioral principle to interface implementations.

A type may satisfy an interface's method signatures but still
violate the behavior expected by the interface's consumers.

## Example in Go

\```go
type PaymentMethod interface {
    Pay(amount float64) error
}

type FakePayment struct{}

func (FakePayment) Pay(amount float64) error {
    // Incorrect if nil means payment succeeded.
    // No payment is actually processed.
    return nil
}
\```

The implementation has the required method signature, so Go
accepts it.

However, if the contract says that nil means the payment was
successful, returning nil without processing the payment violates
the expected behavior.

## Interface Compliance vs LSP

- Interface compliance: Does the type implement the required methods?
- LSP: Does the implementation honor the expected behavior?

A method can compile successfully and still violate LSP.

## Important Nuance

Returning an error is not automatically an LSP violation.
Errors may be part of the documented contract.

The key question is whether the implementation fulfills the
behavior that callers reasonably expect.

## Interview Takeaway

Can I replace one implementation with another without breaking
the calling code's expected behavior?