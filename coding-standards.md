# Coding Standards

## Control flow blocks

Always wrap `if`/`else`/`for`/`foreach`/`while`/`try`/`catch` bodies in curly braces, even for a single statement.

Never:
```csharp
if (x) return;
```

Always:
```csharp
if (x)
{
    return;
}
```

Exceptions: expression-bodied members (`=> expr`) and ternary operators (`? :`) are fine as one-liners.
