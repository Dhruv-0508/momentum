# Momentum - The Intelligent Task Manager

Momentum is a proactive task management application that organizes tasks into "Upcoming," "Completed," and "Missed" buckets based on deadlines and provides AI-powered prioritization to highlight the most important task.

## Features
### Core Features (MVP)
- **Manual Task Management**: Create, view, update, delete, and mark tasks as complete.
- **Time-Aware Auto-Bucketing**: Tasks are categorized dynamically based on deadlines and completion status.
- **Dynamic UI**: Responsive, real-time interface using React, Tailwind CSS, with tabbed buckets and a date picker.

### Innovation Feature: AI-Powered Prioritization
- **Description**: Suggests the "Most Important Task" (MIT) by using llama3-70b-8192 LLM with groq and if groq didn't work, then  scoring tasks based on urgency keywords (e.g., "urgent," "critical") and deadline proximity.
- **Why It's Useful**: Helps users focus on high-priority tasks, reducing overwhelm and boosting productivity.
- **Implementation**: The backend scores tasks via the `/api/prioritize/` endpoint, and the frontend displays the MIT with a badge.

## Tech Stack
- **Frontend**: Vite, React (JavaScript), Tailwind CSS
- **Backend**: Django, Django REST Framework
- **Database**: PostgreSQL

## Setup Instructions
### Prerequisites
- Node.js (v18+)
- Python (v3.10+)
- PostgreSQL (v15+)
- npm

### Backend Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo/momentum.git
   cd momentum/backend
   ```
2. Create and activate a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```
3. Configure PostgreSQL:
   - Create a database named `momentum`.
   - Update `settings.py` with your database credentials.
4. Run migrations:
   ```bash
   python manage.py migrate
   ```
5. Start the server:
   ```bash
   python manage.py runserver
   ```

### Frontend Setup
1. Navigate to the frontend directory:
   ```bash
   cd ../frontend
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Set the API URL in `.env`:
   ```env
   VITE_API_URL=http://localhost:8000/api
   ```
4. Start the development server:
   ```bash
   npm run dev
   ```
5. Open `http://localhost:5173`.

### Deployment
- **Frontend**: Deploy to Vercel/Netlify.
- **Backend**: Deploy to Railway with PostgreSQL.
- **Environment Variables**:
  - Backend: `DJANGO_SECRET_KEY`, `DB_NAME`, `DB_USER`, `DB_PASSWORD`, `DB_HOST`, `DB_PORT`.
  - Frontend: `VITE_API_URL`.

## Architectural Decisions
- **Auto-Bucketing**: Uses on-the-fly calculation in the `/api/tasks/` endpoint for simplicity and real-time accuracy. Status is computed based on `deadline` and `is_completed` fields, avoiding the need for a task queue like Celery in the MVP.
- **AI Prioritization**: Scores tasks using urgency keywords and deadline proximity, extensible for future NLP integration.

## API Endpoints
- `GET /api/tasks/`: List tasks with dynamic status.
- `POST /api/tasks/`: Create a task.
- `PUT /api/tasks/:id/`: Update a task.
- `DELETE /api/tasks/:id/`: Delete a task.
- `GET /api/prioritize/`: Get the most important task.

## Future Improvements
- Add Celery for scalable auto-bucketing.
- Add user authentication and notifications.

## Live Demo
#Deployed backend URL
[https://momentum-gav3.onrender.com]

#Railway as database
[https://railway.com/project/ee9faba6-2488-40ab-a9f4-cf589e6d2964/service/8d659185-cee3-4cb4-bc00-9e20552c7b9c/data?environmentId=add001c4-633d-4af3-9608-6ffd1747e5e7]

#Frontend hosted on local host
[http://localhost:5173/]
