# CertiCraft - Technical Documentation

## 1. Introduction
CertiCraft is a full-stack web application designed for organizations and educational institutions to manage events and automate the generation and distribution of certificates. It features a modern, premium UI with a University-inspired aesthetic (Navy & Gold).

## 2. System Architecture
CertiCraft follows a decoupled **Client-Server Architecture**.

### 2.1 Frontend (Client)
- **Framework**: React.js (built with Vite for performance).
- **State Management**: React Hooks (`useState`, `useEffect`, `useContext`).
- **Routing**: `react-router-dom` for navigation.
- **API Client**: Axios with interceptors for automatic JWT token attachment.
- **Styling**: Vanilla CSS with a global Design System (`index.css`) for high flexibility and performance.
- **Charts**: Recharts for visualizing event analytics.

### 2.2 Backend (Server)
- **Runtime**: Node.js.
- **Framework**: Express.js.
- **ORM**: Sequelize (supports PostgreSQL, MySQL, SQLite).
- **Authentication**: Stateless JWT-based authentication.
- **File Handling**: Multer for processing high-quality certificate templates and CSV participant lists.

### 2.3 Database Schema
The system uses a relational schema:
- **User**: Stores organizer details (name, email, password hashes).
- **Event**: Core entity representing a ceremony or seminar.
- **Participant**: Individuals registered for an event.
- **Certificate**: Metadata about generated certificates, including verification IDs.
- **Template**: Storage paths and coordinate settings (X, Y) for dynamic PDF positioning.
- **Collaborator**: Relationship mapping for team-based event management.
- **Message**: Internal communication logs for event teams.

---

## 3. Core Features & Logic

### 3.1 Dynamic PDF Generation
The system uses `pdfkit` and `canvas` to overlay participant names onto organized templates. 
- **Coordinates**: Users can visually or numerically set X/Y coordinates for the name and QR code.
- **QR Codes**: Every certificate contains a unique QR code linked to a verification URL.

### 3.2 Verification System
CertiCraft provides a public route (`/verify/:id`) that allows anyone with the certificate's unique ID or QR code to verify its authenticity against the database.

### 3.3 Bulk Actions
- **CSV Upload**: Organizers can upload a CSV to import hundreds of participants at once.
- **Mass Emailing**: Uses Nodemailer with Gmail/SMTP to send certificates to all participants in one click.
- **ZIP Download**: Bundles all generated PDFs into a single ZIP file for offline storage.

### 3.4 Team Collaboration
Owners can invite other users to help manage events. Permissions are enforced so only the owner can delete events or remove teammates.

---

## 4. Tech Stack Dependencies

### Backend Dependencies
- `express`: Web framework.
- `sequelize`: ORM for database operations.
- `jsonwebtoken`: Secure user sessions.
- `bcrypt`: Password hashing.
- `pdfkit`: PDF generation library.
- `canvas`: Pixel-perfect rendering for QR codes and image processing.
- `nodemailer`: Email dispatching.
- `archiver`: ZIP compression logic.
- `multer`: File upload middleware.

### Frontend Dependencies
- `react`: UI library.
- `react-router-dom`: SPA routing.
- `axios`: Promise-based HTTP requests.
- `recharts`: Data visualization charts.
- `@lottiefiles/dotlottie-react`: Lightweight animations.

---

## 5. Directory Structure
```text
CertiCraft/
├── backend/
│   ├── src/
│   │   ├── models/       # Sequelize definitions
│   │   ├── routes/       # API endpoints (Auth, Events, Certs)
│   │   ├── utils/        # Generators, Emailers, Helpers
│   │   └── index.js      # Entry point
│   ├── uploads/          # Physical storage for PDF/Images
│   └── .env              # Backend configuration
├── frontend/
│   ├── src/
│   │   ├── components/   # React components (Dashboard, Management)
│   │   ├── services/     # API abstraction layer
│   │   └── App.jsx       # Main router
│   └── vite.config.js    # Build configuration
└── documentation/        # Detailed project guides
```
