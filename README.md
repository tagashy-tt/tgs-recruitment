# TGS Studio — Recruitment

> Job application system for TGS Studio. Built with vanilla HTML/CSS/JS and Supabase as backend.

## Files

| File | Description |
|------|-------------|
| `tgs-apply.html` | Public application form for candidates |
| `tgs-admin.html` | Private admin panel to review applications (local only) |

## Setup

### 1. Supabase — Create the table

Run this SQL in your Supabase SQL Editor:

```sql
create table tgs_applicants (
  id          uuid primary key default gen_random_uuid(),
  nombre      text not null,
  tiktok      text not null,
  anios       text not null,
  habilidades text,
  descripcion text,
  portfolio   text,
  motivacion  text,
  revisado    boolean default false,
  created_at  timestamptz default now()
);

alter table tgs_applicants enable row level security;
create policy "insert_public" on tgs_applicants for insert with check (true);
create policy "read_admin"    on tgs_applicants for select using (true);
create policy "update_admin"  on tgs_applicants for update using (true);
create policy "delete_admin"  on tgs_applicants for delete using (true);
```

### 2. Deploy

Upload `tgs-apply.html` to GitHub Pages or any static host — that's the public link you share with candidates.

Keep `tgs-admin.html` local. Open it directly in your browser — no server needed.

## Admin Panel

The admin panel is password-protected. Default password: `tgs2024`

Features:
- View all applications with stats (total / pending / reviewed)
- Search and filter by status or experience level
- Mark applications as reviewed
- Delete entries
- Export all data as CSV

## Stack

- HTML / CSS / JavaScript (no frameworks)
- [Supabase](https://supabase.com) — Postgres database + REST API

---

Made by [Tagashy](https://github.com/tagashy-tt) · TGS Studio
