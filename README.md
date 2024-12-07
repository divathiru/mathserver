# Ex.05 Design a Website for Server Side Processing
# Date:
20/11/2024
# AIM:
To design a website to calculate the power of a lamp filament in an incandescent bulb in the server side.

# FORMULA:
P = I2R
P --> Power (in watts)
 V --> Volts
 R --> Resistance

# DESIGN STEPS:
## Step 1:
Clone the repository from GitHub.

## Step 2:
Create Django Admin project.

## Step 3:
Create a New App under the Django Admin project.

## Step 4:
Create python programs for views and urls to perform server side processing.

## Step 5:
Create a HTML file to implement form based input and output.

## Step 6:
Publish the website in the given URL.

# PROGRAM :
views.py
~~~
from django.shortcuts import render

def index(request):
    result = None  # To store the calculation result
    if request.method == 'POST':
        try:
            # Retrieve inputs from the POST request
            voltage = float(request.POST.get('voltage'))
            resistance = float(request.POST.get('resistance'))
            
            # Validate resistance to avoid division by zero
            if resistance > 0:
                result = (voltage ** 2) / resistance
                
                # Log inputs and outputs to the server console
                print(f"Input received - Voltage: {voltage}V, Resistance: {resistance}Ω")
                print(f"Calculated Power: {result}W")
            else:
                result = "Resistance must be greater than zero."
                print("Error: Resistance must be greater than zero.")
        except ValueError:
            result = "Invalid input. Please enter numeric values."
            print("Error: Invalid input. Non-numeric values entered.")
    else:
        print("GET request received; no calculation performed.")
    
    return render(request, 'index.html', {'result': result})
~~~
index.html
~~~
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lamp Filament Power Calculator</title>
    <!-- Include Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&family=Playfair+Display:wght@700&display=swap" rel="stylesheet">
    <style>
        body {
            background: linear-gradient(to bottom right, #f8f9fa, #e8eaf6);
            font-family: 'Roboto', sans-serif;
        }
        .container {
            margin-top: 50px;
            max-width: 600px;
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        }
        h1 {
            font-family: 'Playfair Display', serif;
            font-size: 2.5rem;
            text-align: center;
            color: #343a40;
            margin-bottom: 1rem;
        }
        .formula {
            font-family: 'Playfair Display', serif;
            font-size: 1.5rem;
            color: #007BFF;
            text-align: center;
            margin-bottom: 2rem;
            animation: fadeIn 1.5s;
        }
        .form-control {
            border-radius: 10px;
            padding: 10px;
        }
        .btn {
            background-color: #007BFF;
            border-radius: 10px;
            padding: 10px 20px;
            font-size: 1rem;
        }
        .btn:hover {
            background-color: #0056b3;
        }
        .result {
            margin-top: 20px;
            font-size: 1.3rem;
            text-align: center;
            color: #28a745;
            animation: popUp 1s ease-out;
        }
        footer {
            margin-top: 30px;
            text-align: center;
            font-size: 0.9rem;
            color: #6c757d;
        }
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        @keyframes popUp {
            0% {
                opacity: 0;
                transform: scale(0.8);
            }
            100% {
                opacity: 1;
                transform: scale(1);
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Lamp Filament Power Calculator</h1>
        <div class="formula">
            <strong>Power = V² / R</strong>
        </div>
        <form method="POST">
            {% csrf_token %}
            <div class="mb-4">
                <label for="voltage" class="form-label">Voltage (V):</label>
                <input type="text" id="voltage" name="voltage" class="form-control" placeholder="Enter voltage in volts" required>
            </div>
            <div class="mb-4">
                <label for="resistance" class="form-label">Resistance (Ω):</label>
                <input type="text" id="resistance" name="resistance" class="form-control" placeholder="Enter resistance in ohms" required>
            </div>
            <button type="submit" class="btn btn-primary w-100">Calculate Power</button>
        </form>
        {% if result is not None %}
            <div class="result">
                <strong>Calculated Power:</strong> {{ result }} W
            </div>
        {% endif %}
    </div>
    <footer>
        &copy; 2024 Lamp Calculator | Designed with ❤️ and Bootstrap
    </footer>
    <!-- Include Bootstrap JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
~~~
# SERVER SIDE PROCESSING:
![Screenshot 2024-12-06 190115](https://github.com/user-attachments/assets/90e56033-17a9-444e-aecb-3e3f003666b9)

# HOMEPAGE:
![Screenshot 2024-12-06 190036](https://github.com/user-attachments/assets/dedd8311-d5e7-429e-882e-69cef67ad89a)
![Screenshot 2024-12-06 190055](https://github.com/user-attachments/assets/62db75d6-831d-4420-bc46-ef1b21565a11)

# RESULT:
The program for performing server side processing is completed successfully.
