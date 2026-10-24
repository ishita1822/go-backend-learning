# Interface Segregation Principle (ISP)

## Interview Definition

The Interface Segregation Principle states that clients should
not be forced to depend on interfaces they do not use.

## Simple Explanation

Do not force a component to depend on methods it does not need.

## Example in Go

Consider a repository with several operations:

\```go
type User struct {
    ID   string
    Name string
}

type UserRepository interface {
    GetUser(id string) (User, error)
    CreateUser(user User) error
    DeleteUser(id string) error
}
\```

A profile service may only need to retrieve users, while a
cleanup job only needs to delete users.

We can define smaller interfaces based on those capabilities:

\```go
type UserReader interface {
    GetUser(id string) (User, error)
}

type UserDeleter interface {
    DeleteUser(id string) error
}
\```

Now the profile service can depend on UserReader, while the
cleanup job can depend on UserDeleter.

A concrete repository can implement both interfaces.

## Benefits

- Reduces unnecessary dependencies.
- Makes testing easier.
- Keeps interfaces focused on consumer needs.

## Important Nuance

Do not split every interface automatically. Split an interface
when doing so meaningfully reduces unnecessary dependencies or
makes the code easier to maintain.

## Interview Takeaway

Is this component forced to depend on methods it never uses?