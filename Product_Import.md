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
