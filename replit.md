# JinYiTai Energy Technology - Project Overview

## Overview

JinYiTai Energy Technology (金毅泰節能科技) is a B2B energy solutions company website built as a single-page application. The application showcases the company's services in solar photovoltaic systems, heat pump technology, energy storage, and AI-powered energy management systems (EMS). The website targets Taiwanese enterprises seeking sustainable energy solutions and net-zero carbon emissions.

The application is a full-stack TypeScript project using React for the frontend and Express for the backend, with a PostgreSQL database for storing contact inquiries.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework**: React 18 with TypeScript, using Vite as the build tool and development server.

**Routing**: Wouter is used for client-side routing, providing a lightweight alternative to React Router. The application is primarily a single-page site with one main route (`/`) and a 404 page.

**UI Component System**: The project uses shadcn/ui components built on Radix UI primitives, providing accessible and customizable components. The design system follows a "New York" style variant with extensive Tailwind CSS customization.

**State Management**: TanStack Query (React Query) manages server state and API interactions. No global client state management library is used, keeping state local to components.

**Styling Approach**: Tailwind CSS with custom design tokens defined in CSS variables. The design follows specific guidelines for Traditional Chinese typography using Noto Sans TC and Montserrat fonts. Color scheme uses a professional teal/green palette (`--primary: 174 100% 33%`, `--secondary: 145 63% 42%`) aligned with energy and sustainability themes.

**Key Design Patterns**:
- Component composition with reusable UI primitives
- Intersection Observer API for scroll-triggered animations
- Responsive design with mobile-first approach
- Traditional Chinese language optimization throughout
- Local image assets stored in `attached_assets/stock_images/` and `attached_assets/generated_images/`

**Page Sections** (in order):
1. HeroSection - Full-screen hero with background image
2. AboutSection - Company introduction with team photo
3. ServicesSection - 5 core services (solar, heat pump, storage, AI EMS, ESCO)
4. SolarPVDiagram - Technical diagram explaining solar photovoltaic system principles, specifications, and benefits
5. HeatPumpDiagram - Technical diagram explaining heat pump system operation
6. EnergyStorageDiagram - Technical diagram explaining energy storage integration, applications, and benefits
7. ESCODiagram - Technical diagram explaining ESCO service model, process steps, and target audience
8. CasesSection - 6 success case studies with category filtering
9. PartnersSection - Partner logos/names
10. ContactSection - Contact form with validation and map

### Backend Architecture

**Framework**: Express.js server running on Node.js with TypeScript.

**API Design**: RESTful API with two main endpoints:
- `POST /api/contact` - Creates contact inquiries from website forms
- `GET /api/contact` - Retrieves all contact inquiries (admin functionality)

**Request Handling**: Express middleware stack includes:
- JSON body parsing with raw body preservation for webhook verification
- URL-encoded form data support
- Request logging with timestamp and duration tracking
- Static file serving for production builds

**Development vs Production**:
- Development: Vite dev server middleware with HMR support
- Production: Serves pre-built static files from `dist/public`
- Build process uses esbuild for server bundling with selective dependency bundling

**Error Handling**: Input validation using Zod schemas with detailed error responses. Server errors return appropriate HTTP status codes with user-friendly messages in Traditional Chinese.

### Data Storage Solutions

**Database**: PostgreSQL accessed via Neon Serverless driver for serverless-compatible connection pooling.

**ORM**: Drizzle ORM provides type-safe database queries and schema management. Schema definitions use Drizzle's PostgreSQL column types with automatic TypeScript type inference.

**Schema Structure**:
- `users` table: Basic authentication structure (id, username, password) - appears to be planned but not actively used
- `contact_inquiries` table: Stores website contact form submissions (id, name, email, company, message, created_at)

**Data Access Pattern**: Repository pattern implemented through `DatabaseStorage` class, abstracting database operations behind an interface (`IStorage`). This allows for potential storage backend swapping without changing application logic.

**Migrations**: Drizzle Kit manages schema migrations with configuration pointing to `./migrations` directory. Schema source is `./shared/schema.ts`.

### Authentication and Authorization

**Authentication System**: Session-based authentication using express-session with bcrypt password hashing.

**Admin Interface** (`/admin`):
- Login page at `/admin/login`
- Dashboard for content management at `/admin`
- Access link in website footer

**Default Admin Credentials**:
- Username: `admin`
- Password: `admin123`

**Protected Endpoints**: All content modification endpoints (PUT, POST, DELETE) require authentication. Read endpoints are public for website display.

### Content Management System (CMS)

**Database Tables**:
- `content_sections`: Defines editable sections (hero, about, services, contact, footer)
- `content_blocks`: Individual editable fields within sections (text, rich_text, image types)
- `media_assets`: Uploaded images with metadata

**Content Types**:
- `text`: Single-line text fields
- `rich_text`: Multi-line text areas
- `image`: Uploaded image files

**Admin Features**:
- Edit text content for any section
- Upload and replace images
- View content in organized tabs by section
- Logout and view live site buttons

### External Dependencies

**Database Service**: Neon Serverless PostgreSQL - provides serverless-compatible PostgreSQL with connection pooling optimized for edge deployments.

**Frontend Libraries**:
- Radix UI primitives for accessible component foundations
- Lucide React for icon system
- React Icons for additional social media icons
- TanStack Query for data fetching and caching
- React Hook Form with Zod resolvers for form validation
- Wouter for lightweight routing

**Development Tools**:
- Vite with React plugin for development server
- Replit-specific plugins for error overlays and development banners
- ESBuild for production server bundling
- Drizzle Kit for database migrations
- PostCSS with Tailwind CSS and Autoprefixer

**Build & Deployment**:
- Custom build script (`script/build.ts`) orchestrates both client (Vite) and server (esbuild) builds
- Server dependencies are selectively bundled to reduce cold start times
- Static assets served from `dist/public` in production

**Font Delivery**: Google Fonts CDN delivers Noto Sans TC and Montserrat fonts, optimized for Traditional Chinese typography.

**Potential Third-Party Services** (referenced but not configured):
- Email services (nodemailer dependency suggests planned email notifications)
- Session management (express-session, connect-pg-simple for PostgreSQL-backed sessions)
- File uploads (multer dependency present)

### Email Notifications (Resend Integration)

**Email Service**: Resend integration is configured to send email notifications when new contact form submissions are received.

**Configuration File**: `server/resend.ts` - Contains the Resend client initialization and email sending function.

**How It Works**:
1. When a visitor submits the contact form, the server saves the inquiry to the database
2. An email notification is sent to `osric@ledaplus.com.tw` with the inquiry details
3. The email includes: sender name, email, company (if provided), and message

**Email Format**:
- Subject: `[金毅泰] 新客戶諮詢 - {name}`
- HTML formatted table with inquiry details
- Reply-to set to the customer's email address

**Admin Dashboard Features**:
- Two main tabs: "客戶訊息" (Customer Inquiries) and "內容管理" (Content Management)
- Customer inquiries are displayed with name, email, company, message, and submission date
- Inquiries can be viewed and emails can be sent directly via mailto links

**Domain Verification Required**:
To enable email sending in production, the sending domain must be verified in the Resend dashboard. Currently using the Replit Resend integration which requires domain verification for custom "from" addresses.

**Fallback Behavior**:
If email sending fails (e.g., due to domain verification issues), the contact form submission is still saved to the database. The admin can view all inquiries through the admin dashboard.