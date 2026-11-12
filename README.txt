KASTING + AUDICIJA — prijave glumaca, admin panel i podela uloga
================================================================

Ovo NIJE statički sajt: ima server (Node.js 18 ili noviji, bez ikakvih dodatnih paketa).
Server čuva naloge, prijave i fotografije, i jedini on odlučuje ko je admin.

POKRETANJE NA RAČUNARU (za probu)
  node server.js          →  http://localhost:3000

OBJAVLJIVANJE (hosting sa Node.js-om: Render, Railway, Fly.io, VPS, cPanel "Node.js App"...)
  1. Otpremi sve (server.js, package.json, folder public).  Start komanda:  node server.js
  2. Podesi promenljive okruženja:
       ADMIN_PHONE   tvoj broj telefona, npr. +381601234567   (OBAVEZNO podesi — samo taj broj može biti admin)
       TRUST_PROXY   1      (ako je hosting iza proksija/HTTPS-a, što je skoro uvek)
       DATA_DIR      putanja do TRAJNOG diska (npr. /var/data) — bez ovoga se prijave gube pri svakom restartu!
       DEFAULT_CC    381    (pozivni broj za brojeve koji počinju sa 0; podrazumevano Srbija)
  3. Obavezno koristi HTTPS (ugrađen je kod Render/Railway/Fly).

ADMIN
  Otvori  https://tvoj-sajt/#/admin-login  (ili link "Admin" na dnu stranice)
  Prijava: broj telefona + @baki + lozinka.
  Posle prve prijave u panelu: "Lozinka" → postavi sopstvenu novu lozinku (bar 10 znakova).
  Lozinka nije upisana u kod, samo njen heš.

KAKO RADI
  - Samo admin može da pravi, menja, zatvara i briše audicije (server proverava svaki zahtev).
  - Admin: uloge (sa opisom), rok, i šta se traži: za svako polje "ne traži / opciono / obavezno"
    (godine, visina, fotografija, video link, monolog, CV...) + sopstvena pitanja.
  - Glumac: registracija brojem telefona + lozinka, pa prijava za audiciju: ime, kontakt podaci,
    do 3 uloge po redu želje i polja koja je admin postavio. Prijavu može da menja dok je audicija otvorena.
  - Admin klikne "Otvori u Audiciji ▶": prijave se same pojavljuju kao kandidati sa željama, kontaktom,
    odgovorima i fotografijom. Nove prijave stižu same (na 20 s ili dugme "Osveži prijave"). Ocene i podela
    se čuvaju na serveru.
  - Glumac koji zaboravi lozinku: admin je resetuje u pregledu prijava ("Resetuj lozinku glumca").

BEZBEDNOST
  - Lozinke se čuvaju kao scrypt heš; sesije su HttpOnly kolačići; zaštita od prečestih pokušaja prijave.
  - Fotografije vide samo admin i vlasnik prijave.
  - Pravi SMS potvrdu broja telefona nije uključena (traži plaćeni SMS servis); broj je korisničko ime.
