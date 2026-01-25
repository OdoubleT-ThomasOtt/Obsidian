# YagniConventions

## Purpose & Scope
YAGNI (You Aren't Gonna Need It) is a fundamental principle that prevents over-engineering and speculative development. This convention ensures that only currently required functionality is implemented, maintaining simplicity and reducing technical debt across the entire development lifecycle.

---

## Core Principles

### YAGNI Core
- Implement only what's explicitly required RIGHT NOW
- No features "for later"
- No "what if" scenarios
- Delete speculative code immediately
- Today's requirements only

### YAGNI Decisions
- Will this be used today? No = Don't build it
- Is this a current requirement? No = Skip it
- Nice to have = Not needed
- "Maybe useful" = Definitely not

### YAGNI Mindset
- Assume requirements won't expand
- Trust that refactoring is cheap
- Adding code later is fine
- Maintaining unused code is expensive
- The future is unpredictable - don't guess

---

## Implementation Guidelines

### Decision Framework
1. **Is it in the User Story?** - If not, don't implement
2. **Is it required for the current sprint?** - If not, defer
3. **Will it be used within 2 weeks?** - If not, skip
4. **Is it speculative?** - If yes, delete

### Code Review Criteria
- No unused methods or classes
- No "future-proofing" abstractions
- No complex patterns for simple problems
- No premature optimization
- No gold-plating features

### Architecture Guidelines
- Start with the simplest solution
- Add complexity only when proven necessary
- Resist the urge to "make it flexible"
- Hardcoding is acceptable initially
- Generalize only after 3+ uses

---

## Standards & Specifications

### Red Flag Phrases
- "We might need this when..."
- "It would be easy to add..."
- "While I'm here, I'll just..."
- "This will save time later..."
- "What if the client wants..."
- "Let's make it configurable..."
- "We should prepare for..."
- "It's better to have it and not need it..."

### Acceptable Exceptions
- Security requirements (always implement)
- Accessibility standards (always follow)
- Data validation (always include)
- Error handling (always necessary)
- Logging for debugging (within reason)

---

## Best Practices

### Development Approach
- Write the minimum code that works
- Solve today's problem, not tomorrow's
- Implement features Just-In-Time
- Prefer concrete over abstract
- Choose simple over clever

### Refactoring Strategy
- Refactor when needed, not preemptively
- Extract abstractions after patterns emerge
- Generalize after multiple implementations
- Clean up as you go, not in advance

### Testing Focus
- Test what exists, not what might exist
- No tests for unused code
- Remove tests when removing features
- Keep test coverage focused on used paths

---

## Quality Assurance

### YAGNI Checklist
- [ ] Every line of code has a current purpose
- [ ] No unused variables, methods, or classes
- [ ] No speculative features implemented
- [ ] No over-engineered solutions
- [ ] No premature abstractions
- [ ] No future-proofing without requirements
- [ ] All code directly supports current User Stories

### Validation Questions
- Can I trace this code to a requirement?
- Will this be used in the next release?
- Is there a simpler solution?
- Am I solving an actual problem?
- Is this complexity justified today?

---

## Examples

### Bad Example (Violates YAGNI)
```csharp
// Over-engineered for potential future needs
public interface IDataProcessor<T> where T : class
{
    Task<T> ProcessAsync(T data, ProcessingOptions options);
}

public class ProcessingOptions
{
    public bool EnableCaching { get; set; }  // Not required
    public int RetryCount { get; set; }      // Not required
    public string Format { get; set; }       // Not required
}

// Only needed: simple order processing
public class OrderProcessor : IDataProcessor<Order> { }
public class CustomerProcessor : IDataProcessor<Customer> { } // Not needed yet
public class ProductProcessor : IDataProcessor<Product> { }   // Not needed yet
```

### Good Example (Follows YAGNI)
```csharp
// Simple, direct solution for current need
public class OrderService
{
    public async Task<Order> ProcessOrderAsync(Order order)
    {
        // Direct implementation for current requirement
        ValidateOrder(order);
        await SaveOrderAsync(order);
        return order;
    }
}
```

### Refactoring Example
```csharp
// Step 1: Initial implementation (hardcoded, simple)
public decimal CalculateDiscount(decimal amount)
{
    return amount * 0.1m; // 10% discount
}

// Step 2: After second use case emerges
public decimal CalculateDiscount(decimal amount, CustomerType type)
{
    return type == CustomerType.Premium ? amount * 0.2m : amount * 0.1m;
}

// Step 3: Only after third use case and clear pattern
public decimal CalculateDiscount(decimal amount, IDiscountStrategy strategy)
{
    return strategy.Calculate(amount);
}
```

---

## Notes & Exceptions

### When YAGNI Doesn't Apply
- Security measures (implement comprehensively)
- Data integrity constraints (always enforce)
- Regulatory compliance (implement fully)
- Performance critical paths (optimize when proven necessary)
- Public APIs (design carefully upfront)

### Balance with Other Principles
- YAGNI complements DRY (Don't Repeat Yourself)
- Works with KISS (Keep It Simple, Stupid)
- Supports Agile incremental development
- Enables faster time-to-market
- Reduces maintenance burden

---

End of YagniConventions