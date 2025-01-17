# Python-week-eight
Weather Project


import requests

def get_weather(city, api_key):
    """
    Fetch weather data for a given city.
    """
    base_url = "http://api.openweathermap.org/data/2.5/weather"
    params = {
        "q": city,
        "appid": api_key,
        "units": "metric"  # Use "imperial" for Fahrenheit
    }
    response = requests.get(base_url, params=params)
    
    if response.status_code == 200:
        return response.json()
    else:
        print(f"Error: Unable to fetch weather data (HTTP {response.status_code})")
        return None

def display_weather(data):
    """
    Display weather information.
    """
    if data:
        city = data['name']
        country = data['sys']['country']
        temp = data['main']['temp']
        weather = data['weather'][0]['description']
        humidity = data['main']['humidity']
        wind_speed = data['wind']['speed']

        print(f"\nWeather in {city}, {country}:")
        print(f"Temperature: {temp}°C")
        print(f"Condition: {weather.capitalize()}")
        print(f"Humidity: {humidity}%")
        print(f"Wind Speed: {wind_speed} m/s")
    else:
        print("No data to display.")

def main():
    print("Welcome to the Weather Application!")
    api_key = "your_openweathermap_api_key"  # Replace with your API key
    while True:
        city = input("\nEnter the city name (or 'exit' to quit): ").strip()
        if city.lower() == 'exit':
            print("Thank you for using the Weather Application!")
            break
        
        weather_data = get_weather(city, api_key)
        display_weather(weather_data)

if __name__ == "__main__":
    main()

