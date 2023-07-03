- 👋 Hi, I’m @slimecoding2025
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
slimecoding2025/slimecoding2025 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
C.py
import requests
import json

def get_user_location():
    return input("Enter your location: ")

def get_weather_data(api_key, location):
    api_url = f"http://api.openweathermap.org/data/2.5/weather?q={location}&appid={api_key}"
    response = requests.get(api_url)
    if response.status_code == 200:
        return response.text
    else:
        raise IOError(f"Failed to retrieve weather data. Response Code: {response.status_code}")

def extract_temperature(weather_data):
    data = json.loads(weather_data)
    temperature_kelvin = data['main']['temp']
    temperature_celsius = temperature_kelvin - 273.15
    return f"{temperature_celsius:.1f}"

def main():
    try:
        api_key = "YOUR_API_KEY"  # Replace with your OpenWeatherMap API key
        location = get_user_location()

        weather_data = get_weather_data(api_key, location)
        temperature = extract_temperature(weather_data)

        print(f"Location: {location}")
        print(f"Temperature: {temperature}°C")
    except Exception as e:
        print(f"An error occurred while fetching weather data: {str(e)}")

if __name__ == "__main__":
    main()
