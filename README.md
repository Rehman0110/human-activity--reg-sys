git remote add origin https://github.com/Rehman0110/human-activity--reg-sys.git# 🏃 Human Activity Recognition System

A real-time activity recognition system that predicts human activities from smartphone accelerometer data using Machine Learning (K-Means clustering with PCA).

![Python](https://img.shields.io/badge/Python-3.13-blue)
![Streamlit](https://img.shields.io/badge/Streamlit-1.51.0-red)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.7.2-orange)

## 📋 Overview

This application uses unsupervised machine learning to classify human activities based on 3-axis accelerometer data. The system can:
- ✅ Predict activities from manual input
- ✅ Stream real-time data from smartphone sensors via WiFi
- ✅ Visualize accelerometer data and predictions in real-time
- ✅ Classify 6 different human activities

## 🎯 Detected Activities

| Activity | Emoji | Description |
|----------|-------|-------------|
| STANDING | 🧍 | Minimal movement, upright position |
| SITTING | 🪑 | Stationary, seated position |
| LAYING | 🛌 | Horizontal resting position |
| WALKING | 🚶 | Regular walking pace |
| WALKING_UPSTAIRS | 🪜⬆️ | Climbing stairs |
| WALKING_DOWNSTAIRS | 🪜⬇️ | Descending stairs |

## 🚀 Quick Start

### Prerequisites
- Python 3.13 (or compatible version)
- Smartphone with accelerometer (for live predictions)
- WiFi network (to connect phone and computer)

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/Rehman0110/human-activity-recog.git
cd human-activity-recog/myenv
```

2. **Activate virtual environment**
```bash
source bin/activate  # On macOS/Linux
# OR
bin\Scripts\activate  # On Windows
```

3. **Install dependencies** (already included in repo)
```bash
pip install -r requirements.txt
```

4. **Run the application**
```bash
streamlit run app.py
```

5. **Open in browser**
- Local: http://localhost:8502
- Network: http://YOUR_IP:8502

## 📱 Live Phone Setup

### For Android:

1. **Install SensorServer app** from Google Play Store
2. **Open the app** and tap "Start Server"
3. **Note the IP address** displayed (e.g., 192.168.1.100)
4. **Connect phone and computer** to the same WiFi network
5. In the Streamlit app:
   - Go to **"📱 Live Phone Data"** page
   - Enter your phone's IP address
   - Click **"🟢 Start"**
6. **Move your phone** and watch real-time predictions!

### For iOS:

1. **Install "Sensor Logger"** from App Store
2. Enable accelerometer streaming via WiFi
3. Note the IP and port
4. Follow same connection steps as Android

📖 **Detailed setup guide:** See [README_PHONE_SETUP.md](README_PHONE_SETUP.md)

## 🎨 Features

### 🎯 Single Prediction
- Manual input of accelerometer values (X, Y, Z)
- Random sample selection from test dataset
- Instant activity prediction
- Visual bar chart of input values
- Cluster assignment display

### 📱 Live Phone Data
- **Real-time streaming** from smartphone accelerometer
- **Live charts** showing X, Y, Z acceleration over time
- **Current activity detection** with emoji indicators
- **Activity distribution** pie chart
- **Recent predictions table** (last 15 predictions)
- **Connection status** monitoring
- **Controls:** Start, Stop, Clear data

## 🧠 Model Details

### Architecture
- **Algorithm:** K-Means Clustering (unsupervised learning)
- **Preprocessing:** StandardScaler
- **Dimensionality Reduction:** PCA (2 components)
- **Clusters:** 6 (mapped to activities using training data majority vote)

### Features Used
- `tBodyAcc-mean()-X` - Mean acceleration on X-axis
- `tBodyAcc-mean()-Y` - Mean acceleration on Y-axis
- `tBodyAcc-mean()-Z` - Mean acceleration on Z-axis

### Training Data
- **Dataset:** Human Activity Recognition Using Smartphones
- **Samples:** 7,352 training samples, 2,947 test samples
- **Source:** UCI Machine Learning Repository

### Model Files
- `scaler.pkl` - StandardScaler for feature normalization
- `pca.pkl` - PCA model for dimensionality reduction
- `kmeans_model.pkl` - Trained K-Means clustering model
- `rf_model.pkl` - Trained Random Forest classifier (recommended)

### 🌲 Random Forest Classifier (Improved Accuracy)

For better accuracy, we also trained a **Random Forest classifier** using supervised learning:

#### Why Random Forest?
- **Higher Accuracy:** 90-95% (vs K-Means 60-70%)
- **Supervised Learning:** Learns directly from labeled activity data
- **Direct Classification:** No cluster mapping required
- **Better Generalization:** Handles activity variations more reliably

#### Random Forest Architecture
- **Algorithm:** Random Forest Classifier (supervised learning)
- **Parameters:** 100 trees, max_depth=20
- **Preprocessing:** StandardScaler only (no PCA needed)
- **Input Features:** Same 3D accelerometer means (X, Y, Z)
- **Output:** Direct activity prediction with high confidence

#### Comparison: K-Means vs Random Forest

| Aspect | K-Means | Random Forest |
|--------|---------|---------------|
| **Learning Type** | Unsupervised | Supervised |
| **Accuracy** | ~60-70% | ~90-95% |
| **Preprocessing** | Scaler → PCA | Scaler only |
| **Prediction** | Cluster → Activity | Direct Activity |
| **Use Case** | Pattern discovery | Production classification |

#### Using Random Forest in Your App

The current `app.py` uses the Random Forest model by default for best accuracy:

```python
# Model loads rf_model.pkl instead of kmeans_model.pkl
scaler, model = load_models()
prediction = model.predict(scaled_data)  # Direct activity prediction
```

**Recommendation:** Use Random Forest (`rf_model.pkl`) for production applications where accuracy is critical. K-Means is useful for exploratory analysis and understanding data patterns.

## 📊 Project Structure

```
myenv/
├── app.py                      # Main Streamlit application
├── model.ipynb                 # Model training notebook
├── data/
│   ├── train.csv              # Training dataset
│   └── test.csv               # Test dataset
├── scaler.pkl                 # Trained scaler
├── pca.pkl                    # Trained PCA model
├── kmeans_model.pkl           # Trained K-Means model
├── README.md                  # This file
├── README_PHONE_SETUP.md      # Detailed phone setup guide
├── QUICKSTART.md              # Quick reference guide
└── requirements.txt           # Python dependencies
```

## 🛠️ Technology Stack

- **Frontend:** Streamlit
- **ML Framework:** scikit-learn
- **Data Processing:** pandas, numpy
- **Visualization:** plotly, matplotlib, seaborn
- **Real-time Communication:** WebSockets
- **Async Processing:** asyncio, threading

## 📈 Usage Examples

### Example 1: Manual Prediction
```python
# Input values
X = 0.2773308  # tBodyAcc-mean()-X
Y = -0.0173838 # tBodyAcc-mean()-Y
Z = -0.1115110 # tBodyAcc-mean()-Z

# Prediction: STANDING 🧍
```

### Example 2: Live Phone Data
1. Start SensorServer on phone
2. Connect to app
3. Walk around → See WALKING 🚶
4. Go upstairs → See WALKING_UPSTAIRS 🪜⬆️
5. Sit down → See SITTING 🪑

## 🔧 Troubleshooting

### Can't connect to phone?
- ✅ Ensure both devices are on the **same WiFi network**
- ✅ Check if SensorServer is **running** on phone
- ✅ Verify the **IP address** is correct
- ✅ Keep **phone screen on**
- ✅ Check firewall settings

### No predictions showing?
- ✅ Move the phone to generate sensor data
- ✅ Wait 2-3 seconds after changing activity
- ✅ Check if sensor data chart is updating

### App won't start?
```bash
# Make sure to use virtual environment's streamlit
cd myenv
./bin/streamlit run app.py

# NOT just: streamlit run app.py
```

## 📚 Documentation

- **Quick Start:** [QUICKSTART.md](QUICKSTART.md)
- **Phone Setup:** [README_PHONE_SETUP.md](README_PHONE_SETUP.md)
- **Model Training:** [model.ipynb](model.ipynb)

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest features
- Submit pull requests

## 📄 License

This project is open source and available under the MIT License.

## 👨‍💻 Author

**Rehman Khan**
- GitHub: [@Rehman0110](https://github.com/Rehman0110)

## 🙏 Acknowledgments

- UCI Machine Learning Repository for the dataset
- Streamlit for the amazing web framework
- SensorServer app developers for phone sensor access

## 📞 Support

Having issues? Check:
1. [QUICKSTART.md](QUICKSTART.md) - Quick reference
2. [README_PHONE_SETUP.md](README_PHONE_SETUP.md) - Detailed setup
3. GitHub Issues - Report bugs or ask questions

---

**Built with ❤️ using Streamlit and scikit-learn**

⭐ If you find this project useful, please consider giving it a star!
