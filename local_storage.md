## Basic Usage

```javascript
// Storing data
localStorage.setItem('key', 'value');

// Retrieving data
const value = localStorage.getItem('key');

// Removing data
localStorage.removeItem('key');

// Clearing all data
localStorage.clear();
```

## Practical Examples with Different Data Formats

### Storing and Retrieving Simple Strings
```javascript
// Store username
localStorage.setItem('username', 'john_doe');

// Retrieve username
const username = localStorage.getItem('username');
console.log(username); // Output: john_doe
```

### Working with Numbers
```javascript
// Store a number (gets converted to string)
localStorage.setItem('counter', 42);

// Retrieve and convert back to number
const counter = Number(localStorage.getItem('counter'));
console.log(counter + 1); // Output: 43

```

### Storing and Retrieving Objects (JSON)

```javascript
const user = {
  id: 1,
  name: 'Alice',
  preferences: {
    theme: 'dark',
    fontSize: 14
  }
};

// Convert object to JSON string and store
localStorage.setItem('user', JSON.stringify(user));

// Retrieve and parse JSON
const storedUser = JSON.parse(localStorage.getItem('user'));
console.log(storedUser.name); // Output: Alice
```

### Working with Arrays

```javascript
const todoList = [
  { id: 1, task: 'Buy groceries', completed: false },
  { id: 2, task: 'Walk the dog', completed: true }
];

// Store array
localStorage.setItem('todos', JSON.stringify(todoList));

// Retrieve array
const storedTodos = JSON.parse(localStorage.getItem('todos') || '[]');

// Add new item
storedTodos.push({ id: 3, task: 'Learn local storage', completed: false });
localStorage.setItem('todos', JSON.stringify(storedTodos));
```

## Minimal Safe Implementation
basic protection without verbose try-catch blocks:

```javascript
// Safe set with fallback
function setStorage(key, value) {
  try {
    localStorage.setItem(key, JSON.stringify(value));
    return true;
  } catch {
    return false; // Silently fail
  }
}

// Safe get with fallback
function getStorage(key, fallback = null) {
  try {
    const data = localStorage.getItem(key);
    return data ? JSON.parse(data) : fallback;
  } catch {
    return fallback;
  }
}

// Usage
setStorage('prefs', { darkMode: true });
const prefs = getStorage('prefs', { darkMode: false });
```

## When to use JSON.parse()
Must Use JSON.parse() When: You stored data using JSON.stringify() (objects, arrays, numbers, booleans, etc.)
localStorage only stores strings, so structured data (objects, arrays) must be converted to/from JSON strings.

```javascript
localStorage.setItem('user', JSON.stringify({ name: 'Alice' }));
const user = JSON.parse(localStorage.getItem('user')); // { name: 'Alice' }
```

Can Skip JSON.parse() When: you stored plain strings (no complex data).

```javascript
localStorage.setItem('name', 'Alice');
const name = localStorage.getItem('name'); // "Alice" (no parse needed)
```


