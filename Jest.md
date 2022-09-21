[[JavaScript]]

# Jest

## Tags:
#package, #testing 

## Links:
- [Jest Docs](https://jestjs.io/)

---

## Description
- Package for testing [[JavaScript]] base code

## Tips and Tricks
- For testing stuff in `setTimeout` use `jest.useFakeTimers` and `jest.runAllTimers`
	- To return to using real timers use `jest.useRealTimers`
- For testing stuff in `setInterval` use `jest.useFakeTimers` and `jest.advanceTimersByTime`
- If jest **doesn't exit after 1 second** when all tests are concluded then some async function did not finish, try and mock that function to resolve this issue

