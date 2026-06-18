ForecastIQ — Enterprise AI Demand Forecasting Platform
A full-stack enterprise-grade AI-powered demand forecasting platform built with FastAPI, MySQL, React 18, and Tailwind CSS.

Table of Contents
Project Overview
Tech Stack
Project Structure
Phase Summary
Prerequisites
Installation & Setup
Database Setup
Running the Application
Default Login
API Documentation
Features by Module
ML Models
Sample Datasets
Known Issues & Fixes
Environment Variables
Project Overview
ForecastIQ is an enterprise AI demand forecasting platform that enables organizations to:

Upload and process sales, inventory, and customer datasets
Run ML-powered demand forecasts using multiple models
Detect anomalies in demand patterns
Analyze business intelligence through executive dashboards
Collaborate on forecasts with comments, sharing, and revisions
Manage approvals, workflows, KPIs, and governance
Support multi-organization enterprise structures
Tech Stack
Layer	Technology
Backend	FastAPI (Python 3.12), SQLAlchemy ORM
Database	MySQL 8.0+
ML Models	Scikit-learn, Prophet (Meta)
Frontend	React 18, Vite, Tailwind CSS
Charts	Recharts
Auth	JWT (python-jose), bcrypt
HTTP Client	Axios
Phase Summary
Phase	Version	Key Features
Phase 1–2	v2.0	Auth, JWT, RBAC, Dataset upload, ML forecasting, Admin panel, Notifications
Phase 3	v3.0	Anomaly detection, Ensemble model, Region/category analytics, Global search, Dark mode
Phase 4	v4.0	Scheduled forecasts, Threshold alerts, ERP/webhook integrations, AI features (EOQ, spikes), Dashboard widgets
Phase 5	v5.0	Forecast workspaces, What-If scenarios, Executive BI dashboard, AI insights engine, Collaboration, Accuracy center
Phase 6	v6.0	Multi-org management, Approval workflow, Workflow automation, KPI management, Governance center, Data quality scoring
Prerequisites
Python 3.12 (not 3.13+)
Node.js 18+ and npm
MySQL 8.0+
Running the Application
Start Backend
cd D:\forecast-phase5\backend
venv\Scripts\activate
uvicorn main:app --reload
Backend runs at: http://localhost:8000

Start Frontend
cd D:\forecast-phase5\frontend
npm run dev
Frontend runs at: http://localhost:3000

API Documentation
Swagger UI: http://localhost:8000/docs

Authentication in Swagger
Go to http://localhost:8000/docs
Click POST /api/auth/token
Enter grant_type=password, your username and password
Copy the access_token value
Click the Authorize button at the top
Paste: Bearer your_token_here
Click Authorize
Key API Endpoints
POST   /api/auth/register          Register new user
POST   /api/auth/login             Login
GET    /api/auth/me                Get current user

POST   /api/datasets/upload        Upload CSV/Excel dataset
GET    /api/datasets/              List datasets

POST   /api/forecasts/             Create forecast
GET    /api/forecasts/             List forecasts
POST   /api/forecasts/compare      Compare models

GET    /api/dashboard/stats        Dashboard KPIs
GET    /api/analytics/region-wise  Region breakdown
GET    /api/analytics/ai-insights  AI insights

POST   /api/anomalies/detect       Run anomaly detection
GET    /api/intelligence/executive-dashboard  Executive BI
POST   /api/scenarios/             Create what-if scenario
POST   /api/scenarios/compare      Compare scenarios

GET    /api/organizations/         List organizations
POST   /api/approvals/submit       Submit forecast for approval
POST   /api/approvals/{id}/review  Approve or reject
POST   /api/workflows/{id}/run     Execute workflow
GET    /api/kpis/                  List KPIs
POST   /api/governance/data-quality/{id}  Run quality check
Features by Module
Core (Phase 1–2)
JWT authentication with role-based access control (super_admin, analyst, viewer)
Dataset upload (CSV, Excel) with automatic processing
ML forecasting with 6 model types
Admin panel with user management
Real-time notifications
Analytics (Phase 3)
Anomaly detection using IQR + Z-Score
Ensemble forecasting (weighted by R² score)
Region-wise and category-wise breakdowns
Revenue prediction and inventory risk analysis
DB-backed API caching
Dark/light mode
Automation (Phase 4)
Automated forecast schedules (daily/weekly/monthly)
Threshold-based alerts with email notifications
ERP, webhook, and external API integrations
AI features: EOQ, demand spikes, buying behavior, low-stock prediction
Configurable dashboard widgets
API rate limiting
Business Intelligence (Phase 5)
Executive Dashboard with KPIs, revenue trends, model performance
What-If Scenario Analysis with variable sliders
Side-by-side scenario comparison charts
AI Insights Engine with demand opportunity detection
Forecast Accuracy Center with model leaderboard
Collaboration: comments, replies, share links, revision history
Forecast Workspaces (Projects) with activity tracking
Executive report export (HTML → PDF via browser print)
Enterprise (Phase 6)
Multi-organization management with member roles
Forecast Approval Workflow with audit trail
Configurable Workflow Automation engine
KPI Management with progress tracking and alerts
Strategic Targets (annual/quarterly/monthly)
Governance Center with forecast lifecycle management
Data Quality Scoring (completeness, consistency, validity)
Organization-wide Announcements
ML Models
Model	Description	Best For
linear_regression	Fast baseline	Simple linear trends
ridge_regression	L2 regularized linear	Noisy linear data
random_forest	Ensemble of decision trees	Non-linear patterns
gradient_boosting	Boosting ensemble	High accuracy needs
prophet	Meta's time-series model	Strong seasonality
ensemble	Weighted combo of all 4	Best overall accuracy
How Ensemble Works
Runs all 4 sklearn models, weights each by its R² score, returns a weighted average prediction. Automatically picks the best combination for your data.

Sample Datasets
sales_data.csv
date, product, category, region, channel,
units_sold, unit_price, revenue, discount_pct,
cost_per_unit, profit, customer_id, warehouse
Use for: Forecasting (target: revenue or units_sold), Analytics, AI Features

inventory_data.csv
date, product, warehouse, opening_stock, units_received,
units_sold, closing_stock, reorder_point, safety_stock,
days_of_supply, stock_status
Use for: Low-stock prediction, Inventory risk analysis

customer_behaviour.csv
date, customer_id, product, category, region, channel,
visit_count, purchase_count, avg_order_value,
days_since_last_purchase, customer_segment, churn_risk
Use for: Buying behavior analysis

demand_forecast.csv
date, product, region, actual_demand, forecasted_demand,
forecast_error, mape_pct, trend, seasonality_index, promotion_active
Use for: Model comparison, Accuracy benchmarking

Environment Variables
Variable	Description	Example
DATABASE_URL	MySQL connection string	mysql+pymysql://root:pass@localhost:3306/demand_forecasting
SECRET_KEY	JWT signing key (min 32 chars)	my-super-secret-key-32-chars-long
UPLOAD_DIR	Directory for dataset uploads	uploads
SMTP_HOST	Email server host	smtp.gmail.com
SMTP_PORT	Email server port	587
SMTP_USER	Email sender address	alerts@company.com
SMTP_PASSWORD	Email password or app password	your-app-password
RATE_LIMIT_ENABLED	Enable API rate limiting	true
License
This project is proprietary enterprise software developed for internal use.
