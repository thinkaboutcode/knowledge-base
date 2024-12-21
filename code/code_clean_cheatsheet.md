# Clean Code Cheatsheet

## 1. **Naming Conventions**
- **Use meaningful and descriptive names**: Clearly describe what the variable, function, or class represents.
    ```python
    # Bad
    int d; // elapsed time in days
    
    # Good
    int elapsedTimeInDays;
    ```
- **Avoid disinformation**: Names should not mislead.
    ```python
    # Bad
    int accountList[]; // It's not a list

    # Good
    int accounts[]; 
    ```
- **Use pronounceable names**: Make names easier to discuss.
    ```python
    # Bad
    String genymdhms; // generation date, year, month, day, hour, minute, second
    
    # Good
    String generationTimestamp;
    ```

- **Use searchable names**: Avoid single-letter names or obscure abbreviations.
    ```python
    # Bad
    for (int i = 0; i < 5; i++) {...}

    # Good
    for (int userIndex = 0; userIndex < 5; userIndex++) {...}
    ```

## 2. **Functions**
- **Keep functions small**: A function should ideally do one thing.
    ```python
    # Bad
    def fetchDataAndParseResponseAndSaveToDB(): {...}

    # Good
    def fetchData(): {...}
    def parseResponse(): {...}
    def saveToDB(): {...}
    ```

- **Use descriptive function names**: A function’s name should tell what it does.
    ```python
    # Bad
    def handle(): {...}

    # Good
    def handleUserLogin(): {...}
    ```

- **Function arguments (≤ 3)**: Try to limit function parameters to three or fewer.
    ```python
    # Bad
    def createUser(firstName, lastName, age, address, phoneNumber): {...}

    # Good
    def createUser(firstName, lastName): {...}
    ```

## 3. **Comments**
- **Comments should explain why, not what**: Use comments to explain the reasoning behind code, not what the code does.
    ```python
    # Bad
    # Increment age by 1
    age += 1;

    # Good
    # User's age is calculated based on their birthdate stored in the system.
    ```

- **Use self-explanatory code instead of comments**: Refactor code to be more readable.
    ```python
    # Bad
    # Check if the user is an administrator
    if user.isAdmin == True: {...}

    # Good
    if user.isAdministrator(): {...}
    ```

## 4. **Error Handling**
- **Use exceptions, not return codes**: Use exceptions for error handling.
    ```python
    # Bad
    def divide(a, b):
        if b == 0:
            return -1
        return a / b

    # Good
    def divide(a, b):
        if b == 0:
            raise ValueError('b cannot be zero')
        return a / b
    ```

- **Fail fast**: Immediately handle unexpected conditions.
    ```python
    # Bad
    def fetchUserData(id):
        if id != None:
            # fetch data
            pass

    # Good
    def fetchUserData(id):
        if id is None:
            raise ValueError('ID cannot be None')
        # fetch data
    ```

## 5. **Formatting**
- **Use consistent indentation and spacing**: Keeps code readable.
    ```python
    # Bad
    def add(a,b):
        return a+b

    # Good
    def add(a, b):
        return a + b
    ```

- **Keep related lines together**: Functions, variables, and blocks of code that are closely related should be near each other.

## 6. **Classes**
- **Single Responsibility Principle**: A class should have one reason to change (it should only do one thing).
    ```python
    # Bad
    class UserManager:
        def manageUserLogin(): {...}
        def handlePayment(): {...}

    # Good
    class UserManager:
        def manageUserLogin(): {...}

    class PaymentManager:
        def handlePayment(): {...}
    ```

- **Encapsulate what changes**: Hide implementation details and expose only what is necessary.
    ```python
    # Bad
    class Car:
        def __init__(self, engine):
            self.engine = engine

    # Good
    class Car:
        def __init__(self, engine):
            self.__engine = engine  # hide the internal details
    ```

## 7. **SOLID Principles**
- **S**: **Single Responsibility Principle**: A class should only have one responsibility.
- **O**: **Open/Closed Principle**: Software entities should be open for extension, but closed for modification.
- **L**: **Liskov Substitution Principle**: Subtypes must be substitutable for their base types.
- **I**: **Interface Segregation Principle**: No client should be forced to depend on methods it doesn't use.
- **D**: **Dependency Inversion Principle**: Depend on abstractions, not on concrete implementations.

## 8. **DRY (Don't Repeat Yourself)**
- Avoid duplication of code by abstracting common functionality.
    ```python
    # Bad
    def createAdminUser(): {...}
    def createGuestUser(): {...}

    # Good
    def createUser(role): {...}
    ```

## 9. **YAGNI (You Aren’t Gonna Need It)**
- Don’t add functionality until it is necessary.

## 10. **Testing**
- **Write tests for every piece of code**: Unit tests ensure your code behaves as expected.
    ```python
    def test_add_user():
        assert add_user('John') == True
    ```

## 11. **Refactoring**
- Continuously improve your code without changing its functionality.
    ```python
    # Before refactoring
    def calculate_total(order):
        tax = 0.05
        total = order.subtotal + (order.subtotal * tax)
        return total
    
    # After refactoring
    def calculate_total(order, tax_rate=0.05):
        return order.subtotal * (1 + tax_rate)
    ```

## 12. **Code Smells to Avoid**
- **Long methods**: Break them down into smaller, reusable methods.
- **Large classes**: Break them down based on functionality (SRP).
- **Duplicate code**: Refactor and extract common logic.
- **Magic numbers**: Use constants instead of hardcoded values.
    ```python
    # Bad
    if user.age > 18: {...}

    # Good
    LEGAL_AGE = 18
    if user.age > LEGAL_AGE: {...}
    ```

---

**References**:
- "Clean Code: A Handbook of Agile Software Craftsmanship" by Robert C. Martin
- "The Pragmatic Programmer" by Andrew Hunt and David Thomas
