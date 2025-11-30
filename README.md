### GEN-AI POWERED PERSONALIZED LEARNING TUTOR


### Problem Statement:
Most students struggle with learning because traditional educational systems follow a one-size-fits-all approach. Each learner has unique strengths, weaknesses, pace, and preferred learning styles, but current teaching methods cannot provide personalized guidance, real-time doubt clarification, or adaptive learning paths for every student. As a result, learners often experience knowledge gaps, low motivation, and poor academic performance.

There is a need for an AI-driven, interactive, and adaptive learning system that can analyze student behavior, understand their learning needs, and provide customized explanations, quizzes, feedback, and study plans—anytime, anywhere.

### Technologies Used: 
- 🧠 IBM Watsonx (Granite LLM via LangChain)
- 🚀 FastAPI + Uvicorn
- 📊 Pinecone Vector DB
- 🌐 Google Classroom API
- 🖥️ Streamlit (Role-based Dashboards)
- 🔐 OAuth (Google Auth)
- 📦 Python Environment Management with venv

### Overall Achitecture: 
`EDUTUTOR-AI/
├── .streamlit/                 # Streamlit credentials & secrets     
│   ├── client_secret.json
│   └── secrets.toml
│
├── backend/                      
│   ├── routes/                   # Route handlers for API endpoints
│   │   ├── auth.py             # FastAPI backend logic
│   │   ├── educator.py
│   │   ├── quiz.py
│   │   ├── submission.py
│   │   ├── user.py
│   │   └── user_auth.py
│   │
│   ├── services/                 # Services for external integrations
│   │   ├── llm_service.py        # Watsonx / Granite model logic
│   │   └── vector_service.py     # Pinecone vector search logic
│   │
│   ├── utils/                    # Helper and auth logic
│   │   ├── api.py
│   │   ├── auth.py
│   │   ├── session.py
│   │   └── watsonx_auth.py
│   │
│   ├── .env                      # Environment variables
│   ├── main.py                   # FastAPI entry point
│   └── students.db               # SQLite database file (or used for local storage)
│
├── frontend/                     # Streamlit frontend
│   ├── pages/                    # Individual UI screens
│   │   ├── google_login.py
│   │   ├── students_dashboard.py
│   │   └── take_quiz.py
│   ├── app.py                    # Main app file
│   └── static/                   # Static assets like CSS/images
│       └── style.css
│
├── requirements.txt              # Python dependencies
├── README.md                     # Project documentation
└── venv/                         # Python virtual environment `

### Demo -- 
Because of GitHub’s file size limitations, you can watch the full working demo of EduTutor AI here:
https://drive.google.com/file/d/1DaxhifKEBoEx6gESNGl0nPU1KA6fpFNd/view?usp=drive_link

###  Project Work flow :
 **Requirement Setup**
Technologies used:
- fastapi, uvicorn.
- langchain_ibm.
- pinecone-client.
- streamlit.
- google-auth-oauthlib.
- google-api-python-client.
- python-dotenv.

Install them via:
pip install -r requirements.txt

**Environment Initialization:**
- .env file stores all keys securely for:
- IBM Watsonx
- Pinecone DB
- OAuth credentials

**FastAPI Backend:**
Handles student/educator login, quiz generation, answer evaluation, classroom sync, and metadata updates.
![](https://www.googleapis.com/download/storage/v1/b/kaggle-user-content/o/inbox%2F15106171%2F8b6aefeaae4b9e8910881c397572f9e7%2FScreenshot%20(10).png?generation=1764514023823629&alt=media)
**Google Classroom Sync**
- Login via Google OAuth
- Retrieve class names, topics, student data using Classroom APIs
**Pinecone Integration**
- Embeddings stored for each user
- Metadata like quiz scores, topics, dates
**Vector similarity used for personalized quiz suggestions**
![](https://www.googleapis.com/download/storage/v1/b/kaggle-user-content/o/inbox%2F15106171%2F64a3e6f1d772578399dbd9e2dfaa0f7c%2FScreenshot%20(18).png?generation=1764514425548663&alt=media)
**Streamlit Frontend**
Student Panel
- Google/Manual Login
- Personalized Dashboard
- Take Quiz
- View Quiz History
![](https://www.googleapis.com/download/storage/v1/b/kaggle-user-content/o/inbox%2F15106171%2F5067f431dae938253e19da88a185c502%2FScreenshot%20(14).png?generation=1764514585080500&alt=media)

![](https://www.googleapis.com/download/storage/v1/b/kaggle-user-content/o/inbox%2F15106171%2Fca8d6439a809c6af43ca365c3a05332a%2FScreenshot%20(16).png?generation=1764514662110687&alt=media)
**Educator Panel**
Dashboard with performance insights
- View student activity
- Analyze progress via Pinecone data.

### How to Run the Project Locally:
1️⃣ Clone the Repository:
git clone https://github.com/yourusername/edututor-ai.git
cd edututor-ai

2️⃣ Create and Activate Virtual Environment:
# Windows
python -m venv venv
venv\Scripts\activate

# macOS/Linux
python3 -m venv venv
source venv/bin/activate

3️⃣ Install Dependencies:
pip install -r requirements.txt

4️⃣ Configure Environment Variables:
Create a .env file in the root directory with the following:
WATSONX_MODEL_ID=granite-13b-instruct-v2
WATSONX_API_KEY=your_ibm_watsonx_api_key
WATSONX_ENDPOINT=https://us-south.ml.cloud.ibm.com
WATSONX_PROJECT_ID=your_project_id

PINECONE_API_KEY=your_pinecone_api_key
PINECONE_INDEX_NAME=edututor

5️⃣ Run Backend (FastAPI):
cd backend
uvicorn main:app --reload
Visit API Docs: http://127.0.0.1:8000/docs

6️⃣ Run Frontend (Streamlit):
cd frontend
streamlit run app.py
