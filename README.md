# AI-Powered-Medical-Report-Reader
AI-Powered Medical Report Reader
This is a full-stack web application designed to help patients understand their medical reports. Users can input their report either by typing/pasting text or by uploading a scanned image. The application then uses AI to generate a simplified, patient-friendly summary of the findings.
The project is built with a Node.js/Express backend and a React/Vite frontend.
Core Features
Text Summarization: Paste your medical report text to get a simplified summary.
Image Summarization (OCR): Upload an image of your report, and the app will use Optical Character Recognition (OCR) to extract the text before summarizing it.
Image Validation: Before processing, the application uses an AI vision model to verify that the uploaded image is a text document, preventing analysis of irrelevant photos.
Interactive Chat: After receiving a summary, users can ask follow-up questions about their report in a simple chat interface.
Multi-Language Translation: The generated summary can be instantly translated into numerous languages, including a wide selection of Indian languages.
Powered by Groq: Utilizes the high-speed Groq API with the Llama 3.1 model for near-instant AI responses.
Technology & Project Structure
This is a full-stack application with two main parts:
frontend/ (The User Interface): A single-page application built with React and Vite. It provides a fast, modern user interface for interacting with the app. Styled with Tailwind CSS.
backend/ (The Engine): A server built with Node.js and Express. It handles all the heavy lifting, including file uploads, OCR processing, image validation, and communicating with the Groq and Hugging Face AI APIs.
Deployment Guide
This project can be deployed to the web using modern hosting platforms. The recommended setup is using Render for the backend and Vercel for the frontend.
1. Backend Deployment (Render)
Push your entire project to a GitHub repository.
Sign up for a free account on Render.com.
Create a new "Web Service" and connect it to your GitHub repository.
Configure the settings:
Root Directory: backend
Build Command: npm install
Start Command: node src/server.js
In the "Environment" tab, add your secret API keys:
GROQ_API_KEY
HF_API_KEY
Deploy the service. Render will provide you with a public URL for your backend (e.g., https://your-backend-name.onrender.com).
2. Frontend Deployment (Vercel)
In your frontend/src/App.jsx file, replace all http://localhost:5001 API calls with your new public backend URL from Render.
Push this change to your GitHub repository.
Sign up for a free account on Vercel.com.
Create a new project and connect it to the same GitHub repository.
Configure the settings:
Root Directory: frontend
Vercel will automatically detect the Vite setup. Click "Deploy."
Your application will be live at the public URL provided by Vercel.
Folder Structure
AI-Powered-Medical-Report-Reader/
├── backend/
│   ├── node_modules/       
│   ├── src/
│   │   ├── prompts/          # New folder for organizing AI prompts
│   │   │   └── summarizePrompt.js # The main prompt for summarization
│   │   └── server.js       # The main Express server file with all API logic
│   ├── .env                
│   ├── .gitignore          
│   ├── package.json        
│   └── package-lock.json   
│
├── frontend/
│   ├── dist/               
│   ├── node_modules/       
│   ├── public/             
│   ├── src/
│   │   ├── components/     
│   │   ├── App.jsx         
│   │   ├── index.css       
│   │   └── main.jsx        
│   ├── .gitignore          
│   ├── index.html          
│   ├── package.json        
│   ├── postcss.config.js   
│   └── tailwind.config.js  
│
└── README.md


Example Inputs for Testing
You can use these fictional snippets to test the text input functionality.
Example 1 (Metabolic Panel with High Value):
Patient: John Doe, DOB: 1985-05-15
Test: Comprehensive Metabolic Panel
Date: 2024-09-20

GLUCOSE: 95 mg/dL (Ref: 65-99)
SODIUM: 140 mEq/L (Ref: 135-145)
POTASSIUM: 4.1 mEq/L (Ref: 3.5-5.0)
WBC: 12.5 x 10^9/L (Ref: 4.5-11.0) - HIGH
RBC: 4.8 x 10^12/L (Ref: 4.2-5.9)
PLATELETS: 250 x 10^9/L (Ref: 150-450)


Example 2 (Lipid Panel with Multiple Concerns):
Patient: Jane Smith, DOB: 1972-11-30
Test: Lipid Panel - Fasting
Collected: 2024-10-04 08:30

CHOLESTEROL, TOTAL: 215 mg/dL (Desirable: <200) - Borderline High
HDL CHOLESTEROL: 45 mg/dL (Desirable: >40)
TRIGLYCERIDES: 180 mg/dL (Desirable: <150) - High
LDL CHOLESTEROL (Calculated): 134 mg/dL (Desirable: <100) - High


