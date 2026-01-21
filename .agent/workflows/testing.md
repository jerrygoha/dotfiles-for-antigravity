---
description: Testing workflow for unit and integration tests
---

# Testing Workflow

Comprehensive testing strategy including advanced techniques.

---

## Test Structure

**AAA Pattern**: `Arrange → Act → Assert`

```
tests/
├── unit/           # Fast, isolated (<100ms each)
├── integration/    # External dependencies
├── e2e/            # Full user flows
└── fixtures/       # Test data and mocks
```

---

## Unit Testing

### What to Test
- Pure functions with business logic
- State management (stores, reducers)
- Utilities and helpers
- Component rendering (isolated)

### Best Practices
- **One assertion per test** (when practical)
- **Descriptive names**: `should_return_X_when_Y`
- **Test factories** for consistent test data
- **Mock boundaries**, not internals

### Example

```javascript
describe('calculateTotal', () => {
  it('should sum items when cart has products', () => {
    // Arrange
    const cart = [
      { price: 100, quantity: 2 },
      { price: 50, quantity: 1 }
    ];
    
    // Act
    const result = calculateTotal(cart);
    
    // Assert
    expect(result).toBe(250);
  });
  
  it('should return 0 when cart is empty', () => {
    expect(calculateTotal([])).toBe(0);
  });
});
```

---

## Edge Case Testing (MANDATORY)

### Boundary Value Analysis

| Input Type | Test Cases |
|------------|-----------|
| Numbers | `0`, `-1`, `MAX_INT`, `NaN`, `Infinity` |
| Strings | `""`, `" "`, very long, unicode, `null` |
| Arrays | `[]`, single item, max size |
| Objects | `{}`, `null`, `undefined`, nested |

```javascript
describe('Edge Cases', () => {
  it.each([
    [[], 0],           // Empty
    [[1], 1],          // Single
    [[-1, -2], -3],    // Negatives
    [[0, 0, 0], 0],    // Zeros
  ])('sum(%p) should be %i', (input, expected) => {
    expect(sum(input)).toBe(expected);
  });
});
```

---

## Property-Based Testing

**Define properties that always hold, not just examples.**

```javascript
import fc from 'fast-check';

describe('Property-based: sort function', () => {
  it('should preserve array length', () => {
    fc.assert(fc.property(
      fc.array(fc.integer()),
      (arr) => sort(arr).length === arr.length
    ));
  });
  
  it('should be idempotent', () => {
    fc.assert(fc.property(
      fc.array(fc.integer()),
      (arr) => {
        const once = sort(arr);
        const twice = sort(once);
        return JSON.stringify(once) === JSON.stringify(twice);
      }
    ));
  });
});
```

---

## Integration Testing

### What to Test
- API endpoints (request/response)
- Database operations (CRUD)
- External service integrations

### Best Practices
- Use test databases
- Clean up after each test (`afterEach`)
- Test both success and error paths
- Mock external APIs, not internal modules

---

## Running Tests

// turbo
```bash
npm test
```

// turbo
```bash
npm run test:coverage
```

// turbo
```bash
npm test -- --testPathPattern="filename"
```

---

## Coverage Requirements

| Module Type | Line Coverage | Branch Coverage |
|-------------|--------------|-----------------|
| Core/Critical | 90%+ | 85%+ |
| Business Logic | 80%+ | 75%+ |
| Utilities | 100% | 100% |
| UI Components | 70%+ | 60%+ |

---

## Related Workflows

- `/tdd` - Test-driven development for new features
- `/test-coverage` - Analyze and improve coverage
- `/e2e` - End-to-end testing
