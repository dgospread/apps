---
layout: content
title: Tablomat
---

Embed the Tablomat
===

Embed the Tablomat with the following code snipped. In the callback you get an application
instance to control the application from your script context or an error instance if any
error occurred.

```html
<script type="text/javascript" src="//spreadshirt.github.io/apps/spreadshirt.min.js"></script>
<script type="text/javascript">
    spreadshirt.create("tablomat", {
        shopId: 123456, // your shop id
        platform: "EU"  // or NA
        // ... additional parameter (see below)
    }, function(err, app) {

        if (err) {
            // something went wrong
            console.log(err);
        } else {
            // cool I can control the application (see below)
            app.setProductTypeId(6);
        }
    });
</script>
```

Parameters
---

The parameter shopId and platform should be present. You'll find your shopId in the user
area of spreadshirt. The platform decided if you like to speak with the European (EU) or the
North American (NA) platform.

All other parameters are optional and change the initialization of the application. E.g. you
could deeplink a specific productType (iPhone: 776) or add an image to the product. The
list of product types id, available appearances and designs you get from the
[API](https://developer.spreadshirt.net/display/API).

```js
var possibleParameter = {
    // required parameter
    shopId: 123456,         // your own shopId
    platform: "EU",         // the spreadshirt platform: "EU", "NA"

    // optional design deeplinks

    designUrl: null,        /* an URL to an image, it will be uploaded.
                             * **You agree that you will have the rights to use this image**
                             */
    designId: null,         // the id of an exisitng design
    designColor1: null,     // the printColor Id for layer 1
    designColor2: null,     //                       layer 2
    designColor3: null,     //                       layer 3
    designColorRgb1: null,  // or if you like RGB codes for the following layers
    designColorRgb2: null,
    designColorRgb3: null,

    // product relevant deeplinks
    productId: null,        // id of an existing product
    appearanceId: null,     // load the appearance (color) for the product type
    sizeId: null,           // preselect the product type size
    viewId: null,           // show this view of the product

    // product type
    productTypeId: null,    // start with the product type - cannot be used in combination with productId

    // text deeplinks
    tx1: null,              // first line of text
    tx2: null,              // second line of text ...
    tx3: null,              // ... and guess, the third line

    textColorRgb: null,     // you can specify colors either as rgb value
    textColor: null,        // or as id of an print type

    // independent
    departmentId: null,     // load this product type department
    productTypeCategoryId: null,    // or this product type category

    // also independent, but for designs
    designCategoryId: null, // open this designCategory
    designSearch: null,     // or perform a search for designs with the term

    panel: null             // show the following panel first - "productTypes", "designs", "upload", "imageNetwork"
}
```

Controlling the application
---

Beside the deeplinking feature, the Tablomat can be controlled during runtime by the
following methods. Each method has its own signature and is executed
*(due the limitations of the cross-domain boundary)* asynchronously. The return value
of the method can be get in a callback method, passed as the last parameter.

The signature of the callback looks always like `function(error, returnValue)`.

### Product type

```js
setProductType: function(productTypeId, callback) {
    // loads the product type by id & converts all configurations to the new product type
}

getProductType: function(callback) {
    // returns the id of the current product type
}

setAppearanceId: function(appearanceId, callback) {
    // switches to the appearance of the current product type

    // the returnValue will be true, if the appearnce is contained in the current product type, otherwise it will be false
}

getAppearanceId: function(callback) {
    // returns the id of the current product type appearance
}

getAppearanceColor: function(callback) {
    // returns the main color of the current appearance as hexadecimal rgb value
}
```

### Configurations

```js
deselectConfiguration: function() {
    // deselects the configuration, what else ?
}

addImage: function(url, callback) {
    // url to the image
    // AGAIN: you confirm that you have the rights to use this image
}

saveProduct: function(callback) {
    // returns the id of the current product when clicking the "add to basket" button
}
```
