# magento1snipplets
Some quickies about M1

###### How to get cart items total
```php
<?php echo Mage::helper('checkout/cart')->getItemsCount();?>
```

###### Is this a product page
```php
if(Mage::registry('current_product'))
{
}
```

###### Is this a category page
```php
if(Mage::registry('current_category') && !Mage::registry('current_product'))
{
}
```

###### Is this the homepage
```php
if (Mage::getBlockSingleton('page/html_header')->getIsHomePage())
{
}
```
