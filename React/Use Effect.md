Renders on every user change

# Example (Debounce)
```
  useEffect(() => {
    const handler = setTimeout(() => {
      setDebouncedState(value);
    }, delay);

    return () => {
      clearTimeout(handler);
    };
  }, [value, delay]);
```
- This has a cleanup function `return () =>` that clears the timeout so that the state is only set after a certain timeout