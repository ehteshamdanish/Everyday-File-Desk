# Everyday File Desk

A fast, responsive, and privacy-first online image utility built with React, Vite, TypeScript, and Tailwind CSS. All core image operations run 100% locally in the user's browser with zero server uploads, no paid API keys, and no required registration.

---

## 🌟 Features

### 1. 100% Client-Side Privacy Guarantee
- Images are decoded and processed in memory using the browser's native **HTML5 Canvas** and **File APIs**.
- Zero bytes are ever sent to an external server or cloud service.
- No analytics collecting filenames, dimensions, or personal data.
- Temporary Object URLs are automatically revoked to prevent browser memory leaks.

### 2. Fully Functional Image Compressor (`/image-compressor`)
- **Multi-File Drag & Drop**: Batch upload up to 20 images at once.
- **Magic-Byte Header Validation**: Inspects binary signatures to verify genuine JPEG, PNG, and WebP files rather than trusting arbitrary extensions.
- **Adjustable Quality Control**: Smooth slider (10% to 100%) with numerical percentage readout for lossy formats (JPEG and WebP).
- **Format Conversion**: Convert between JPEG, PNG, and WebP.
- **Lossless PNG Notice**: Clear educational indicator that browser canvas PNG encoding is lossless and does not support lossy compression levels.
- **Transparency Safeguard**: Warns users before converting transparent PNGs/WebPs to JPEG and allows choosing a background fill color (white, black, off-white, or custom hex).
- **Actual Byte Size Calculation**: Computes real byte reductions and handles cases where re-encoding might yield a larger output.
- **Batch Export**: Download files individually or bundle all processed images into a single `.ZIP` file.

### 3. Fully Functional Image Resizer (`/image-resizer`)
- **Proportional Dimension Scaling**: Lock aspect ratio enabled by default; changing width updates height proportionally and vice-versa.
- **Percentage Quick Scales**: 25%, 50%, 75%, 100%, 150%, 200%.
- **Standard & Social Presets**: 256×256, 512×512, 1024×1024, 1080×1080 (Square Post), 1200×630 (Social Share), 1920×1080 (Full HD).
- **Fit Strategies**:
  - `Contain`: Fits entire image within dimensions without distortion (with customizable letterbox fill).
  - `Crop`: Covers full dimensions and center-crops extra edges.
  - `Stretch`: Forces exact pixel dimensions.
- **Safety Limits**: Prevents canvas out-of-memory crashes with configurable maximum dimension limits (8,192 px max).

### 4. Professional Homepage & Shared System
- **Hero & Action CTAs**: Direct navigation to both functional tools.
- **Tool Cards & Roadmap**: Highlights active tools and explicitly labels upcoming features (PDF Merge, PDF Split, Image-to-PDF) as "Coming Soon".
- **How It Works**: 3-step intuitive workflow guide.
- **FAQ Section**: Addresses privacy, cost, quality, mobile support, and formats.
- **Responsive Navigation**: Accessible mobile drawer, zero horizontal overflow, and focus indicators.
- **SEO & Discoverability**: Semantic HTML, dynamic titles/meta descriptions, `robots.txt`, `sitemap.xml`, and SPA fallback configuration (`_redirects`, `vercel.json`).

---

## 🛠️ Technology Stack & Dependencies

| Dependency | Purpose |
|---|---|
| **React 18** | Declarative component UI library |
| **Vite 6** | Ultra-fast development server and optimized production bundler |
| **TypeScript 5** | Strict type checking and developer ergonomics |
| **Tailwind CSS 3** | Utility-first styling with custom neutral and indigo brand palette |
| **Lucide React** | Clean, accessible SVG line icons |
| **React Router 6** | Client-side routing with direct URL support |
| **JSZip** | In-browser ZIP bundling for multi-file downloads |
| **Vitest & React Testing Library** | Automated unit and integration testing in JSDOM |

---

## 🚀 Getting Started

### Prerequisites
- Node.js (v18 or higher recommended; developed on Node v24)
- npm (v9 or higher)

### 1. Installation
```bash
npm install
```

### 2. Start Local Development Server
```bash
npm run dev
```
Open [http://localhost:5173](http://localhost:5173) in your browser.

### 3. Run Automated Tests
```bash
npm run test
```

### 4. Production Build & Typecheck
```bash
npm run build
```
The compiled, tree-shaken static assets will be output to the `dist/` directory.

### 5. Preview Production Build Locally
```bash
npm run preview
```

---

## 📁 Project Structure

```
├── public/
│   ├── _redirects          # SPA fallback rule for Netlify / Cloudflare Pages
│   ├── robots.txt          # Search engine crawler instructions
│   └── sitemap.xml         # XML sitemap for SEO indexation
├── src/
│   ├── components/
│   │   ├── common/
│   │   │   ├── AlertBanner.tsx       # Accessible info/warning/error alerts
│   │   │   ├── FileUploader.tsx      # Drag-and-drop file upload with validation
│   │   │   ├── Footer.tsx            # Site footer with disclosures and navigation
│   │   │   ├── Header.tsx            # Sticky header with responsive mobile drawer
│   │   │   └── SeoHead.tsx           # Dynamic title, meta description & canonical tags
│   │   ├── compressor/
│   │   │   ├── CompressionControls.tsx # Quality slider, format selector, transparency alert
│   │   │   └── CompressionResults.tsx  # Output cards, size comparisons, ZIP download
│   │   └── resizer/
│   │       ├── ResizerControls.tsx   # Width/height inputs, aspect lock, fit modes
│   │       └── ResizerResults.tsx    # Output previews, dimension diffs, ZIP download
│   ├── config/
│   │   └── site.ts                   # Centralized brand name, limits, and FAQ data
│   ├── lib/
│   │   ├── file-validation/
│   │   │   └── fileValidation.ts     # Magic bytes inspection, size & dimension checks
│   │   ├── image-processing/
│   │   │   ├── canvasOps.ts          # HTML5 Canvas compression and resizing engine
│   │   │   └── zipExport.ts          # JSZip multi-file download generator
│   │   └── utils/
│   │       └── formatters.ts         # Byte size formatters, filename sanitization
│   ├── pages/
│   │   ├── ContactPage.tsx           # Contact and support information
│   │   ├── HomePage.tsx              # Landing page with hero, cards, how-it-works, FAQ
│   │   ├── ImageCompressorPage.tsx   # Dedicated image compressor route
│   │   ├── ImageResizerPage.tsx      # Dedicated image resizer route
│   │   ├── NotFoundPage.tsx          # Custom 404 page
│   │   └── PrivacyPolicyPage.tsx     # Comprehensive client-side privacy disclosures
│   ├── styles/
│   │   └── index.css                 # Tailwind base styles and accessibility focus rings
│   ├── test/
│   │   └── setup.ts                  # Vitest environment setup and Canvas polyfills
│   ├── types/
│   │   └── index.ts                  # Shared TypeScript interfaces
│   ├── App.tsx                       # React Router configuration
│   └── main.tsx                      # Application mounting point
├── tests/
│   ├── canvasOps.test.ts             # Tests for scaling, contain/crop math
│   ├── components.test.tsx           # Integration tests for routes and components
│   ├── formatters.test.ts            # Tests for byte formatting and filename sanitization
│   └── validation.test.ts            # Tests for magic-bytes detection and error limits
├── index.html                        # Application HTML shell
├── package.json                      # Scripts and dependencies
├── tailwind.config.js                # Tailwind theme customization
├── tsconfig.json                     # Strict TypeScript compiler options
├── vercel.json                       # Vercel SPA rewrite configuration
└── vite.config.ts                    # Vite build configuration
```

---

## 🌐 Deployment Instructions

Because Everyday File Desk is a 100% client-side application with zero backend dependencies, it can be deployed to any static host.

### Cloudflare Pages
1. Connect your Git repository or upload the `dist/` directory.
2. Build command: `npm run build`
3. Output directory: `dist`
4. Direct route routing is handled automatically by `public/_redirects`.

### Netlify
1. Connect your repository.
2. Build command: `npm run build`
3. Publish directory: `dist`
4. Netlify will detect `dist/_redirects` for SPA fallback.

### Vercel
1. Import the project repository into Vercel.
2. Framework Preset: `Vite`.
3. Output directory: `dist`.
4. `vercel.json` ensures all route requests (`/image-compressor`, `/image-resizer`) rewrite to `/index.html`.

---

## 🔍 Known Limitations & Future Roadmap

- **PNG Lossless Behavior**: In standard browser canvas implementations, PNG export uses lossless compression. While quality sliders cannot alter PNG compression directly, users are warned and encouraged to select WebP for significant file size savings.
- **Browser Memory Limits**: Extremely large images (>8,192 px or >40 Megapixels) are restricted by configurable safeguards (`SITE_CONFIG.maxDimensionPixels`) to prevent mobile browsers from exhausting memory.
- **Future Milestone Expansion**: The codebase is architected to easily accommodate PDF Merge, PDF Split, Image-to-PDF conversion, and PDF Compression in subsequent milestones without architectural refactoring.
