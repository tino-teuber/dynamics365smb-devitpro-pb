---
title: "ColumnFilter Property"
ms.custom: na
ms.date: 10/01/2020
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d8dc69ca-ba8f-4f9b-82fd-4976e26817f2
caps.latest.revision: 14
author: SusanneWindfeldPedersen
---

# ColumnFilter Property

Sets a filter on the column filter row of a query.  
  
## Applies to  

Query columns and filter rows  
  
## Property Value  

Filter expression.  
  
The filter expression must follow the required syntax. For more information, see [Entering Criteria in Filters](../devenv-entering-criteria-in-filters.md).  
  
## Remarks  

In a query, Columns and Filter rows specify fields of the underlying table of the parent DataItem. Columns appear in the resulting dataset, whereas Filter rows do not. You use a ColumnFilter property to apply a condition on a field to limit the records in query’s resulting dataset. The ColumnFilter property resembles the [DataItemTableFilter Property](devenv-dataitemtable-filter-property.md) of the DataItem, but there are differences. The ColumnFilter property has the following behavior:  
  
- Unlike filters that are set by the DataItemTableFilter property, filters that are set by the ColumnFilter property can be overwritten at runtime by calling the [SETFILTER Method (Query)](../methods-auto/query/queryinstance-setfilter-method.md) and [SETRANGE Method (Query)](../methods-auto/query/queryinstance-setrange-method.md) from AL code.  
  
     There can be multiple calls to the SETFILTER and SETRANGE methods in AL, but it is the first call in the method that overwrites the ColumnFilter property.  
  
- If the ColumnFilter property specifies a filter on the same field as the DataItemTableFilter property, then the filters of the two properties are combined. In SQL SELECT statements, this combination corresponds to an AND operator. To be included in the query dataset, records must meet the condition of both the filters. For example, if the DataItemTableFilter property sets a filter on a field to include values less than fifty (<50) and the ColumnFilter property sets a filter on the same field to include values greater than twenty (>20), then the resultant filter on the field includes values that are greater than twenty and less than fifty (20< value <50). However, if the same field is also set with a filter from AL code by calling the SETFILTER or SETRANGE methods, then only the DataItemTableFilter property filter is applied because, even though the method overwrites the ColumnFilter property filter, the method filter is ignored.  
  
- You can set the ColumnFilter property on any Column or Filter row in the query, this includes columns that are set with the totaling method using the [Method Property](devenv-method-property.md).  
  
- In an SQL SELECT statement, a filter that is set by the ColumnFilter property that is not applied a totaling method would correspond to a WHERE clause. A filter on a column that is applied a totaling method would correspond to a HAVING clause.  
  
## Example  

The following example sets a filter on the ColumnFilter property of the Quantity column of a query so that the resulting dataset will only include records where the value of the Quantity column is between 20 and 50.  
  
```AL
Quantity=FILTER(>20&<50);  
```  

## See Also

[Properties](devenv-properties.md)  