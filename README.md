# SvelteKit Blogi

Tämä on kevyt ja nopea blogisovellus, joka on toteutettu nykyaikaisilla web-teknologioilla. Sovelluksessa on valmiina käyttäjänhallinta (kirjautuminen ja rekisteröityminen) sekä täydelliset CRUD-toiminnot (sisällön luominen, lukeminen, muokkaaminen ja poistaminen).

## 🛠 Teknologiat

* **SvelteKit** – Sovelluskehys
* **Remote Functions** – Tyypitetyt palvelinkutsut
* **Better Auth** – Autentikaatio ja istunnot
* **Drizzle ORM & SQLite** – Tietokannanhallinta
* **Pico CSS** – Minimalistinen ulkoasu

---

## 🚀 Käyttöönotto

Noudata näitä ohjeita ajaaksesi projektin paikallisesti:

### 1. Riippuvuuksien asennus

Asenna tarvittavat paketit npm-paketinhallinnalla:

```bash
npm install

```

### 2. Ympäristömuuttujat

Luo projektin juureen tiedosto nimeltä `.env` ja lisää sinne seuraavat rivit:

```env
BETTER_AUTH_SECRET=LONG-PASSWORD-INSERTED-HERE
BETTER_AUTH_URL=http://localhost:(VALUE)
DATABASE_URL=file:local.db

```

### 3. Tietokannan alustus

Luo tietokantataulut Drizzle-skeeman mukaisesti (tämä luo `local.db` tiedoston):

```bash
npm run db:push

```

### 4. Käynnistys

Käynnistä kehityspalvelin:

```bash
npm run dev

```

Sovellus on nyt käytettävissä osoitteessa: **http://localhost:5173**

