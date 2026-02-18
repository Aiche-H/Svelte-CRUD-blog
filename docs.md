# Projektin dokumentaatio: SvelteKit-blogi

Tämä on kevyt ja suorituskykyinen blogialusta, joka hyödyntää tyypitettyjä etäfunktioita, modernia autentikaatiota ja minimalistista CSS-kehystä.

---

## Teknologiapino (Tech Stack)

### Kehitysympäristö (Neovim)

Käytin kehitysympäristönä Neovimiä, jonka olen konfiguroinut vastaamaan modernia IDE-ympäristöä Lua-pohjaisilla asetuksilla. Hyödynsin natiivia LSP-tukea (`lsp.lua`) TypeScript-virheiden tunnistamiseen ja Treesitteriä (`treesitter.lua`) koodin syntaksin korostukseen. Käytin Telescopea (`telescope.lua`) nopeaan tiedostojen hakuun ja Fugitivea (`fugitive.lua`) Git-hallintaan, mikä mahdollisti tehokkaan kehitystyön suoraan terminaalissa.

### Virheiden etsiminen ja korjaaminen ohjelmakoodista

Etsin ja korjasin virheitä hyödyntämällä Neovimiin konfiguroitua LSP-diagnostiikkaa, joka ilmoitti tyyppivirheistä reaaliajassa. Käytin Trouble.lua-liitännäistä projektin kaikkien virheiden ja varoitusten listaamiseen sekä selaimen kehittäjätyökaluja (DevTools) verkkoliikenteen ja Remote Function -kutsujen vianetsintään varmistaen datan eheyden.

---

## Tietokanta ja ORM (SQLite & Drizzle)

* **SQLite**: Paikallinen tiedostopohjainen tietokanta.
* **Drizzle ORM**: Käytetään skeemojen määrittelyyn, migraatioihin ja tyypitettyihin kyselyihin.
* **CRUD**: Toteutettu Drizzlen vakiofunktioilla (`select`, `insert`, `update`, `delete`).

---

## Autentikaatio (Better Auth)

Käyttäjien hallinta (login/signup) toteutettu Better Auth -kirjastolla. Istunnonhallinta on integroitu `hooks.server.ts`-tiedostoon globaalia pääsynvalvontaa varten.

---

## Remote Functions (RPC)

Kommunikaatio palvelimen ja frontentin välillä hoituu SvelteKit Remote Functions -kirjastolla. Tämä korvaa perinteiset REST-endpointit tyypitetyillä etäfunktiokutsuilla, mikä takaa päästä-päähän (end-to-end) tyyppiturvallisuuden.

---

# Ohjelmiston toimintalogiikka

## Toteutusteknologiat

Toteutin blogin toimintalogiikan SvelteKitillä ja TypeScriptillä. Käytin SvelteKit Remote Functions -kirjastoa hallitsemaan palvelinpuolen operaatioita (kuten postausten luomista ja muokkaamista), mikä takaa tyyppiturvallisen tiedonsiirron frontentin ja backentin välillä.

---

## Tietovarasto

Valitsin tietovarastoksi SQLite-tietokannan. Se on kevyt, tiedostopohjainen ja suorituskykyinen ratkaisu paikalliseen kehitykseen ja pienehköihin web-sovelluksiin, tarjoten silti täyden relaatiotietokannan edut ja SQL-tuen.

---

## Yhteys tietovarastoon

Muodostin yhteyden tietokantaan käyttämällä Drizzle ORM -kirjastoa. Määritin tietokantarakenteen (schema) TypeScriptillä, minkä pohjalta Drizzle hoitaa yhteyden muodostamisen, kyselyiden suorittamisen sekä tietokantamigraatiot.

---

## Rajapinnat ja tietojen käsittely

Hyödynsin sovelluksessa RPC-rajapintaa (Remote Procedure Call) Remote Functionsin kautta. Käytin tätä rajapintaa tiedon välittämiseen: esimerkiksi lomakkeelta tuleva data validoidaan palvelimella ja tallennetaan Drizzlen avulla tietokantaan JSON-pohjaisena objektina.

---

## Ohjelmiston tietoturva

Huomioin tietoturvan käyttämällä Better Auth -kirjastoa, joka hoitaa salasanojen suolauksen ja suojatun istunnonhallinnan. Estin luvattomat CRUD-operaatiot tarkistamalla käyttäjän session palvelinpuolella (`hooks.server.ts`) ennen tietokantakutsuja. Lisäksi Drizzle ORM suojaa sovelluksen SQL-injektioilta.

---

## Versionhallinnan käyttö

Käytin projektin hallintaan GitHub-versionhallintaa. Dokumentoin kehitysprosessin tekemällä säännöllisiä committeja suoraan Neovim-editorista käsin ja synkronoimalla koodin etärepositorioon, mikä varmisti koodin jatkuvan varmuuskopioinnin ja muutoshistorian säilymisen.

---

## Virheiden etsiminen ja korjaaminen ohjelmakoodista

Etsin ja korjasin virheitä hyödyntämällä TypeScriptin staattista analyysia sekä SvelteKitin kehityspalvelimen virheilmoituksia. Käytin myös selaimen kehittäjätyökaluja (DevTools) verkkoliikenteen tarkasteluun ja Remote Function -kutsujen vianetsintään, varmistaen datan oikean muodon siirtymisen palvelimelle.

---

## Ohjelman toimintojen testaaminen

Testasin ohjelman toiminnot manuaalisesti kehityksen aikana varmistaen, että jokainen CRUD-operaatio, kirjautuminen ja rekisteröityminen toimii odotetusti. Varmistin myös, että Better Auth -suojaukset estävät pääsyn rajapintoihin ilman voimassa olevaa istuntoa.

---

## Rakenteisen ohjelmoinnin käyttö toteutuksissa

Sovellettu rakenteista ohjelmointia jakamalla sovellus selkeisiin moduuleihin:

* Käyttöliittymäkomponentit
* Palvelinpuolen etäfunktiot (Remote Functions)
* Tietokantaschemat

Tämä modulaarinen rakenne tekee ohjelman suoritusjärjestyksestä selkeän ja helposti seurattavan.

---

## Ylläpidettävän ohjelmakoodin kirjoittaminen

Kirjoitin ylläpidettävää koodia noudattamalla TypeScriptin tiukkaa tyypitystä ja johdonmukaista nimeämiskäytäntöä. Käytin Pico CSS -kehystä pitääkseni käyttöliittymän koodin minimalistisena ja erotin tietokantakyselyt omaksi kerroksekseen Drizzle ORM:n avulla, mikä helpottaa jatkokehitystä.

---

## Suunnitelmien tulkinta ja käyttöliittymän toteutus

Toteutin käyttöliittymän tulkitsemalla alkuperäistä visiota minimalistisesta ja responsiivisesta blogista. Käytin Svelte-komponentteja ja Pico CSS:ää rakentaakseni semanttisen HTML-rakenteen, joka mukautuu automaattisesti eri päätelaitteille ja tarjoaa käyttäjälle selkeän polun kirjautumiseen ja sisällönhallintaan.

---

## Suunnitelmien tulkinta ja ohjelmiston toimintojen toteutus

Muunsin suunnitelman toiminnalliseksi ohjelmistoksi toteuttamalla Better Auth -pohjaisen tunnistautumisen ja Drizzle-pohjaisen CRUD-logiikan. Varmistin, että jokainen toteutettu ominaisuus, kuten postausten luonti ja poisto, vastaa teknisiä vaatimuksia ja toimii saumattomasti osana kokonaisuutta.

---

# Ohjelman julkaisu tuotantoympäristöön

Paikallisen kehitysympäristön siirtäminen tuotantoon vaatii hallitun prosessin, jotta sovellus toimii luotettavasti julkisella palvelimella.

## 1. Ympäristömuuttujien ja salaisuuksien hallinta

Tuotantoympäristössä sovellus tarvitsee omat `.env`-asetukset, kuten tietokantapolun ja Better Auth -avaimet. Nämä eivät siirry GitHubin kautta tietoturvasyistä, vaan ne määritellään suoraan tuotantopalvelimen hallintapaneelissa tai salatussa ympäristössä. Tämä varmistaa, että sovellus osaa yhdistää oikeaan tietokantaan ja käyttää oikeita salausavaimia.

## 2. Build-prosessi (Kääntäminen)

SvelteKit-sovellus on käännettävä tuotantomuotoon komennolla:

```bash
npm run build
```

Tämä prosessi optimoi TypeScript-koodin ja Svelte-komponentit tehokkaaksi JavaScriptiksi ja CSS:ksi, mikä parantaa sovelluksen suorituskykyä ja pienentää tiedostokokoja verrattuna paikalliseen kehitystilaan.

## 3. Tietokannan migraatiot

Tuotannossa oleva SQLite-tietokanta on saatettava samaan tilaan kuin koodin skeemat. Tämä tehdään ajamalla Drizzle-migraatiot palvelimella. Se varmistaa, että kaikki taulut ja sarakkeet ovat paikoillaan, jotta uudet koodimuutokset eivät aiheuta virheitä tietokantahauissa.

