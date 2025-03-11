 2311CS030578--ArgiConnect
AgriConnect is a simple tool that helps farmers and fishermen track weather updates. It stores the latest 5 weather reports, allows quick city searches, and sorts data by temperature using Merge Sort. This helps in better planning for agriculture and fishing. It's easy to use and works even without the internet.

from collections import deque

class AgriConnect:
    def _init_(self):
        self.recent_reports = deque(maxlen=5)  # Stores last 5 reports
        self.weather_data = {}  # Dictionary to store weather info
    
    def add_weather_report(self, city, temperature, humidity, description):
        """Adds a weather report for a city."""
        report = {
            "city": city.capitalize(),
            "temperature": temperature,
            "humidity": humidity,
            "description": description
        }
        self.recent_reports.append(report)
        self.weather_data[city.lower()] = report
    
    def get_recent_reports(self):
        """Returns the last 5 weather reports."""
        return list(self.recent_reports)
    
    def search_weather(self, city):
        """Search for weather data using dictionary lookup."""
        return self.weather_data.get(city.lower(), "No data found")
    
    def merge_sort(self, data):
        """Sorts weather data by temperature using Merge Sort."""
        if len(data) <= 1:
            return data
        mid = len(data) // 2
        left, right = self.merge_sort(data[:mid]), self.merge_sort(data[mid:])
        sorted_list = []
        while left and right:
            sorted_list.append(left.pop(0) if left[0]["temperature"] < right[0]["temperature"] else right.pop(0))
        return sorted_list + left + right
    
    def get_sorted_weather(self):
        """Returns weather reports sorted by temperature."""
        return self.merge_sort(list(self.weather_data.values()))

# Example Usage
agri = AgriConnect()
agri.add_weather_report("Hyderabad", 32.5, 45, "Clear sky")
agri.add_weather_report("Mumbai", 30.2, 55, "Cloudy")
agri.add_weather_report("Delhi", 29.8, 50, "Haze")
agri.add_weather_report("Chennai", 34.0, 60, "Sunny")
agri.add_weather_report("Bangalore", 28.5, 48, "Partly cloudy")

# Display Outputs
print("Recent Reports:")
print(agri.get_recent_reports())

print("\nSearch Mumbai Weather:")
print(agri.search_weather("Mumbai"))

print("\nSorted Weather Reports (by Temperature):")
print(agri.get_sorted_weather())
