# Layout XML

### How do I remove a block from a page?

The `<remove />` tag is only used to remove resources from the `<head>` block of a page, such as a css or js file. [See the docs.](http://devdocs.magento.com/guides/v2.1/frontend-dev-guide/layouts/xml-instructions.html)

To remove a block from a page, set the `remove` attribute to `true` on either a `referenceBlock` node or a `referenceContainer` node. [See the docs.](http://devdocs.magento.com/guides/v2.1/frontend-dev-guide/layouts/xml-instructions.html)

Example: This will remove the catalog compare sidebar block.
```xml
<?xml version="1.0"?>
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
    <body>
        <referenceBlock name="catalog.compare.sidebar" remove="true" />
    </body>
</page>
```
