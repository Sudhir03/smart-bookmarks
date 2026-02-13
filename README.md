# SmartBookmarks — Real-Time Private Bookmark Manager

SmartBookmarks is a full-stack web application that allows users to securely save, manage, and organize their personal bookmarks. The system provides real-time synchronization across multiple tabs and enforces strict per-user data isolation using Supabase Row Level Security (RLS).

---

## 🚀 Features

### Authentication

- Google OAuth login via Supabase
- Secure session management
- No email/password handling required

### Bookmark Management

- Add bookmarks with title and URL validation
- Edit existing bookmarks
- Delete bookmarks
- Automatic URL normalization

### Real-Time Updates

- Instant synchronization across browser tabs using Supabase Realtime subscriptions

### Security

- Row Level Security (RLS) ensures:
  - Users can only access their own bookmarks
  - Backend-level data protection

---

## 🏗 Tech Stack

**Frontend**

- Next.js (App Router)
- React
- Tailwind CSS

**Backend / Services**

- Supabase (PostgreSQL + Auth + Realtime)

**Deployment**

- Vercel

---

## ⚙️ Getting Started

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd smart-bookmarks
```

---

### 2. Install dependencies

```bash
npm install
```

---

### 3. Configure environment variables

Create a `.env.local` file:

```env
NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
NEXT_PUBLIC_SUPABASE_PUBLISHABLE_DEFAULT_KEY=your_publishable_default_key
```

---

### 4. Run development server

```bash
npm run dev
```

Open:

```
http://localhost:3000
```

---

## 🗄 Database Setup (Supabase)

Create a table:

### Table: `bookmarks`

| Column     | Type               |
| ---------- | ------------------ |
| id         | uuid (primary key) |
| title      | text               |
| url        | text               |
| user_id    | uuid               |
| created_at | timestamp          |

---

### Enable Row Level Security

Run in Supabase SQL editor:

```sql
alter table bookmarks enable row level security;

create policy "Users can view own bookmarks"
on bookmarks for select
using (auth.uid() = user_id);

create policy "Users can insert own bookmarks"
on bookmarks for insert
with check (auth.uid() = user_id);

create policy "Users can update own bookmarks"
on bookmarks for update
using (auth.uid() = user_id);

create policy "Users can delete own bookmarks"
on bookmarks for delete
using (auth.uid() = user_id);
```

---

## 🌐 Deployment

This project is deployed using Vercel.

### Steps:

1. Push code to GitHub
2. Import repository into Vercel
3. Add environment variables
4. Deploy

---

## 📌 Key Highlights

- Real-time full-stack architecture
- Secure multi-user data isolation
- Modern UI with responsive design
- Production-grade authentication and authorization

---

## 📄 License

This project is for educational and demonstration purposes.
