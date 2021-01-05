## Snippets

```jsx
// For pages without responsiveness:
<meta name="viewport" content="width=1440, viewport-fit=cover" />

//If you want inputs to be zoomed in when focus:
<meta name="viewport" content="width=device-width, initial-scale=1" />

//Otherwise:
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1" />

```

```js
// <input type="text" name="publisher_name" value="a" />
// <input type="text" name="purchaser_name" value="b" />
// => {publisher_name: "a", purchaser_name: "b"}
export const formInputsToObject = ({elements}) => {
  return mapValues(
    keyBy(
      filter(elements, (x) => get(x, "name") && !isEmpty(get(x, "value"))).map(
        (x) => ({
          name: get(x, "name"),
          value: get(x, "value"),
        })
      ),
      "name"
    ),
    "value"
  )
}
```

```js
  React.useEffect(() => {
    window.addEventListener("resize", onResize)

    return () => {
      window.removeEventListener("resize", onResize)
    }
  }, [svgWidth])
```

```js
  const ___observer = React.useRef()
  const ___$el = React.useRef()

  React.useEffect(() => {
    ___observer.current = new IntersectionObserver(
      (elements) => {
        const $target = first(elements)

        console.log(get($target, 'intersectionRatio'))
      },
      {
        rootMargin: '0px 0px',
      }
    )
  }, [])

  React.useEffect(() => {
    if (___observer.current && ___$el.current) {
      ___observer.current.observe(___$el.current)
    }

    return () => {
      if (___observer.current) {
        ___observer.current.disconnect()
      }
    }
  }, [])

```
