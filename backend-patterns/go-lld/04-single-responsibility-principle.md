# Lesson 4: Single Responsibility Principle (SRP)

## Definition

A module or struct should have one clear responsibility—one main reason to change. This does not mean it can have only one method.

## Example of mixed responsibilities

A preference service that validates input, executes SQL, and sends email has several unrelated reasons to change:
- Validation rules may change.
- Database access may change.
- Email delivery may change.

## Separate responsibilities

A common backend structure is:

- Handler: HTTP request/response handling.
- Service: business rules and workflow coordination.
- Repository: persistence operations.
- Notifier/client: external communication.

These are useful boundaries, not a requirement to create a separate struct for every tiny operation.

## Example skeleton

```go
type Preference struct {
    UserID int
    Theme  string
}

type PreferenceValidator struct{}

func (v PreferenceValidator) Validate(p Preference) bool {
    return p.Theme == "light" || p.Theme == "dark"
}

type PreferenceRepository interface {
    Save(p Preference) error
}

type Notifier interface {
    Notify(p Preference) error
}

type PreferenceService struct {
    validator PreferenceValidator
    repo      PreferenceRepository
    notifier  Notifier
}

func (s PreferenceService) Update(p Preference) error {
    if !s.validator.Validate(p) {
        return fmt.Errorf("invalid theme")
    }

    if err := s.repo.Save(p); err != nil {
        return err
    }

    return s.notifier.Notify(p)
}
```

This snippet assumes `fmt` is imported and concrete implementations are supplied during setup.

## Why this helps

Database and notification implementations can change independently of the business workflow. Dependencies can also be replaced with fakes in unit tests.

## Practice question

A `UserService` validates input, runs SQL queries directly, and sends emails. What would you separate to give each component a clearer responsibility?
