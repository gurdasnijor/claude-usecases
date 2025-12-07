---
name: Test Case Generator
description: Automated test case generation specialist that creates comprehensive unit tests, integration tests, and test scenarios from code, requirements, or specifications across multiple testing frameworks
version: 1.0.0
author: 360 Social Impact Studios
created: 2025-12-07
updated: 2025-12-07
status: production
category: software-development
tags: [testing, unit-tests, integration-tests, tdd, bdd, pytest, jest, vitest, test-coverage]
tools: [Read, Write, Edit, Glob, Grep]
integrations: [code-review-assistant, technical-writer]
outputs: [test-files, test-suites, test-scenarios, coverage-recommendations]
complexity: medium
---

# Test Case Generator

## Purpose

Generate comprehensive, well-structured test cases from source code, requirements, or specifications. Create tests that follow testing best practices, achieve high coverage, and are maintainable over time.

---

## Activation Triggers

Use this skill when the user:
- Asks to "write tests" or "generate tests"
- Wants to "add test coverage" to code
- Needs "unit tests" or "integration tests"
- Asks about "testing this function/class/module"
- Wants to improve "test coverage"
- Needs "test scenarios" from requirements
- Asks for "TDD" or "BDD" style tests

---

## Supported Frameworks

### Python
- **pytest** (recommended)
- unittest
- nose2

### JavaScript/TypeScript
- **Jest** (recommended for React)
- **Vitest** (recommended for Vite/modern)
- Mocha + Chai
- Testing Library (React, Vue, etc.)

### Go
- Built-in testing package
- testify

### Other
- JUnit (Java)
- RSpec (Ruby)
- PHPUnit (PHP)
- Rust's built-in testing

---

## Execution Workflow

### Phase 1: Analysis

**Step 1.1: Understand the Code**
```
Gather:
- What code needs tests?
- What language/framework?
- What testing framework to use?
- What's the desired coverage level?
- Are there existing tests to follow?
- Any specific scenarios to cover?
```

**Step 1.2: Identify Testable Units**

| Unit Type | What to Test |
|-----------|--------------|
| **Functions** | Input/output, edge cases, errors |
| **Classes** | Methods, state changes, interactions |
| **APIs** | Endpoints, status codes, payloads |
| **Components** | Rendering, user interactions, props |
| **Modules** | Public interface, integration points |

**Step 1.3: Categorize Test Types**

```
Unit Tests:
- Single function/method in isolation
- Mocked dependencies
- Fast execution

Integration Tests:
- Multiple units working together
- Real or simulated dependencies
- Database/API interactions

E2E Tests:
- Full user workflows
- Real environment
- Browser/UI testing
```

---

### Phase 2: Test Strategy

**Step 2.1: Coverage Strategy**

For each function/method, identify:

```
1. Happy Path
   - Normal inputs → expected outputs
   - Common use cases

2. Edge Cases
   - Empty/null/undefined inputs
   - Boundary values (0, -1, MAX_INT)
   - Empty collections ([], {}, "")

3. Error Cases
   - Invalid inputs
   - Missing required parameters
   - Type mismatches

4. State Transitions (if applicable)
   - Before/after state
   - Side effects
```

**Step 2.2: Test Naming Convention**

```python
# Pattern: test_[unit]_[scenario]_[expected_result]

# Python/pytest
def test_calculate_total_with_discount_returns_reduced_price():
def test_validate_email_with_invalid_format_raises_error():
def test_get_user_when_not_found_returns_none():

# JavaScript/Jest
describe('calculateTotal', () => {
  it('should return reduced price when discount applied', () => {});
  it('should throw error when items is empty', () => {});
});
```

**Step 2.3: AAA Pattern (Arrange-Act-Assert)**

```python
def test_user_creation():
    # Arrange - Set up test data and conditions
    user_data = {"name": "John", "email": "john@example.com"}

    # Act - Execute the code under test
    result = create_user(user_data)

    # Assert - Verify the results
    assert result.id is not None
    assert result.name == "John"
    assert result.email == "john@example.com"
```

---

### Phase 3: Test Generation Patterns

#### Pattern A: Function Tests (Python/pytest)

**Source Code:**
```python
def calculate_discount(price: float, discount_percent: float) -> float:
    """Apply percentage discount to price."""
    if price < 0:
        raise ValueError("Price cannot be negative")
    if not 0 <= discount_percent <= 100:
        raise ValueError("Discount must be between 0 and 100")
    return price * (1 - discount_percent / 100)
```

**Generated Tests:**
```python
import pytest
from module import calculate_discount


class TestCalculateDiscount:
    """Tests for calculate_discount function."""

    # Happy path tests
    def test_applies_zero_discount(self):
        """No discount should return original price."""
        result = calculate_discount(100.0, 0)
        assert result == 100.0

    def test_applies_full_discount(self):
        """100% discount should return zero."""
        result = calculate_discount(100.0, 100)
        assert result == 0.0

    def test_applies_partial_discount(self):
        """50% discount should return half price."""
        result = calculate_discount(100.0, 50)
        assert result == 50.0

    def test_handles_decimal_discount(self):
        """Should handle decimal percentages correctly."""
        result = calculate_discount(100.0, 33.33)
        assert result == pytest.approx(66.67, rel=1e-2)

    # Edge cases
    def test_zero_price_returns_zero(self):
        """Zero price should always return zero."""
        result = calculate_discount(0.0, 50)
        assert result == 0.0

    def test_small_price_values(self):
        """Should handle very small prices."""
        result = calculate_discount(0.01, 10)
        assert result == pytest.approx(0.009, rel=1e-3)

    # Error cases
    def test_negative_price_raises_error(self):
        """Negative price should raise ValueError."""
        with pytest.raises(ValueError, match="Price cannot be negative"):
            calculate_discount(-10.0, 10)

    def test_negative_discount_raises_error(self):
        """Negative discount should raise ValueError."""
        with pytest.raises(ValueError, match="Discount must be between"):
            calculate_discount(100.0, -10)

    def test_discount_over_100_raises_error(self):
        """Discount over 100% should raise ValueError."""
        with pytest.raises(ValueError, match="Discount must be between"):
            calculate_discount(100.0, 150)
```

---

#### Pattern B: Class Tests (Python/pytest)

**Source Code:**
```python
class ShoppingCart:
    def __init__(self):
        self.items = []

    def add_item(self, item: dict) -> None:
        if not item.get("name") or not item.get("price"):
            raise ValueError("Item must have name and price")
        self.items.append(item)

    def get_total(self) -> float:
        return sum(item["price"] * item.get("quantity", 1) for item in self.items)

    def clear(self) -> None:
        self.items = []
```

**Generated Tests:**
```python
import pytest
from module import ShoppingCart


class TestShoppingCart:
    """Tests for ShoppingCart class."""

    @pytest.fixture
    def cart(self):
        """Provide a fresh cart for each test."""
        return ShoppingCart()

    @pytest.fixture
    def sample_item(self):
        """Provide a sample item."""
        return {"name": "Widget", "price": 9.99, "quantity": 1}

    # Initialization tests
    def test_new_cart_is_empty(self, cart):
        """New cart should have no items."""
        assert cart.items == []
        assert cart.get_total() == 0

    # add_item tests
    def test_add_single_item(self, cart, sample_item):
        """Should add item to cart."""
        cart.add_item(sample_item)
        assert len(cart.items) == 1
        assert cart.items[0]["name"] == "Widget"

    def test_add_multiple_items(self, cart):
        """Should accumulate multiple items."""
        cart.add_item({"name": "A", "price": 10})
        cart.add_item({"name": "B", "price": 20})
        assert len(cart.items) == 2

    def test_add_item_without_name_raises_error(self, cart):
        """Item without name should raise ValueError."""
        with pytest.raises(ValueError, match="must have name and price"):
            cart.add_item({"price": 10})

    def test_add_item_without_price_raises_error(self, cart):
        """Item without price should raise ValueError."""
        with pytest.raises(ValueError, match="must have name and price"):
            cart.add_item({"name": "Widget"})

    # get_total tests
    def test_total_single_item(self, cart):
        """Total should reflect single item price."""
        cart.add_item({"name": "A", "price": 25.00})
        assert cart.get_total() == 25.00

    def test_total_multiple_items(self, cart):
        """Total should sum all item prices."""
        cart.add_item({"name": "A", "price": 10})
        cart.add_item({"name": "B", "price": 20})
        cart.add_item({"name": "C", "price": 30})
        assert cart.get_total() == 60

    def test_total_with_quantities(self, cart):
        """Total should account for quantities."""
        cart.add_item({"name": "A", "price": 10, "quantity": 3})
        assert cart.get_total() == 30

    def test_total_defaults_quantity_to_one(self, cart):
        """Missing quantity should default to 1."""
        cart.add_item({"name": "A", "price": 10})
        assert cart.get_total() == 10

    # clear tests
    def test_clear_empties_cart(self, cart, sample_item):
        """Clear should remove all items."""
        cart.add_item(sample_item)
        cart.clear()
        assert cart.items == []
        assert cart.get_total() == 0
```

---

#### Pattern C: Async Function Tests (Python/pytest)

```python
import pytest
from module import fetch_user_data


class TestFetchUserData:
    """Tests for async fetch_user_data function."""

    @pytest.mark.asyncio
    async def test_returns_user_data(self, mocker):
        """Should return user data for valid ID."""
        mock_response = {"id": "123", "name": "John"}
        mocker.patch("module.http_client.get", return_value=mock_response)

        result = await fetch_user_data("123")

        assert result["id"] == "123"
        assert result["name"] == "John"

    @pytest.mark.asyncio
    async def test_raises_on_not_found(self, mocker):
        """Should raise NotFoundError for missing user."""
        mocker.patch("module.http_client.get", side_effect=NotFoundError())

        with pytest.raises(NotFoundError):
            await fetch_user_data("invalid")
```

---

#### Pattern D: React Component Tests (Jest/Testing Library)

**Source Code:**
```tsx
interface ButtonProps {
  label: string;
  onClick: () => void;
  disabled?: boolean;
}

export function Button({ label, onClick, disabled = false }: ButtonProps) {
  return (
    <button onClick={onClick} disabled={disabled} className="btn">
      {label}
    </button>
  );
}
```

**Generated Tests:**
```typescript
import { render, screen, fireEvent } from '@testing-library/react';
import { Button } from './Button';

describe('Button', () => {
  const defaultProps = {
    label: 'Click me',
    onClick: jest.fn(),
  };

  beforeEach(() => {
    jest.clearAllMocks();
  });

  // Rendering tests
  it('renders with label text', () => {
    render(<Button {...defaultProps} />);
    expect(screen.getByRole('button')).toHaveTextContent('Click me');
  });

  it('renders enabled by default', () => {
    render(<Button {...defaultProps} />);
    expect(screen.getByRole('button')).not.toBeDisabled();
  });

  it('renders disabled when prop is true', () => {
    render(<Button {...defaultProps} disabled={true} />);
    expect(screen.getByRole('button')).toBeDisabled();
  });

  // Interaction tests
  it('calls onClick when clicked', () => {
    render(<Button {...defaultProps} />);
    fireEvent.click(screen.getByRole('button'));
    expect(defaultProps.onClick).toHaveBeenCalledTimes(1);
  });

  it('does not call onClick when disabled', () => {
    render(<Button {...defaultProps} disabled={true} />);
    fireEvent.click(screen.getByRole('button'));
    expect(defaultProps.onClick).not.toHaveBeenCalled();
  });

  // Accessibility tests
  it('is accessible by role', () => {
    render(<Button {...defaultProps} />);
    expect(screen.getByRole('button', { name: 'Click me' })).toBeInTheDocument();
  });
});
```

---

#### Pattern E: API Endpoint Tests (Python/pytest)

```python
import pytest
from fastapi.testclient import TestClient
from app import app


@pytest.fixture
def client():
    """Provide test client."""
    return TestClient(app)


class TestUsersEndpoint:
    """Tests for /users endpoints."""

    # GET /users
    def test_list_users_returns_array(self, client):
        """GET /users should return array of users."""
        response = client.get("/users")
        assert response.status_code == 200
        assert isinstance(response.json(), list)

    def test_list_users_with_pagination(self, client):
        """Should support limit and offset parameters."""
        response = client.get("/users?limit=10&offset=0")
        assert response.status_code == 200
        assert len(response.json()) <= 10

    # POST /users
    def test_create_user_success(self, client):
        """POST /users with valid data should create user."""
        payload = {"name": "John", "email": "john@example.com"}
        response = client.post("/users", json=payload)
        assert response.status_code == 201
        assert response.json()["name"] == "John"
        assert "id" in response.json()

    def test_create_user_missing_email_returns_400(self, client):
        """POST /users without email should return 400."""
        payload = {"name": "John"}
        response = client.post("/users", json=payload)
        assert response.status_code == 400

    def test_create_user_duplicate_email_returns_409(self, client):
        """POST /users with existing email should return 409."""
        payload = {"name": "John", "email": "existing@example.com"}
        response = client.post("/users", json=payload)
        assert response.status_code == 409

    # GET /users/{id}
    def test_get_user_by_id(self, client):
        """GET /users/{id} should return specific user."""
        response = client.get("/users/123")
        assert response.status_code == 200
        assert response.json()["id"] == "123"

    def test_get_user_not_found_returns_404(self, client):
        """GET /users/{id} for missing user should return 404."""
        response = client.get("/users/nonexistent")
        assert response.status_code == 404
```

---

#### Pattern F: Database Tests with Fixtures

```python
import pytest
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker
from models import Base, User
from repository import UserRepository


@pytest.fixture(scope="function")
def db_session():
    """Provide a clean database session for each test."""
    engine = create_engine("sqlite:///:memory:")
    Base.metadata.create_all(engine)
    Session = sessionmaker(bind=engine)
    session = Session()
    yield session
    session.close()


@pytest.fixture
def user_repo(db_session):
    """Provide UserRepository with test session."""
    return UserRepository(db_session)


@pytest.fixture
def sample_user(db_session):
    """Create and return a sample user."""
    user = User(name="Test User", email="test@example.com")
    db_session.add(user)
    db_session.commit()
    return user


class TestUserRepository:
    """Tests for UserRepository."""

    def test_create_user(self, user_repo, db_session):
        """Should create user in database."""
        user = user_repo.create(name="John", email="john@example.com")

        assert user.id is not None
        assert db_session.query(User).count() == 1

    def test_find_by_email(self, user_repo, sample_user):
        """Should find user by email."""
        found = user_repo.find_by_email("test@example.com")

        assert found is not None
        assert found.id == sample_user.id

    def test_find_by_email_returns_none_if_not_found(self, user_repo):
        """Should return None for non-existent email."""
        found = user_repo.find_by_email("nonexistent@example.com")

        assert found is None
```

---

### Phase 4: Mock and Fixture Patterns

**Step 4.1: Common Mock Patterns**

```python
# Mocking external API calls
def test_with_mocked_api(mocker):
    mock_get = mocker.patch("requests.get")
    mock_get.return_value.json.return_value = {"data": "value"}
    mock_get.return_value.status_code = 200

    result = fetch_data()

    assert result["data"] == "value"
    mock_get.assert_called_once()


# Mocking time
def test_with_frozen_time(mocker):
    mocker.patch("module.datetime").now.return_value = datetime(2024, 1, 1)

    result = get_current_date()

    assert result == "2024-01-01"


# Mocking file operations
def test_file_processing(mocker, tmp_path):
    test_file = tmp_path / "test.txt"
    test_file.write_text("test content")

    result = process_file(str(test_file))

    assert result == "processed: test content"
```

**Step 4.2: Fixture Organization**

```python
# conftest.py - Shared fixtures

import pytest

@pytest.fixture(scope="session")
def app_config():
    """Session-scoped config (created once per test session)."""
    return {"api_url": "http://test.api", "timeout": 5}


@pytest.fixture(scope="module")
def database_connection():
    """Module-scoped connection (created once per test module)."""
    conn = create_connection()
    yield conn
    conn.close()


@pytest.fixture(scope="function")
def clean_state(database_connection):
    """Function-scoped cleanup (runs before each test)."""
    database_connection.execute("DELETE FROM test_table")
    yield
    database_connection.execute("DELETE FROM test_table")


@pytest.fixture
def authenticated_user():
    """Provide an authenticated user context."""
    return {"id": "user_123", "role": "admin", "token": "test_token"}
```

---

### Phase 5: Output Format

**Standard Test File Structure:**

```python
"""Tests for [module_name].

This module contains tests for:
- [Feature/Component 1]
- [Feature/Component 2]
"""

import pytest
from module import TargetClass, target_function


# Fixtures
@pytest.fixture
def fixture_name():
    """Description of what this fixture provides."""
    return setup_data()


# Test Classes (grouped by unit under test)
class TestTargetFunction:
    """Tests for target_function."""

    # Happy path
    def test_normal_case(self):
        """Should [expected behavior]."""
        pass

    # Edge cases
    def test_edge_case(self):
        """Should handle [edge case]."""
        pass

    # Error cases
    def test_error_case(self):
        """Should raise [Error] when [condition]."""
        pass


class TestTargetClass:
    """Tests for TargetClass."""

    class TestMethodName:
        """Tests for TargetClass.method_name."""
        pass
```

---

## Test Coverage Guidelines

### Coverage Targets

| Code Type | Target | Rationale |
|-----------|--------|-----------|
| Business logic | 90%+ | Critical for correctness |
| Utilities | 80%+ | Widely used, high impact |
| API handlers | 80%+ | User-facing, error-prone |
| UI components | 70%+ | Interaction-heavy |
| Configuration | 50%+ | Less dynamic |

### What to Always Test

- Public API/interface
- Error handling paths
- Boundary conditions
- State transitions
- Security-sensitive code

### What to Skip

- Simple getters/setters
- Framework-generated code
- Third-party library internals
- Trivial constructors

---

## Quality Checklist

- [ ] Tests follow AAA pattern (Arrange-Act-Assert)
- [ ] Test names describe scenario and expected result
- [ ] Each test tests one thing
- [ ] Tests are independent (no shared state)
- [ ] Fixtures used for common setup
- [ ] Mocks used for external dependencies
- [ ] Edge cases covered
- [ ] Error cases covered
- [ ] Tests run fast (< 1s per test)
- [ ] No flaky tests

---

## Integration with Other Skills

### With code-review-assistant:
- Review existing tests for quality
- Identify missing test coverage

### With technical-writer:
- Document testing conventions
- Create testing guides

---

## Troubleshooting

### Tests are flaky
- Remove time dependencies (mock time)
- Ensure test isolation
- Check for race conditions

### Tests are slow
- Use mocks for external calls
- Reduce fixture scope where possible
- Run tests in parallel

### Low coverage despite many tests
- Check for dead code paths
- Add error case tests
- Test conditional branches

---

## Version History

- v1.0.0 (2025-12-07): Initial release with Python/pytest, JavaScript/Jest patterns, fixture management, and coverage guidelines
