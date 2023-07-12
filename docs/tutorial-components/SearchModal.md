---
sidebar_position: 10
sidebar_label: 'SearchModal.jsx'
---

# SearchModal Components

File: `code/client/components/search/SearchModal.jsx`

## Description

SearchModal allow to render the search modal of the website. It is used to search for a product.
In the search modal, the user can search by tire, wheel, and accessories.

- Tire: The user can search by vehicle or by size.
- Wheel: The user can search by vehicle or by size.
- Accessories: The user can search by vehicle or by category.

## State

| State Name | Type | Default | Description |
|---|---|---|---|
| productType | string  | Constant | ProductTypes.TIRES  | product type |
| searchType | string  | Constant | SearchTypes.VEHICLE  | search type |
| defaultSearchType | string  | Constant | SearchTypes.VEHICLE  | default search type |
| yearList | array  | []  | year list |
| categoryList | array  | []  | category list |
| modelList | array  | []  | model list |
| year | string  | ''  | year |
| selectedMakeId | string  | ''  | selected make id |
| category | string  | ''  | category |
| model | string  | ''  | model |
| vehicleYears | array  | []  | vehicle years |
| vehicleMakes | array  | []  | vehicle makes |
| vehicleSecondaryMakes | array  | []  | vehicle secondary makes |
| vehicleModels | array  | []  | vehicle models |
| selectedYear | string  | ''  | selected year |
| selectedMake | string  | ''  | selected make |
| selectedModel | string  | ''  | selected model |
| runRecaptcha | boolean  | false  | run recaptcha |

## Props

| Prop Name | Type | Default | Description |
|---|---|---|---|
| prop1  | type  | default value | description |
| prop2  | type  | default value | description |

## Where is this component used?

File `code/client/components/ApplicationRefactor.jsx`

```jsx title="code/client/components/ApplicationRefactor.jsx"

 renderSearchModal: function () {
    if (this.props.toggleSearch) {
      if (this.enableFullScreenSearch()) {
        return <SearchModalFullScreen/>;
      } else {
        return <SearchModal/>;
      }

    } else {
      return false;
    }
  },

  ```

<!-- ### prop1

Here, explain in detail about prop1.

### prop2

Here, explain in detail about prop2.

## Code Examples

Provide examples of how to use the component.

```jsx
<ComponentName prop1={value1} prop2={value2} />

``` -->

## Interactive Playground

Provide a link to the interactive playground if it exists, or embed a live demo if possible.

## Visuals

Embed screenshots or animations showing the component in action. Here is an example of how to include an image:

`![ComponentName Screenshot](url_to_screenshot)`

## Best Practices

Here, write about any best practices or recommendations for using your component.

## Technical Details

Discuss any technical details that are relevant to the component. This could include how the component manages its state, performance considerations, or any third-party libraries it relies on.
