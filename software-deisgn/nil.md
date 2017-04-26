# Nil

- Nil is unfriendly and error-prone
- In the worst case it forces you to use defensive programming
- Solutions to deal with nil:
  - NullObject
    - Remove conditional logic
    - Encapsulate logic around nothingness
    - Polymorphism, duck typing
    - When nil is always handled the same
    - It helps you to make explicit the implicit meaning of ni
  - exceptions
    - Remove conditional logic
    - Avoid invalid situations
    - Prevent hard-to-debug issues
    - It is useful when nil is unexpected
  - Maybe
    - Forces conditional logic
    - Avoid invalid scenarios
    - nils need individual handling
