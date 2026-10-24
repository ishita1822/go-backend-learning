# Dependency Injection (DI)

## The problem: tightly coupled code

```go
type EmailSender struct{}

func (e EmailSender) Send(message string) {
    fmt.Println("Email:", message)
}

func Notify(message string) {
    sender := EmailSender{} // dependency created inside the function
    sender.Send(message)
}
```

`Notify` always creates an email sender itself, making it harder to replace the sender or test different implementations.

## Inject the dependency

```go
type NotificationSender interface {
    Send(message string)
}

type NotificationService struct {
    sender NotificationSender
}

func (n NotificationService) Notify(message string) {
    n.sender.Send(message)
}
```

The caller supplies the sender:

```go
service := NotificationService{sender: EmailSender{}}
service.Notify("Hello!")
```

## Definition

Dependency Injection means supplying a component's dependencies from outside rather than having the component construct them internally.

An interface and DI are related but different:
- Interface: describes required behaviour.
- DI: supplies the dependency from outside.
- DI can use interfaces or concrete types.
