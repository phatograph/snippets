## Snippets

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

```
  React.useEffect(() => {
    window.addEventListener("resize", onResize)

    return () => {
      window.removeEventListener("resize", onResize)
    }
  }, [svgWidth])
```

```
  const observer = React.useRef()

  React.useEffect(() => {
    observer.current = new IntersectionObserver(
      (elements) => {
        const $target = first(elements)
        // get($target, "intersectionRatio")
      },
      {
        rootMargin: "0px 0px",
      }
    )
  }, [])

  React.useEffect(() => {
    const $el = document.querySelector(".AppPublisher__handle")

    if (observer.current && $el) {
      observer.current.observe($el)
    }

    return () => {
      if (observer.current) {
        observer.current.disconnect()
      }
    }
  }, [])
```
