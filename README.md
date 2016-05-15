## MyWeather.Forms

This is a small sample application showing how to query OpenWeatherMap.org to gather weather for a current location.

Built with C# 6 features, you must be running VS 2015 or Xamarin Studio to compile.

Built with Xamarin.Forms with support for:
* iOS
* Android
* UWP

Grabs current weather and 5 day forecast.

![](Images/promo.png)

## โครงสร้างโปรเจค

```
├── MyWeather
│   ├── App.cs
│   ├── Helpers
│   │   └── Settings.cs
│   ├── Model
│   │   └── Weather.cs
│   ├── Properties
│   │   └── AssemblyInfo.cs
│   ├── Services
│   │   └── WeatherService.cs
│   ├── View
│   │   ├── ForecastView.xaml
│   │   ├── ForecastView.xaml.cs
│   │   ├── WeatherView.xaml
│   │   └── WeatherView.xaml.cs
│   └── ViewModel
│       └── WeatherViewModel.cs
└── MyWeather.iOS
    ├── AppDelegate.cs
    ├── Helpers
    │   └── Settings.cs
    └── Main.cs
```

## Api เกี่ยวข้อง

- Xam.Plugins.Settings - https://github.com/jamesmontemagno/Xamarin.Plugins/tree/master/Settings

## ตัวอย่าง Api ใน WeatherService.cs

```csharp
const string WeatherCoordinatesUri = "http://api.openweathermap.org/data/2.5/weather?lat={0}&lon={1}&units={2}&appid=fc9f6c524fc093759cd28d41fda89a1b";
const string WeatherCityUri = "http://api.openweathermap.org/data/2.5/weather?q={0}&units={1}&appid=fc9f6c524fc093759cd28d41fda89a1b";
const string ForecaseUri = "http://api.openweathermap.org/data/2.5/forecast?id={0}&units={1}&appid=fc9f6c524fc093759cd28d41fda89a1b";

public async Task<WeatherRoot> GetWeather(double latitude, double longitude, Units units = Units.Imperial) {
    using (var client = new HttpClient()) {
        var url = string.Format(WeatherCoordinatesUri, latitude, longitude, units.ToString().ToLower());
        var json = await client.GetStringAsync(url);

        if (string.IsNullOrWhiteSpace(json))
            return null;

        return DeserializeObject<WeatherRoot>(json);
    }
}
```