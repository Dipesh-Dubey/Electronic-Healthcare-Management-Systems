# Electronic Healthcare Management System (EHCMS)

A comprehensive healthcare management platform built with the MERN stack, featuring patient management, appointment scheduling, prescription management, and OCR-powered document processing.

## 🏗️ Architecture

### Tech Stack
- **Frontend**: React 18 + TypeScript + Vite
- **Backend**: Node.js + Express.js
- **Database**: MongoDB with Mongoose ODM
- **OCR Service**: Python Flask + Google Gemini API
- **UI Framework**: Tailwind CSS + Shadcn UI
- **Authentication**: JWT-based with role-based access control

### System Components
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   React Frontend │    │  Node.js Backend │    │  Python OCR     │
│   (Port 8080)   │◄──►│   (Port 5000)   │◄──►│   (Port 5001)   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                              │
                              ▼
                       ┌─────────────────┐
                       │    MongoDB      │
                       │   (Port 27017)  │
                       └─────────────────┘
```

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ and npm
- Python 3.8+ and pip
- MongoDB (local or cloud)
- Google Gemini API key

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd Electronic-Healthcare-Management-Systems
   ```

2. **Backend Setup**
   ```bash
   cd backend
   npm install
   cp .env.example .env
   # Edit .env with your MongoDB URI and JWT secret
   ```

3. **OCR Service Setup**
   ```bash
   cd backend/ocr_service
   pip install -r requirements.txt
   # Set GOOGLE_API_KEY in your environment
   ```

4. **Frontend Setup**
   ```bash
   cd ../../
   npm install
   ```

### Environment Variables

**Backend (.env)**
```env
MONGO_URI=mongodb://localhost:27017/ehcms
JWT_SECRET=your_jwt_secret_here
PORT=5000
```

**OCR Service**
```env
GOOGLE_API_KEY=your_google_gemini_api_key
```

## 🏃‍♂️ Running the Application

### Development Mode

1. **Start MongoDB** (if running locally)
   ```bash
   mongod
   ```

2. **Start OCR Service**
   ```bash
   cd backend/ocr_service
   python app.py
   ```

3. **Start Backend**
   ```bash
   cd backend
   npm run dev
   ```

4. **Start Frontend**
   ```bash
   npm run dev
   ```

### Production Mode

Use the provided batch files:
```bash
# Windows
start_project.bat

# Or manually
start_fixed.bat
```

## 📋 Core Features

### 1. User Management
- **Patient Registration**: Complete onboarding with demographics
- **Doctor Management**: Provider profiles and specialties
- **Role-based Access**: Patient, Doctor, and Front Desk roles
- **JWT Authentication**: Secure login/logout with token management

### 2. Appointment System
- **Booking**: Patients can book appointments with available doctors
- **Scheduling**: Real-time availability checking
- **Management**: View, cancel, and reschedule appointments
- **Queue System**: Token-based queue management for same-day visits

### 3. Prescription Management
- **E-Prescriptions**: Digital prescription creation and management
- **OCR Processing**: Automatic prescription data extraction from images
- **Patient Access**: View prescriptions and medication history
- **Refill Management**: Track medication refills and reminders

### 4. Document Processing (OCR)
- **ID Card Scanning**: Extract patient information from ID cards
- **Insurance Card Processing**: Parse insurance details
- **Prescription OCR**: Extract medication data from prescription images
- **Lab Results**: Process and categorize lab reports

### 5. Clinical Management
- **Encounter Documentation**: SOAP notes and clinical documentation
- **Patient Records**: Comprehensive medical history
- **Lab Orders**: Order and track laboratory tests
- **Billing Integration**: Invoice and claims management

## 🔐 User Roles & Permissions

### Patient
- Book and manage appointments
- View prescriptions and lab results
- Upload documents for OCR processing
- Access personal medical records

### Doctor
- View patient appointments and schedules
- Create and manage prescriptions
- Document clinical encounters
- Access patient medical records
- Process lab orders and results

### Front Desk
- Manage appointment queue
- Check-in patients
- Handle patient registration
- Process insurance information

## 🛠️ API Endpoints

### Authentication
- `POST /api/auth/login` - User login
- `POST /api/auth/signup` - User registration
- `GET /api/auth/me` - Get current user

### Appointments
- `GET /api/appointments/patient` - Get patient appointments
- `GET /api/appointments/provider` - Get doctor appointments
- `POST /api/appointments/book` - Book new appointment
- `PUT /api/appointments/:id/cancel` - Cancel appointment
- `GET /api/appointments/slots` - Get available time slots

### Prescriptions
- `GET /api/prescriptions/patient` - Get patient prescriptions
- `GET /api/prescriptions/doctor` - Get doctor prescriptions
- `POST /api/prescriptions` - Create new prescription
- `PUT /api/prescriptions/:id` - Update prescription

### Documents
- `POST /api/documents/upload` - Upload document for OCR
- `GET /api/documents` - Get user documents
- `GET /api/documents/:id` - Get specific document

### OCR Service
- `POST /ocr/classify` - Classify document type
- `POST /ocr/extract` - Extract data from document

## 📁 Project Structure

```
Electronic-Healthcare-Management-Systems/
├── backend/                    # Node.js backend
│   ├── controllers/           # API route handlers
│   ├── models/               # MongoDB schemas
│   ├── routes/               # Express routes
│   ├── middleware/           # Authentication & validation
│   ├── ocr_service/          # Python OCR service
│   ├── uploads/              # File uploads
│   └── server.js             # Main server file
├── src/                      # React frontend
│   ├── components/           # Reusable UI components
│   │   ├── auth/            # Authentication components
│   │   ├── doctor/          # Doctor-specific components
│   │   ├── patient/         # Patient-specific components
│   │   ├── layout/          # Layout components
│   │   └── ui/              # Base UI components
│   ├── pages/               # Page components
│   ├── hooks/               # Custom React hooks
│   ├── lib/                 # Utility functions
│   └── App.tsx              # Main app component
├── public/                   # Static assets
└── README.md                # This file
```

## 🔧 Development Workflow

### 1. Database Setup
```bash
# Connect to MongoDB
mongosh

# Create database
use ehcms

# Seed initial data (optional)
cd backend
node scripts/seed-data.js
```

### 2. API Development
- Controllers handle business logic
- Models define data schemas
- Routes define API endpoints
- Middleware handles authentication and validation

### 3. Frontend Development
- Components are organized by feature
- Pages handle routing and layout
- Hooks manage state and side effects
- UI components provide consistent styling

### 4. OCR Integration
- Python service processes documents
- Google Gemini API extracts data
- Results are stored in MongoDB
- Frontend displays processed information

## 🧪 Testing

### Backend Testing
```bash
cd backend
npm test
```

### Frontend Testing
```bash
npm test
```

### API Testing
Use the debug endpoints:
- `GET /api/debug/users` - List all users
- `GET /api/debug/appointments` - List all appointments
- `GET /api/debug/patients` - List all patients
- `GET /api/debug/stats` - Database statistics

## 🚀 Deployment

### Backend Deployment
1. Set production environment variables
2. Build and start the server:
   ```bash
   cd backend
   npm start
   ```

### Frontend Deployment
1. Build the production bundle:
   ```bash
   npm run build
   ```
2. Serve the `dist` folder with a web server

### OCR Service Deployment
1. Install Python dependencies
2. Set environment variables
3. Start the Flask service:
   ```bash
   cd backend/ocr_service
   python app.py
   ```

## 📊 Database Schema

### Core Models
- **User**: Authentication and basic profile
- **Patient**: Extended patient information
- **Appointment**: Scheduling and status tracking
- **Prescription**: Medication management
- **Document**: File storage and OCR results
- **Encounter**: Clinical documentation
- **Order**: Lab and imaging orders
- **Billing**: Financial transactions

### Relationships
- User → Patient (1:1)
- Patient → Appointments (1:many)
- Doctor → Appointments (1:many)
- Patient → Prescriptions (1:many)
- Doctor → Prescriptions (1:many)

## 🔒 Security Features

- JWT-based authentication
- Role-based access control
- Password hashing with bcrypt
- CORS configuration
- Input validation and sanitization
- File upload restrictions
- API rate limiting

## 🐛 Troubleshooting

### Common Issues

1. **MongoDB Connection Error**
   - Check MongoDB is running
   - Verify connection string in .env
   - Ensure database permissions

2. **OCR Service Not Working**
   - Verify Google API key is set
   - Check Python dependencies
   - Ensure service is running on port 5001

3. **Frontend Build Errors**
   - Clear node_modules and reinstall
   - Check TypeScript configuration
   - Verify all dependencies are installed

4. **Authentication Issues**
   - Check JWT secret is set
   - Verify token expiration
   - Clear localStorage and re-login

### Debug Mode
Enable debug logging by setting:
```env
NODE_ENV=development
DEBUG=ehcms:*
```

## 📈 Performance Optimization

- Database indexing on frequently queried fields
- Image compression for OCR processing
- Lazy loading for large datasets
- Caching for frequently accessed data
- Connection pooling for database

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🆘 Support

For support and questions:
- Check the troubleshooting section
- Review the API documentation
- Open an issue on GitHub

## 🔄 Version History

- **v1.0.0** - Initial release with core features
- **v1.1.0** - Added OCR integration
- **v1.2.0** - Enhanced prescription management
- **v1.3.0** - Improved appointment system
- **v1.4.0** - Added clinical documentation

---

**Built with ❤️ for better healthcare management**
