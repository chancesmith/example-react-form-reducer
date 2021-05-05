# Example React Form Reducer
Example of test + creating a reducer for a large form

**Form.test.js**
```javascript
// test
it('should have empty search field and update', () => {
  const { getByLabelText } = render(<Component />)
  const inputText = 'cool things'
  const input = getByLabelText('search')
  fireEvent.change(input, { target: { value:  inputText} })

  expect(input.value).toBe(inputText)
})
```

**Form.js**
```javascript
const BY_SELLING = {
  ALL: 'ALL',
  IN: 'IN',
  NOT: 'NOT'
}
const BY_SALES_RANGE_DROPDOWN = {
  YTD: 'YTD',
  Q1: 'Q1'
}

const initialState = {
  searchText: '',
  locationState: '',
  locationCounty: '',
  locationCity: '',
  storeWithinMiles: '',
  storeWithinZipcode: '',
  bySelling: BY_SELLING['ALL'],
  bySalesRangeStart: 0,
  bySalesRangeEnd: 100000,
  bySalesRangeDropdown: BY_SALES_RANGE_DROPDOWN['YTD'],
  byTag: [],
  byTagIsNot: false
}

function FormReducer(state, action) {
  switch (action.type) {
    case 'reset': {
      return initialState;
    }
    case 'updateSearch': {
      return {...state, searchText: action.payload};
    }
    // ...other cases
    default:
      throw new Error('Unknown action type');
  }
}

const Component = () => {
  const [state, dispatch] = useReducer(FormReducer, initialState)

  function handleSearchText(e){
    dispatch({type: 'updateSearch', payload: e.target.value})
  }

  // return ...
}
```
