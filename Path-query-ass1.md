## What are path parameter

1. What are path parameters in FastAPI?
Answer: Path parameters are basically portions of a given URL that are used to capture specific values and then pass them to your API endpoint for processing.

2. How are path parameters defined in FastAPI route declarations?
Answer: Path parameters are defined within the URL path and marked by curly brace {}


3. Can path parameters have default values? If yes, how can they be set?
Answer: No

4. Provide an example of a FastAPI route with path parameters.
Answer:
``` python 
from fastapi import FastAPI
	App = FastApi()
	@app.get(“/items/{item_id}”)
	async def read_item(item_id:int):
		return {“item_id”: item_id}
```
6. What are query parameters in FastAPI?
Answer: Query parameter are key value pairs appended to the end of a URL, separated by a question mark and separated from each other by an ampersand. 

7. How are query parameters defined in FastAPI route declarations?
Answer: You can define a query parameter directly in the function section using python type hint.

8. What is the difference between path parameters and query parameters?
Answer: Path parameters are used for resource identification, while path query are you for filtering, sorting or providing additional data.

9. Can query parameters have default values? If yes, how can they be set?
Answer: Default parameters can be set in the function parameter declaration within the route declaration.

10. Provide an example of a FastAPI route with query parameters.
Combining Path and Query Parameters:
Answer:
``` python
from fastapi import FastAPI
	App = FastAPI()
	@app.get(“/items/”)
	Async def read_item(category: str = None, price_range: str = None):
return {“category”:category, “price_range”:price_range}
```
12. Can a FastAPI route have both path parameters and query parameters? If yes,
provide an example.
Answer:
``` python
from fastapi import FastAPI
	app = FastAPI()
	@app.get("/items/{item_id}")
	async def read_item(item_id: int, q: str = None):
			return {"item_id": item_id, "q": q}
```
14. What is the order of precedence if a parameter is defined both in the path and as
a query parameter?
Answer: The value in the path parameter takes precedence over the query parameter
Data Types and Validation:

15. How does FastAPI handle data types and validation for path and query
Parameters?
Answer: FastAPI automatically handles data types and validation for both path and query parameters based on the type annotations based on the type annotation provided in the route declaration.

16. What are some common data types that can be used for path and query
Parameters?
Answer: int, str, float

17. How can you enforce validation rules on path and query parameters in FastAPI?
Usage and Benefits:
Answer: You can enforce validation rules on path and query parameters using pydantic models. Benefits includes pydantic enforcing validation rules ensuring that the incoming data meets the format and constraint reducing errors and ensuring data integrity.

18. In what scenarios would you use path parameters over query parameters, and
vice versa?
Answer: In a case of resource identification its advisable to use path parameters, in case of filtering and sorting, query parameters are advisable.

19.  What are the benefits of using path and query parameters in API design?
Answer: They provide resource identification, sorting and filtering, searching among other things

20. Can you provide examples of real-world use cases where path and query parameters would be employed effectively?
Answer:/organizations{org_id}/projects/{project_id} => To access a specific project within an organization
Use-case: Path parameters can represent hierarchical relationships between resources, providing a clear structure for accessing nested or related data
Answer2: /products?category=electronics&brand=apple => to filter products by category and brand
Use-case: Query parameter allow clients to filter and sort data based on specific criteria, enabling customized data retrieval tailored to user preference.

Error Handling:
How does FastAPI handle errors related to missing or invalid path/query Parameters?
Answer: When an error occurs due to missing or invalid parameters, FastAPI automatically generates an appropriate error response with detailed information about the error.

Can you customize error responses for cases where required parameters are missing or validation fails?
Answer: Yes you can customize the error responses for cases where required parameters are missing or validation fails by defining custom exception handlers. FastAPI provides a convenient way to define custom exception handlers using the HTTPExeception class.
