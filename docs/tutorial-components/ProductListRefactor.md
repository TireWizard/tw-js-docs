---
sidebar_position: 1
sidebar_label: ProductListRefactor
---

# ProductListRefactor Component

## Redux Toolkit State Below
<!-- 
```js title="ProductListRefactor.js redux/features/productList.js"
   // redux mapStateToProps function
      comparisonList:state.productList.comparisonList,
      comparisonLoadedSuccessfully:state.productList.comparisonLoadedSuccessfully,
      productList:state.productList.productList,
      partLoading:state.productList.productListLoaded,
      seasonCountArray:state.productList.seasonCountArray,
      selectedSeason:state.productList.selectedSeason,
      tireSizeSpecIdCountArray:state.productList.tireSizeSpecIdCountArray,
      tireListMaxPrice:state.productList.tireListMaxPrice,
      tireListMinPrice:state.productList.tireListMinPrice,
      loadRatingList:state.productList.loadRatingList,
      speedRatingList:state.productList.speedRatingList,
      plyRatingList:state.productList.plyRatingList,
      vehicleFullTireSizeInfo:state.productList.vehicleFullTireSizeInfo,
      tireSize:state.productList.subModelTireId,
      productFeaturedList:state.productList.productFeaturedList,
      filteredBrandIds:state.productList.filteredBrandIds,
      tireSizeFilters:state.productList.tireSizeFilters,
      accessoryCategoryShadowList:state.productList.accessoryCategoryShadowList,
      visualizerColours:state.productList.visualizerColours,
      visualizerForeground:state.productList.visualizerForeground,
      visualizerShadow:state.productList.visualizerShadow,
      colourCodes:state.productList.colourCodes,
      colourCodeInDetail:state.productList.colourCodeInDetail,
      filterByTireSize:state.productList.filterByTireSize,
      tireLoading:state.productList.reduxCall
``` -->

### When Updating the Component

```js title="ProductListRefactor.js componentDidUpdate
// if we need to make any update regarding the props, or current state

componentDidUpdate: function(lastProps, lastState) {
    if (this.props.tireLoading && 
    this.shouldLoadParts(lastProps lastState) // this function for any update to update the loadParts of the component 
    ) {
      this.loadParts(); // this will render the updated parts
    }

    this.shouldLoadParts 

```

## Product List Page Main Component

This component is the core component for the product list page. It provides a range of functionalities and deals with several sub-components.

## Core Functionalities

The component handles several key functionalities:

1. **Buy Now Button**: This feature enables instant purchasing of products.
2. **Add to Cart Button**: This feature allows users to add products to their shopping cart for future purchase.
3. **Add to Compare Button**:  It will allow users to add products to a comparison list.
4. **Add to Wishlist Button**: It will enable users to add products to a wishlist for future reference.
5. **Product List**: It will enable users to view a list of products that match their search criteria.

The component also deals with the product list and product list filters, providing users with a streamlined and user-friendly shopping experience.

## Child Components

Two significant child components that this main component interacts with are `<ProductTitle/>` and `<FilterPanel/>`.

1. **`<ProductTitle/>` Component**: This sub-component handles the display of the product title and the product image.
2. **`<FilterPanel/>` Component**: This sub-component manages the filter panel and its functionalities, allowing users to filter and sort the product list according to their preferences.
