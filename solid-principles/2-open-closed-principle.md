# Open/Closed Principle (OCP)

## Interview Definition

Software entities should be open for extension but closed for modification.

## Simple Explanation

We should be able to add new behavior without repeatedly changing stable, existing code.

## Example in Go

Imagine a checkout system supports different discount policies.

```go
type DiscountPolicy interface {
    Calculate(price float64) float64
}

type RegularDiscount struct{}

func (RegularDiscount) Calculate(price float64) float64 {
    return price * 0.05
}

type PremiumDiscount struct{}

func (PremiumDiscount) Calculate(price float64) float64 {
    return price * 0.15
}

func FinalPrice(price float64, policy DiscountPolicy) float64 {
    return price - policy.Calculate(price)
}
```

A new discount policy can be added by implementing
DiscountPolicy without changing FinalPrice.

## Benefits

- Makes it easier to introduce new behavior.
- Reduces repeated changes to stable logic.
- Helps keep code modular and testable.

## Interview Takeaway

Can I add a new variation by creating another implementation
instead of repeatedly modifying existing business logic?