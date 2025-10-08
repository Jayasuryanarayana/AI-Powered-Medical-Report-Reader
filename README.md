\documentclass[11pt, a4paper]{article}

% --- PACKAGES ---
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage{geometry}
\usepackage{hyperref}
\usepackage{listings}
\usepackage{xcolor}
\usepackage{titlesec}
\usepackage{enumitem}

% --- DOCUMENT CONFIGURATION ---
\geometry{
    a4paper,
    left=2.5cm,
    right=2.5cm,
    top=2.5cm,
    bottom=2.5cm
}

% Hyperlink colors
\hypersetup{
    colorlinks=true,
    linkcolor=blue,
    filecolor=magenta,      
    urlcolor=cyan,
}

% Section title formatting
\titleformat{\section}
  {\normalfont\Large\bfseries\color{black}}
  {\thesection}{1em}{}
\titleformat{\subsection}
  {\normalfont\large\bfseries\color{black}}
  {\thesubsection}{1em}{}
\titleformat{\subsubsection}
  {\normalfont\normalsize\bfseries\color{black}}
  {\thesubsubsection}{1em}{}

% Code block (listings) style
\definecolor{codegray}{rgb}{0.95,0.95,0.95}
\definecolor{deepblue}{rgb}{0,0,0.5}
\definecolor{deepred}{rgb}{0.6,0,0}
\definecolor{deepgreen}{rgb}{0,0.5,0}

\lstdefinestyle{mystyle}{
    backgroundcolor=\color{codegray},
    commentstyle=\color{deepgreen},
    keywordstyle=\color{deepblue},
    stringstyle=\color{deepred},
    basicstyle=\ttfamily\footnotesize,
    breakatwhitespace=false,         
    breaklines=true,                 
    captionpos=b,                    
    keepspaces=true,                 
    numbers=left,                    
    numbersep=5pt,                  
    showspaces=false,                
    showstringspaces=false,
    showtabs=false,                  
    tabsize=2,
    frame=single,
    rulecolor=\color{black!30},
    framerule=0.5pt,
    framesep=3pt,
    framexleftmargin=5pt
}
\lstset{style=mystyle}

% --- DOCUMENT TITLE ---
\title{\textbf{AI-Powered Medical Report Reader}}
\author{Jayasuryanarayana}
\date{\today}

% --- DOCUMENT START ---
\begin{document}
\maketitle
\hrule
\vspace{1em}

\section*{Overview}
This is a full-stack web application designed to help patients understand their medical reports. Users can input their report either by typing/pasting text or by uploading a scanned image. The application then uses AI to generate a simplified, patient-friendly summary of the findings. The project is built with a Node.js/Express backend and a React/Vite frontend.

\section{Core Features}
\begin{itemize}[leftmargin=*]
    \item \textbf{Text Summarization:} Paste your medical report text to get a simplified summary.
    \item \textbf{Image Summarization (OCR):} Upload an image of your report, and the app will use Optical Character Recognition (OCR) to extract the text before summarizing it.
    \item \textbf{Image Validation:} Before processing, the application uses an AI vision model to verify that the uploaded image is a text document, preventing analysis of irrelevant photos.
    \item \textbf{Interactive Chat:} After receiving a summary, users can ask follow-up questions about their report in a simple chat interface.
    \item \textbf{Multi-Language Translation:} The generated summary can be instantly translated into numerous languages, including a wide selection of Indian languages.
    \item \textbf{Powered by Groq:} Utilizes the high-speed Groq API with the Llama 3.1 model for near-instant AI responses.
\end{itemize}

\section{Technology \& Project Structure}
This is a full-stack application with two main parts:
\begin{itemize}[leftmargin=*]
    \item \textbf{`frontend/` (The User Interface):} A single-page application built with React and Vite. It provides a fast, modern user interface for interacting with the app. Styled with Tailwind CSS.
    \item \textbf{`backend/` (The Engine):} A server built with Node.js and Express. It handles all the heavy lifting, including file uploads, OCR processing, image validation, and communicating with the Groq and Hugging Face AI APIs.
\end{itemize}

\section{Deployment Guide}
This project can be deployed using modern hosting platforms. The recommended setup is using Render for the backend and Vercel for the frontend.

\subsection{Backend Deployment (Render)}
\begin{enumerate}
    \item Push your entire project to a GitHub repository.
    \item Sign up for a free account on \href{https://render.com}{Render.com}.
    \item Create a new "Web Service" and connect it to your GitHub repository.
    \item Configure the settings:
    \begin{itemize}
        \item \textbf{Root Directory:} \texttt{backend}
        \item \textbf{Build Command:} \texttt{npm install}
        \item \textbf{Start Command:} \texttt{node src/server.js}
    \end{itemize}
    \item In the "Environment" tab, add your secret API keys: \texttt{GROQ\_API\_KEY} and \texttt{HF\_API\_KEY}.
    \item Deploy the service. Render will provide you with a public URL for your backend.
\end{enumerate}

\subsection{Frontend Deployment (Vercel)}
\begin{enumerate}
    \item In your \texttt{frontend/src/App.jsx} file, replace all \texttt{http://localhost:5001} API calls with your new public backend URL from Render.
    \item Push this change to your GitHub repository.
    \item Sign up for a free account on \href{https://vercel.com}{Vercel.com}.
    \item Create a new project and connect it to the same GitHub repository.
    \item Configure the settings:
    \begin{itemize}
        \item \textbf{Root Directory:} \texttt{frontend}
    \end{itemize}
    \item Vercel will automatically detect the Vite setup. Click "Deploy."
    \item Your application will be live at the public URL provided by Vercel.
\end{enumerate}

\section{Folder Structure}
\begin{lstlisting}[language=bash, caption={Project Directory Tree}, label={lst:folder}]
AI-Powered-Medical-Report-Reader/
├── backend/
│   ├── src/
│   │   ├── prompts/
│   │   │   └── summarizePrompt.js
│   │   └── server.js
│   ├── .env
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── App.jsx
│   │   ├── index.css
│   │   └── main.jsx
│   ├── index.html
│   └── package.json
└── README.md
\end{lstlisting}

\section{Example Inputs for Testing}
\subsection{Example 1 (Metabolic Panel with High Value)}
\begin{lstlisting}[language=text, caption={Sample Report 1}]
Patient: John Doe, DOB: 1985-05-15
Test: Comprehensive Metabolic Panel
Date: 2024-09-20

GLUCOSE: 95 mg/dL (Ref: 65-99)
SODIUM: 140 mEq/L (Ref: 135-145)
POTASSIUM: 4.1 mEq/L (Ref: 3.5-5.0)
WBC: 12.5 x 10^9/L (Ref: 4.5-11.0) - HIGH
RBC: 4.8 x 10^12/L (Ref: 4.2-5.9)
PLATELETS: 250 x 10^9/L (Ref: 150-450)
\end{lstlisting}

\subsection{Example 2 (Lipid Panel with Multiple Concerns)}
\begin{lstlisting}[language=text, caption={Sample Report 2}]
Patient: Jane Smith, DOB: 1972-11-30
Test: Lipid Panel - Fasting
Collected: 2024-10-04 08:30

CHOLESTEROL, TOTAL: 215 mg/dL (Desirable: <200) - Borderline High
HDL CHOLESTEROL: 45 mg/dL (Desirable: >40)
TRIGLYCERIDES: 180 mg/dL (Desirable: <150) - High
LDL CHOLESTEROL (Calculated): 134 mg/dL (Desirable: <100) - High
\end{lstlisting}

\end{document}
