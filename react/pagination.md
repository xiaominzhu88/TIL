# Pagination with React

First, site needs to display 15 cards with different contents, the API returns 104 total pages.
User can click the pagination button at bottom of the site, or click the Previous / Next button to switch the page.

👉 When the site initial loads , the pagination needs to display the first and last three buttons, the middle buttons are displayed with ellipsis.

<img src='./image/pagination1.png' height='30px'/>

👉 When user switches up to page 4, a previous button appears in the front of pagination, it will only display the first and last buttons, as well as the current page button and two before / after buttons, the other buttons are displayed with ellipsis.

<img src='./image/pagination2.png' height='30px'/>

👉 User can jump to the last page, the Next button should disappear at this time, the pagination only displays the first, last three buttons and the Previous button, the middle buttons are displayed with ellipsis

<img src='./image/pagination3.png' height='30px'/>

Parent component:

- update data with api response, pass them to Pagination child component

```jsx
const ParentComponent = () => {
  const [pageResult, setPageResult] = useState({});

  // first render page 1
   useEffect(() => {
     async function fetchTrial() {
       const data = await Client.trialPageList.get(1);
       setPageResult(data);
     }
     fetchTrial();
    }, []);

  // fetch page from Pagination Component
  const fetchPageData = async (page) => {
    const result = await Client.trialPageList.get(page);
    setPageResult(result);
  };

  const pageTotal = pageResult?.meta?.last_page;
  const currentPage = pageResult?.meta?.current_page;
  const buttonLinks = pageResult?.meta?.links;


  return ...

  <Pagination
    pageTotal={pageTotal}
    currentPage={currentPage}
    buttonLinks={buttonLinks}
    fetchPageData={fetchPageData}
   />
   ...
}
```

Pagination Component:

- define Previous, Page, Next, ellipsis conditional rendered buttons

```jsx
const Pagination = ({ fetchPageData, pageTotal, currentPage, buttonLinks }) => {
  return (
    <div className={styles.pagination}>

     // should only visible if current page >= 4
      {currentPage >= 4 && (
        <Button
          onClick={() => fetchPageData(String(currentPage - 1))}
          className={classNames(styles.activeBtn, {
            [styles.invisible]: currentPage === 1,
          })}
          theme="pagination"
        >
          <Image src={smallArrowLongLeft} />
          Previous
        </Button>
      )}

     // the first button always appears
      <Button
        className={classNames(styles.circle, {
          [styles.activeButton]: currentPage === 1,
        })}
        onClick={() => {
          fetchPageData(1);
        }}
        shape="bubble"
      >
        1
      </Button>

      // these buttons should be visible if the current page <=3 or >= total - 2
      {(currentPage <= 3 || currentPage >= pageTotal - 2) && (
        <Button
          className={classNames(styles.circle, {
            [styles.activeButton]: currentPage === 2,
          })}
          onClick={() => {
            fetchPageData(2);
          }}
          shape="bubble"
        >
          2
        </Button>
      )}

      {(currentPage <= 3 || currentPage >= pageTotal - 2) && (
        <Button
          className={classNames(styles.circle, {
            [styles.activeButton]: currentPage === 3,
          })}
          onClick={() => {
            fetchPageData(3);
          }}
          shape="bubble"
        >
          3
        </Button>
      )}


     // should only visible if the current page >= 4
      {currentPage >= 4 && (
        <Button className={styles.dots} disabled>
          ...
        </Button>
      )}

     // filter out three buttons for the pages >= 4 or <= total -3
      {buttonLinks
        ?.filter(
          (item) =>
            item.label === String(currentPage) ||
            item.label === String(currentPage - 1) ||
            item.label === String(currentPage + 1),
        )
        .map((btn) => {
          return (
            currentPage >= 4 &&
            currentPage <= pageTotal - 3 && (
              <Button
                key={btn.label}
                onClick={() => {
                  fetchPageData(btn.label);
                }}
                className={classNames(styles.circle, {
                  [styles.activeButton]: btn.label === String(currentPage),
                })}
                shape="bubble"
              >
                {btn.label}
              </Button>
            )
          );
        })}

      // should only visible if the last three buttons are visible
      {currentPage < pageTotal - 2 && (
        <Button className={styles.dots} disabled>
          ...
        </Button>
      )}

      // these buttons appear if the current page < 4 or >= total - 2
      {(currentPage >= pageTotal - 2 || currentPage < 4) && (
        <Button
          className={classNames(styles.circle, {
            [styles.activeButton]: currentPage === pageTotal - 2,
          })}
          onClick={() => {
            fetchPageData(String(pageTotal));
          }}
          shape="bubble"
        >
          {String(pageTotal - 2)}
        </Button>
      )}
      {(currentPage >= pageTotal - 2 || currentPage < 4) && (
        <Button
          className={classNames(styles.circle, {
            [styles.activeButton]: currentPage === pageTotal - 1,
          })}
          onClick={() => {
            fetchPageData(String(pageTotal));
          }}
          shape="bubble"
        >
          {String(pageTotal - 1)}
        </Button>
      )}

      // the last button always appears
      <Button
        className={classNames(styles.circle, {
          [styles.activeButton]: currentPage === pageTotal,
        })}
        onClick={() => {
          fetchPageData(String(pageTotal));
        }}
        shape="bubble"
      >
        {String(pageTotal)}
      </Button>

      // should always be visible if the current page is not the last one
      {currentPage !== pageTotal && (
        <Button
          onClick={() => fetchPageData(currentPage + 1)}
          className={styles.activeBtn}
          theme="pagination"
          disabled={currentPage === pageTotal}
        >
          Next
          <Image src={smallArrowLongRight} />
        </Button>
      )}
    </div>
  );
};

export default Pagination;
```

- use `onClick` on each button, call `fetchPageData` function to fetch every page like this: `fetchPageData(currentPage)` regarding to the current page number

---

It is also important that the button style should be updated according to the current page, use react [classnames](https://www.npmjs.com/package/classnames) on each button with page number to render conditional style

---

```jsx
.activeButton {
  display:none;
  @include media-breakpoint-up(sm){
    display:block;
    margin: ...;
    color: ...;
    background: ...;
    border-radius:999px;
    &:active,
    &:focus {
      box-shadow:inset 0 1px 2px ...;
      color: ...
    }
  }
}
```
