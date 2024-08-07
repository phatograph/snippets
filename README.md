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
                const elements = (e?.target as HTMLFormElement)?.elements

                const inputs = formInputsToObject({
                  elements,
                })
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
  const ___observer = React.useRef<IntersectionObserver>()
  const ___$el = React.useRef()

  React.useEffect(() => {
    ___observer.current = new IntersectionObserver(
      (elements) => {
        const $target = elements?.[0]

        console.log($target?.intersectionRatio)
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
const ___clientX = React.useRef()
const swipeThreshold = 50

<div
  className="BlogShow__related__dl__wrapper-outer"
  onTouchStart={(e) => {
    ___clientX.current = e?.touches?.[0].clientX
  }}
  onTouchEnd={(e) => {
    if (Number(___clientX.current) - Number(e?.changedTouches?.[0]?.clientX) > swipeThreshold) {
      if (__relatedIndexSmol + 1 < ARTICLES?.length) {
        __relatedIndexSmolSet(__relatedIndexSmol + 1)
      } else {
        __relatedIndexSmolSet(0)
      }
    } else if (Number(___clientX.current) - Number(e.changedTouches?.[0]?.clientX) < swipeThreshold * -1) {
      if (__relatedIndexSmol > 0) {
        __relatedIndexSmolSet(__relatedIndexSmol - 1)
      } else {
        __relatedIndexSmolSet(ARTICLES?.length - 1)
      }
    }
  }}
>
</div>
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
// smoothscroll-polyfill
// http://iamdustan.com/smoothscroll/
window.scroll({ top: 2500, left: 0, behavior: 'smooth' })
document.querySelector('.hello').scrollIntoView({ behavior: 'smooth' })
window.history.pushState(null, null, '#contact')
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

```jsx
import ReactDOMServer from 'react-dom/server';

ReactDOMServer.renderToStaticMarkup(element)
```

```jsx
            <img
              className='Index__hero__img'
              alt='Index__hero__img'
              src='/images/Index__hero__img.png'
              srcSet='/images/Index__hero__img--2x.png 2x'
            />
```

```jsx
  React.useEffect(() => {
    const handleClickOutside = (event: MouseEvent) => {
      if (
        __isActive &&
        ___$el.current &&
        !___$el.current.contains(event.target as any)
      ) {
        __isActiveSet(false)
      }
    }

    document.addEventListener('click', handleClickOutside)

    return () => {
      document.removeEventListener('click', handleClickOutside)
    }
  }, [__isActive])
```

```jsx
import React from 'react'
import {find} from 'lodash'
import className from 'classnames'
import {useRouter} from 'next/router'
import pagination from 'pagination'
import Link from 'next/link'

const Pagination = ({}) => {
  const router = useRouter()

  const current = router?.query?.page ?? 1
  const paginator = new pagination.SearchPaginator({
    current,
    totalResult: 9 * 13,
    rowsPerPage: 9,
    pageLinks: 3,
  })

  const paginatorData = paginator.getPaginationData()

  const LinkWithPage = ({page, children}) => {
    return (
      <Link
        href={{
          query: {
            ...router?.query,
            page,
          },
        }}
      >
        {children}
      </Link>
    )
  }

  return (
    <div className='Pagination'>
      <LinkWithPage page={paginatorData?.first}>
        <a
          className={className('Pagination__a', {
            'Pagination__a--disabled': !paginatorData?.first,
          })}
        >
          <img
            className='Pagination__a__img'
            src='/images/Pagination__a__img--first.svg'
          />
        </a>
      </LinkWithPage>

      <LinkWithPage page={paginatorData?.previous}>
        <a
          className={className('Pagination__a', {
            'Pagination__a--disabled': !paginatorData?.previous,
          })}
        >
          <img
            className='Pagination__a__img'
            src='/images/Pagination__a__img--prev.svg'
          />
        </a>
      </LinkWithPage>

      <div className='Pagination__numbers'>
        {!find(paginatorData?.range, (x) => x == 1) && (
          <LinkWithPage page={paginatorData?.first}>
            <a className='Pagination__numbers__a Pagination__numbers__a--first'>
              1
            </a>
          </LinkWithPage>
        )}

        {!find(paginatorData?.range, (x) => x == 2) &&
          paginatorData?.range?.length > 0 && (
            <span className='Pagination__numbers__dots'>
              <img
                className='Pagination__numbers__dots__img'
                src='/images/Pagination__numbers__dots__img.svg'
              />
            </span>
          )}

        {(paginatorData?.range || []).map((x: any, i: any) => (
          <LinkWithPage page={x} key={i}>
            <a
              className={className('Pagination__numbers__a', {
                'Pagination__numbers__a--active': paginatorData?.current == x,
              })}
            >
              {x}
            </a>
          </LinkWithPage>
        ))}

        {!find(
          paginatorData?.range,
          (x) => x == paginatorData?.pageCount - 1
        ) &&
          paginatorData?.range?.length > 0 && (
            <span className='Pagination__numbers__dots'>
              <img
                className='Pagination__numbers__dots__img'
                src='/images/Pagination__numbers__dots__img.svg'
              />
            </span>
          )}

        {!find(paginatorData?.range, (x) => x == paginatorData?.pageCount) &&
          paginatorData?.range?.length > 0 && (
            <LinkWithPage page={paginatorData?.last}>
              <a className='Pagination__numbers__a Pagination__numbers__a--last'>
                {paginatorData?.last}
              </a>
            </LinkWithPage>
          )}
      </div>

      <LinkWithPage page={paginatorData?.next}>
        <a
          className={className('Pagination__a', {
            'Pagination__a--disabled': !paginatorData?.next,
          })}
        >
          <img
            className='Pagination__a__img'
            src='/images/Pagination__a__img--next.svg'
          />
        </a>
      </LinkWithPage>

      <LinkWithPage page={paginatorData?.last}>
        <a
          className={className('Pagination__a', {
            'Pagination__a--disabled': !paginatorData?.last,
          })}
        >
          <img
            className='Pagination__a__img'
            src='/images/Pagination__a__img--last.svg'
          />
        </a>
      </LinkWithPage>
    </div>
  )
}

export default Pagination
```
