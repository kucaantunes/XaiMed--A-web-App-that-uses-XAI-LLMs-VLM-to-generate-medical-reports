# XaiMed
AI Radiograph. A web app that uses XAI, LLMs, VLM to generate medical reports

![image](https://github.com/user-attachments/assets/b9ba30e0-4d6c-4c9b-ad88-e8c79bd04f9f)

![image](https://github.com/user-attachments/assets/45d97e0f-b08f-4007-9290-b3892a806f57)



![image](https://github.com/user-attachments/assets/8c037055-8a76-498b-a455-dfd24af07e3d)


![image](https://github.com/user-attachments/assets/ad563498-04be-4f78-8c4d-bfd971c444f0)


![image](https://github.com/user-attachments/assets/96a3a71b-d948-488c-bc21-e6070aade970)


![image](https://github.com/user-attachments/assets/82cc8d6f-657c-460d-b562-022f0864a3a2)


![image](https://github.com/user-attachments/assets/6ea89ad2-cc47-4a0c-a99c-a9bc1a539c38)



![image](https://github.com/user-attachments/assets/d9425a97-9455-4049-9201-4287ce933c17)



![image](https://github.com/user-attachments/assets/1f9f813a-762f-4b21-948d-1dac3a4a856c)



![image](https://github.com/user-attachments/assets/26cc5105-67d9-4e5a-a4b5-ed884c37d5ca)




![image](https://github.com/user-attachments/assets/0359e6d0-9237-4ba6-8340-f9007e1e71e7)


In order to achieve #Objective_3 the research led to an improvement of the previous applications developed by the authors where a video chat was implemented plus XAI strategies to handle image data, and use of a VLM and LLM to generate the medical report (source code at: kucaantunes/XaiMed--A-web-App-that-uses-XAI-LLMs-VLM-to-generate-medical-reports), several preprocessing functions are defined. One function resizes the input images to a standard size and normalizes pixel values to optimize performance in deep learning models. Another function uses a chest X-ray verification model to assess whether the uploaded image is indeed a chest X-ray, providing a probability value.
The core of the model’s interpretability is Grad-CAM, a technique used to generate heatmaps that highlight the regions of an image most relevant to the model’s decision. The app contains a function that computes this heatmap by evaluating gradients and activations from the model's layers. Another key function converts images into Base64 format for easy transmission over the web. This allows the app to send images as strings in JSON responses, which is essential for web-based applications.
The main prediction route processes uploaded images and uses the transformer-based model to extract features, which are then classified. A Grad-CAM visualization is generated, and all results, including predictions and images, are returned as a JSON response with Base64-encoded images.
Additionally, there is a route for serving random example images, offering users a way to view sample images from a predefined directory. The app includes custom error handling for common HTTP errors, such as 404 (Page Not Found) and 405 (Method Not Allowed), ensuring a smooth user experience by redirecting users to appropriate routes or displaying error messages when necessary.

 
Figure 14. Improvements on the previously developed application (Antunes, et al. 2024) adapted from  (Pitumbur, 2023).

Algorithm 4, begins by initializing a Flask application to handle HTTP requests. It loads two pre-trained models: CLIP for image classification and GPT-Neo for the generation of detailed medical reports. Upon receiving a GET request, the home template is rendered. If a POST request is received, the input image undergoes preprocessing, including resizing and normalization. If the input image is recognized as a chest X-ray, the CLIP model is used to classify the image into one of three categories: Normal, COVID-19, or Pneumonia. Subsequently, the algorithm generates a Grad-CAM heatmap to highlight regions within the image that contribute significantly to the model's decision. If the image file is absent, the algorithm responds with a 400 Bad Request error. Once the image is successfully loaded and pre-processed, convolutional neural network (CNN) features are extracted, flattened, and passed through the classification model to generate a prediction. A comprehensive clinical report is then generated using GPT-Neo, contextualized by the classification output.
The Grad-CAM heatmap is superimposed onto the original image, providing a visual representation of the model’s decision-making process. The original image, heatmap, and superimposed image are converted to Base64 format to facilitate seamless transmission. The response includes the predicted class, associated probability, a detailed medical report, and visualizations. In the event of an error during processing, the algorithm returns a 500 Internal Server Error to indicate server-side failure.

Algorithm 4: Chest X-ray Image Classification and Grad-CAM Visualization

Input:
An image file via POST request.
Output:
Predicted class.
Prediction probability.
Medical report. 
Chest X-ray probability and visualizations (original image, heatmap, and superimposed image).
Steps:
Initialize Flask app.
Load pre-trained model CLIP for image classification.
Load pre-trained model GPT-Neo for report generation.
Render home template for GET request.
if request is POST then
   Render error message.
End If
Preprocess input image (resize and normalize).
If image is chest X-ray, then
   Predict the class using the pre-trained CLIP model (Normal, COVID-19, or Pneumonia).
End If
Generate Grad-CAM heatmap.
If request is missing file, then
   return 400 Bad Request.
End If
Load and preprocess image for prediction.
Extract features from image using CNN model.
Flatten CNN features.
Predict class.
Generate a detailed clinical report using GPT-Neo based on the classification results.
Generate Grad-CAM heatmap for visualization by extracting features from the image using the CLIP model.
Superimpose heatmap on original image.
Convert original image, heatmap, and superimposed image to Base64.
Return prediction results and images in response.
If error occurs, then
   return 500 Internal Server Error.
End If




![image](https://github.com/user-attachments/assets/abae0355-eee5-49f6-a2c0-3204972425af)




