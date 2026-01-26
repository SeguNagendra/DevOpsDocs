---
sidebar_position: 11
---

<!-- ## Working with APIs and JSON -->

### 1. What is an API?

API stands for **Application Programming Interface**. It's a way for different software systems to communicate with each other.

* For Python, we often use **REST APIs**.
* We use the `requests` module to interact with them.

### 2. Making HTTP Requests with `requests`

```python
import requests

# GET Request
response = requests.get('https://api.github.com')
print(response.status_code)
print(response.json())

# POST Request
payload = {"name": "Alice", "age": 25}
response = requests.post('https://httpbin.org/post', json=payload)
print(response.json())
```

---

### 3. Common HTTP Methods

* `GET`: Fetch data
* `POST`: Send new data
* `PUT`: Update existing data
* `DELETE`: Remove data

---

### 4. Working with Response Data

```python
response = requests.get('https://api.github.com')
data = response.json()
print(data['current_user_url'])
```

---

### 5. Status Codes

HTTP responses come with status codes:

* `200`: OK
* `404`: Not Found
* `500`: Server Error

```python
if response.status_code == 200:
    print("Success!")
else:
    print("Something went wrong")
```

---

### 6. Sending Query Parameters

```python
params = {"q": "python", "sort": "stars"}
response = requests.get("https://api.github.com/search/repositories", params=params)
print(response.url)  # Shows full URL with params
```

---

### 7. Headers and Authentication

Some APIs need headers like tokens or content-type.

```python
headers = {
    "Authorization": "Bearer your_token_here",
    "Content-Type": "application/json"
}
response = requests.get("https://api.example.com/data", headers=headers)
```

---

### 8. JSON Basics in Python

JSON = JavaScript Object Notation

* Python `dict` ⇔ JSON object
* Use `json` module

```python
import json

# Convert Python dict to JSON string
person = {"name": "Bob", "age": 30}
json_string = json.dumps(person)

# Convert JSON string to Python dict
parsed = json.loads(json_string)
print(parsed["name"])
```

---

### 9. Reading JSON from a File

```python
with open('data.json', 'r') as file:
    data = json.load(file)
print(data)
```

---

### 10. Writing JSON to a File

```python
person = {"name": "Eve", "age": 22}

with open('output.json', 'w') as file:
    json.dump(person, file)
```

---

### 11. Real-Time API Example: OpenWeatherMap

```python
API_KEY = 'your_api_key_here'
city = 'London'
url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={API_KEY}"

response = requests.get(url)
data = response.json()
print(data['weather'][0]['description'])
```

---

### 12. Handling API Errors

```python
try:
    response = requests.get('https://api.github.com/invalid')
    response.raise_for_status()
except requests.exceptions.HTTPError as err:
    print(f"HTTP Error: {err}")
```

---
