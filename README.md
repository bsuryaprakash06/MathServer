# Ex-05 Design a Website for Server Side Processing
## Date: 24-10-2025

## AIM:
 To design a website to calculate the power of a lamp filament in an incandescent bulb in the server side. 


## FORMULA:
P = I<sup>2</sup>R
<br> P --> Power (in watts)
<br> I --> Intensity
<br> R --> Resistance

## DESIGN STEPS:

### Step 1:
Clone the repository from GitHub.

### Step 2:
Create Django Admin project.

### Step 3:
Create a New App under the Django Admin project.

### Step 4:
Create python programs for views and urls to perform server side processing.

### Step 5:
Create a HTML file to implement form based input and output.

### Step 6:
Publish the website in the given URL.

## PROGRAM :

<details>
<summary> POWER.HTML</summary>

 ```html
{% load static %}
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>Power of Lamp in Incandescent Bulb</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="{% static 'app.css' %}">

</head>

<body>
    <div class="box">
        <h1>Power of Lamp in Incandescent Bulb</h1>

        <form method="POST">
            {% csrf_token %}
            <div>
                <span class="label">Intensity:</span>
                <input type="text" name="Intensity" value="{{ I }}" placeholder="Enter current (A)"> (in A)
            </div>

            <div>
                <span class="label">Resistance:</span>
                <input type="text" name="Resistence" value="{{ R }}" placeholder="Enter resistance (Ω)"> (in Ω)
            </div>

            <div>
                <span class="label">Power:</span>
                <input type="text" name="Power" value="{{ Power }}" readonly> W
            </div>

            <div>
                <input type="submit" value="Calculate">
            </div>
        </form>
    </div>
</body>

</html>
```
</details>
<details>
<summary> APP.CSS</summary>

 ```css
body {
    font-family: 'Segoe UI', sans-serif;
    background: #f0f8ff;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

.box {
    width: 500px;
    min-height: 300px;
    font-size: 18px;
    background: rgb(99, 237, 118);
    border-radius: 15px;
    box-shadow: rgba(239, 5, 24, 0.35) 0px 5px 15px;
    padding: 25px;
    text-align: center;
}

h1 {
    color: #333;
    margin-bottom: 20px;
}

input[type="text"] {
    width: 60%;
    padding: 6px;
    margin: 8px 0;
    border-radius: 5px;
    border: 1px solid #999;
    font-size: 16px;
    text-align: center;
}

input[type="submit"] {
    margin-top: 10px;
    padding: 8px 20px;
    font-size: 16px;
    background-color: #2ecc71;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    color: white;
    transition: 0.3s ease;
}

input[type="submit"]:hover {
    background-color: #27ae60;
}

.label {
    font-weight: bold;
}
```
</details>


## SERVER SIDE PROCESSING:

<details>
<summary> Django Files</summary><br>

<details>
<summary> views.py</summary>

```python
from django.shortcuts import render

def powerlamp(request):
    context = {}
    context['Power'] = ""
    context['I'] = ""
    context['R'] = ""
    if request.method == 'POST':
        print("POST method is used")
        I = request.POST.get('Intensity', '')
        R = request.POST.get('Resistence', '')
        print('Intensity=', I)
        print('Resistence=', R)
        Power = int(I) * int(I) * int(R)
        context['Power'] = Power
        context['I'] = I
        context['R'] = R
        print('Power=', Power)
    return render(request, 'power.html', context)
```
</details>

<details>
<summary>urls.py (app)</summary>

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.powerlamp, name='powerlamp'),
]


```
</details>
<details>
<summary>urls.py (project)</summary>

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('pcalc.urls')),
]

```
</details>
</details>

## HOMEPAGE:

<img width="1919" height="1158" alt="P_web" src="https://github.com/user-attachments/assets/b3a3296d-ee50-47b2-a222-dc2e97ae7586" />

## OUTPUT:

<img width="1567" height="161" alt="image" src="https://github.com/user-attachments/assets/42f8a613-b4e8-466e-b095-3127a6dfc24e" />


## RESULT:
The program for performing server side processing is completed successfully.
