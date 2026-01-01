---
description: Testing workflow for unit and integration tests
---

# Testing Workflow

Guidelines for writing and running tests.

## Test Structure

Follow the **AAA Pattern**:

```
Arrange → Act → Assert
```

### Directory Structure

```
tests/
├── unit/           # Fast, isolated tests
├── integration/    # Tests with external dependencies
├── e2e/            # End-to-end browser tests
└── fixtures/       # Test data and mocks
```

## Unit Test Guidelines

### What to Test
- Pure functions with business logic
- State management (stores, reducers)
- Utility functions
- Component rendering (without external deps)

### Best Practices
- One assertion per test (when possible)
- Descriptive test names: `should_return_X_when_Y`
- Use factories for test data
- Mock external dependencies

### Example (Jest)

```javascript
describe('calculateTotal', () => {
  it('should return sum of items when cart has products', () => {
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

## Integration Test Guidelines

### What to Test
- API endpoints
- Database operations
- Third-party service integrations

### Best Practices
- Use test databases
- Clean up after each test
- Test both success and error paths

## Running Tests

// turbo
1. Run all tests:
```bash
npm test
```

// turbo
2. Run with coverage:
```bash
npm run test:coverage
```

// turbo
3. Run specific test file:
```bash
npm test -- --testPathPattern="filename"
```

## Coverage Requirements

- Minimum **80%** line coverage for core modules
- **100%** coverage for utility functions
- Critical paths must have explicit tests
