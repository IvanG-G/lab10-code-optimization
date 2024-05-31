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
  const fragment = document.createDocumentFragment();

  items.forEach(item => {
    const listItem = document.createElement("li");
    listItem.textContent = item;
    fragment.appendChild(listItem);
  });

  list.textContent = '';
  list.appendChild(fragment);
}
```

