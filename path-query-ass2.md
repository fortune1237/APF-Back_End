Code Writing: Path Parameters
## What are query parameters
1. Write a FastAPI route that accepts a path parameter for user identification (user_id) and returns the user's profile information.
Answer:
``` python
from fastapi import FastAPI
          app = FastAPI()

          @app.get("/users/{user_id})
          async def read_user(user_id)
            return {"user_id": user_id}
```
3. Implement error handling for the case when the user_id path parameter is missing.
Answer:
``` python
from fastapi import FastAPI, HTTPException
        app = FastAPI()

        @app.get("/users/{user_id}")
        async def read_user(user_id: str):
          if user_id == NONE
            raise HTTPException (status_code = 404, detail = "user not found")
          return{"user_id" user_id}
```
Code Writing: Query Parameters
3. Create a FastAPI route that accepts query parameters for filtering a list of products by category and price range.
Answer: 
``` python
from fastapi import FastAPI, Query

app = FastAPI()

# Sample product data
products = [
    {"id": 1, "name": "TV", "category": "Electronics", "price": 100},
    {"id": 2, "name": "T-shirt", "category": "Clothing", "price": 50},
    {"id": 3, "name": "Laptop", "category": "Electronics", "price": 200},
    {"id": 4, "name": "RDPD", "category": "Books", "price": 30},
]

@app.get("/products")
async def get_products(category: str = None, min_price: float = None, max_price: float = None):
    print("Received request with:")
    print("Category:", category)
    print("Min Price:", min_price)
    print("Max Price:", max_price)

    filtered_products = products

    # Filter by category if provided
    if category:
        category = category.lower()  # Convert category to lowercase
        print("Category converted to lowercase:", category)2  
        filtered_products = [p for p in filtered_products if p["category"].lower() == category]

    # Filter by price range if provided
    if min_price is not None:
        filtered_products = [p for p in filtered_products if p["price"] >= min_price]
    if max_price is not None:
        filtered_products = [p for p in filtered_products if p["price"] <= max_price]

    print("Filtered Products:", filtered_products)

    return filtered_products

```
4. Implement default values for the query parameters (category defaulting to 'all' and price_range defaulting to a specific range).
Answer:
``` python
from fastapi import FastAPI, Query

    app = FastAPI()

    # Sample product data
    products = [
        {"id": 1, "name": "TV", "category": "Electronics", "price": 100},
        {"id": 2, "name": "T-Shirt", "category": "Clothing", "price": 50},
        {"id": 3, "name": "Laptop", "category": "Electronics", "price": 200},
        {"id": 4, "name": "RDPD", "category": "Books", "price": 30},
    ]

    @app.get("/products")
    async def get_products(category: str = Query('all', description="Filter by category (default: all)"),
                          min_price: float = Query(0, description="Minimum price (default: 0)"),
                          max_price: float = Query(9999, description="Maximum price (default: 9999)")):
        filtered_products = products

        # Filter by category if provided
        if category != 'all':
            filtered_products = [p for p in filtered_products if p["category"] == category]

        # Filter by price range if provided
        filtered_products = [p for p in filtered_products if min_price <= p["price"] <= max_price]

        return filtered_products
```
## Combining Path and Query Parameters:
5. Write a FastAPI route that accepts a path parameter for city (city_id) and query parameters for filtering restaurants by cuisine type (cuisine) and rating (min_rating).
Answer:
``` python
from fastapi import FastAPI, Query

    app = FastAPI()

    restaurants = [
        {"id": 1, "name": "Transcorp", "city_id": "1", "cuisine": "Italian", "rating": 4.5},
        {"id": 2, "name": "Chinox", "city_id": "1", "cuisine": "Mexican", "rating": 4.0},
        {"id": 3, "name": "City_link", "city_id": "2", "cuisine": "Chinese", "rating": 4.2},
        {"id": 4, "name": "Gold_Touch", "city_id": "2", "cuisine": "Italian", "rating": 4.8},
    ]

    @app.get("/restaurants/{city_id}")
    async def get_restaurants(city_id: str, cuisine: str = None, min_rating: float = None):
        filtered_restaurants = [r for r in restaurants if r["city_id"] == city_id]

        if cuisine:
            filtered_restaurants = [r for r in filtered_restaurants if r["cuisine"] == cuisine]

        if min_rating is not None:
            filtered_restaurants = [r for r in filtered_restaurants if r["rating"] >= min_rating]

        return filtered_restaurants
```
6. Ensure that the city ID is a path parameter while cuisine type and minimum rating
are query parameters.
Answer:
``` python
from fastapi import FastAPI, Query

    app = FastAPI()

        restaurants = [
        {"id": 1, "name": "Transcorp", "city_id": "1", "cuisine": "Italian", "rating": 4.5},
        {"id": 2, "name": "Chinox", "city_id": "1", "cuisine": "Mexican", "rating": 4.0},
        {"id": 3, "name": "City_link", "city_id": "2", "cuisine": "Chinese", "rating": 4.2},
        {"id": 4, "name": "Gold_Touch", "city_id": "2", "cuisine": "Italian", "rating": 4.8},
    ]

    @app.get("/restaurants/{city_id}")
    async def get_restaurants(city_id: str, 
                              cuisine: str = Query(None, description="Filter by cuisine type"), 
                              min_rating: float = Query(None, description="Filter by minimum rating")):
        filtered_restaurants = [r for r in restaurants if r["city_id"] == city_id]

        if cuisine:
            filtered_restaurants = [r for r in filtered_restaurants if r["cuisine"] == cuisine]

        if min_rating is not None:
            filtered_restaurants = [r for r in filtered_restaurants if r["rating"] >= min_rating]

        return filtered_restaurants
```
## Data Validation:
7. Modify an existing FastAPI route that accepts a path parameter for user_id to ensure that user_id is an integer and greater than zero.
Answer:
``` python
from fastapi import FastAPI, Path

    app = FastAPI()

    @app.get("/users/{user_id}")
    async def read_user(user_id: int = Path(..., title="User ID", description="The ID of the user (greater than zero)", gt=0)):
        return {"user_id": user_id}
```
9. Add validation to a query parameter start_date to ensure it is a valid date format. Usage and Benefits:
Answer:
``` python
from fastapi import FastAPI, Query
from datetime import datetime

    app = FastAPI()

    @app.get("/events/")
    async def get_events(start_date: datetime = Query(..., title="Start Date", description="Start date for filtering events")):
        return {"start_date": start_date}
```
11. Analyze a given FastAPI application and identify instances where using path
parameters would be more appropriate than query parameters, and vice versa.
Answer:
``` python
from fastapi import FastAPI, Path, Query

    app = FastAPI()

    @app.get("/users/{user_id}")
    async def get_user(user_id: int = Path(..., title="User ID", description="The ID of the user")):
        return {"user_id": user_id}

    @app.get("/items/")
    async def get_items(category: str = Query(None, title="Category", description="Filter by category")):
        return {"category": category}
```
10.Discuss the benefits of using path and query parameters in the provided FastAPI application and how it enhances API design.
Answer: 
## Benefits of Using Path Parameters:

1. Semantic Clarity: Path parameters are integral parts of the endpoint's URL, making the purpose of the API endpoint clear and explicit. For example, in /users/{user_id}, it's evident that we're retrieving information about a specific user identified by user_id.

2. SEO Friendly: Path parameters can improve the search engine optimization (SEO) of your API by including relevant keywords in the URL. This can make your API more discoverable and accessible to users searching for specific resources.

3. Hierarchical Structure: Path parameters are ideal for representing hierarchical relationships between resources. For instance, /users/{user_id}/posts suggests that we're fetching posts belonging to a specific user, maintaining a logical structure.

4. Caching: Path parameters can be utilized for caching responses at different levels (e.g., CDN caching), as the URL remains consistent for a given resource. This can improve performance and reduce server load by serving cached responses for repeated requests.

## Benefits of Using Query Parameters:

1. Flexibility: Query parameters provide flexibility by allowing users to include additional parameters in the URL without affecting the overall structure. Users can choose which parameters to include based on their specific requirements.

2. Filtering and Pagination: Query parameters are commonly used for filtering, sorting, and pagination, enabling users to narrow down search results or retrieve specific subsets of data. For example, /items/?category=electronics filters items by category.

3. Optional Parameters: Query parameters are optional, meaning users can choose whether to include them in the request or not. This simplifies the API usage, as users can customize their requests based on their needs without being constrained by mandatory parameters.

4. Backward Compatibility: Adding new query parameters to an existing endpoint typically doesn't break existing client implementations, as clients can ignore unknown parameters. This promotes backward compatibility and facilitates API evolution over time.

# Enhancements to API Design:

1. Clarity and Readability: By appropriately using path and query parameters, API endpoints become more descriptive and readable, enhancing developer experience and reducing the learning curve for API consumers.

2. Scalability and Maintainability: Well-designed APIs with clear separation of concerns using path and query parameters are easier to scale and maintain over time. They facilitate modular development and allow for incremental enhancements without impacting existing functionality.

3. User Experience: By providing options for both path and query parameters, API designers empower users to interact with the API in a way that best suits their preferences and requirements. This fosters a positive user experience and encourages adoption of the API.

In conclusion, leveraging path and query parameters in FastAPI enhances API design by improving semantic clarity, providing flexibility, supporting filtering and pagination, and facilitating scalability and maintainability. Understanding when and how to use each type of parameter is key to designing intuitive, efficient, and user-friendly APIs
