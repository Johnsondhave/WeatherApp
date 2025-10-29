# React Weather App ☀️
Responsive weather app fetching live data from OpenWeather API.

## Features
- City-based search  
- Real-time temperature & description  
- Responsive layout  

## Tech Stack
React | CSS | OpenWeather API

import React, { useState } from "react";

function App() {
  const [city, setCity] = useState("");
  const [data, setData] = useState(null);

  const fetchWeather = async () => {
    const res = await fetch(
      `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=YOUR_API_KEY`
    );
    setData(await res.json());
  };

  return (
    <div className="p-6 text-center">
      <h1 className="text-2xl font-bold mb-4">Weather App</h1>
      <input
        className="border p-2"
        placeholder="Enter city"
        value={city}
        onChange={(e) => setCity(e.target.value)}
      />
      <button onClick={fetchWeather} className="ml-2 p-2 bg-blue-500 text-white">
        Search
      </button>

      {data && data.main && (
        <div className="mt-4">
          <h2 className="text-xl">{data.name}</h2>
          <p>{data.main.temp} °C</p>
          <p>{data.weather[0].description}</p>
        </div>
      )}
    </div>
  );
}
export default App;
