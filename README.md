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

```Javascript
function updateList(items) {
  const list = document.getElementById("itemList");
  const documentFragment = document.createDocumentFragment();
  listItem.innerHTML = "";

  items.forEach(item => {
    const listItem = document.createElement("li");
    listItem.innerHTML = item;
    documentFragment.appendChild(listItem);
  });

  list.appendChild(documentFragment);
}
```
1. Using For each in this case is better than using a for.
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
2. Using the interface as an example, we can send them the startIndex, and the number of elements that we need, in this case we will need 100, and then we also send the type of Class that we are retrieving from database, this to ensure we can retrieve multiple entities from database.

