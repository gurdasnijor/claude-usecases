# Test Case Generator

> Automated test generation for comprehensive code coverage

## Overview

The Test Case Generator creates well-structured test cases from source code, requirements, or specifications. It supports multiple testing frameworks and follows best practices for maintainable, reliable tests.

## When to Use

- **Adding tests to existing code** - Generate comprehensive test suites
- **TDD/BDD development** - Create test cases from specifications
- **Improving coverage** - Identify and fill testing gaps
- **Learning testing patterns** - See best practices in action

## Supported Frameworks

| Language | Frameworks |
|----------|------------|
| **Python** | pytest (primary), unittest |
| **JavaScript/TypeScript** | Jest, Vitest, Testing Library |
| **Go** | testing, testify |
| **Java** | JUnit |
| **Ruby** | RSpec |

## Quick Example

**Input:**
```python
def calculate_discount(price: float, discount_percent: float) -> float:
    if price < 0:
        raise ValueError("Price cannot be negative")
    return price * (1 - discount_percent / 100)
```

**Generated Tests:**
```python
class TestCalculateDiscount:
    def test_applies_discount_correctly(self):
        assert calculate_discount(100.0, 20) == 80.0

    def test_zero_discount_returns_original(self):
        assert calculate_discount(100.0, 0) == 100.0

    def test_negative_price_raises_error(self):
        with pytest.raises(ValueError):
            calculate_discount(-10.0, 10)
```

## Test Types Generated

| Type | Purpose | Coverage |
|------|---------|----------|
| **Happy Path** | Normal inputs → expected outputs | Core functionality |
| **Edge Cases** | Boundary values, empty inputs | Robustness |
| **Error Cases** | Invalid inputs, exceptions | Error handling |
| **State Tests** | Before/after state changes | Side effects |

## Coverage Targets

| Code Type | Target |
|-----------|--------|
| Business logic | 90%+ |
| API handlers | 80%+ |
| Utilities | 80%+ |
| UI components | 70%+ |

## Test Quality Standards

All generated tests follow:
- **AAA Pattern** - Arrange, Act, Assert
- **Descriptive names** - `test_[unit]_[scenario]_[expected]`
- **Single responsibility** - One assertion focus per test
- **Independence** - No shared mutable state
- **Fast execution** - Mocked external dependencies

## Usage

```
Generate tests for this code:
[paste your code]

Framework: pytest
Coverage goal: 80%
```

Or specify test types:
```
Generate error handling tests for this API endpoint:
[paste endpoint code]
```

## Related Skills

- **code-review-assistant** - Review test quality
- **technical-writer** - Document testing standards

## Version

- **Current:** v1.0.0
- **Last Updated:** 2025-12-07
- **Author:** 360 Social Impact Studios
