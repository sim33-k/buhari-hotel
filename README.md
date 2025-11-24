A web-based restaurant ordering application for Buhari Hotel. This system allows waiters to manage customer orders and view business reports.

## Live Deployment

**Live Application:** https://buhari-frontend.vercel.app/menu

## Technology Stack

- **Frontend:** React 19.x, TypeScript, Vite, Tailwind CSS 4.x, Shadcn UI, Radix UI
- **Backend:** Node.js, Express.js 5.x, TypeScript 5.x
- **Database:** PostgreSQL with Prisma ORM 6.x
- **Backend as a Service:** Supabase
- **Additional Libraries:** Recharts, React Router

## Features

- Menu browsing with categorization (Main Dish, Side Dish, Dessert)
- Order creation with business rule enforcement
- Order history and management
- Business analytics and reports:
  - Daily sales revenue
  - Most famous main dish
  - Most famous side dish
  - Most famous dessert
  - Side dish combinations with main dishes
  - Sales history trends

## Deployment Instructions

### Prerequisites

Before deploying the application, ensure the following software is installed:

- Node.js (v18.0.0 or higher)
- npm (v9.0.0 or higher)
- Git (for cloning the repository)
- Supabase account (for database hosting)

### Database Setup with Supabase

#### Option 1: Supabase Cloud (Recommended)

**Step 1: Create Supabase Project**

1. Go to https://supabase.com and sign up or login
2. Click "New Project"
3. Enter project name, database password, and select region
4. Wait for project to be provisioned

**Step 2: Get Database Connection Strings**

1. Go to Project Settings → Database
2. Copy the "Connection Pooling" URL (for DATABASE_URL)
3. Copy the "Direct Connection" URL (for DIRECT_URL)

#### Option 2: Local Supabase (Development)

```bash
# Install Supabase CLI
npm install -g supabase

# Initialize Supabase locally
supabase init

# Start local Supabase
supabase start
```

#### Step 3: Configure Environment Variables

Create a `.env` file in the `backend` directory:

```bash
BACKEND_URL=http://localhost:3000

# Connection pooling URL (for queries)
DATABASE_URL="postgresql://postgres.[PROJECT-REF]:[PASSWORD]@aws-1-ap-southeast-1.pooler.supabase.com:5432/postgres"

# Direct connection URL (for migrations)
DIRECT_URL="postgresql://postgres.[PROJECT-REF]:[PASSWORD]@aws-1-ap-southeast-1.pooler.supabase.com:5432/postgres"
```

**Note:** Replace `[PROJECT-REF]` and `[PASSWORD]` with your actual Supabase credentials.

#### Step 4: Run Database Migrations

```bash
cd backend
npx prisma migrate dev
npx prisma generate
```

#### Step 5: Seed Database

Populate the database with initial menu items:

```bash
npx prisma db seed
```

This creates 3 types (Main Dish, Side Dish, Dessert) and 9 menu items (Rice, Rotty, Noodles, Wadai, Dhal Curry, Fish Curry, Watalappam, Jelly, Pudding).

### Backend Setup

**Step 1: Install Dependencies**

```bash
cd backend
npm install
```

**Step 2: Build the Application**

```bash
npm run build
```

**Step 3: Start the Server**

```bash
# Production mode
npm start

# Development mode (with auto-reload)
npm run dev
```

The backend server will start on `http://localhost:3000`

### Frontend Setup

**Step 1: Install Dependencies**

```bash
cd frontend
npm install
```

**Step 2: Configure API Endpoint**

Ensure the frontend is configured to connect to the backend API. Update the API base URL in the frontend configuration if needed.

**Step 3: Build and Start**

```bash
# Development mode
npm run dev

# Production build
npm run build
npm run preview
```

The frontend application will be available at `http://localhost:5173` (development) or `http://localhost:4173` (preview).

### Accessing the Application

1. Ensure both backend and frontend servers are running
2. Open a web browser
3. Navigate to `http://localhost:5173` (or the configured frontend URL)
4. The application is ready to use

## Troubleshooting

**Database Connection Issues:**
- Verify Supabase project is active
- Check DATABASE_URL and DIRECT_URL in .env file
- Ensure credentials are correct

**Port Conflicts:**
- Change PORT in backend .env file if 3000 is in use
- Update frontend API configuration to match new backend port

**Build Errors:**
- Delete node_modules and package-lock.json
- Run `npm install` again
- Ensure Node.js version meets requirements

## Project Structure

```
.
├── backend/
│   ├── src/
│   │   ├── config/          # Configuration files
│   │   ├── controllers/     # HTTP request handlers
│   │   ├── services/        # Business logic
│   │   ├── repositories/    # Data access layer
│   │   ├── routes/          # API route definitions
│   │   ├── middleware/      # Express middleware
│   │   └── utils/           # Utility functions
│   ├── prisma/
│   │   └── schema.prisma    # Database schema
│   └── server.ts            # Application entry point
├── frontend/
│   ├── src/
│   │   ├── pages/           # Page components
│   │   ├── components/      # Reusable UI components
│   │   ├── types/           # TypeScript type definitions
│   │   └── lib/             # Utility functions
│   └── public/              # Static assets
└── README.md
```

