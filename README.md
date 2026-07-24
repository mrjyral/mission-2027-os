# Mission 2027 OS - Deployment Paket V3 Final

## Inhalt
- index.html (V3 Full mit Dexie + Supabase + PWA)
- manifest.json (PWA Manifest)
- sw.js (Service Worker Cache First)
- icon-192.png, icon-512.png, apple-touch-icon.png
- README

## Veröffentlichung in 5 Schritten

### 1. Supabase vorbereiten (2 Min)
Gehe zu supabase.com -> Neues Projekt -> SQL Editor -> Führe aus:

create table contacts (id text primary key, data jsonb, updated_at timestamp default now());
create table follow_ups (id text primary key, contact_id text, data jsonb, updated_at timestamp default now());
create table events (id text primary key, data jsonb);
create table kpis (id text primary key, data jsonb);
alter table contacts enable row level security;
create policy "allow all for auth" on contacts for all using (auth.role() = 'authenticated');
alter table follow_ups enable row level security;
create policy "allow all for auth" on follow_ups for all using (auth.role() = 'authenticated');

Kopiere URL und anon Key aus Project Settings -> API.

### 2. Hosting wählen (3 Min)

Option A - Vercel (empfohlen):
- vercel.com -> New Project -> Upload diesen Ordner
- Framework: Other, Build Command leer, Output Directory .
- Deploy -> Fertig, HTTPS automatisch

Option B - Netlify:
- netlify.com -> Drag & Drop diesen Ordner auf Deploy
- Fertig

Option C - Cloudflare Pages:
- pages.cloudflare.com -> Upload -> Fertig

### 3. App konfigurieren (1 Min)
- Öffne deine Live URL
- Gehe zu Mehr -> Cloud Sync -> Trage Supabase URL + Anon Key ein -> Speichern
- Mehr -> KI Einstellungen -> Trage neuen OpenAI Key ein (BYOK, nur lokal)

### 4. Als App installieren (30 Sek)
Android: Chrome öffnet URL -> Menü (3 Punkte) -> Zum Startbildschirm hinzufügen -> Installieren
iPhone: Safari öffnet URL -> Teilen Icon -> Zum Home-Bildschirm -> Hinzufügen
Danach läuft sie wie native App im Vollbild, offline fähig.

### 5. Test Checkliste
- [ ] CRM -> Kontakt -> Paket Tracking -> Sequenz 1/3/7/10 startet -> erscheint in Heute
- [ ] Heute -> Morgenroutine startet -> 7 Schritte
- [ ] Content -> Facebook/LinkedIn Toggle wechselt Hooks
- [ ] Mehr -> Jetzt syncen -> Supabase Tabellen füllen sich
- [ ] Offline Test: Flugmodus an -> App neu laden -> funktioniert -> Follow Up erstellen -> Flugmodus aus -> Jetzt syncen -> erscheint in Supabase

Fertig. Du bist live.
