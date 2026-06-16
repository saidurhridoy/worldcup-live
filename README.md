# ⚽ FIFA World Cup 2026 Companion

A highly scalable, edge-optimized World Cup match companion built on **free-tier infrastructure**.

![Next.js](https://img.shields.io/badge/Next.js-14-black?style=flat-square&logo=next.js)
![Firebase](https://img.shields.io/badge/Firebase-Firestore--Auth-FFCA28?style=flat-square&logo=firebase)
![Vercel](https://img.shields.io/badge/Deploy-Vercel-black?style=flat-square&logo=vercel)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-v3-38BDF8?style=flat-square&logo=tailwindcss)

## ✨ Features

- **🔴 Live Dashboard** — Real-time match scores with animated updates
- **📊 Match Predictor** — Predict scores before kickoff to earn leaderboard points
- **💬 Fan Chat** — Real-time chat rooms per match via Firestore Subcollections
- **🏆 Leaderboard** — Compete globally with other fans
- **📝 Live Commentary** — Color-coded text commentary feed
- **📱 Mobile-First** — Fully responsive glassmorphism UI

## 🏗️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Next.js 14 (App Router), React 18 |
| Styling | Tailwind CSS v3, Shadcn/ui, Lucide Icons |
| Backend | Firebase (Firestore + Auth) |
| Deployment | Vercel |
| Auth | GitHub OAuth via Firebase Auth |

## 🚀 Quick Start

### 1. Clone & Install

```bash
git clone https://github.com/YOUR_USERNAME/worldcup-companion.git
cd worldcup-companion
npm install
```

### 2. Configure Firebase

1. Create a free project at [Firebase Console](https://console.firebase.google.com/)
2. Create a **Cloud Firestore** database (start in production or test mode)
3. Go to **Authentication > Sign-in method** and enable **GitHub**
   - Register a GitHub App/OAuth settings on GitHub
   - Copy the Authorization Callback URL from Firebase Console and add it to GitHub
   - Add the Client ID and Client Secret in Firebase Auth Console
4. Register a **Web App** in your Firebase project to get the config keys

### 3. Configure Environment

```bash
cp .env.local.example .env.local
```

Edit `.env.local` with your credentials:
```env
NEXT_PUBLIC_FIREBASE_API_KEY=your_api_key_here
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your_project_id.firebaseapp.com
NEXT_PUBLIC_FIREBASE_PROJECT_ID=your_project_id_here
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=your_project_id.appspot.com
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=your_messaging_sender_id_here
NEXT_PUBLIC_FIREBASE_APP_ID=your_app_id_here
```

### 4. Seed Firestore Database

Run the seeding script to upload teams and matches:
```bash
node scripts/seed-firebase.mjs
```

### 5. Run Development Server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

## 🌐 Deploy to Vercel

### Option A: One-Click Deploy

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/YOUR_USERNAME/worldcup-companion)

### Option B: CLI Deploy

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel

# Add environment variables
vercel env add NEXT_PUBLIC_FIREBASE_API_KEY
vercel env add NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN
vercel env add NEXT_PUBLIC_FIREBASE_PROJECT_ID
vercel env add NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET
vercel env add NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID
vercel env add NEXT_PUBLIC_FIREBASE_APP_ID
```

## 📁 Project Structure

```
src/
├── app/
│   ├── layout.tsx              # Root layout with providers
│   ├── page.tsx                # Live Dashboard (home)
│   ├── loading.tsx             # Skeleton loading state
│   ├── matches/[id]/           # Match Companion Hub
│   ├── predictions/            # Prediction game
│   ├── leaderboard/            # Global leaderboard
│   └── auth/                   # Login page
├── components/
│   ├── ui/                     # Shadcn/ui primitives
│   ├── dashboard/              # MatchCard, MatchTabs, LivePulse
│   ├── match/                  # Commentary, FanChat, Events
│   ├── layout/                 # Navbar, Footer
│   └── providers/              # Auth providers
├── hooks/                      # Realtime subscription hooks
├── lib/                        # Utilities + Firebase client config
└── types/                      # TypeScript interfaces
scripts/
└── seed-firebase.mjs           # Firestore database seed script
```

## ⚡ Performance Architecture

| Layer | Strategy |
|---|---|
| **ISR** | Dashboard revalidates every 30s, match pages every 10s |
| **Realtime** | Direct Firestore `onSnapshot` listeners client-side |
| **Edge API** | Bypassed. Writes and listens query Firebase endpoints directly |
| **DB** | Denormalized data model, queries designed to avoid custom index requirements |

## 📊 Prediction Scoring

| Prediction | Points |
|---|---|
| Exact score match | **+10 pts** |
| Correct draw prediction | **+5 pts** |
| Correct winner prediction | **+3 pts** |

## ⚖️ Legal Compliance

This application does **NOT** include:
- Video streaming or embedded players
- Links to streaming services
- Any copyrighted broadcast content

It focuses entirely on **live data, stats, predictions, and community engagement**.

## 📄 License

MIT License — See [LICENSE](LICENSE) for details.
