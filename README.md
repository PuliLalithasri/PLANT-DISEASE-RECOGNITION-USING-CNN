# PLANT-DISEASE-RECOGNITION-USING-CNN
. Django Backend Code
views.py (Main Logic for Handling Requests)
This file handles requests, user authentication, image uploads, and interactions with 
the ML model.
Key Functions in views.py:
def login_user(request):
 if request.method == "POST":
 username = request.POST["username"]
 password = request.POST["password"]
 user = authenticate(username=username, password=password)
 if user:
 login(request, user)
 return redirect('dashboard')
 else:
 messages.error(request, "Invalid credentials")
 return render(request, "login.html")
Explanation:
• Checks if a user exists in the database.
• If valid, redirects to the dashboard; otherwise, shows an error message.
Handling Image Upload and Prediction
def predict_disease(request):
 if request.method == "POST" and request.FILES["plant_image"]:
 image_file = request.FILES["plant_image"]
 image_path = f"media/uploads/{image_file.name}"
 
 # Save the image to media folder
 with open(image_path, "wb") as f:
 for chunk in image_file.chunks():
 f.write(chunk)
 # Load CNN model and predict
 model = load_model("plant_disease_model.h5")
 result = classify_image(image_path, model)
 # Store result in database
 DiseasePrediction.objects.create(image=image_file.name, 
result=result, user=request.user)
 
 return render(request, "result.html", {"result": result})
 
 return render(request, "upload.html")
Explanation:
• The function reads an uploaded image, saves it, and sends it to the CNN model.
• The load_model() function loads a pre-trained CNN model 
(plant_disease_model.h5).
• The classify_image() function processes the image and predicts the disease.
• Stores the result in the database and displays it to the user.
2. Machine Learning (CNN Model Code)
CNN Model Definition (train_model.py)
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Conv2D, MaxPooling2D, Flatten, 
Dense
from tensorflow.keras.preprocessing.image import ImageDataGenerator
model = Sequential([
 Conv2D(32, (3,3), activation='relu', input_shape=(128,128,3)),
 MaxPooling2D(pool_size=(2,2)),
 
 Conv2D(64, (3,3), activation='relu'),
 MaxPooling2D(pool_size=(2,2)),
 
 Flatten(),
 Dense(128, activation='relu'),
 Dense(4, activation='softmax') # 4 output classes
])
model.compile(optimizer='adam', loss='categorical_crossentropy', 
metrics=['accuracy'])
model.fit(training_data, epochs=10, validation_data=validation_data)
model.save("plant_disease_model.h5")
Explanation:
• The CNN model has two convolutional layers followed by max pooling.
• The final Dense layer outputs predictions for 4 types of plant diseases.
• Uses categorical cross-entropy as the loss function.
• The trained model is saved as plant_disease_model.h5 for later use.
3. Image Classification Function
Image Preprocessing and Prediction (classify_image.py)
python
CopyEdit
import cv2
import numpy as np
from tensorflow.keras.models import load_model
def classify_image(image_path, model):
 image = cv2.imread(image_path)
 image = cv2.resize(image, (128, 128)) # Resize to match model 
input size
 image = np.expand_dims(image, axis=0) # Add batch dimension
 image = image / 255.0 # Normalize pixel values
 predictions = model.predict(image)
 classes = ["Bacterial Spot", "Early Blight", "Late Blight", 
"Healthy"]
 return classes[np.argmax(predictions)]
Explanation:
• Loads an image and resizes it to 128x128 pixels.
• Normalizes the image by dividing pixel values by 255.
• Runs the CNN model on the image to predict the disease.
4. Database Integration (MySQL with 
Django)
Database Models (models.py)
from django.db import models
from django.contrib.auth.models import User
class DiseasePrediction(models.Model):
 user = models.ForeignKey(User, on_delete=models.CASCADE)
 image = models.ImageField(upload_to="uploads/")
 result = models.CharField(max_length=100)
 timestamp = models.DateTimeField(auto_now_add=True)
#db.txt
create database PlantDiseaseDB;
use PlantDiseaseDB;
create table register(username varchar(30) primary key,
password varchar(30),
contact varchar(12),
email varchar(30),
address varchar(40));
create table locations(username varchar(50),
image_name varchar(50),
predicted_disease varchar(200),
latitude varchar(50),
longitude varchar(50));
Explanation:
• Stores user-uploaded images and their predicted disease results in the 
database.
• Uses Django’s built-in User model for authentication.
5. Geo-Location Tracking (IP-based 
Location Fetching)
Fetching User Location (location.py)
import requests
import geoip2.database
def get_user_location(ip_address):
 reader = geoip2.database.Reader("GeoLite2-City.mmdb")
 response = reader.city(ip_address)
 latitude = response.location.latitude
 longitude = response.location.longitude
 return latitude, longitude
Explanation:
• Extracts latitude and longitude from the user’s IP address.
• Helps track plant disease outbreaks in different regions.
Final Summary
• The project is a Django-based web application that uses CNNs to detect plant 
diseases from images.
• Users upload an image, and the system processes it using OpenCV before 
sending it to a deep learning model for classification.
• Django manages user authentication, database storage (MySQL), and file 
handling.
• The CNN model is trained to classify 4 plant diseases with high accuracy.
• GeoIP tracking helps identify where diseases are most reported, enabling better 
farming insights
