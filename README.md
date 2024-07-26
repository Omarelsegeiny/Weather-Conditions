Simple Weather App
A simple web application built with Flask that displays the weather in specific locations using the OpenWeather API.

Features
Get current weather information for any city
Display temperature, weather conditions, humidity, and wind speed
User-friendly interface
Screenshots
Include screenshots of your app here

Getting Started
Prerequisites
Python 3.x
Flask
Requests library
You can install Flask and Requests using pip:

bash
Copy code
pip install Flask requests
OpenWeather API Key
You need an API key from OpenWeather to use their API. Sign up on their website to get your API key.

Installation
Clone the repository:
bash
Copy code
git clone https://github.com/your-username/simple-weather-app.git
cd simple-weather-app
Create a .env file in the root directory and add your OpenWeather API key:
env
Copy code
API_KEY=your_openweather_api_key
Run the application:
bash
Copy code
python app.py
Open your web browser and navigate to http://127.0.0.1:5000/.
Usage
Enter the name of the city you want to check the weather for.
Click the "Get Weather" button.
View the weather details displayed on the page.
Code Structure
app.py: Main Flask application file.
templates/: Directory containing HTML templates.
index.html: Main page template.
static/: Directory containing static files (CSS, JavaScript, images).
Example
python
Copy code
from flask import Flask, render_template, request
import requests

app = Flask(__name__)

@app.route('/', methods=['GET', 'POST'])
def index():
    if request.method == 'POST':
        city = request.form['city']
        api_key = 'your_openweather_api_key'
        weather_data = get_weather(city, api_key)
        return render_template('index.html', weather=weather_data, city=city)
    return render_template('index.html')

def get_weather(city, api_key):
    url = f'http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric'
    response = requests.get(url)
    data = response.json()
    if data['cod'] == 200:
        weather = {
            'temperature': data['main']['temp'],
            'description': data['weather'][0]['description'],
            'humidity': data['main']['humidity'],
            'wind_speed': data['wind']['speed']
        }
    else:
        weather = None
    return weather

if __name__ == '__main__':
    app.run(debug=True)
License
This project is licensed under the MIT License - see the LICENSE file for details.
