---
sidebar_position: 3
---

# Live Debuging Session TireWizards

We currently are experiencing a bug in TireWizards where the user can not use the FilterPanel to filter though TireSize.
We will be using the Chrome Dev Tools to debug the issue, and React Dev Tools to inspect the React Components.

## Problem Statement

We have encountered a bug in the TireWizards application. The user is unable to utilize the **FilterPanel** to filter through **TireSize**. To resolve this issue, we will be using Chrome Dev Tools for debugging, and React Dev Tools to inspect our React Components.

## Debugging Procedure

### Step 1: Inspecting React Components with React Dev Tools

1. Launch the Chrome Dev Tools.
2. Navigate to the React tab.
3. Inspect the FilterPanel component.
4. Go back to the Elements tab.
5. Identify the parent component of FilterPanel, which is ProductListRefactor.

### Step 2: Locating and Addressing the Problematic Component

1. Identify the problematic component, in our case FilterPanel.
2. Understand its relation with the parent component ProductListRefactor.
3. Look for the `<FilterPanel>` within the ProductListRefactor component.
4. Determine that the issue resides in the rendering of the list props of FilterPanel when the list is empty.

Here is a code snippet from `ProductListRefactor.js`:

```jsx title="ProductListRefactor.js"

// Our Current code
    console.log('tireSizeSpecIdCountArray',getFilteredTiresizeList(this.props.vehicleFullTireSizeInfo,this.state.tireSizeSpecIdCountArray))
    // we are getting a return of an empty array

            <FilterPanel onSelect={this.onTiresizeFilter} title={this.t('product.tireSize')} list={getFilteredTiresizeList(this.props.vehicleFullTireSizeInfo,this.state.tireSizeSpecIdCountArray)} countList={this.state.tireSizeSpecIdCountArray} initial={this.props.tireSizeFilters} open={true} single={true} />

```

### Identified Issue

The problem lies in the fact that the list is empty, which causes the component not to render the `list` prop.

### Proposed Solution

The next step is to investigate why the list is empty and to ascertain why the `FilterPanel` component isn't rendering the `list` prop when it's empty. We need to ensure that the `getFilteredTiresizeList` function returns a non-empty array, and if it does return an empty array, the FilterPanel component should have a mechanism to handle this gracefully.

We need to find out why the list is empty, and why the component is not rendering the list prop

:::info When comparing your development process, make sure to adhere to the following guidelines

- Always ensure to compare your current Development Branch, which in our case is the redux branch.

- For comparison, either checkout or use a comparison tool to analyze the differences with the staggered-stock branch.

:::

### Step 3: Debugging the Issue

```js title="ServiceVehicle.js"
export const getFilteredTiresizeList = function(list = [],countList=[]) {
  let info = list;
  var temp = [];
//  console log list and countList 

    console.log('list',list)
    console.log('countList',countList)
    // This will allow to insure that we are getting the correct data


  for (var i in info) {
    if (info[i] && countList.hasOwnProperty(info[i]['vehicleSubmodelTiresizeId'])) {
      temp.push({ key: info[i]['vehicleSubmodelTiresizeId'], value: getTiresizeListValue(info[i]['vehicleSubmodelTiresizeId'],info) });
    }
  }
  return sortTiresizeList(temp,info);
};

```

During our initial process, we identified certain findings from the staggered-stock branch that gave us important insights.  document Bugs to  accurately identify the issue and to provide a solution.

This approach aids in comprehending the changes, additions, and removals between the two branches, thus promoting effective version control and streamlined development. Understanding these differences also helps to identify any discrepancies and provide insights for enhancements or bug resolutions.

```json title="Current Data"
// our Expected Values 

 [
    {
        "key": "103044",
        "value": "255/65R17 / Original Size - Has Wheels"
    },
    {
        "key": "103043",
        "value": "265/65R17 / Alternate Size - Has Wheels"
    },
    {
        "key": "103045",
        "value": "265/60R18 / Original Size"
    }
]
// Currently Values 

[
    {
        "key": "103044",
        "value": "Undefined / Undefined"
    },
    {
        "key": "103043",
        "value": "Undefined / Undefined"
    },
    {
        "key": "103045",
        "value": "Undefined / Undefined"
    }
]

```

```js title="VehicleService.js"

const getTiresizeListValue = function(tiresize,list) {
  var temp = '', info = productListStore.data.vehicleFullTireSizeInfo;
  for (var i in list) {
    if (list[i]) {
      if (list[i].secondaryTireSizeSpecId == 0) {
        if (list[i].vehicleSubmodelTiresizeId == tiresize) {

          temp = list[i].formattedTireSize + getTypeDescription(list[i]) + (list[i].hasWheels == "1" && displayHasWheels() ? getHasWheelsText() : "");

        }
      } else {
        if (list[i].vehicleSubmodelTiresizeId == tiresize) {
          var dictionary = languageStore.getDictionary();

          temp = dictionary.product.front + ': ' + list[i].formattedTireSize + ' ' + dictionary.product.rear + ': ' + list[i].secondaryFormattedTireSize + getTypeDescription(list[i]) + (list[i].hasWheels == "1" && displayHasWheels() ? getHasWheelsText() : "");

        }
      }
    }
  }
  return temp;
};

```

During our initial debugging process, we identified that three values - formattedTireSize, sizeTypeDescription, and hasWheels  were not present in our initial state.

The problem lies in the **extractTireSizeInfo** function within `VehicleService.js`. The function currently omits the `formattedTireSize`, `sizeTypeDescription`, and hasWheels values when transforming `vehicleFullTireSizeInfo`.

```js title="service/VehicleService.js"
export const extractTireSizeInfo= (payload)=>{


  let {vehicleId,vehicleFullTireSizeInfo,vehicleOriginalTiresize} = payload;

  let _vehicleFullTireSizeInfo = _.map(vehicleFullTireSizeInfo,function (tireInfo) {
    return {
      id: tireInfo.vehicleSubmodelTiresizeId,
      tireSizeSpecId: tireInfo.tireSizeSpecId,
      secondaryTireSizeSpecId: tireInfo.secondaryTireSizeSpecId,
      tireSize: tireInfo.formattedTireSize,
      secondaryTireSize: tireInfo.secondaryFormattedTireSize,
      sizeType: tireInfo.sizeTypeCode,
      seasonType: tireInfo.seasonalSizeCode
    };
  });
  return {
    vehicleId,
    vehicleFullTireSizeInfo:_vehicleFullTireSizeInfo,
    vehicleOriginalTiresize
  };
};

```
### Solution 

To address this issue, we can revise the function to include the missing properties. 
The function will now look as follows:

``` js title="Solution"

 let {vehicleId,vehicleFullTireSizeInfo,vehicleOriginalTiresize} = payload;

  let _vehicleFullTireSizeInfo = _.map(vehicleFullTireSizeInfo,function (tireInfo) {
    return {
      ...tireInfo,
      id: tireInfo.vehicleSubmodelTiresizeId,
      tireSizeSpecId: tireInfo.tireSizeSpecId,
      secondaryTireSizeSpecId: tireInfo.secondaryTireSizeSpecId,
      tireSize: tireInfo.formattedTireSize,
      secondaryTireSize: tireInfo.secondaryFormattedTireSize,
      sizeType: tireInfo.sizeTypeCode,
      seasonType: tireInfo.seasonalSizeCode
      seasonType: tireInfo.seasonalSizeCode,
      vehicleSubmodelTiresizeId:tireInfo.vehicleSubmodelTiresizeId,
      formattedTireSize:tireInfo.formattedTireSize,
      sizeTypeDescription:tireInfo.sizeTypeDescription,
      hasWheels:tireInfo.hasWheels,
    };
  });
  ```

In this improved version, we've included the missing payload key-value pairs. We've added the missing values to the object to ensure all necessary properties are present in the transformed `vehicleFullTireSizeInfo` array.


If needed to Install[React Dev Tools Extension](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)
