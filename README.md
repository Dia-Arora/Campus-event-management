# Campus Event Management System

A full-stack web application for managing campus events, enabling students and administrators to create, view, and participate in events efficiently.

## Features

- **User Authentication**: Secure login and registration
- **Event Management**: Create, view, and delete campus events
- **User Roles**: Support for both admin and participant roles
- **Event Participation**: Users can join and leave events
- **Event Analytics**: Dashboard with event statistics and analytics
- **Real-time Updates**: View participant counts 


## Tech Stack

### Backend
- **Node.js** - JavaScript runtime
- **Express.js** - Web framework
- **MongoDB** - NoSQL database


### Frontend
- **React** - UI library


## Project Structure

```
campus-event-management/
├── server.js              # Backend server entry point
├── package.json           # Backend dependencies
├── README.md             # This file
└── frontend/             # React frontend application
    ├── package.json      # Frontend dependencies
    ├── public/           # Static files
    │   ├── index.html
    │   ├── manifest.json
    │   └── robots.txt
    └── src/              # React source code
        ├── App.js        # Main React component
        ├── App.css       # Application styles
        ├── index.js      # React entry point
        ├── index.css     # Global styles
        └── ...
```

## Getting Started

### Prerequisites

- **Node.js** (v14 or higher)
- **npm** or **yarn** package manager
- **MongoDB** account and connection string

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd campus-event-management
   ```

2. **Backend Setup**
   ```bash
   # Install backend dependencies
   npm install

   # Create a .env file (optional, for production)
   # Add your MongoDB connection string and JWT secret
   ```

3. **Frontend Setup**
   ```bash
   cd frontend
   npm install
   ```

### Running the Application

#### Start the Backend Server
```bash
# From the root directory
npm start
# or for development with auto-reload
npm run dev
```
The backend server will run on `http://localhost:5000`

#### Start the Frontend Application
```bash
# From the frontend directory
cd frontend
npm start
```
The frontend will run on `http://localhost:3000`

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register a new user
- `POST /api/auth/login` - Login user
- `POST /api/auth/logout` - Logout user

### Events
- `GET /api/events` - Get all events
- `GET /api/events/:id` - Get event details
- `POST /api/events` - Create a new event (admin only)
- `PUT /api/events/:id` - Update event (admin only)
- `DELETE /api/events/:id` - Delete event (admin only)
- `POST /api/events/:id/join` - Join an event
- `POST /api/events/:id/leave` - Leave an event

### Users
- `GET /api/users/profile` - Get user profile
- `PUT /api/users/profile` - Update user profile
- `GET /api/users/:id/events` - Get user's events

### Analytics
- `GET /api/analytics/dashboard` - Get dashboard analytics

## User Roles

### Admin
- Create, edit, and delete events
- Manage participants
- View analytics and reports
- Access admin dashboard

### Participant
- Browse and view events
- Join and leave events
- View their registered events
- Access personal dashboard

## Database Schema

### User Model
```javascript
{
  name: String (required),
  email: String (required, unique),
  password: String (required),
  role: String (enum: 'admin', 'participant', default: 'participant'),
  createdAt: Date (default: now)
}
```

### Event Model
```javascript
{
  title: String (required),
  description: String (required),
  date: String (required),
  time: String (required),
  venue: String (required),
  organizer: String (required),
  maxParticipants: Number (default: 100),
  participants: [User IDs],
  status: String (enum: 'upcoming', 'completed', 'cancelled', default: 'upcoming'),
  createdBy: User ID,
  createdAt: Date (default: now)
}
```

## Configuration

### Environment Variables

Create a `.env` file in the root directory:

```env
PORT=5000
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/campus_events
JWT_SECRET=your_secret_key_here
NODE_ENV=development
```

**Important**: Change the JWT secret and MongoDB credentials in production!

## Security Notes

⚠️ **Current Security Issues** (To be addressed):
- JWT secret is hardcoded in `server.js` - move to environment variables
- MongoDB credentials are exposed - use environment variables
- CORS is open to all origins - configure for specific domains in production
- Input validation should be added to all endpoints
- Password reset functionality should be implemented

## Usage Examples

### Register a User
```bash
curl -X POST http://localhost:5000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com",
    "password": "password123",
    "role": "participant"
  }'
```

### Create an Event
```bash
curl -X POST http://localhost:5000/api/events \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <token>" \
  -d '{
    "title": "Tech Conference 2024",
    "description": "Annual tech conference",
    "date": "2024-12-15",
    "time": "10:00",
    "venue": "Main Auditorium",
    "organizer": "CS Club",
    "maxParticipants": 200
  }'
```

## Authors

- Dia Arora

