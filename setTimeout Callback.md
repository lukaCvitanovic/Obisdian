[[Bugs and Fixes]]

# setTimeout Callback

## Tags:
#react, #frontend 

---

## Description
In this exsample

```ts
const proxyRedirect = (route: string) => {
    console.log(start, trigger);
    if (start) navigate(`${prefix}/${route}`);
 };
 
const exploreIterator = (routes: string[], prefix: string, timeout: number) => {
        return {
            next: () => {
                if (routes.length > index) {
                    console.log(routes[index]);
                    return {
                        value: () => {
                            const route = routes[index];
                            setIndex((currentIndex) => currentIndex + 1);
                            setTimeout(() => {
                                // if (start) navigate(`${prefix}/${route}`);
                                proxyRedirect(route);
                            }, timeout);
                        },
                        done: false,
                    }
                }
                onDone();
                return {
                    value: () => {},
                    done: true,
                };
            },
        };
    };
 ```

regardless of the current value of the start variable the `proxyRedirect` performs with the values like they were when the setTimeout was called

### Solution
Unknown