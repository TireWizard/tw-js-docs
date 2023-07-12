---
sidebar_position: 10
sidebar_label: 'HomePage'
---

# Homepage

## Description

Homepage allow to render the homepage of the website. It is the first page that the user will see when he will access the website.

## State

| State Name | Type | Default | Description |
|---|---|---|---|
| carouselItems | array  | [] | List of items to display in the carousel |
| featuredItems | array  | [] | List of items to display in the featured section |
| carousel | object  | {} | Carousel object |
| carouselIndex | number  | 0 | Index of the carousel item to display |
| lastCarouselIndex | number  | 0 | Index of the last carousel item |
| allowSwitching | boolean  | true | Allow switching between carousel items |
| switchingFunction | function  | () => {} | Function to call when switching between carousel items |
| yearlist | array  | [] | List of years to display in the year list |
| yearselect | number  | 0 | Year selected in the year list |
| yearselected | boolean  | false | Is a year selected in the year list |
| partList | array  | [] | List of parts to display in the part list |
| partListShowAll | boolean  | false | Show all parts in the part list |
| initialized | boolean  | false | Is the component initialized |
<!-- ## Props

| Prop Name | Type | Default | Description |
|---|---|---|---|
| prop1  | type  | default value | description |
| prop2  | type  | default value | description | -->

<!-- ## Detailed Props Explanation

For complex props, write a more detailed explanation here. -->

<!-- ### prop1

Here, explain in detail about prop1.

### prop2

Here, explain in detail about prop2. -->

## Rendering Code Examples

Provide examples of how to use the component.

```jsx

  render: function() {
    switch(defaultTemplate) {
      case 'audi_2021':
        return this.renderHomepageAudi();
      case 'hyundai':
        return this.renderHomepageHyundai();
      case 'kia_2021':
        return this.renderHomepageKia();
      case 'mazda':
        return this.renderHomepageReduced();
      case 'volkswagen':
        return this.renderHomepageRefactor();
      case "mercedes_2022":
        return this.renderHomepageMercedes();
      case 'volkswagen_2020':
        return this.renderHomepageVolkswagen();
      default:
        return this.renderHomepage();
    }
  },

```

Please note that the render function is not the same in the different templates. The code above is the render function of the default template.
:::tip Created a new template
If a new template is added, please add the render function of the new template in the code example.

:::

## Carousel/ Landing Image Code Examples

 ```js title="Homepage.jsx"
  renderCarousel: function() {
    if (this.state.carousel && sizeOf(this.state.carouselItems) > 0) {
      return renderCarousel(this.state.carouselItems, false, this.state.carouselIndex, this.state.lastCarouselIndex, this.setCarouselIndex);
    } else {
      return false;
    }
  },

  ```

<!-- ## Interactive Playground

Provide a link to the interactive playground if it exists, or embed a live demo if possible.

## Visuals

Embed screenshots or animations showing the component in action. Here is an example of how to include an image: -->

`![ComponentName Screenshot](url_to_screenshot)`

<!-- ## Best Practices

Here, write about any best practices or recommendations for using your component. -->

## Technical Details

Discuss any technical details that are relevant to the component. This could include how the component manages its state, performance considerations, or any third-party libraries it relies on.
