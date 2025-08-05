# Real-Time Weather AQI Monitoring Dashboard

A comprehensive Power BI dashboard that integrates live weather data and Air Quality Index (AQI) monitoring using WeatherAPI. This project demonstrates how to build dynamic, real-time visualizations with interactive features and health-based recommendations.

## 🌟 Features

- **Real-time Weather Data**: Live temperature, humidity, wind speed, and weather conditions
- **Air Quality Monitoring**: Complete AQI tracking with color-coded indicators
- **Interactive City Selection**: Dynamic filtering and city-based comparisons
- **Health Recommendations**: Smart suggestions based on AQI levels
- **Responsive Design**: Clean, professional dashboard layout
- **Reusable Components**: Template DAX measures for easy scalability

## 📊 Dashboard Components

### Weather Metrics
- Current temperature and "feels like" temperature
- Humidity and atmospheric pressure
- Wind speed and direction
- Weather condition icons and descriptions

### Air Quality Index (AQI)
- PM2.5, CO, NO2, SO2, and O3 levels
- Color-coded status indicators (Good to Hazardous)
- Health-based activity recommendations
- Historical trend visualization

### Interactive Features
- City selection slicers
- Map visualizations with location markers
- Dynamic filtering capabilities
- Real-time data refresh

## 🛠️ Prerequisites

- **WeatherAPI Account**: Free or paid account at [WeatherAPI.com](https://weatherapi.com)
- **Power BI Desktop**: Latest version installed
- **Basic Power BI Knowledge**: Understanding of data models and Power Query
- **Internet Connection**: For real-time data fetching

## 🚀 Quick Start

### 1. Get Your WeatherAPI Key
1. Sign up at [WeatherAPI.com](https://weatherapi.com)
2. Navigate to your dashboard and copy your API key
3. Keep this key secure for authentication

### 2. Set Up the Data Connection
1. Open Power BI Desktop
2. Click **Get Data** → **Web**
3. Enter the API URL:
   ```
   https://api.weatherapi.com/v1/current.json?key=YOUR_API_KEY&q=CITY_NAME
   ```
4. Replace `YOUR_API_KEY` with your actual key
5. Replace `CITY_NAME` with your desired location

### 3. Transform the Data
1. In Power Query Editor, expand the `current` record
2. Expand nested records like `condition` and `air_quality`
3. Rename columns for better readability
4. Click **Close & Apply**

### 4. Build Your Dashboard
- Add cards for key metrics (temperature, humidity)
- Create gauges for wind speed and direction
- Insert charts for trend analysis
- Set up city selection slicers

## 📐 DAX Measures Templates

The project includes reusable DAX templates for AQI monitoring:

### AQI Color Coding
```dax
AQI Color TEMPLATE =
VAR AQI = ROUND(SELECTEDVALUE('Current'[current.air_quality.COLUMN_NAME]),0)
RETURN
SWITCH(
    TRUE(),
    AQI <= 50, "#43d946",     -- Good (Green)
    AQI <= 100, "#fff570",    -- Moderate (Yellow)
    AQI <= 150, "#ff9800",    -- Unhealthy for Sensitive (Orange)
    AQI <= 200, "#d99343",    -- Unhealthy (Red)
    AQI <= 300, "#ff5b0f",    -- Very Unhealthy (Purple)
    "#d95243"                 -- Hazardous (Maroon)
)
```

### Health Recommendations
```dax
AQI Suggestion TEMPLATE =
VAR AQI = ROUND(SELECTEDVALUE('Current'[current.air_quality.COLUMN_NAME]),0)
RETURN
SWITCH(
    TRUE(),
    AQI <= 50, "Air is clean and healthy",
    AQI <= 100, "Acceptable air quality, stay active",
    AQI <= 150, "Sensitive groups should reduce outdoor time",
    AQI <= 200, "Limit prolonged outdoor exertion",
    AQI <= 300, "Avoid outdoor activity if possible",
    "Stay indoors, wear a mask if outside"
)
```

### Status Labels
```dax
AQI Status TEMPLATE =
VAR AQI = ROUND(SELECTEDVALUE('Current'[current.air_quality.COLUMN_NAME]),0)
RETURN
SWITCH(
    TRUE(),
    AQI <= 50, "Good",
    AQI <= 100, "Moderate",
    AQI <= 150, "Unhealthy for Sensitive",
    AQI <= 200, "Unhealthy",
    AQI <= 300, "Very Unhealthy",
    "Hazardous"
)
```

**Usage**: Replace `COLUMN_NAME` with specific pollutants:
- `pm2_5` for PM2.5 particles
- `co` for Carbon Monoxide
- `no2` for Nitrogen Dioxide
- `so2` for Sulfur Dioxide
- `o3` for Ozone

## 🎨 Customization

### Adding New Cities
1. Modify the API URL parameter `q` with new city names
2. Update data source in Power Query
3. Refresh the dataset

### Extending AQI Monitoring
1. Copy the DAX template measures
2. Replace `COLUMN_NAME` with new pollutant fields
3. Add corresponding visualizations

### Styling Options
- Custom color themes for weather conditions
- Icon integration for visual appeal
- Map visualizations for geographic context
- Responsive layout adjustments

## 📈 Data Refresh

### Manual Refresh
- Click **Refresh** in Power BI Desktop
- Data updates automatically from WeatherAPI

### Automatic Refresh (Power BI Service)
- Publish to Power BI Service
- Configure scheduled refresh
- Set refresh frequency (hourly/daily)

## 🔐 Security Best Practices

- Store API keys securely
- Use environment variables for production
- Implement rate limiting considerations
- Monitor API usage quotas

## 📚 Learning Resources

- [WeatherAPI Documentation](https://weatherapi.com/docs/)
- [Power BI Documentation](https://docs.microsoft.com/power-bi/)
- [DAX Reference Guide](https://docs.microsoft.com/dax/)
- [Air Quality Index Guidelines](https://airnow.gov/aqi/aqi-basics/)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [WeatherAPI.com](https://weatherapi.com) for providing reliable weather data
- Power BI community for inspiration and best practices
- Environmental agencies for AQI standards and guidelines

## 📞 Support

If you encounter any issues or have questions:
- Open an issue in this repository
- Check the [WeatherAPI documentation](https://weatherapi.com/docs/)
- Review Power BI community forums

---

**Happy Dashboarding! 🎨📊**
