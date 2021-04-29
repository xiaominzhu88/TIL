# List open Ports on Mac

Want to know which ports are open on Mac

```jsx
lsof -i -P | grep -i "listen"
```

This gives a list with all applications and their open ports, something like:

```jsx
mysqld  1491 username  29u  IPv6  0x4d..... 0t0  TCP localhost:3306 (LISTEN)
```
