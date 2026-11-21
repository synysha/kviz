# Rodinný kvíz

Kvíz pre rodinu: jeden telefón (premietaný na TV) ukazuje otázky, ostatní odpovedajú na svojich telefónoch a body sa synchronizujú cez Firebase.

## Nastavenie Firebase (zadarmo, ~5 minút)

1. Choď na https://console.firebase.google.com a vytvor projekt (Analytics netreba).
2. V projekte pridaj **webovú aplikáciu** (ikona `</>`). Skopíruj objekt `firebaseConfig`.
3. V menu **Build → Realtime Database** vytvor databázu (región podľa seba, napr. europe-west1).
4. Na karte **Rules** vlož:
   ```json
   {
     "rules": {
       "kviz": {
         "$room": { ".read": true, ".write": true }
       }
     }
   }
   ```
   a daj **Publish**. (Kto pozná odkaz, môže písať. Pre rodinný kvíz stačí.)
5. V `index.html` nahraď hodnoty v `firebaseConfig` (`apiKey`, `databaseURL`, `projectId`) svojimi. `databaseURL` nájdeš v Realtime Database nad dátami.

## Nahratie na GitHub Pages

1. Vytvor repozitár a nahraj všetky súbory z priečinka: `index.html`, priečinok `avatars` (10 obrázkov), `icon.svg`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png`, `manifest.webmanifest` a `README.md`.
2. **Settings → Pages**: Source = *Deploy from a branch*, branch `main`, priečinok `/ (root)`.
3. Po minúte bude kvíz na `https://<meno>.github.io/<repozitar>/`.

## Hranie

- Všetci otvoria ten istý odkaz. Telefón pre TV zvolí **📺 Toto je TV**, ostatní **📱 Som hráč** a zadajú meno.
- Viac samostatných hier naraz: pridaj `?room=nazov` k odkazu (predvolená miestnosť je `rodina`).
- Hru ovláda TV tlačidlom dole. Po poslednom kole tlačidlo **Nová hra** vymaže hráčov a začne od nuly.
- Otázky a bonusové tipy sú v poli `TOPICS` a `BONUS` na začiatku skriptu v `index.html`.

## Karty a ikona

- Dole sú karty: **Kvíz**, **Hodnotenie** (poradie, body po kolách), **Profil** (meno a avatar, uložené v telefóne; na TV sa nezobrazuje) a **Nastavenia** (QR kód na pozvanie ďalšieho telefónu, zmena roly a mena, vynulovanie hry).
- QR kód sa generuje knižnicou z cdnjs, takže treba internet.
- Ikona kvízu je `icon.svg` (a PNG verzie). Na mobile ju získaš cez **Pridať na plochu**.
