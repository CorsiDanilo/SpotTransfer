[⬅ Previous](./02-structure.md) | [🏠 Index](./README.md) | [Next ➡](./04-api-reference.md)

# Local Development Setup

This guide provides instructions for setting up the SpotTransfer development environment. The project consists of a Flask backend and a React (Vite) frontend.

## 1. Prerequisites

Ensure you have the following installed on your system:

*   **Python 3.10+**: Required for the backend.
*   **Node.js 18+**: Required for the frontend.
*   **pnpm**: The project uses `pnpm` as the package manager.
*   **Git**: For version control.

## 2. Clone and Install

### Clone the Repository
```bash
git clone https://github.com/your-username/SpotTransfer.git
cd SpotTransfer
```

### Backend Setup
1. Navigate to the backend directory:
   ```bash
   cd backend
   ```
2. Create and activate a virtual environment:
   ```bash
   # Windows
   python -m venv venv
   .\venv\Scripts\activate

   # macOS/Linux
   python3 -m venv venv
   source venv/bin/activate
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

### Frontend Setup
1. Navigate to the frontend directory:
   ```bash
   cd ../frontend
   ```
2. Install dependencies:
   ```bash
   pnpm install
   ```

## 3. Environment Variables

You must configure the environment variables for both the backend and frontend to enable API communication and authentication.

### Backend Configuration
Copy the example file and update the values:
```bash
cd ../backend
cp .env.example .env
```

Edit `.env` with your credentials:
| Variable | Description |
| :--- | :--- |
| `SPOTIPY_CLIENT_ID` | Your Spotify Developer Client ID |
| `SPOTIPY_CLIENT_SECRET` | Your Spotify Developer Client Secret |
| `FRONTEND_URL` | (Optional) Override if not using `http://localhost:5173` |

### Frontend Configuration
Copy the example file and update the values:
```bash
cd ../frontend
cp .env.example .env
```

Edit `.env` to point to your backend:
| Variable | Description |
| :--- | :--- |
| `VITE_API_URL` | The URL where the Flask backend is running (default: `http://localhost:8080`) |

## 4. Running the Project

You need to run both the backend and frontend servers simultaneously.

### Start the Backend
From the `backend/` directory:
```bash
python main.py
```
*The backend will typically start on port 8080.*

### Start the Frontend
From the `frontend/` directory:
```bash
pnpm dev
```
*The frontend will typically start on port 5173. Open the URL displayed in your terminal (usually `http://localhost:5173`) to access the application.*

## 5. Running Tests

The project currently relies on manual verification of API endpoints and UI components.

*   **Backend**: You can verify the backend is running by navigating to `http://localhost:8080/` in your browser.
*   **Frontend**: Run the linter to check for code quality issues:
    ```bash
    cd frontend
    pnpm lint
    ```

## 6. Common Issues and Troubleshooting

### Backend: "ModuleNotFoundError"
If you encounter missing modules, ensure your virtual environment is activated. If you installed new packages, update your `requirements.txt`:
```bash
pip freeze > requirements.txt
```

### Frontend: "VITE_API_URL" Connection Errors
If the frontend cannot communicate with the backend:
1. Ensure the backend is running on the port specified in `frontend/.env` (`VITE_API_URL`).
2. Check that `Flask-Cors` is correctly configured in `backend/main.py` to allow requests from your frontend origin.

### CORS Errors
If you see CORS errors in the browser console, verify that the `Flask-Cors` configuration in `backend/main.py` allows the origin `http://localhost:5173`.

### Dependency Conflicts
If `pnpm install` fails in the frontend:
```bash
rm -rf node_modules
pnpm install
```

[⬅ Previous](./02-structure.md) | [🏠 Index](./README.md) | [Next ➡](./04-api-reference.md)