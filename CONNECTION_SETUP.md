# Backend and Frontend Connection Setup

This guide explains how to connect the backend and frontend applications.

## Architecture Overview

- **Backend**: Next.js app running on port 3000 with Supabase integration
- **Frontend**: Next.js app running on port 3001 that connects to backend APIs
- **Database**: Supabase (PostgreSQL)

## Setup Instructions

### 1. Backend Setup (Port 3000)

1. Navigate to the `BACK END` directory:
   ```bash
   cd "BACK END"
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create environment file:
   ```bash
   cp .env.local.example .env.local
   ```

4. Update `.env.local` with your Supabase credentials:
   ```
   NEXT_PUBLIC_SUPABASE_URL=your_supabase_url_here
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key_here
   ```

5. Start the backend server:
   ```bash
   npm run dev
   ```

### 2. Frontend Setup (Port 3001)

1. Navigate to the `FRONT END` directory:
   ```bash
   cd "FRONT END"
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create environment file:
   ```bash
   cp .env.local.example .env.local
   ```

4. Update `.env.local` with backend URL:
   ```
   NEXT_PUBLIC_API_URL=http://localhost:3000
   ```

5. Start the frontend server:
   ```bash
   npm run dev -- -p 3001
   ```

### 3. API Endpoints

The backend now provides the following API endpoints:

#### Authentication
- `POST /api/auth/login` - User login

#### Drills
- `GET /api/drills` - Get all drills (optional coachId filter)
- `POST /api/drills` - Create new drill

#### Assignments
- `GET /api/assignments` - Get assignments (optional coachId/athleteId filters)
- `POST /api/assignments` - Create new assignment
- `PUT /api/assignments/[id]` - Update assignment

#### Dashboard
- `GET /api/dashboard/stats` - Get dashboard statistics

### 4. Features Connected

✅ **Authentication System**
- Frontend login forms connect to backend API
- Session management with localStorage
- Protected routes with authentication context

✅ **API Integration**
- Frontend uses API client to communicate with backend
- CORS configured for cross-origin requests
- Error handling and loading states

✅ **Real-time Data**
- Dashboard statistics from backend
- Drill management through API
- Assignment tracking and updates

### 5. Running Both Applications

To run both applications simultaneously:

1. **Terminal 1** - Backend:
   ```bash
   cd "BACK END"
   npm run dev
   ```

2. **Terminal 2** - Frontend:
   ```bash
   cd "FRONT END"
   npm run dev -- -p 3001
   ```

### 6. Testing the Connection

1. Open http://localhost:3001 in your browser
2. Click "Coach Login" or "Athlete Login"
3. Use test credentials to login (ensure you have data in your Supabase database)
4. Navigate through the application to test API connectivity

### 7. Troubleshooting

**CORS Issues:**
- Ensure backend is running on port 3000
- Check that CORS headers are properly configured in `next.config.ts`

**API Connection Issues:**
- Verify backend is running and accessible at http://localhost:3000
- Check browser network tab for failed requests
- Ensure environment variables are properly set

**Authentication Issues:**
- Verify Supabase credentials are correct
- Check that user data exists in the database
- Ensure database tables are properly set up

## Next Steps

1. Set up your Supabase database with the provided schema
2. Add test data for coaches and athletes
3. Test the complete flow: login → dashboard → create drills → assign drills → submit videos
4. Customize the UI and add additional features as needed
