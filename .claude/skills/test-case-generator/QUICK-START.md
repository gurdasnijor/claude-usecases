# Test Case Generator - Quick Start

## Request Tests

```
Generate tests for:
[paste code]

Framework: [pytest/jest/vitest]
```

---

## Test Coverage Checklist

For each function, test:
- [ ] Happy path (normal inputs)
- [ ] Edge cases (empty, zero, boundary)
- [ ] Error cases (invalid, missing)
- [ ] State changes (if applicable)

---

## AAA Pattern

```python
def test_example():
    # Arrange - Setup
    data = {"input": "value"}

    # Act - Execute
    result = function_under_test(data)

    # Assert - Verify
    assert result == expected
```

---

## Naming Convention

```
test_[what]_[scenario]_[expected]

test_calculate_total_with_discount_returns_reduced_price
test_validate_email_with_invalid_format_raises_error
test_get_user_when_not_found_returns_none
```

---

## Common Test Patterns

**Value Test:**
```python
def test_returns_correct_value():
    result = add(2, 3)
    assert result == 5
```

**Exception Test:**
```python
def test_raises_on_invalid():
    with pytest.raises(ValueError):
        validate(-1)
```

**Mock Test:**
```python
def test_calls_api(mocker):
    mock = mocker.patch("module.api_call")
    function_that_calls_api()
    mock.assert_called_once()
```

**Fixture Test:**
```python
@pytest.fixture
def user():
    return User(name="Test")

def test_user_name(user):
    assert user.name == "Test"
```

---

## Coverage Targets

| Type | Target |
|------|--------|
| Business logic | 90% |
| API/handlers | 80% |
| Utilities | 80% |
| UI components | 70% |

---

## Quick Fixes

| Issue | Solution |
|-------|----------|
| Flaky tests | Mock time/external calls |
| Slow tests | Add mocks, reduce scope |
| Low coverage | Add error case tests |
| Shared state | Use fixtures, isolate tests |
