# WEATHER-APP
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Weather App</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background-color: #a3cef1;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
  }
  .weather-container {
    background: #ffffff;
    padding: 20px 30px;
    border-radius: 12px;
    box-shadow: 0 6px 15px rgba(0,0,0,0.1);
    width: 320px;
    text-align: center;
  }
  input[type="text"] {
    width: 75%;
    padding: 10px;
    border: 2px solid #ddd;
    border-radius: 8px;
    font-size: 16px;
  }
  button {
    padding: 10px 15px;
    margin-left: 5px;
    border: none;
    border-radius: 8px;
    background-color: #057a9e;
    color: white;
    font-size: 16px;
    cursor: pointer;
  }
  button:hover {
    background-color: #045d73;
  }
  .result {
    margin-top: 25px;
    display: none;
  }
  .result h2 {
    margin: 0;
  }
  .weather-icon {
    margin-top: 10px;
    width: 90px;
    height: 90px;
  }
</style>
</head>
<body>

<div class="weather-container">
  <h1>Weather App</h1>
  <input type="text" id="city" placeholder="Enter city name" />
  <button onclick="fetchWeather()">Search</button>

  <div class="result" id="result">
    <h2 id="cityName"></h2>
    <img id="icon" class="weather-icon" alt="Weather Icon" />
    <p id="temp"></p>
    <p id="desc"></p>
    <p id="wind"></p>
  </div>
</div>

<script>
  const apiKey = 'YOUR_OPENWEATHERMAP_API_KEY'; // Replace with your own API key

  async function fetchWeather() {
    const city = document.getElementById('city').value.trim();
    if (!city) {
      alert('Please enter a city name');
      return;
    }

    const url = `https://api.openweathermap.org/data/2.5/weather?q=${encodeURIComponent(city)}&appid=${apiKey}&units=metric`;

    try {
      const response = await fetch(url);
      const data = await response.json();

      if (response.ok) {
        document.getElementById('result').style.display = 'block';
        document.getElementById('cityName').textContent = data.name;
        document.getElementById('temp').textContent = `Temperature: ${data.main.temp} °C`;
        document.getElementById('desc').textContent = `Condition: ${data.weather[0].description}`;
        document.getElementById('wind').textContent = `Wind Speed: ${data.wind.speed} m/s`;
        document.getElementById('icon').src = `http://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`;
        document.getElementById('icon').alt = data.weather[0].description;
      } else {
        alert('City not found, please try again.');
        document.getElementById('result').style.display = 'none';
      }
    } catch (error) {
      alert('Unable to fetch weather data.');
      document.getElementById('result').style.display = 'none';
    }
  }
</script>

</body>
</html>
