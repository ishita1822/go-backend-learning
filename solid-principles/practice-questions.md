# SOLID Practice Questions

Try answering each question yourself before checking your notes.

## 1. Single Responsibility Principle (SRP)

A service validates user input, executes SQL queries, and sends
emails. What responsibilities could be separated?

## 2. Open/Closed Principle (OCP)

A checkout function has an expanding switch statement for each
discount type. How could an interface improve the design?

## 3. Liskov Substitution Principle (LSP)

An implementation satisfies an interface but returns success
without actually completing the promised operation. Does it
honor LSP? Explain your answer.

## 4. Interface Segregation Principle (ISP)

A component only needs GetUser(), but its dependency also requires
CreateUser() and DeleteUser(). How could the interface design
be improved?

## 5. Dependency Inversion Principle (DIP)

An OrderService creates a PostgreSQL repository internally.
What changes would allow it to use another repository without
modifying the service?

---

# Quick Revision

- SRP: One primary responsibility and one main reason to change.
- OCP: Open for extension, closed for modification.
- LSP: Preserve expected behavior when substituting implementations.
- ISP: Do not force clients to depend on unused methods.
- DIP: High-level and low-level modules depend on abstractions.