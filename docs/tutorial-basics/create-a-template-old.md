---
sidebar_position: 1
sidebar_label: Create a Template Old Design
---

# Create a Template with Older Design System

Add **Template Files** files to following pages  to create a **standalone template**:
`code/server.js` -- we can Located where skins are being displayed

this piece of code, is how's the template is being displayed;
**please don't change code below**

``` javascript

  function getSkin(template) {
    var skins = Config.get('skins');
    if (skins[template]) return skins[template];
    else return '';
  }

 line:244 res.render('template.html'
 // an object given 
 skin: skin,


```

## Adding to our Default.json

File Direcotry   `config/default.json`

  ``` json
  "skins": {
   'template_name': 'template_name'
  }
  ```

Above we can see that need to apply our new template_name to our default.json file. This will allow us to use our new template_name.

### Adding Images for our new Template

File Directory `public/img/{template_name}`

These Images will be used for our new template.

- Note these would be provided by the design team, or you can use pre-existing images from the default template.

### Less Files are Created

- `less/{template_name}/components`
  - button.less
  - carousel.less
  - filters-bar.less
  - header.less
  - launcher.less
  - login-form.less
  - modal-details.less
  - modal-search.less
  - nav.less
  - product-caregoires.less
  - product-list.less
  - select-dealer.less
  - select-model.less
  - select-simple.less
  - select-trim.less
  - visualizer.less
  - wishlist.less
- `less/{template_name}/shared`
  - config.less
  - general.less
  - mixins.less
  - typography.less

#### Helpful Tip for Less Files

  Copy the previous template's less files and rename them to the new template name. Then, update the `@import` statements in `less/{template_name}/shared/general.less` to point to the new template name.

### Template Font Files

File Directory `public/webfontkit-{template_name}`
  **Please enquiry with the design team for any additional requirements. Design team will be provide fontkit**


### Template Rendering in Homepage 

If we have a new component that we want to render in the homepage, we need to add the component to the `code/client/components/Homepage.js` file.

**Please Take a look at the Homepage Component [Template Render Function](/docs/tutorial-components/Homepage#rendering-code-examples).**



This is the minimum data/asset requirements to have a new Retail Site Template created for use.
  **Please enquiry with the design team for any additional requirements**
Design Features:

- header logo (image file)
- header background color
- header text color
- homepage product selection images
- navigation background color
- navigation text color
- button background color
- product tile background color
- attach title font (preferably with eot, woff, woff2, ttf, svg)
- attach body font (preferably with eot, woff, woff2, ttf, svg)
- dropdown background color
- dropdown border color
- dropdown text color
- dropdown arrow color
- dropdown list background color
- dropdown list text color
- dropdown list border color
- dropdown list selected color
- dropdown list has border between options (yes or no)




