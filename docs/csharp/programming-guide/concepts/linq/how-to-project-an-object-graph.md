---
title: 如何：投影对象图 (C#)
ms.date: 07/20/2015
ms.assetid: 293d15d5-3eaf-48de-9a02-3e13cb117b5b
ms.openlocfilehash: dcfdd8cba95d729a1f9bda3adb4b5fd8690b724a
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69592986"
---
# <a name="how-to-project-an-object-graph-c"></a>如何：投影对象图 (C#)
本主题演示如何从 XML 投影或填充对象图。  
  
## <a name="example"></a>示例  
 以下代码使用[示例 XML 文件中的 `Address`、`PurchaseOrder` 和 `PurchaseOrderItem` 类填充对象图：典型采购订单 (LINQ to XML)](./sample-xml-file-typical-purchase-order-linq-to-xml-1.md) XML 文档。  
  
```csharp  
class Address  
{  
    public enum AddressUse  
    {  
        Shipping,  
        Billing,  
    }  
  
    private AddressUse addressType;  
    private string name;  
    private string street;  
    private string city;  
    private string state;  
    private string zip;  
    private string country;  
  
    public AddressUse AddressType {  
        get { return addressType; } set { addressType = value; }  
    }  
  
    public string Name {  
        get { return name; } set { name = value; }  
    }  
  
    public string Street {  
        get { return street; } set { street = value; }  
    }  
  
    public string City {  
        get { return city; } set { city = value; }  
    }  
  
    public string State {  
        get { return state; } set { state = value; }  
    }  
  
    public string Zip {  
        get { return zip; } set { zip = value; }  
    }  
  
    public string Country {  
        get { return country; } set { country = value; }  
    }  
  
    public override string ToString()  
    {  
        StringBuilder sb = new StringBuilder();
        sb.Append($"Type: {(addressType == AddressUse.Shipping ? "Shipping" : "Billing")}\n");
        sb.Append($"Name: {name}\n");
        sb.Append($"Street: {street}\n");
        sb.Append($"City: {city}\n");
        sb.Append($"State: {state}\n");
        sb.Append($"Zip: {zip}\n");
        sb.Append($"Country: {country}\n");
        return sb.ToString();
    }  
}  
  
class PurchaseOrderItem  
{  
    private string partNumber;  
    private string productName;  
    private int quantity;  
    private Decimal usPrice;  
    private string comment;  
    private DateTime shipDate;  
  
    public string PartNumber {  
        get { return partNumber; } set { partNumber = value; }  
    }  
  
    public string ProductName {  
        get { return productName; } set { productName = value; }  
    }  
  
    public int Quantity {  
        get { return quantity; } set { quantity = value; }  
    }  
  
    public Decimal USPrice {  
        get { return usPrice; } set { usPrice = value; }  
    }  
  
    public string Comment {  
        get { return comment; } set { comment = value; }  
    }  
  
    public DateTime ShipDate {  
        get { return shipDate; } set { shipDate = value; }  
    }  
  
    public override string ToString()  
    {  
        StringBuilder sb = new StringBuilder();
        sb.Append($"PartNumber: {partNumber}\n");
        sb.Append($"ProductName: {productName}\n");
        sb.Append($"Quantity: {quantity}\n");
        sb.Append($"USPrice: {usPrice}\n");
        if (comment != null)
            sb.Append($"Comment: {comment}\n");
        if (shipDate != DateTime.MinValue)
            sb.Append($"ShipDate: {shipDate:d}\n");
        return sb.ToString();
    }  
}  
  
class PurchaseOrder  
{  
    private string purchaseOrderNumber;  
    private DateTime orderDate;  
    private string comment;  
    private List<Address> addresses;  
    private List<PurchaseOrderItem> items;  
  
    public string PurchaseOrderNumber {  
        get { return purchaseOrderNumber; } set { purchaseOrderNumber = value; }  
    }  
  
    public DateTime OrderDate {  
        get { return orderDate; } set { orderDate = value; }  
    }  
  
    public string Comment {  
        get { return comment; } set { comment = value; }  
    }  
  
    public List<Address> Addresses {  
        get { return addresses; } set { addresses = value; }  
    }  
  
    public List<PurchaseOrderItem> Items {  
        get { return items; } set { items = value; }  
    }  
  
    public override string ToString()  
    {  
        StringBuilder sb = new StringBuilder();
        sb.Append($"PurchaseOrderNumber: {purchaseOrderNumber}\n");
        sb.Append($"OrderDate: {orderDate:d}\n");
        sb.Append("\n");
        sb.Append("Addresses\n");
        sb.Append("=====\n");
        foreach (Address address in addresses)
        {
            sb.Append(address);
            sb.Append("\n");
        }
        sb.Append("Items\n");
        sb.Append("=====\n");
        foreach (PurchaseOrderItem item in items)
        {
            sb.Append(item);
            sb.Append("\n");
        }
        return sb.ToString();
    }  
}  
  
class Program {  
    public static void Main()  
    {  
        XElement po = XElement.Load("PurchaseOrder.xml");  
        PurchaseOrder purchaseOrder = new PurchaseOrder {  
            PurchaseOrderNumber = (string)po.Attribute("PurchaseOrderNumber"),  
            OrderDate = (DateTime)po.Attribute("OrderDate"),  
            Addresses = (  
                            from a in po.Elements("Address")  
                            select new Address {  
                                AddressType = ((string)a.Attribute("Type") == "Shipping") ?  
                                    Address.AddressUse.Shipping :   
                                    Address.AddressUse.Billing,  
                                Name = (string)a.Element("Name"),  
                                Street = (string)a.Element("Street"),  
                                City = (string)a.Element("City"),  
                                State = (string)a.Element("State"),  
                                Zip = (string)a.Element("Zip"),  
                                Country = (string)a.Element("Country")  
                            }  
                        ).ToList(),  
            Items = (  
                        from i in po.Element("Items").Elements("Item")  
                        select new PurchaseOrderItem {  
                            PartNumber = (string)i.Attribute("PartNumber"),  
                            ProductName = (string)i.Element("ProductName"),  
                            Quantity = (int)i.Element("Quantity"),  
                            USPrice = (Decimal)i.Element("USPrice"),  
                            Comment = (string)i.Element("Comment"),  
                            ShipDate = (i.Element("ShipDate") != null) ?  
                                (DateTime)i.Element("ShipDate") :  
                                DateTime.MinValue  
                        }  
                    ).ToList()  
        };  
        Console.WriteLine(purchaseOrder);  
    }  
}  
```  
  
 在此示例中，[!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询的结果以 <xref:System.Collections.Generic.IEnumerable%601> 的 `PurchaseOrderItem` 形式返回。 `PurchaseOrder` 类中各项的类型都是 <xref:System.Collections.Generic.IEnumerable%601> 的 `PurchaseOrderItem`。 该代码使用 <xref:System.Linq.Enumerable.ToList%2A> 扩展方法，根据查询结果来创建 <xref:System.Collections.Generic.List%601> 集合。  
  
 此示例产生以下输出：  
  
```  
PurchaseOrderNumber: 99503  
OrderDate: 10/20/1999  
  
Addresses  
=====  
Type: Shipping  
Name: Ellen Adams  
Street: 123 Maple Street  
City: Mill Valley  
State: CA  
Zip: 10999  
Country: USA  
  
Type: Billing  
Name: Tai Yee  
Street: 8 Oak Avenue  
City: Old Town  
State: PA  
Zip: 95819  
Country: USA  
  
Items  
=====  
PartNumber: 872-AA  
ProductName: Lawnmower  
Quantity: 1  
USPrice: 148.95  
Comment: Confirm this is electric  
  
PartNumber: 926-AA  
ProductName: Baby Monitor  
Quantity: 2  
USPrice: 39.98  
ShipDate: 5/21/1999  
```  
  
## <a name="see-also"></a>请参阅

- <xref:System.Linq.Enumerable.Select%2A>
- <xref:System.Linq.Enumerable.ToList%2A>
