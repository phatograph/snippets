## Snippets

```jsx
// For pages without responsiveness:
<meta name="viewport" content="width=1440, viewport-fit=cover" />

// If you want inputs to be zoomed in when focus:
<meta name="viewport" content="width=device-width, initial-scale=1" />

// Otherwise:
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1" />

```

```jsx
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

```jsx
  const getWindowWidth = () => {
    return (
      window?.innerWidth ||
      document?.documentElement?.clientWidth ||
      document?.body?.clientWidth
    )
  }

  const ___onResizeTO = React.useRef<any>()
  const onResize = () => {
    const _w = getWindowWidth()

    if (_w != ___windowWidth.current) {
      ___windowWidth.current = _w

      window.clearTimeout(___onResizeTO.current)
      ___onResizeTO.current = window.setTimeout(() => {
      }, 200)
    }
  }

  React.useEffect(() => {
    window.addEventListener("resize", onResize)

    return () => {
      window.removeEventListener("resize", onResize)
    }
  }, [svgWidth])
```

```jsx
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

```jsx
<img
  ref={$img}
  className='FaceBlur__slider__img'
  alt='FaceBlur__slider__img'
  src='/images/FaceBlur__slider__img--blurred.jpg'
/>

<a
  draggable
  onDragStart={(e) => {
    e.dataTransfer.setDragImage($blank.current, 0, 0)

    onDragStart({_clientX: e.clientX})
  }}
  onDrag={(e) => {
    onDrag({
      _clientX: e.clientX,
    })
  }}
  onDragEnd={(e) => {
    onDragEnd({
      _clientX: e.clientX,
    })
  }}
  onTouchStart={(e) => {
    onDragStart({_clientX: get(e, 'touches[0].clientX')})
  }}
  onTouchMove={(e) => {
    onDrag({
      _clientX: get(e, 'touches[0].clientX'),
    })
  }}
  onTouchEnd={(e) => {
    onDragEnd({
      _clientX: get(e, 'changedTouches[0].clientX'),
    })
  }}
/>
```

```jsx
<dl
  className='Index__how-to-order__dl'
  onTouchStart={(e) => {
    ___clientX.current = get(e, 'touches[0].clientX')
  }}
  onTouchEnd={(e) => {
    if (
      Number(___clientX.current) >
      Number(get(e, 'changedTouches[0].clientX'))
    ) {
      if (__indexHowToOrder < 2) {
        __indexHowToOrderSet(__indexHowToOrder + 1)
      }
    } else if (
      Number(___clientX.current) <
      Number(get(e, 'changedTouches[0].clientX'))
    ) {
      if (__indexHowToOrder > 0) {
        __indexHowToOrderSet(__indexHowToOrder - 1)
      }
    }
  }}
>
</dl>
```

```jsx
const MyApp = ({Component, pageProps}: AppProps) => {
  const ___$WebkitFillAvailable = React.useRef<HTMLDivElement>()

  const [__isWebkitFillAvailable, __isWebkitFillAvailableSet] =
    React.useState(false)

  React.useEffect(() => {
    smoothscroll.polyfill()
  }, [])

  React.useEffect(() => {
    if (___$WebkitFillAvailable?.current?.clientHeight > 0) {
      __isWebkitFillAvailableSet(true)
    }
  }, [])

  const title = 'Ravebit Bakery'
  const description = 'Ravebit Bakery'

  return (
    <React.Fragment>
      <Head>
        <title>{title}</title>
        <meta name='description' content={description} />

        <meta
          name='viewport'
          content='width=device-width, initial-scale=1, maximum-scale=1'
          // content='width=1300, viewport-fit=cover'
        />

        <meta property='og:title' content={title} />
        <meta property='og:description' content={description} />
        <meta property='og:image' content='/images/og.png' />

        <link rel='icon' type='image/png' href='/images/pat.png' />
      </Head>

      <div
        className={className('Layout', {
          'Layout--webkit-fill-available': __isWebkitFillAvailable,
        })}
      >
        <Component
          {...{
            ...pageProps,
          }}
        />
      </div>
    </React.Fragment>
  )
}
```

```jsx
                <svg
                  className='ProductForm__images__body__label__svg'
                  viewBox='0 0 1 1'
                  onDrop={(e) => {
                    e.preventDefault()
                    __isFileHoveringSet(false)

                    const _file = e?.dataTransfer?.files?.item?.(0)

                    if (['image/png', 'image/jpeg'].includes(_file?.type)) {
                      __filesSet([...__files, _file])
                    }
                  }}
                  onDragOver={(e) => {
                    e.preventDefault()
                  }}
                  onDragEnter={() => {
                    __isFileHoveringSet(true)
                  }}
                  onDragLeave={() => {
                    __isFileHoveringSet(false)
                  }}
                />
```
