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

###### Prev & Next - pagination link in header
```php
if(Mage::registry('current_category') && !Mage::registry('current_product'))
{
    $category = Mage::registry('current_category');
    $prodCol = $category->getProductCollection()->addAttributeToFilter('status', 1)->addAttributeToFilter('visibility', array('in' => array(Mage_Catalog_Model_Product_Visibility::VISIBILITY_IN_CATALOG, Mage_Catalog_Model_Product_Visibility::VISIBILITY_BOTH)));
    $tool = $this->getLayout()->createBlock('page/html_pager')->setLimit($this->getLayout()->createBlock('catalog/product_list_toolbar')->getLimit())->setCollection($prodCol);
    $linkPrev = false;
    $linkNext = false;
    if ($tool->getCollection()->getSelectCountSql())
    {
        if ($tool->getLastPageNum() > 1)
        {
            if (!$tool->isFirstPage())
            {
                $linkPrev = true;
                if ($tool->getCurrentPage() == 2)
                {
                    $url = explode('?', $tool->getPreviousPageUrl());
                    $prevUrl = @$url[0];
                } else
                {
                    $prevUrl = $tool->getPreviousPageUrl();
                }
            }
            if (!$tool->isLastPage())
            {
                $linkNext = true;
                $nextUrl = $tool->getNextPageUrl();
            }
        }
    }
    if ($prevUrl) echo '<link rel="prev" href="' . htmlspecialchars($prevUrl, ENT_QUOTES, 'UTF-8') . '" />';
    if ($linkNext) echo '<link rel="next" href="' . htmlspecialchars($nextUrl, ENT_QUOTES, 'UTF-8') . '" />';
}
```
