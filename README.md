# Case Styles in Coding: Uses and Conventions

A comprehensive guide to naming conventions across programming languages, with particular focus on shell (zsh), Python, and Go.

## Overview of Case Styles

Different case styles serve distinct purposes in programming, helping developers distinguish between variables, functions, classes, and constants at a glance. Adhering to language-specific conventions improves code readability and maintains consistency across projects.

### Common Case Styles

**snake_case** (all lowercase with underscores)
- Example: `user_name`, `calculate_total_price`
- Used for: Variables, functions, file names

**SCREAMING_SNAKE_CASE** (all uppercase with underscores)
- Example: `MAX_CONNECTIONS`, `API_KEY`
- Used for: Constants, environment variables

**camelCase** (first word lowercase, subsequent words capitalised)
- Example: `userName`, `calculateTotalPrice`
- Used for: Variables, functions, methods

**PascalCase** (all words capitalised, including first)
- Example: `UserName`, `CalculateTotalPrice`
- Used for: Classes, types, interfaces

**kebab-case** (all lowercase with hyphens)
- Example: `user-name`, `calculate-total-price`
- Used for: URLs, file names, CSS classes

**SCREAMING-KEBAB-CASE** (all uppercase with hyphens)
- Example: `USER-NAME`, `API-KEY`
- Used for: Rarely, some configuration files

## Shell (zsh/bash) Conventions

Shell scripting has evolved distinct conventions that prioritise readability in the context of system administration and automation.

### Variables

**Local variables and function-scoped variables** use lowercase `snake_case`:

```zsh
user_name="david"
file_count=10
home_directory="/Users/bing"

calculate_total() {
    local item_count=$1
    local price_per_item=$2
    echo $((item_count * price_per_item))
}
```

**Environment variables and constants** use `SCREAMING_SNAKE_CASE`:

```zsh
export PATH="/usr/local/bin:$PATH"
export DATABASE_URL="postgresql://localhost/mydb"

readonly MAX_RETRIES=3
readonly CONFIG_FILE="/etc/myapp/config.yml"
```

### Functions

Function names should use `snake_case`:

```zsh
get_user_input() {
    read -r input
    echo "$input"
}

validate_email_address() {
    local email=$1
    [[ $email =~ ^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$ ]]
}
```

### Script Files

Shell scripts typically use `kebab-case` or `snake_case` for file names:

```
backup-database.sh
deploy_application.sh
system-health-check.zsh
```

### Special Considerations

- Avoid using hyphens in variable names (they're interpreted as minus operators)
- Use descriptive names for better self-documentation
- Prefix private functions with underscore: `_internal_helper()`
- Use `$()` for command substitution over backticks for clarity

## Python Conventions

Python follows the [PEP 8](https://pep8.org/) style guide, which provides clear and widely adopted naming conventions.

### Variables and Functions

Use `snake_case` for variables, functions, and methods:

```python
user_name = "David"
total_count = 42
api_response_time = 1.23

def calculate_total_price(items, tax_rate):
    subtotal = sum(item.price for item in items)
    return subtotal * (1 + tax_rate)

def fetch_user_data(user_id):
    return database.query(user_id)
```

### Constants

Use `SCREAMING_SNAKE_CASE` for constants:

```python
MAX_CONNECTIONS = 100
DEFAULT_TIMEOUT = 30
API_BASE_URL = "https://api.example.com"
DATABASE_PORT = 5432
```

### Classes

Use `PascalCase` for class names:

```python
class UserAccount:
    def __init__(self, username, email):
        self.username = username
        self.email = email
    
    def validate_email(self):
        return "@" in self.email

class DatabaseConnection:
    pass

class HTTPRequestHandler:
    pass
```

### Private and Protected Members

Use a single leading underscore for "internal use" (protected):

```python
class DataProcessor:
    def __init__(self):
        self._cache = {}  # Protected attribute
    
    def _internal_helper(self):  # Protected method
        pass
```

Use double leading underscore for name mangling (private):

```python
class SecureVault:
    def __init__(self):
        self.__secret_key = "xyz123"  # Private attribute
```

### Module and Package Names

Use short, all-lowercase names, preferably without underscores:

```python
import json
import os
import requests
from datetime import datetime

# For multi-word modules, underscores are acceptable
import data_processing
import user_authentication
```

### File Names

Python files should use `snake_case`:

```
user_manager.py
database_connection.py
api_client.py
test_user_manager.py
```

### Type Hints

Type aliases and type variables use `PascalCase`:

```python
from typing import List, Dict, TypeVar

UserId = int
UserData = Dict[str, str]
T = TypeVar('T')

def get_user(user_id: UserId) -> UserData:
    pass
```

## Go Conventions

Go has strong opinions about naming, with conventions that differ from Python and many other languages.

### Variables and Functions

**Package-level and local variables** use `camelCase`:

```go
var userName string
var itemCount int

func calculateTotalPrice(items []Item, taxRate float64) float64 {
    var subtotal float64
    for _, item := range items {
        subtotal += item.Price
    }
    return subtotal * (1 + taxRate)
}
```

**Exported (public) identifiers** use `PascalCase`:

```go
// Exported function - available to other packages
func FetchUserData(userID int) (*User, error) {
    return db.Query(userID)
}

// Exported variable
var DefaultTimeout = 30 * time.Second

// Exported constant
const MaxConnections = 100
```

**Unexported (private) identifiers** use `camelCase`:

```go
// Unexported function - package-private
func validateEmailAddress(email string) bool {
    return strings.Contains(email, "@")
}

// Unexported variable
var internalCache = make(map[string]interface{})
```

### Constants

Constants follow the same exported/unexported rules:

```go
// Exported constants (PascalCase)
const (
    StatusActive   = "active"
    StatusInactive = "inactive"
    MaxRetries     = 3
)

// Unexported constants (camelCase)
const (
    defaultBufferSize = 1024
    maxCacheItems     = 1000
)
```

### Types and Interfaces

Types and interfaces use `PascalCase` when exported, `camelCase` when unexported:

```go
// Exported types
type User struct {
    ID       int
    Username string
    Email    string
}

type DataProcessor interface {
    Process(data []byte) error
    Validate() bool
}

// Unexported types
type internalCache struct {
    data map[string]interface{}
}
```

### Acronyms

Go has a special convention for acronyms: keep them together and use the same case:

```go
// Correct
var userID int
var apiURL string
func ServeHTTP()
type XMLParser struct{}

// Incorrect
var userId int
var apiUrl string
func ServeHttp()
type XmlParser struct{}
```

### Package Names

Package names should be short, concise, lowercase, and singular:

```go
package user
package http
package json
package auth
```

Avoid underscores or mixed caps in package names.

### File Names

Go files use `snake_case`:

```
user_manager.go
database_connection.go
api_client.go
user_manager_test.go
```

### Receivers

Method receiver names should be short (1-2 characters) and consistent:

```go
type User struct {
    Name string
}

func (u *User) Validate() error {
    if u.Name == "" {
        return errors.New("name required")
    }
    return nil
}

func (u *User) GetDisplayName() string {
    return u.Name
}
```

## Other Languages (Brief Overview)

### JavaScript/TypeScript

- **Variables/Functions**: `camelCase`
- **Classes/Types**: `PascalCase`
- **Constants**: `SCREAMING_SNAKE_CASE` or `camelCase`
- **Files**: `camelCase.js` or `PascalCase.tsx` for React components

```javascript
const userName = "David";
const MAX_RETRIES = 3;

function calculateTotal(items) { }

class UserAccount { }
```

### Java

- **Variables/Methods**: `camelCase`
- **Classes/Interfaces**: `PascalCase`
- **Constants**: `SCREAMING_SNAKE_CASE`
- **Packages**: `lowercase.with.dots`

```java
String userName = "David";
public static final int MAX_CONNECTIONS = 100;

public void calculateTotal() { }

public class UserAccount { }
```

### C/C++

- **Variables/Functions**: `snake_case` (traditional) or `camelCase` (modern)
- **Classes**: `PascalCase`
- **Macros/Constants**: `SCREAMING_SNAKE_CASE`
- **Files**: `snake_case.h`, `snake_case.cpp`

```cpp
int user_count = 0;
#define MAX_BUFFER_SIZE 1024

void calculate_total() { }

class UserAccount { };
```

### Rust

- **Variables/Functions**: `snake_case`
- **Types/Traits**: `PascalCase`
- **Constants/Statics**: `SCREAMING_SNAKE_CASE`
- **Macros**: `snake_case!`

```rust
let user_name = "David";
const MAX_CONNECTIONS: u32 = 100;

fn calculate_total() { }

struct UserAccount { }
```

### Ruby

- **Variables/Methods**: `snake_case`
- **Classes/Modules**: `PascalCase`
- **Constants**: `SCREAMING_SNAKE_CASE` or `PascalCase`

```ruby
user_name = "David"
MAX_RETRIES = 3

def calculate_total
end

class UserAccount
end
```

### PHP

- **Variables**: `$camelCase` or `$snake_case` (varies by framework)
- **Functions**: `camelCase` or `snake_case`
- **Classes**: `PascalCase`
- **Constants**: `SCREAMING_SNAKE_CASE`

```php
$userName = "David";
define('MAX_CONNECTIONS', 100);

function calculateTotal() { }

class UserAccount { }
```

## Best Practices

### Consistency is Key

The most important aspect of case styles is consistency within a project. Mixed conventions create confusion and reduce code readability.

### Follow Language Idioms

Each language has established conventions for a reason. Fighting against them makes your code harder for others to understand and maintain.

### Use Descriptive Names

Regardless of case style, prioritise clarity:

```python
# Good
user_authentication_token = get_token()

# Avoid
t = get_token()
```

### Consider Context

Different parts of your codebase may have different conventions:

- **Configuration files**: Often use `kebab-case` or `SCREAMING_SNAKE_CASE`
- **Environment variables**: Always `SCREAMING_SNAKE_CASE`
- **URL paths**: `kebab-case` for readability
- **Database columns**: Often `snake_case`

### Tool Support

Use linters and formatters to enforce conventions:

- **Python**: `black`, `flake8`, `pylint`
- **Go**: `gofmt`, `golint`, `go vet`
- **Shell**: `shellcheck`, `shfmt`

### Documentation

When working on a team or open-source project, document your naming conventions in a `CONTRIBUTING.md` or style guide.

## Summary Table

| Language | Variables | Functions | Classes/Types | Constants | Files |
|----------|-----------|-----------|---------------|-----------|-------|
| **Shell (zsh)** | `snake_case` | `snake_case` | N/A | `SCREAMING_SNAKE_CASE` | `kebab-case` |
| **Python** | `snake_case` | `snake_case` | `PascalCase` | `SCREAMING_SNAKE_CASE` | `snake_case.py` |
| **Go** | `camelCase` / `PascalCase`* | `camelCase` / `PascalCase`* | `PascalCase` / `camelCase`* | `PascalCase` / `camelCase`* | `snake_case.go` |
| JavaScript | `camelCase` | `camelCase` | `PascalCase` | `SCREAMING_SNAKE_CASE` | `camelCase.js` |
| Java | `camelCase` | `camelCase` | `PascalCase` | `SCREAMING_SNAKE_CASE` | `PascalCase.java` |
| Rust | `snake_case` | `snake_case` | `PascalCase` | `SCREAMING_SNAKE_CASE` | `snake_case.rs` |

*In Go, capitalisation determines visibility: `PascalCase` for exported (public), `camelCase` for unexported (private).

## Conclusion

Understanding and applying proper case conventions is fundamental to writing idiomatic, maintainable code. While the specifics vary across languages, the underlying principle remains constant: use conventions that make your code's structure and intent immediately clear to other developers (and your future self).

When in doubt, consult the official style guide for your language, examine popular open-source projects in that language, and most importantly, maintain consistency throughout your codebase.
