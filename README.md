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

1. Vytvor repozitár a nahraj `index.html` (a tento README).
2. **Settings → Pages**: Source = *Deploy from a branch*, branch `main`, priečinok `/ (root)`.
3. Po minúte bude kvíz na `https://<meno>.github.io/<repozitar>/`.

## Hranie

- Všetci otvoria ten istý odkaz. Telefón pre TV zvolí **📺 Toto je TV**, ostatní **📱 Som hráč** a zadajú meno.
- Viac samostatných hier naraz: pridaj `?room=nazov` k odkazu (predvolená miestnosť je `rodina`).
- Hru ovláda TV tlačidlom dole. Po poslednom kole tlačidlo **Nová hra** vymaže hráčov a začne od nuly.
- Otázky a bonusové tipy sú v poli `TOPICS` a `BONUS` na začiatku skriptu v `index.html`.
