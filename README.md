import json
import urllib.request
import urllib.parse

def get_weather(city):
    api_url = (
        "https://wttr.in/"
        + urllib.parse.quote(city)
        + "?format=j1"
    )

    try:
        request = urllib.request.Request(
            api_url,
            headers={"User-Agent": "Mozilla/5.0"}
        )

        with urllib.request.urlopen(
            request, timeout=10
        ) as response:
            data = json.loads(response.read())

        current = data["current_condition"][0]

        print("\n=== Weather Report ===")
        print(f"City: {city}")
        print(f"Temperature: {current['temp_C']} C")
        print(f"Feels like: {current['FeelsLikeC']} C")
        print(f"Humidity: {current['humidity']}%")
        print(
            "Condition:",
            current["weatherDesc"][0]["value"]
        )

    except Exception as error:
        print("Could not retrieve weather data.")
        print("Error:", error)

def main():
    print("=== Python Weather App ===")
    city = input("Enter city name: ").strip()

    if city:
        get_weather(city)
    else:
        print("Please enter a city name.")

if __name__ == "__main__":
    main()
