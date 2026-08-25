+++
date = '2026-08-25T23:58:30+05:30'
draft = false
title = 'Chapter 01 First Web App'
+++

What's covered in this chapter:
1. Create a controller with request methods
2. Create a view using Thymeleaf template

## 1. Controller
### Product
```java
class Product {
    private String name;
    private double price;

    public void setName(String name) {
        this.name = name;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }
}
```

### Service
```java
@Service
class ProductService {
    
    public List<Product> findAll() {
        return List.of(
            new Product("Dell", 35000),
            new Product("Acer", 45000),
            new Product("Lenovo", 55000)
        );
    }
}
```

### Controller
```java
@Controller
class ProductController {

    private final ProductService productService;
    public ProductController(ProductService productService) {
        this.productService = productService;
    }
    
    @GetMapping("/products") 
    //@RequestMapping("/products", method = RequestMethod.GET) <- Alternative approach
    public String findAll(Model model) {
        List<Product> products = productService.findAll();
        model.addAttribute("products", products);
        return "products.html";
    }

    @PostMapping("/products")
    //@RequestMapping("/products", method = RequestMethod.POST) <- Alternative approach
    public String addProduct(@RequestParam("name") String name, @RequestParam("price") double price, Model model) {
        Product product = new Product();
        product.setName(name);
        product.setPrice(price);
        model.addAttribute("product", product);
        return "product.html";
    }
}
```

## 2. View

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://thymeleaf.org">

<head>
    <meta charset="UTF-8">
    <title>Home Page</title>
</head>

<body>
    <h2>Welcome to the product store!</h2>
    <table>
        <tr>
            <th>PRODUCT NAME</th>
            <th>PRODUCT PRICE</th>
        </tr>
        <tr th:each="product: ${products}">
            <td th:text="${product.name}"></td>
            <td th:text="${product.price}"></td>
        </tr>
    </table>

    <form action="/products" method="POST">
        <label for="name">Name: </label>
        <input type="text" name="name">
        <br>
        <label for="price">Price: </label>
        <input type="number" name="price">
        <br>
        <button type="submit">Add Product</button>
    </form>
</body>

</html>
```