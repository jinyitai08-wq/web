# 金毅泰節能科技 Design Guidelines

## Design Approach
**Reference-Based + System Hybrid**: Drawing inspiration from professional B2B tech companies (Siemens, Schneider Electric) combined with modern web patterns for trust and credibility. Focus on clean, professional layouts that emphasize expertise and technical capability.

## Core Design Principles
- **Professional Trust**: B2B-focused design emphasizing technical credibility and corporate reliability
- **Content Clarity**: Information-dense sections presented with breathing room and clear hierarchy
- **Cultural Appropriateness**: Traditional Chinese language optimization with Noto Sans TC font family throughout

## Typography System
**Font Stack**: 'Noto Sans TC', 'Microsoft JhengHei', sans-serif (via Google Fonts CDN)

**Hierarchy**:
- H1 (Hero Headlines): 2.5rem (40px), weight 800, tight line-height 1.2
- H2 (Section Headers): 2rem (32px), weight 700, with decorative underline accent
- H3 (Card Titles): 1.25rem (20px), weight 600
- Body Text: 1rem (16px), weight 400, line-height 1.6
- Small Text/Labels: 0.9-0.95rem, weight 500

## Layout System
**Spacing Primitives**: Use Tailwind units of 4, 8, 12, 16, 20, 24, 32, 40, 80
- Section vertical padding: py-20 (80px)
- Card gaps: gap-8 (32px)
- Inner content spacing: p-5 or p-6
- Form field margins: mb-5

**Container Strategy**:
- Full-width sections with max-w-7xl centered containers
- Content sections: max-w-6xl
- Forms: max-w-2xl (600px)

## Component Library

### Navigation
- Fixed header at top, semi-transparent backdrop
- Horizontal navigation with 25px gaps between items
- Smooth scroll behavior for anchor links
- Underline hover animation from left to right
- Mobile: Stack vertically with 15px gaps

### Hero Section
- Height: 90vh minimum 500px
- Background image with 55% opacity overlay
- Centered content with max-width 1000px
- Prominent CTA button below headline and description
- Text with subtle shadow for readability over images

### Service/Feature Cards
- Fixed width 280px desktop, full-width mobile (max 350px)
- Image at top (height 180px, object-fit cover)
- Padding inside card content: 20px
- Rounded corners: 16px
- Lift on hover: translateY(-10px)
- Shadow elevation on hover

### Forms
- Max-width 600px centered
- Label above input pattern
- Input fields: 12px padding, 8px border-radius
- Textarea minimum height: 120px
- Full-width submit button at bottom
- Light background (#fafafa) with focus state transition

### Image Cards (Case Studies/News)
- 3-column grid on desktop, single column mobile
- Consistent aspect ratio for images
- Overlay title and brief description
- "Learn More" link or button

### Partner Logos Section
- Horizontal scrollable row or grid layout
- Grayscale logos with subtle hover brightness
- Even spacing between logos

### Footer
- Multi-column layout (Company Info | Quick Links | Contact)
- Copyright and address information clearly displayed
- Social media icon links if applicable

## Images Strategy

**Hero Section**: Large, high-impact background image showing solar panels, modern energy facilities, or green technology. Source from Unsplash with keywords: "solar panel technology", "industrial green energy", "modern sustainable building"

**Service Cards**: Each service needs a representative image:
- Solar/Photovoltaic: Solar panel arrays, installation work
- Heat Pump: HVAC systems, mechanical equipment
- Energy Storage: Battery systems, power cabinets
- AI EMS: Data dashboards, monitoring screens, IoT sensors
- ESCO Solutions: Industrial facility improvements

**Success Cases**: Real project photography preferred, or high-quality stock images of:
- Commercial buildings with solar installations
- Factory facilities
- Green building exteriors
- Energy monitoring displays

**About Section**: Team photo or modern office environment showing professionalism

## Interaction Patterns
- Scroll-triggered fade-in animations for sections (opacity 0→1, translateY 40px→0)
- Smooth scroll navigation between sections
- Card hover states with elevation change
- Button hover with subtle lift (3px) and shadow increase
- Form input focus states with border accent transition

## Responsive Breakpoints
- Desktop: 1024px+
- Tablet: 768px - 1023px
- Mobile: < 768px

**Mobile Adaptations**:
- Navigation: Vertical stack, centered
- Cards: Single column, centered, max-width 350px
- Hero: Maintain readable text size (1.8rem H1)
- Form: Reduce padding to 20px
- Section padding: Reduce to py-12

## Page-Specific Layouts

**Homepage**:
- Hero with CTA
- Brief company intro (max-w-4xl centered)
- 3-column technology highlights with icons
- Partner logos horizontal strip
- Secondary CTA section

**Services Page**:
- Brief intro paragraph
- 4-5 service cards in responsive grid
- Each card links to detailed service info

**Success Cases**:
- Grid layout with filtering option (if applicable)
- Each case shows: image, project name, key metrics, brief description
- Click to expand or navigate to full case study

**Contact Page**:
- Two-column layout: Form left, Info/Map right (stack on mobile)
- Include LINE and phone CTAs as buttons
- Embedded Google Map

## Accessibility Standards
- Semantic HTML structure
- Sufficient contrast ratios for text
- Focus states on all interactive elements
- Alt text for all meaningful images
- Form labels properly associated with inputs
- ARIA labels where needed for Chinese content