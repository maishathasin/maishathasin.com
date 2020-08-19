---
layout: post
title:  "Project 3: A weather web app! ☀️"
date:   2020-07-25 13:42:19 -0400
categories: software engineering
---

# Project 3: A weather web app! ☀️
Another web application built using flask! but this time i'm building this to get familiar with APIs I used https://www.metaweather.com/api/location/4118/ to find the weather in toronto at any given time and according to the state it also prints a emoji.

```python
@app.route('/')
def weather():
    response = requests.get('https://www.metaweather.com/api/location/4118/')
    x = response.json()

    y = x["consolidated_weather"]
    current_state = y[0]
    state = current_state['weather_state_name']
    temp = current_state['the_temp']
    l = 'l'
```
now for the different states
```python
    if (state == 'snow'):
        l = '🌨' 
    elif(state== 'Thunderstorm'):
        l = '🌩' 
    elif(state == 'Showers'):
        l = '⛈'
    elif(state == 'Clear'):
        l = '☀️'
    elif(state == 'Heavy Cloud'):
        l = '☁️'
    elif(state == 'Light Cloud'):
        l = '🌥'
    return render_template('weather.html', state=state,temp=temp,emoji=l)
```


**For now you can see the code here:**
https://github.com/maishathasin/weather-webapp