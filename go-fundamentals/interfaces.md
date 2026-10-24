# Interfaces in Go

## Core idea

An interface describes behaviour a type must provide. Go uses implicit interface implementation: a type satisfies an interface by implementing its required methods; it does not need an `implements` declaration.

```go
type NotificationSender interface {
    Send(message string)
}

type EmailSender struct{}

func (e EmailSender) Send(message string) {
    fmt.Println("Sending email:", message)
}

type SMSSender struct{}

func (s SMSSender) Send(message string) {
    fmt.Println("Sending SMS:", message)
}

func Notify(sender NotificationSender, message string) {
    sender.Send(message)
}
```

`Notify` accepts any value whose type implements `Send(message string)`. It can work with both `EmailSender` and `SMSSender`.

## Why it matters

The caller depends on behaviour, not a particular concrete type. This makes implementations easier to swap and test.

## Remember

- An interface defines a contract of behaviour.
- Go implements interfaces implicitly.
- Keep interfaces focused on the behaviour the consumer needs.
