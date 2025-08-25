```markdown
# Plan for Landing Page Redesign for G&M Rental Tools

## Overview
We will create a modern, dynamic landing page to renew the current G&M Rental Tools website. The new design—taking inspiration from samenergy.com.ar—will feature an engaging hero section with bold typography and full-width background imagery, an about/services section with a two-column layout, a partners/clients showcase, and a refined footer. All components will use Tailwind CSS for responsiveness and styling, with careful handling of image loading errors. Best practices in React development, accessibility, and code maintainability will be followed throughout.

## Dependent Files
- **Global Styles**  
  - File: `src/app/globals.css`  
    Update typography, color palette (primary blue, accent yellow, dark text), spacing, and responsive utilities.
- **Main Landing Page**  
  - File: `src/app/page.tsx`  
    Acts as the entry point, importing and assembling the new components.
- **New Components** (to be created under `src/components/`):  
  - `HeroSection.tsx` – Displays the hero area with background image, headline, subheading, and CTA buttons.
  - `AboutSection.tsx` – Contains company information with a two-column layout (text and supporting image).
  - `PartnersSection.tsx` – Showcases a grid or list of client/partner names.
  - `Footer.tsx` – Renders contact details and additional links.
- *Note:* Review existing UI components in `src/components/ui/` for common elements (e.g., buttons) and incorporate them where appropriate.

## Step-by-Step Outline

1. **Update Global Styles (`src/app/globals.css`):**
   - Define a new color palette:
     ```css
     :root {
       --primary-blue: #1A73E8;
       --accent-yellow: #FFC107;
       --text-dark: #333;
     }
     ```
   - Add typography classes for large headers and clean body text:
     ```css
     .hero-text {
       font-size: 2.5rem;
       font-weight: bold;
       color: var(--text-dark);
     }
     ```
   - Include responsive utility classes as needed.

2. **Create the Main Landing Page (`src/app/page.tsx`):**
   - Import the new components:
     ```tsx
     import HeroSection from '../components/HeroSection';
     import AboutSection from '../components/AboutSection';
     import PartnersSection from '../components/PartnersSection';
     import Footer from '../components/Footer';
     ```
   - Assemble the page structure:
     ```tsx
     export default function HomePage() {
       return (
         <div>
           <HeroSection />
           <AboutSection />
           <PartnersSection />
           <Footer />
         </div>
       );
     }
     ```
   - Wrap components in error boundaries if needed for graceful degradation.

3. **Develop the Hero Section (`src/components/HeroSection.tsx`):**
   - Create a functional component with a full-screen background:
     ```tsx
     export default function HeroSection() {
       const bgImage = "https://placehold.co/1920x1080?text=Modern+hero+background+for+G%26M+Rental+Tools+landing+page";
       return (
         <section
           className="relative h-screen flex flex-col justify-center items-center text-white"
           style={{ backgroundImage: `url(${bgImage})`, backgroundSize: 'cover', backgroundPosition: 'center' }}
         >
           <h1 className="hero-text">Bienvenido a G&amp;M Rental Tools</h1>
           <p className="mt-4 text-xl">Equipos de alta calidad para tus proyectos</p>
           <div className="mt-8 flex gap-4">
             <button className="px-6 py-3 bg-blue-500 text-white rounded hover:bg-blue-600">Servicios</button>
             <button className="px-6 py-3 border border-white text-white rounded hover:bg-white hover:text-blue-500">Contáctanos</button>
           </div>
         </section>
       );
     }
     ```
   - Ensure the `<img>` elements (if any) include `onError` handlers for graceful fallback behavior.

4. **Develop the About Section (`src/components/AboutSection.tsx`):**
   - Build a two-column layout:
     ```tsx
     export default function AboutSection() {
       return (
         <section className="py-16 bg-white text-dark px-6">
           <div className="max-w-6xl mx-auto grid md:grid-cols-2 gap-8 items-center">
             <div>
               <h2 className="text-3xl font-bold">¿Quiénes somos?</h2>
               <p className="mt-4 text-lg">
                 Somos una empresa líder en el sector, ofreciendo equipos de alquiler de alta calidad y servicios especializados.
               </p>
             </div>
             <div>
               <img
                 src="https://placehold.co/600x400?text=Professional+team+working+with+industrial+equipment"
                 alt="Professional team working with industrial equipment in a modern industrial setting"
                 onError={(e) => { e.currentTarget.src = 'fallback-image.png'; }}
               />
             </div>
           </div>
         </section>
       );
     }
     ```

5. **Create the Partners Section (`src/components/PartnersSection.tsx`):**
   - Present partner/client names in a clean, responsive grid:
     ```tsx
     export default function PartnersSection() {
       const clients = ["YPF", "YPF Luz", "Tecpetrol", "ProdEng", "Pan American Energy", "Superior", "Río Limay", "TSB"];
       return (
         <section className="py-12 bg-gray-100 px-6">
           <h3 className="text-center text-2xl font-bold mb-8">Nuestros Clientes</h3>
           <div className="flex flex-wrap justify-center gap-8">
             {clients.map((client, index) => (
               <div key={index} className="px-4 py-2 border rounded">
                 {client}
               </div>
             ))}
           </div>
         </section>
       );
     }
     ```
   - Ensure spacing, borders, and typography align with overall design aesthetics.

6. **Develop the Footer Component (`src/components/Footer.tsx`):**
   - Craft a concise footer with contact and copyright information:
     ```tsx
     export default function Footer() {
       return (
         <footer className="bg-blue-500 text-white py-8">
           <div className="max-w-6xl mx-auto px-6 text-center">
             <p>© {new Date().getFullYear()} G&amp;M Rental Tools. Todos los derechos reservados.</p>
             <p>Contacto: info@gymrentaltools.com.ar</p>
           </div>
         </footer>
       );
     }
     ```

7. **Integration & Testing:**
   - Run the Next.js development server and verify that each component renders correctly.
   - Test responsive behavior on multiple device sizes.
   - Validate that image error handling works correctly (simulate broken image URLs to test `onError`).
   - Ensure accessibility through semantic HTML and proper `alt` attributes.

8. **Best Practices & Error Handling:**
   - Use descriptive alt texts for all images.
   - Employ onError handlers to manage image load failures.
   - Keep components modular for ease of maintenance.
   - Utilize Tailwind CSS classes to ensure a consistent visual hierarchy and responsive design.
   - Confirm that each file/component builds without errors; if missing dependencies are detected, re-read related files and adjust the plan accordingly.

## Summary
- The plan updates global styles and creates a new landing page at `src/app/page.tsx` that imports modular components.
- Four new components are developed: HeroSection, AboutSection, PartnersSection, and Footer.
- The hero section uses a full-screen background image with bold typography and clear CTAs, while the about section uses a responsive two-column layout.
- The partners section presents client names in a grid, and the footer provides essential contact info.
- Image elements include onError fallbacks, ensuring robust error handling.
- All components follow best practices in responsiveness, accessibility, and modularity.
