🛠️ Tool Wear Prediction using LSTM
A machine learning project to predict tool wear conditions (Unworn, Worn, Damaged) based on CNC machine sensor data using an LSTM model. The app also predicts if machining is finalized and if the product passes visual inspection.

📦 Features
LSTM-based deep learning model (.h5) trained on sensor data

Real-time predictions via a Streamlit web app

Classifies:

Tool Condition: Unworn, Worn, Damaged

Machining Finalized: Yes / No

Visual Inspection: Passed / Failed

CSV input support

Visual results with color-coded output (green = pass, red = fail)

📁 Folder Structure
bash
Copy
Edit
Tolwear_prediction/
├── toolwear_prediction_app.py       # Main Streamlit app
├── my_lstm_model.h5                 # Trained LSTM model
├── scaler.pkl                       # Scaler used during preprocessing
├── train.csv / train_encoded.csv    # Training data (optional)
├── requirements.txt                 # Python dependencies
├── testalize-me-*.jpg               # Background image (optional)
├── README.md
🚀 Setup Instructions
1. 🔐 Upload to EC2
Make sure you have your .pem key and a running EC2 instance.

Upload project files to the EC2 instance:

bash
Copy
Edit
scp -i toolapp.pem * ubuntu@<your-ec2-ip>:/home/ubuntu/Tolwear_prediction/
SSH into EC2:

bash
Copy
Edit
ssh -i toolapp.pem ubuntu@<your-ec2-ip>
2. 📦 Install Dependencies
bash
Copy
Edit
sudo apt update
sudo apt install python3-pip
pip3 install -r requirements.txt
If requirements.txt is missing, use:

bash
Copy
Edit
pip3 install streamlit tensorflow pandas numpy scikit-learn
🖼️ (Optional) Background Image
If using a background image in your app, make sure your path is relative, not absolute:

python
Copy
Edit
# BAD (Windows path)
add_bg_from_local("D:/guvi/Final_project/testalize-me-xxx.jpg")

# GOOD (Linux relative path)
add_bg_from_local("testalize-me-xxx.jpg")
🧠 Run the App
bash
Copy
Edit
cd ~/Tolwear_prediction
streamlit run toolwear_prediction_app.py --server.port 8501
Visit your EC2 public IP on port 8501:
http://<your-ec2-ip>:8501

🔮 Model Output Format
Your LSTM model predicts 3 things:

Tool Condition: Unworn, Worn, Damaged

Machining Finalized: Yes / No

Visual Inspection: Passed / Failed

These are decoded using argmax() or thresholding as:

python
Copy
Edit
tool_pred = np.argmax(pred_output[0][0])
machining_pred = int(np.round(pred_output[1][0][0]))
visual_pred = int(np.round(pred_output[2][0][0]))
✅ Visual Output Format
Color-coded Streamlit output:

🟢 Green: Passed / Unworn / Yes

🔴 Red: Failed / Worn / Damaged / No

📊 Sample Input Format
Model expects 3D input:

makefile
Copy
Edit
(shape: [1, time_steps, num_features])
Feature order:

python
Copy
Edit
[
 'M1_CURRENT_FEEDRATE', 'X1_ActualAcceleration', 'X1_ActualPosition',
 'X1_ActualVelocity', 'X1_CommandAcceleration', 'X1_CommandPosition',
 'X1_CommandVelocity', 'X1_CurrentFeedback', 'X1_DCBusVoltage',
 'X1_OutputCurrent', 'X1_OutputVoltage', 'Y1_ActualPosition',
 'Y1_CommandPosition', 'Y1_OutputCurrent', 'clamp_pressure', 'feedrate'
]
🤝 Contributions
Pull requests and feature requests are welcome!

📜 License
This project is for educational purposes.
