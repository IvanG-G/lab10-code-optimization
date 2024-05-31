# lab10-code-optimization

## **JavaScript Snippet:**

```Javascript
  // Inefficient loop handling and excessive DOM manipulation
function updateList(items) {
  let list = document.getElementById("itemList");
  list.innerHTML = "";
  for (let i = 0; i < items.length; i++) {
    let listItem = document.createElement("li");
    listItem.innerHTML = items[i];
    list.appendChild(listItem);
  }
}
```

* **Inefficient loops:** for loop can be enhance using parallel for each.
* **Redundant computations:** we are appending one entire list every time we create an element, we can enhance this adding an extra variable to save all the fragments of the documents.

```Javascript
function updateList(items) {
  const list = document.getElementById("itemList");
  const documentFragment = document.createDocumentFragment();
  listItem.innerHTML = "";

  items.async.forEach(item => {
    const listItem = document.createElement("li");
    listItem.innerHTML = item;
    documentFragment.appendChild(listItem);
  });

  list.appendChild(documentFragment);
}
```

1. Using async.each is a parallel loop equals to forEach, but improving the performance and adding readability on the code.
2. Separate the list.appendChild from the loop, and appending all the list at the end will ensure better perfomance.
3. Separate the entire documento into fragments, so within the loop we can only work around document fragments and not the entire document.


## **Java Snippet:**

```Java
// Redundant database queries
public class ProductLoader {
    public List<Product> loadProducts() {
        List<Product> products = new ArrayList<>();
        for (int id = 1; id <= 100; id++) {
            products.add(database.getProductById(id));
        }
        return products;
    }
}
```

* **Inefficient loops:** We are using a loop to obtain 100 list of products, when we can do that with one query directly to database.
* **Redundant computations:** products.add on every iteration is redundant, we should obtain an entire list.
* **Unoptimized database:** We should have a method that returns an entire list and not only an unique object.
  
```Java
public class ProductLoader {
    public List<Product> loadProducts() {
        return products = database.getProductListById(1, 100, Product.class)
    }
}


public interface Database{
    public T List<T> getProductListById(int startIndex, int numberOfElements, Class<T> entityClass);
}
```

1. Refactoring the method loadProducts we can optimize the code, using another method to obtain a list of items directly instead of only 1 item.
2. Using the interface as an example, we can send them the startIndex, and the number of elements that we need, in this case we will need 100, and then we also send the type of Class that we are retrieving from database, this to ensure we can retrieve multiple types of entities from database.


## **C# Snippet:**
```C#
// Unnecessary computations in data processing
public List<int> ProcessData(List<int> data) {
    List<int> result = new List<int>();
    foreach (var d in data) {
        if (d % 2 == 0) {
            result.Add(d * 2);
        } else {
            result.Add(d * 3);
        }
    }
    return result;
}
```
* **Inefficient loops:** Is better to use Parallel for each in this case.
* **Redundant computations:** result.Add is written two times on the code, we can enhance that to use only one .Add
* **Excessive memory:** We are not pre-allocating memory, we know the maximum capacity of the list, so we can pre-allocate memory increasing the performance on the code.

```C#
public List<int> ProcessData(List<int> data) {
    List<int> result = new List<int>(data.Count);

    Parallel.ForEach(data, d => {
        result.Add(d % 2 == 0 ? d * 2 : d * 3);
    }
    return result;
}
```

1. Adding a number to pre-allocate memory, we are sure that our list will not grow further than data.Count, so we can use that to pre-Allocate our memory, giving memory optimization.
2. Using ternary operator and adding at the same time, ternary operators are more readable, since we can only have if-else we can use them.
3. Multiplying d by 2 or 3 depending our case, and that result is added to the list directly so we are saving a variable that we could use on memory.
4. Paralle.ForEach is better than foreach loops, since we are not using the index, we can use forEach to improve the readability.
