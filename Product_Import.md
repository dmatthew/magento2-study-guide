# Product Import

### How do I import a product with values for multiple stores?

In your CSV import file create a separate row for each store view.

Example:
```
sku,store_view_code,product_type,name
simple-product-123,,simple,Default Name
simple-product-123,store1,simple,Store 1 Name
simple-product-123,store2,simple,Store 2 Name
```

### Importing select and multiselect attributes for multiple stores.

When importing select and multiselect attributes for non-admin stores the option value in the import file must be the value for the admin store, even if the store_view_code column is a non-admin store.

For example, you are importing a product with a color value of `red`, which has a value of `rojo` in your Spanish store. In your import file you would want to use `red` in the color column instead of `rojo`.

**Do this:**
```
sku,store_view_code,color
simple-product-123,,red
simple-product-123,spanish_store,red
```

**Not this:**
```
sku,store_view_code,color
simple-product-123,,red
simple-product-123,spanish_store,rojo
```

The code which causes this is [Magento\ImportExport\Model\Import\Entity\AbstractEntity::getAttributeOptions](https://github.com/magento/magento2/blob/develop/app/code/Magento/ImportExport/Model/Import/Entity/AbstractEntity.php#L488-L489).


### How do I add custom attributes to the import CSV?

The documentation shows an example with any extra attributes being added to an additional_attributes column where the structure is attribute_code=value,attribute_code2=value2. This is not needed, but it does work. You can also add custom attributes to the product import CSV file just add them as another column, just like any other column.

**This works:**
```
sku,custom_attribute,custom_attribute_2
abc-123,My Value,Some other value
```

**This also works:**
```
sku,additional_attributes
abc-123,custom_attribute=My Value,custom_attribute_2=Some other value
```

### How do I import configurable products?

You need to add a column `configurable_variations` with a structure like follows:
* sku=SIMPLE_PRODUCT_SKU,CONFIGURABLE_ATTRIBUTE_CODE=SIMPLE_PRODUCT_VALUE

Example:
```
sku,product_type,color,configurable_variations
abc-123,simple,Blue,
def-456,simple,Red,
abc,configurable,,"sku=abc-123,color=Blue|sku=def-456,color=Red"
```

### Can I change the attribute set of a Product using the Product Import process?

No, importing a product that already exists and setting its attribute_set_code column to a different value than it already is will not change its attribute set.

### How do I import images?

You can add the following columns to your import csv

|column|Description|
|---|---|
|base_image|The main image on the product view page.|
|base_image_label|Alt text for the base image.|
|small_image|The product image that is used on the category view page, as well as in related products and other product lists.|
|small_image_label|Alt text for the small image.|
|thumbnail_image|The product image that is used in the shopping cart, as well as in the media gallery no the product view page.|
|thumbnail_image_label|Alt text for the thumbnail image.|
|additional_images|A comma separated list of additional images. These will be used in the media gallery on the product view page.|
|additional_image_labels|A comma separated list of image labels. The labels should be in the same order as the images in the additional_images column.|

#### Uploading images

Images can be imported one of two ways:

1. Importing images from a local server.
  1. Upload images to your Magento server. The directory you upload them to defaults to `pub/media/import`, but you can use a different directory if you specify the relative path to that directory in the "Images File Directory" field when importing your products. In your import CSV file, enter the file name of you image within your "Images File Directory". Once your images are uploaded you can import your products.

1. Importing images from an external server.
  1. The import process can upload images to your server for you if you specify a url in your image columns. Just specify the url to your image and Magento will automatically download the image and save it on your server.
    1. NOTE: The image name will be the same as the url where the image was downloaded from, with certain characters removed. For example, if the image was downloaded from `http://www.example.com/images/my-image.jpg`, the new image file name will be `httpwww.example.comimagesmy-image.jpg`.

**NOTE**: If the image already exists, you may not be able to update its image label through the import process. Image labels may need to be updated through the Admin by editing a product directly. (I ran into this issue, but I cannot confirm if it is the actual behavior)
