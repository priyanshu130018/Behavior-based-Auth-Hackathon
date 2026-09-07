🛡️ Behavior Based Continuous Authentication

A real-time behavioral authentication system that continuously verifies a user's identity through typing patterns, mouse behavior, and machine learning.

📖 Overview

Traditional authentication usually checks a user only when they log in.

This project adds a second layer of security by continuously analyzing how a user interacts with the system during an active session.

The application combines:

Keystroke dynamics

Mouse behavior

Machine learning

Anomaly detection

Behavioral drift detection

Real-time monitoring

Session management

The goal is to detect when the current behavior no longer matches the user's established behavioral profile.

✨ Features

🔐 Authentication

User registration and login

Password validation

Session management

Continuous authentication

Behavioral verification

⌨️ Keystroke Analysis

The system analyzes patterns such as:

Key hold time

Key-to-key flight time

Typing speed

Rhythm and consistency

Typing variation

Digraph and trigraph timing

Error and pause patterns

🖱️ Mouse Analysis

The system analyzes:

Mouse movement

Velocity

Acceleration

Movement smoothness

Click timing

Navigation patterns

Target precision

Scroll behavior

🧠 Machine Learning

The project uses multiple models to evaluate behavioral patterns:

GRU

Autoencoder

One-Class SVM

Incremental k-NN

Passive-Aggressive Classifier

Isolation Forest

The models are combined to improve anomaly detection and behavioral verification.

📊 Monitoring

The dashboard provides:

Authentication status

Behavioral scores

Activity information

Security alerts

Behavioral analytics

Drift information

🎨 Interface

Dark cybersecurity-focused UI

Responsive layout

Interactive calibration

Real-time monitoring

Charts and visual feedback

Animated interface elements

🏗️ Architecture

This project follows a monolithic application structure.

The complete application runs as one backend service while individual responsibilities are kept in separate files and folders.

Behavior-based-Auth-Hackathon/
│
├── app.py
├── config.py
├── requirements.txt
│
├── models/
│   ├── behavioral_models.py
│   └── saved/
│       └── {user_id}/
│           ├── model_gru.h5
│           ├── model_autoencoder.h5
│           └── sklearn_models.pkl
│
├── utils/
│   ├── feature_extractor.py
│   └── drift_detector.py
│
├── database/
│   ├── db_manager.py
│   └── auth_system.db
│
├── static/
│   ├── css/
│   │   └── styles.css
│   │
│   └── js/
│       ├── login.js
│       ├── calib.js
│       └── challenge.js
│
└── templates/
    ├── login.html
    ├── calib.html
    └── challenge.html

🔄 Project Workflow

The application follows this flow:

User
  ↓
Login / Registration
  ↓
Primary Authentication
  ↓
Behavioral Calibration
  ↓
Typing + Mouse Data Collection
  ↓
Feature Extraction
  ↓
Behavioral Model Training
  ↓
User Behavioral Profile
  ↓
Active Session
  ↓
Continuous Behavioral Data Collection
  ↓
Feature Extraction
  ↓
ML Ensemble Prediction
  ↓
Authentication / Anomaly Score
  ↓
Drift Detection
  ↓
Security Decision
  ↓
Dashboard + Alert

1. User Registration and Login

The application starts with the login interface.

A user can create an account and authenticate using their credentials.

The frontend handles the user interaction while the Flask application processes authentication requests.

2. Behavioral Calibration

After authentication, the user completes a calibration process.

Typing calibration

The application collects keyboard timing information to establish the user's normal typing pattern.

Mouse calibration

The application collects mouse movement and interaction data to establish the user's normal mouse behavior.

This information becomes the baseline behavioral profile.

3. Feature Extraction

Raw input events are not directly sent to the machine learning models.

The system first transforms them into behavioral features.

Keyboard features

Examples include:

Hold duration

Flight duration

Typing speed

Rhythm

Timing consistency

Pattern variation

Mouse features

Examples include:

Velocity

Acceleration

Movement distance

Trajectory

Click timing

Navigation efficiency

Feature extraction is handled separately so that the ML layer receives structured behavioral data.

4. Model Training

The extracted calibration data is used to build a behavioral profile for the user.

The project combines multiple machine learning approaches:

Behavioral Features
        ↓
 ┌───────────────────────────────┐
 │        ML Ensemble            │
 ├───────────────────────────────┤
 │ GRU                           │
 │ Autoencoder                   │
 │ One-Class SVM                 │
 │ Incremental k-NN              │
 │ Passive-Aggressive            │
 │ Isolation Forest              │
 └───────────────────────────────┘
        ↓
Combined Behavioral Decision

Per-user model artifacts are stored under the model directory.

5. Continuous Monitoring

Once the user enters the protected application, behavioral data continues to be collected.

The system compares the current behavior with the established user profile.

The purpose is to identify significant behavioral changes during an active session.

6. Anomaly Detection

Each behavioral observation is evaluated by the configured models.

The system produces an authentication or anomaly assessment based on the observed behavior.

A sequence of suspicious observations can trigger a security event.

7. Drift Detection

Human behavior naturally changes over time.

The project therefore includes drift detection to distinguish normal behavioral changes from potentially suspicious activity.

This helps reduce false positives when the user's behavior changes gradually.

8. Dashboard

The monitoring dashboard presents the current security state.

It can display:

Authentication status

Behavioral score

Security events

Behavioral analytics

Drift information

Monitoring state

📂 File Responsibilities

app.py

Main Flask application.

Responsible for:

Application startup

HTTP routes

Authentication flow

Session handling

Real-time communication

Connecting frontend requests with backend logic

config.py

Central configuration.

Contains settings for:

Security

Database

Model paths

Authentication thresholds

Behavioral analysis

Development environment

models/behavioral_models.py

Machine learning implementation.

Responsible for:

Model creation

Model training

Model prediction

Ensemble behavior

Saving and loading user models

utils/feature_extractor.py

Transforms raw keyboard and mouse events into behavioral features.

utils/drift_detector.py

Detects changes between established and recent behavioral patterns.

database/db_manager.py

Handles database operations such as:

User records

Authentication information

Session-related data

Security events

templates/

Server-rendered HTML pages.

login.html
    ↓
Authentication interface

calib.html
    ↓
Behavioral calibration

challenge.html
    ↓
Secure monitoring dashboard

static/js/

Frontend interaction logic.

login.js

Handles the login and registration interface.

calib.js

Collects and manages behavioral calibration data.

challenge.js

Handles active-session monitoring and dashboard updates.

static/css/styles.css

Contains the application UI styling and responsive dark-theme design.

📊 Behavioral Data

Keystroke Dynamics

The project uses timing-based keyboard information to establish a typing signature.

Key measurements include:

Hold time

Flight time

Typing speed

Rhythm

Timing variance

Typing consistency

Pause patterns

Mouse Behavior

The project uses interaction patterns such as:

Movement speed

Acceleration

Cursor trajectory

Click timing

Navigation efficiency

Target accuracy

Scroll patterns

These behavioral signals are combined instead of depending on a single input feature.

⚙️ Configuration

Create a local .env file and configure the application values required by your environment.

Example:

SECRET_KEY=your-secret-key
JWT_SECRET_KEY=your-jwt-secret

DATABASE_PATH=database/auth_system.db

MODELS_BASE_PATH=models/saved

CONFIDENCE_THRESHOLD=0.7
ANOMALY_THRESHOLD=0.8

DEBUG=True
FLASK_ENV=development

Never commit the real .env file.

Use .env.example as the public configuration template.

🚀 Getting Started

Prerequisites

Python 3.8 - 3.11

Modern web browser

Git

Node.js is optional and is only needed when frontend development tooling is used.

1. Clone the Repository

git clone <your-repository-url>
cd Behavior-based-Auth-Hackathon

2. Create Virtual Environment

Windows

python -m venv venv
venv\Scripts\activate

Linux / macOS

python -m venv venv
source venv/bin/activate

3. Install Dependencies

pip install -r requirements.txt

4. Configure Environment

Create:

.env

Copy the values from:

.env.example

and update them for your local environment.

5. Initialize the Application

Initialize the database using the application setup flow provided by the project.

6. Start the Application

python run.py

Open:

http://localhost:5000

🧪 Testing

The project can be tested through the main user workflow:

Registration
    ↓
Login
    ↓
Typing Calibration
    ↓
Mouse Calibration
    ↓
Behavioral Profile
    ↓
Protected Dashboard
    ↓
Continuous Monitoring
    ↓
Behavior Variation Testing
    ↓
Anomaly Detection

Recommended scenarios include:

New user registration

Existing user login

Normal typing behavior

Different typing behavior

Normal mouse navigation

Different mouse behavior

Behavioral drift

Repeated anomalies

Session security

🔐 Security

The project is designed around multiple authentication layers:

Password Authentication
        ↓
Behavioral Verification
        ↓
Anomaly Detection
        ↓
Drift Monitoring
        ↓
Session Security

Important security practices:

Keep secrets in environment variables

Do not commit .env

Do not commit database files containing local data

Do not commit trained model artifacts unless intentionally versioned

Use HTTPS in production

Protect session data

Review thresholds before production use

🗃️ Local Files

The following files/directories should generally remain local and should be excluded from Git:

.env
venv/
__pycache__/
*.pyc
database/auth_system.db
models/saved/
logs/

The repository should contain source code and configuration templates rather than personal user data or generated artifacts.

🚀 Production Considerations

For production deployment, consider:

HTTPS

Secure session configuration

Rate limiting

CSRF protection

Content Security Policy

Persistent session storage

Database indexing

Model caching

Background processing for expensive ML operations

Centralized monitoring and logging

The current project is structured as a monolithic application. Scaling infrastructure can be introduced later without changing the core behavioral-analysis concepts.

🔮 Future Improvements

Better per-user behavioral model lifecycle

More robust model evaluation

Improved behavioral drift adaptation

Persistent production session storage

Better anomaly explanations

Stronger test coverage

Model performance monitoring

Multi-device behavioral profiles

Privacy-preserving learning

Additional behavioral signals

🤝 Contributing

Create a feature branch:

git checkout -b feature/your-feature

Commit your changes:

git add .
git commit -m "Add your feature"

Push the branch:

git push origin feature/your-feature

Then open a pull request.

📄 License

No license file was provided in the original repository. Please select and add your project's chosen license file (e.g., MIT, Apache 2.0) before publishing a public or production release.

🤝 Credits & Acknowledgments

This project is a derivative work based on the original [Behavior-based-Auth-Hackathon](https://github.com/priyanshu130018/Behavior-based-Auth-Hackathon) repository created by Priyanshu Ranjan Verma (`priyanshu130018`).

📌 Project Summary

Behavior Based Continuous Authentication moves authentication beyond a single login event.

Instead of asking only:

"Did the correct user enter the password?"

the system continuously evaluates:

"Does the current behavior still match the established user profile?"

By combining keystroke dynamics, mouse behavior, machine learning, anomaly detection, and drift analysis, the project provides an additional layer of continuous session security.
