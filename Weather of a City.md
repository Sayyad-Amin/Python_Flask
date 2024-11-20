import requests

city = "Islamabad"
api_key = "your_openweathermap_api_key"
url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}"

response = requests.get(url)
data = response.json()

if data.get("cod") == 200:
    weather = data["weather"][0]["description"]
    print(f"Weather in {city} is: {weather}")
else:
    print(f"City {city} not found")
