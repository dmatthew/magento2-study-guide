# Object Repositories

#### Do not call $product->save() directly.
In Magento 1, if you had a product object, you could save it by calling $product->save(). This is a no-no in Magento 2. Currently in Magento 2.1, you can still use this method to save objects; however, the save method used by any model which extends the Magento\Framework\Model\AbstractModel class (which is a lot) is deprecated. Instead you should use object repository classes, such as `Magento\Catalog\Api\ProductRepositoryInterface`.

If you want to save an object, you should not call $object->save(). Instead you should use object repositories. For example, to save a product object, you would call \Magento\Catalog\Api\ProductRepositoryInterface::save($product). Magento guarantees that methods in interfaces with the @api notation will not change without a major version change. This means if you use an @api method, you can be sure that your code will not break until at least Magento 3.0.
