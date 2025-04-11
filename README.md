# wave-height-measurement
import requests
import json

def get_wave_height(lat, lon):
    api_url = f"https://api.stormglass.io/v2/weather/point"
    api_key = "your_api_key_here"  # Replace with your actual API key
    
    params = {
        "lat": lat,
        "lng": lon,
        "params": "waveHeight",
    }
    
    headers = {
        "Authorization": api_key
    }
    
    response = requests.get(api_url, params=params, headers=headers)
    
    if response.status_code == 200:
        data = response.json()
        if "hours" in data:
            wave_heights = [hour["waveHeight"]["sg"] for hour in data["hours"] if "waveHeight" in hour]
            avg_wave_height = sum(wave_heights) / len(wave_heights) if wave_heights else 0
            return f"🌊 Average Wave Height in Miami: {avg_wave_height:.2f} meters"
        else:
            return "No wave height data available."
    else:
        return "Failed to fetch data. Check your API key or connection."

# Coordinates for Miami Beach, FL
latitude = 25.790654
longitude = -80.130045

# Example usage
print(get_wave_height(latitude, longitude))
екуери
