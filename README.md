# Weather-forcasting
Vishal sharma / Ayekpam prithiviraj  project
import requests

def get_weather(api_key, city):
    base_url = "http://api.openweathermap.org/data/2.5/weather"
    params = {
        'q': city,
        'appid': api_key, 
        'units': 'metric'
    }
     
    response = requests.get(base_url, params=params)
    
    print(f"HTTP Status Code: {response.status_code}")
    print(f"Response Content: {response.text}")
    
    if response.status_code == 200:
        data = response.json()
        if data.get('cod') != 200:
            print(f"API Error: {data.get('message')}")
            return None
        
        main = data['main']
        weather = data['weather'][0]
        description = weather['description']
        temperature = main['temp']
        humidity = main['humidity']
        
        return {
            'description': description,
            'temperature': temperature,
            'humidity': humidity
        }
    else:
        return None

def print_weather(weather):
    if weather:
        print(f"Weather description: {weather['description']}")
        print(f"Temperature: {weather['temperature']}°C")
        print(f"Humidity: {weather['humidity']}%")
    else:
        print("Weather data not available.")

def main():
    api_key = '911fb33340872600e73bd3fd82fb1087'  
    city = input("Enter the city name: ")
    weather = get_weather(api_key, city)
    print_weather(weather)

if __name__ == "__main__":
    main()
