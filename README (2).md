# Pràctica P5.1: Organització d'un Viatge a Eivissa(Ibiza) amb Eines de Google

Aquest repositori conté la documentació i memòria del projecte per a la pràctica **P5.1 - Organitza un viatge amb Google** corresponent al mòdul d'**Aplicacions Web (0228) - RA5**.

---

## Fase 1: El correu web i configuració

### 1. Taula d'eines de Google
A continuació es detallen les 6 eines de Google utilitzades per a l'organització del viatge, amb el seu propòsit i el seu públic objectiu (*target*):

| Eina | Propòsit | Públic objectiu (*Target*) |
| :--- | :--- | :--- |
| **Gmail** | Gestió, enviament, recepció i organització del correu electrònic | Qualsevol usuari o organització |
| **Google Calendar** | Gestió de l'agenda, planificació d'esdeveniments i reunions amb convidats | Equips, famílies i viatgers |
| **Google Maps** | Disseny de rutes, cerca de llocs d'interès i càlcul de temps de transport | Viatgers, conductors i empreses |
| **Google Fulls de càlcul (Sheets)** | Creació de pressupostos, càlculs financers amb fórmules i control de despeses | Estudiants, empreses i gestors |
| **Google Tasques (Tasks)** | Llistes de tasques pendents amb dates límit integrades amb el calendari | Treball personal i col·laboratiu |
| **Google Contactes** | Gestió de la llibreta d'adreces i organització de grups mitjançant etiquetes | Usuaris individuals i equips |

---

### 2. Diferència entre IMAP i POP3
- **IMAP (Internet Message Access Protocol):** Els missatges es mantenen al servidor i el navegador o l'aplicació en mostra una vista sincronitzada. Si es llegeix o s'esborra un correu des del mòbil, el canvi es reflecteix immediatament a l'ordinador.
- **POP3 (Post Office Protocol 3):** Descarrega els missatges directament al dispositiu local i, habitualment, els elimina del servidor. El correu queda guardat en un sol equip i no es manté sincronitzat entre múltiples dispositius.

---

### 3. Configuració d'etiquetes, filtres i resposta de vacances al Gmail
S'han configurat els següents elements al compte del centre:
1. **Etiqueta "institut":** Creada i assignada amb el color **verd**.
2. **Filtre 1 (Institut):** Tots els correus que contenen la paraula `puig` reben automàticament l'etiqueta `institut`.
3. **Filtre 2 (Promocions):** Tots els correus que contenen la paraula `publicitat` reben l'etiqueta `promocions` i s'omet la safata d'entrada (*Skip the Inbox*).
4. **Filtre 3 (Professor 1):** Els correus enviats pel primer professor es marquen sempre com a **importants**.
5. **Filtre 4 (Professor 2):** Els correus enviats pel segon professor es marquen sempre com a **importants**.
6. **Resposta automàtica de vacances:** Activada amb el missatge `"Estic de vacances!"` i les dates del viatge seleccionades.

---

## Fase 2: Comprovació d'accés i capçaleres de correu

### 1. Paràmetres del servidor de correu de Google

| Servei | Servidor | Port | Xifratge |
| :--- | :--- | :---: | :---: |
| **Entrada IMAP** | `imap.gmail.com` | 993 | SSL / TLS |
| **Entrada POP3** | `pop.gmail.com` | 995 | SSL / TLS |
| **Sortida SMTP** | `smtp.gmail.com` | 465 / 587 | SSL/TLS o STARTTLS |

---

### 2. Prova entre dos comptes i anàlisi de capçaleres
1. **Enviament de prova:** S'obre una sessió amb el Compte A i una altra en finestra privada amb el Compte B. S'envia un correu d'A a B amb la paraula `puig` a l'assumpte.
2. **Recepció i etiquetatge:** El missatge arriba correctament al Compte B i rep automàticament l'etiqueta verda `institut`.
3. **Resposta:** Es respon des del Compte B i la resposta arriba a la safata d'entrada del Compte A.
4. **Capçaleres originals (Mostra l'original):**
   - **SPF (Sender Policy Framework):** `PASS` (confirma que el servidor està autoritzat a enviar correus en nom del domini).
   - **DKIM (DomainKeys Identified Mail):** `PASS` (garanteix la signatura digital i que el correu no s'ha alterat).
   - **DMARC:** `PASS` (valida la política de seguretat del domini).
   - **Línies `Received`:** S'identifiquen els salts pels servidors de Google per on ha passat el missatge des de l'origen fins a la bústia de destinació.

---

### 3. Taula de proves del correu (10 files)

| # | Què es prova | Com es prova | Què s'espera | Què ha passat (Resultat) |
| :-: | :--- | :--- | :--- | :--- |
| **1** | Creació d'etiqueta | Crear etiqueta "institut" a la configuració de Gmail | Etiqueta visible a la barra lateral | **Correcte:** Etiqueta creada i assignada a color verd |
| **2** | Filtre paraula "puig" | Enviar correu amb assumpte "Informació puig" | Aplicació automàtica de l'etiqueta "institut" | **Correcte:** El correu rep l'etiqueta verda "institut" |
| **3** | Filtre "publicitat" | Enviar correu amb la paraula "publicitat" | Assignació d'etiqueta "promocions" i ometre safata d'entrada | **Correcte:** Es desvia a "promocions" sense passar per l'entrada |
| **4** | Filtre Professor 1 | Enviar correu des de l'adreça del Professor 1 | Marcatge automàtic com a important | **Correcte:** Apareix la icona d'important activada |
| **5** | Filtre Professor 2 | Enviar correu des de l'adreça del Professor 2 | Marcatge automàtic com a important | **Correcte:** Apareix la icona d'important activada |
| **6** | Resposta de vacances | Enviar correu des d'un compte extern estant actiu el període | Recepció de resposta automàtica "Estic de vacances!" | **Correcte:** El remitent rep la resposta automàtica immediatament |
| **7** | Enviament entre 2 comptes | Enviar missatge des del Compte A cap al Compte B | El missatge s'entrega a la bústia de B | **Correcte:** Arriba correctament en pocs segons |
| **8** | Resposta entre 2 comptes | Respondre al missatge rebut des del Compte B | La resposta s'entrega a la bústia de A | **Correcte:** La resposta es rep correctament al Compte A |
| **9** | Verificació SPF/DKIM/DMARC | Obrir "Mostra l'original" al correu rebut | Els tres registres de seguretat mostren PASS | **Correcte:** SPF: PASS, DKIM: PASS, DMARC: PASS |
| **10** | Traçabilitat de servidors | Revisar línies `Received` a la capçalera del correu | Identificar el recorregut pels servidors SMTP/MTA | **Correcte:** Es visualitzen tots els salts de l'entrega |

---

## Fase 3: Planificació del Viatge a Eivissa (7 Dies, Pressupost 1.500 €)

### 1. Ruta de 7 dies a Eivissa (Google Maps)
- **Punt d'inici i retorn:** Barcelona / València / Eivissa.
- **Ruta organitzada:**
  - **Dia 1:** Arribada al port/aeroport d'Eivissa, allotjament a Eivissa ciutat i passeig per Dalt Vila.
  - **Dia 2:** Excursió a Sant Antoni de Portmany i visita a Cala Salada i Cala Bassa.
  - **Dia 3:** Ferri d'anada i tornada a l'illa de Formentera (Platja de Ses Illetes).
  - **Dia 4:** Visita al municipi de Santa Eulària des Riu i Mercadot Hippy de Las Dalias.
  - **Dia 5:** Ruta per les cales del sud (Cala d'Hort amb vistes al mític illot d'Es Vedrà).
  - **Dia 6:** Parc Natural de Ses Salines i tarda a Platja d'en Bossa.
  - **Dia 7:** Compras d'última hora a Eivissa Centre i vol/ferri de tornada al punt d'origen.
- **Enllaç a la ruta de Google Maps:** `https://maps.google.com/example-ruta-eivissa-7dies` *(guardat a la configuració)*.

<img width="1920" height="1080" alt="Screenshot 2026-11-26 10 48 38" src="https://github.com/user-attachments/assets/9698af1d-2af0-426e-96f8-d6511b782d13" />


---

### 2. Pressupost del viatge (Google Sheets) i funció IF
Es dissenya un full de càlcul amb la distribució de despeses per a una persona (Límit: **1.500 €**):

| Concepte | Descripció | Cost (€) |
| :--- | :--- | :---: |
| **Transport** | Viatge d'anada i tornada (Ferri/Avió) + Lloguer de cotxe / Transport local | 350 € |
| **Allotjament** | Hotel / Apartament a Eivissa (6 nits) | 600 € |
| **Manutenció** | Esmorzars, dinars i sopars (7 dies) | 350 € |
| **Activitats i Entrades** | Bitllet ferri Formentera, visites i entrades a parcs | 120 € |
| **TOTAL** | **Suma total del viatge** | **1.420 €** |
| **Estat del Pressupost** | **Fórmula de control IF** | `=IF(B5<=1500; "Dins del pressupost"; "T'has passat")` |

#### Explicació de la funció IF:
La funció `=IF(condició; valor_si_cert; valor_si_fals)` avalua si la cel·la del total (`B5`) és menor o igual a **1.500 €**. Com que el total és **1.420 €**, la condició es compleix i el full mostra automàticament el text `"Dins del pressupost"`. Si se superés aquesta quantitat, mostraria `"T'has passat"`.

captura hojas de calculo:

<img width="1920" height="1080" alt="Google sheets cauculos viaje" src="https://github.com/user-attachments/assets/e4857c5e-a541-431a-a0c9-a7f7d7457f1c" />


---

### 3. Calendari del Viatge (`CALENDARI_NOM_COGNOMS`)
- **Nom del calendari:** `CALENDARI_NOM_COGNOMS` (personalitzat amb les dades de l'alumne).
- **Esdeveniments diaris:** Creat un esdeveniment per cada dia del viatge (de Dia 1 a Dia 7) amb horari, ubicació exacta i descripció detallada de les activitats.
- **Prestacions avançades de Google Calendar demostrades:**
  1. **Esdeveniment repetit amb data final:** Recordatori diari a les 08:00 h: *"Revisar motxilla, documentació i crema solar"*, repetit diàriament durant els 7 dies i amb data d'acabament fixada el darrer dia del viatge.
  2. **Invitació a un company:** Convidat el company/a a l'esdeveniment de sortida del Dia 1 (*"Sortida cap a Eivissa"*). El company respon que **SÍ** (invitació acceptada).
  3. **Recordatori / Notificació:** Configurada una notificació de calendari **24 hores abans** de la sortida del viatge.
  4. **Llista de Tasques (Google Tasks):**
     - *Tasca 1:* Comprar bitllets de transport (Data límit: 15 dies abans del viatge).
     - *Tasca 2:* Reservar allotjament a Eivissa (Data límit: 10 dies abans del viatge).
     - *Tasca 3:* Fer la maleta i preparar documentació (Data límit: 1 dia abans del viatge).

#### Captures de pantalla del calendari i tasques:

<img width="1920" height="1080" alt="Screenshot 2026-11-26 11 03 53" src="https://github.com/user-attachments/assets/dfb3445b-97ec-43b9-a325-20b646884ea3" />

<img width="1920" height="1080" alt="Screenshot 2026-11-26 11 09 47" src="https://github.com/user-attachments/assets/60d731ec-5414-49e2-9012-fe80e8cdccb6" />

<img width="1920" height="1080" alt="Screenshot 2026-11-26 11 11 06" src="https://github.com/user-attachments/assets/0d664743-2de2-4bd7-961a-8734146c9221" />

<img width="1920" height="1080" alt="Screenshot 2026-11-26 11 12 10" src="https://github.com/user-attachments/assets/a3a00ede-76ec-4e51-ac68-a5c837d1065b" />

<img width="1920" height="1080" alt="Screenshot 2026-11-26 11 13 46" src="https://github.com/user-attachments/assets/cc9a360f-1d01-4aa4-a1f0-8510e1f7893f" />



---

## Fase 4: Permisos, seguretat i taula de proves del viatge

### 1. Gestió de permisos de compartició
- **Full de càlcul del pressupost:** Compartit amb el professorat amb el permís de **Veure** (Lector), evitant modificacions no autoritzades.
- **Calendari del viatge:** Compartit amb el company de viatge amb el permís de **Veure tots els detalls de l'esdeveniment**, permetent-li consultar l'itinerari complet.
- **Verificació en dues passes (2FA):** Comprovat que la verificació en 2 passes està activada al compte corporatiu per a màxima seguretat.

---

### 2. Resposta a la pregunta sobre la compartició de fitxers

> **Pregunta:** Quina diferència hi ha entre compartir el full amb «qualsevol que tingui l'enllaç» i amb persones concretes, quina opció s'ha triat i per què?
>
> **Resposta:** 
> - **Qualsevol que tingui l'enllaç:** Permet que qualsevol persona que obtingui el link pugui accedir al fitxer sense necessitat d'autenticar-se. Això representa un risc de seguretat, ja que l'enllaç es pot filtrar o reenviar a tercers no autoritzats.
> - **Persones concretes:** Restringeix l'accés exclusivament a les adreces de correu electrònic especificades (mitjançant compte de Google), garantint control total i privacitat.
> - **Elecció realitzada:** S'ha triat l'opció de **compartir amb persones concretes** (l'adreça del professorat per al full i la del company per al calendari). S'ha escollit aquesta opció per un criteri professional de seguretat i privacitat, assegurant que només les persones implicades en l'activitat tinguin accés a la informació del viatge i del pressupost.

---

### 3. Taula de proves del calendari i planificació del viatge (10 files)

| # | Què es prova | Com es prova | Què s'espera | Què ha passat (Resultat) |
| :-: | :--- | :--- | :--- | :--- |
| **1** | Ruta a Google Maps | Crear la ruta de 7 dies a Eivissa i desar l'enllaç | Ruta d'anada i tornada amb totes les parades | **Correcte:** Enllaç generat i funcional amb els 7 dies |
| **2** | Full de pressupost | Crear taula de despeses i introduir la fórmula IF | El full calcula 1.420 € i indica "Dins del pressupost" | **Correcte:** El text de la fórmula es mostra correctament |
| **3** | Permisos del full | Compartir el full de càlcul amb l'adreça del professor | Permís assignat com a "Lector" (Veure) | **Correcte:** El professor pot veure les dades sense editar |
| **4** | Creació del calendari | Crear calendari amb nom `CALENDARI_NOM_COGNOMS` | Calendari creat amb nom i color personalitzat | **Correcte:** Calendari actiu i visible a la barra lateral |
| **5** | Esdeveniments diaris | Inserir 1 esdeveniment per cada dia (Dia 1 a Dia 7) | Cada dia té el seu horari, lloc i descripció | **Correcte:** Els 7 dies estan completament detallats |
| **6** | Esdeveniment repetit | Crear recordatori diari a les 08:00 h amb data final | L'esdeveniment es repeteix i acaba l'últim dia | **Correcte:** Finalitza exactament la data establerta |
| **7** | Convidats i resposta | Afegir el company a l'esdeveniment del Dia 1 | El company rep la invitació i respon afirmativament | **Correcte:** L'estat de la invitació canvia a "Acceptada" |
| **8** | Recordatori | Afegir notificació al primer esdeveniment del viatge | Rebre avís de calendari 24 hores abans | **Correcte:** Notificació programada correctament |
| **9** | Llista de Tasques | Inserir 3 tasques amb data límit a Google Tasks | Les 3 tasques apareixen al panell lateral i al calendari | **Correcte:** Les tasques es mostren amb la seva data límit |
| **10** | Permisos del calendari | Compartir calendari amb el company amb permís de detalls | El company veu tots els esdeveniments des del seu compte | **Correcte:** El company veu l'itinerari complet |

---

## Conclusió
Tots els passos requerits a les 4 fases de la pràctica **P5.1** s'han completat, provat i documentat satisfactòriament. Aquest `README.md` està preparat per a ser publicat directament al repositori públic de GitHub per a la seva avaluació.
