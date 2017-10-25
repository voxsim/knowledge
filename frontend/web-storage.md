### window.localStorage
- Key/value pairs
- Persistent on page reloads
- No HTTP overhead
- Great for prefs

### window.sessionStorage
- Same as Local storage except for
  - Only last as long as window/tab is open
  - new window/tab is a new session
  - great for sensitive data

### Operations
- setItem(key, value)
- getItem(key)
- removeItem(key)
- key(index)
- clear()
- They accepts only string, so use JSON.stringify before store it and JSON.parse after retrieve it

### Scope
- Same origin policy is in effect 
