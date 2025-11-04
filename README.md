# Event-Oh Client

A modern, full-featured event management platform built with React. Event-Oh connects customers with vendors for seamless event planning, booking, and payment processing.

## 🎯 Overview

Event-Oh is a comprehensive event management application that facilitates bookings between customers and vendors. The platform supports three distinct user roles: **Customers**, **Vendors**, and **Admins**, each with tailored features and permissions.

### Key Features

- 🏛️ **Vendor Management**: Browse and discover venues, freelancers, and event teams
- 📅 **Booking System**: Easy date selection with availability checking
- 💳 **Payment Integration**: Secure Stripe payments with advance and final payment options
- 👤 **Role-Based Access**: Separate dashboards for customers, vendors, and admins
- ✅ **Verification System**: Admin-powered vendor verification workflow
- 📊 **Analytics Dashboard**: Real-time stats for vendors and admins
- 🖼️ **Portfolio Management**: Image uploads and portfolio display for vendors
- 🔍 **Advanced Filtering**: Search vendors by type, city, price, rating, and verification status

## 🚀 Tech Stack

- **Frontend Framework**: React 19.1.1
- **Build Tool**: Vite 7.1.7
- **Routing**: React Router DOM 7.9.5
- **Styling**: TailwindCSS 4.1.16
- **HTTP Client**: Axios 1.13.1
- **Payment Processing**: Stripe (@stripe/stripe-js 8.2.0)
- **Code Quality**: ESLint with React plugins

## 📦 Installation

### Prerequisites

- Node.js (v18 or higher recommended)
- npm or yarn package manager
- Backend API server running (see backend repository)

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd EventOh-Client
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Configure environment variables**
   
   Create a `.env` file in the root directory:
   ```env
   VITE_API_URL=http://localhost:5000/api
   VITE_API_STRIPE_PUBLIC_KEY=your_stripe_public_key_here
   ```

4. **Start the development server**
   ```bash
   npm run dev
   ```

   The application will be available at `http://localhost:5173` (or the port shown in your terminal).

## 🏗️ Project Structure

```
EventOh-Client/
├── src/
│   ├── components/          # Reusable UI components
│   │   ├── Button.jsx
│   │   ├── Dropdown.jsx
│   │   ├── FileUploader.jsx
│   │   ├── InputField.jsx
│   │   ├── Navbar.jsx
│   │   ├── Snackbar.jsx
│   │   └── TextArea.jsx
│   ├── hooks/               # Custom React hooks
│   │   ├── useAuthRedirect.js
│   │   └── useAxios.js      # Axios wrapper with interceptors
│   ├── layout/              # Layout components
│   │   └── Layout.jsx
│   ├── pages/               # Page components
│   │   ├── admin/           # Admin-specific pages
│   │   │   ├── AdminDashboard.jsx
│   │   │   ├── AdminLayout.jsx
│   │   │   └── VendorsList.jsx
│   │   ├── vendors/         # Vendor-specific pages
│   │   │   ├── VendorDashboard.jsx
│   │   │   ├── VendorDetails.jsx
│   │   │   └── VendorPofile.jsx
│   │   ├── CustomerProfile.jsx
│   │   ├── CustomerRegister.jsx
│   │   ├── Home.jsx
│   │   ├── Login.jsx
│   │   ├── PaymentSuccess.jsx
│   │   ├── VendorList.jsx
│   │   └── VendorRegister.jsx
│   ├── router/              # Routing configuration
│   │   └── router.jsx
│   ├── App.jsx              # Main app component
│   ├── main.jsx             # Application entry point
│   └── index.css            # Global styles
├── public/                  # Static assets
├── dist/                    # Build output
├── index.html
├── package.json
├── vite.config.js
└── vercel.json             # Vercel deployment config
```

## 🎭 User Roles & Features

### 👤 Customer
- Browse and search vendors
- View vendor profiles and portfolios
- Book venues/services with date selection
- Make advance payments (20% of total)
- Pay remaining balance after event
- View booking history
- Manage profile

### 💼 Vendor
- Register as venue or freelancer
- Create and manage venue units
- Upload portfolio images
- View booking requests
- Track earnings and statistics
- Manage vendor profile
- View verified/pending status

### 🧠 Admin
- View all registered vendors
- Verify vendor venue units
- Monitor platform statistics
- Access admin dashboard

## 🔐 Authentication & Authorization

The application uses JWT-based authentication with role-based access control:

- **Token Storage**: JWT tokens stored in `localStorage`
- **Protected Routes**: Role-based route guards prevent unauthorized access
- **Auto-redirect**: Users are automatically redirected based on their role after login

### Route Protection

- `ProtectedRoute`: Requires authentication (any role)
- `AdminProtectedRoute`: Requires admin role
- `VendorProtectedRoute`: Requires vendor role

## 💳 Payment Flow

1. **Booking Creation**: Customer selects dates and creates booking
2. **Advance Payment**: 20% advance payment via Stripe Checkout
3. **Booking Confirmation**: Booking status changes to "confirmed"
4. **Final Payment**: Customer can pay remaining 80% after event
5. **Payment Success**: Redirects to success page with booking confirmation

## 🔌 API Integration

The application communicates with a backend API. Key endpoints used:

### Authentication
- `POST /api/auth/login` - User login
- `POST /api/customers/register` - Customer registration
- `POST /api/vendors/register` - Vendor registration

### Vendors
- `GET /api/vendors` - List all vendors
- `GET /api/vendors/:id` - Get vendor details
- `GET /api/vendors/myProfile` - Get logged-in vendor profile
- `GET /api/vendors/:id/booked-dates` - Get booked dates
- `PATCH /api/vendors/:id/availability` - Update availability
- `POST /api/vendors/:id/upload` - Upload images

### Bookings
- `GET /api/bookings` - Get user bookings
- `POST /api/bookings` - Create booking
- `PUT /api/bookings/:id/status` - Update booking status
- `PUT /api/bookings/:id/mark-paid` - Mark as fully paid
- `POST /api/bookings/:id/pay-remaining` - Pay remaining balance

### Payments
- `POST /api/payments/create-checkout-session` - Create Stripe checkout session

### Admin
- `GET /api/admin/vendors` - List all vendors (admin)

## 🛠️ Development

### Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build
- `npm run lint` - Run ESLint

### Code Style

- Uses ESLint for code quality
- Follows React best practices
- TailwindCSS utility-first styling
- Component-based architecture

## 📱 Responsive Design

The application is fully responsive and works seamlessly on:
- Desktop (1920px and above)
- Tablet (768px - 1024px)
- Mobile (320px - 767px)

## 🚀 Deployment

### Vercel Deployment

The project includes `vercel.json` configuration for easy deployment on Vercel:

1. Push code to GitHub
2. Import project in Vercel
3. Configure environment variables
4. Deploy

### Environment Variables for Production

Ensure these are set in your deployment platform:
- `VITE_API_URL` - Your backend API URL
- `VITE_API_STRIPE_PUBLIC_KEY` - Stripe publishable key

## 🔧 Configuration

### Vite Configuration

The `vite.config.js` includes:
- React plugin with SWC for fast refresh
- TailwindCSS plugin
- Proxy configuration for API calls during development
- Base path configuration

### Proxy Setup

During development, API calls are proxied to `http://localhost:5000` to avoid CORS issues.

## 📝 Notes

- The application uses React 19 with modern hooks and patterns
- Image uploads are handled via Cloudinary (backend integration)
- All API calls use the `useAxios` hook with automatic token injection
- Date selection includes overlap checking against existing bookings
- Payment success page handles both advance and final payment flows

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is private and proprietary.

## 👥 Support

For issues or questions, please contact the development team or open an issue in the repository.

---

