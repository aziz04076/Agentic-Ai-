# EWS Agentic - Early Warning System

A production-ready Early Warning System (EWS) that identifies at-risk students and proactively recommends tailored interventions using a LangGraph multi-agent pipeline.

## 🚀 Features

- **Multi-Agent Pipeline**: LangGraph-powered agents handle data ingestion, validation, feature engineering, and risk prediction
- **Real-time Dashboard**: React-based educator dashboard with at-risk student monitoring
- **ML-Powered Risk Scoring**: LightGBM baseline with SHAP explanations and bias monitoring
- **Intervention Recommendations**: AI-generated personalized intervention strategies
- **Privacy-First Design**: Role-based access, audit logging, and minimal PII storage
- **Production Ready**: Docker Compose, monitoring, tests, and CI/CD ready

## 🏗️ Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Frontend      │    │   Backend       │    │   ML Pipeline   │
│   React + TS    │◄──►│   FastAPI       │◄──►│   LangGraph     │
│   TailwindCSS   │    │   SQLAlchemy    │    │   LightGBM      │
│   shadcn/ui     │    │   PostgreSQL    │    │   SHAP          │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## 🛠️ Tech Stack

### Backend
- **Python 3.11+** with FastAPI
- **Database**: PostgreSQL with SQLAlchemy 2 + Alembic
- **Cache/Queue**: Redis with RQ
- **ML**: LightGBM, SHAP, scikit-learn, Pandas
- **Pipeline**: LangGraph multi-agent system
- **Auth**: JWT with role-based access control

### Frontend
- **React 18** with TypeScript
- **Build Tool**: Vite
- **Styling**: TailwindCSS + shadcn/ui
- **State Management**: TanStack Query
- **Charts**: Recharts
- **Icons**: Lucide React
Front Page-
<img width="1904" height="965" alt="image" src="https://github.com/user-attachments/assets/f836ab73-d971-4a41-9019-3fd908cf8376" />
Login Page -
<img width="1909" height="971" alt="image" src="https://github.com/user-attachments/assets/441445ff-8fb6-448d-b3a9-65909f3a2b8f" />
Dashboard Page -
<img width="1919" height="972" alt="image" src="https://github.com/user-attachments/assets/914dc115-61e1-4103-9efa-624dc7fc59b1" />



### Infrastructure
- **Containerization**: Docker Compose
- **Monitoring**: Prometheus metrics
- **Code Quality**: pre-commit, Black, isort, Ruff, mypy

## 🚀 Quick Start

### Prerequisites
- Python 3.11+
- Node.js 18+
- Docker & Docker Compose
- PostgreSQL 15+
- Redis 7+

### Option 1: Docker Compose (Recommended)

```bash
# Clone and setup
git clone <repository-url>
cd ews-agentic

# Copy environment file
cp .env.example .env

# Start all services
docker compose up --build

# Access the application
# Frontend: http://localhost:5173
# Backend API: http://localhost:8000
# API Docs: http://localhost:8000/docs
```

### Option 2: Local Development

#### Backend Setup
```bash
cd backend

# Install dependencies
make setup

# Setup database and run migrations
make migrate

# Seed demo data
make seed

# Start development server
make dev
```

#### Frontend Setup
```bash
cd frontend

# Install dependencies
npm install

# Start development server
npm run dev
```

## 📊 Usage

### 1. Access the Application
- **Landing Page**: http://localhost:5173
- **Login**: Use demo accounts (educator@example.com, admin@example.com, etc.)
- **Dashboard**: View at-risk students and manage interventions

### 2. Demo Accounts
- `educator@example.com` - Educator role
- `admin@example.com` - Admin role  
- `analyst@example.com` - Analyst role
- `student@example.com` - Student role (read-only)

### 3. Key Features
- **At-Risk Students Table**: View students with risk scores and signals
- **Student Details**: Click "Review" to see detailed risk analysis
- **Interventions**: Create and manage intervention strategies
- **Real-time Alerts**: WebSocket-based alert system
- **Analytics**: Risk trends and intervention success rates

## 🔧 Development

### Backend Commands
```bash
# Setup environment
make setup

# Run migrations
make migrate

# Seed demo data
make seed

# Start development server
make dev

# Run tests
make test

# Format code
make fmt

# Lint code
make lint

# Train ML model
make train
```

### Frontend Commands
```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview

# Lint code
npm run lint
```

### ML Training
```bash
# Train baseline model
python -m ml.train --data ./data/training.parquet --out ./ml/artifacts/ews_lgbm.pkl

# Evaluate model
python -m ml.evaluate
```

## 📁 Project Structure

```
ews-agentic/
├── backend/                 # FastAPI backend
│   ├── app/
│   │   ├── main.py         # FastAPI app factory
│   │   ├── core/           # Config, auth, settings
│   │   ├── db/             # Models, schemas, session
│   │   ├── routers/        # API endpoints
│   │   ├── services/       # LangGraph pipeline nodes
│   │   └── utils/          # Utilities
│   ├── ml/                 # ML training and evaluation
│   ├── migrations/         # Alembic migrations
│   ├── tests/              # Test suite
│   └── scripts/            # Seed and utility scripts
├── frontend/               # React frontend
│   ├── src/
│   │   ├── pages/          # Landing, Login, Dashboard
│   │   ├── lib/            # API client, utilities
│   │   └── components/     # Reusable components
│   └── public/             # Static assets
├── docker-compose.yml      # Full stack deployment
├── .env.example           # Environment template
└── README.md              # This file
```

## 🔒 Security & Privacy

- **JWT Authentication**: Secure token-based auth
- **Role-Based Access**: Granular permissions (admin, educator, analyst, student)
- **Audit Logging**: All educator actions are logged
- **PII Minimization**: Minimal sensitive data storage
- **Bias Monitoring**: Subgroup fairness metrics
- **Data Encryption**: Passwords hashed with bcrypt

## 📈 Monitoring

- **Health Checks**: `/healthz` endpoint
- **Metrics**: `/api/metrics` Prometheus endpoint
- **Logging**: Structured logging with loguru
- **Database**: Connection pooling and health monitoring

## 🧪 Testing

```bash
# Run all tests
make test

# Run specific test files
pytest backend/tests/test_api.py
pytest backend/tests/test_pipeline.py
pytest backend/tests/test_risk.py
```

## 📝 API Documentation

- **Interactive Docs**: http://localhost:8000/docs
- **OpenAPI Schema**: http://localhost:8000/openapi.json

### Key Endpoints
- `POST /api/login` - Authentication
- `GET /api/students/{id}/risk` - Student risk score
- `POST /api/interventions` - Create intervention
- `POST /api/feedback` - Log intervention outcome
- `GET /api/alerts/stream` - WebSocket alerts
- `GET /api/metrics` - Prometheus metrics

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Run tests and linting
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🆘 Support

For support and questions:
- Create an issue in the repository
- Check the documentation at `/docs`
- Review the API documentation at `/api/docs`

## 🎯 Roadmap

- [ ] Advanced ML models (XGBoost, Neural Networks)
- [ ] Real-time data streaming
- [ ] Mobile app
- [ ] Advanced analytics dashboard
- [ ] Integration with popular LMS platforms
- [ ] Multi-tenant support
