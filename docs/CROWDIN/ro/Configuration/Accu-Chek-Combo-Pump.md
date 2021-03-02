# Pompa Accu Chek Spirit Combo

**Acesta aplicație face parte dintr-o soluție DIY (do-it-yourself/ o aplicație pe care o construiești singur) și nu este un produs finit; ea solicita implicarea utilizatorului: să citească, să învețe și să înțeleagă sistemul, de la construcție pana la modul de utilizare. Nu este un facut pentru a vă gestiona tratamentul diabetul in totalitate, dar vă permite să vă îmbunătățiți calitatea vieții alaturi de diabet, dacă sunteți dispus să acordați timpul necesar. Acordați-vă timp pentru a învăța sa-l intelegeti si folosi. You alone are responsible for what you do with it.**

## Cerințe hardware

* O pompă de insulină Accu-Chek Combo (orice versiune de firmware, funcționează toate)
* Un dispozitiv Smartpix sau Realtyme împreună cu Softul de Configurare 360 pentru a configura pompa. (Roche sends out Smartpix devices and the configuration software free of charge to their customers upon request.)
* Un telefon compatibil: un telefon Android pe care să poată fi instalat sistemul de operare LineageOS 14.1 (fostul CyanogenMod) sau Android 8.1 (Oreo). 
* Versiunea de LineageOS 14.1 trebuie să fie una relativ recentă, cel puțin mai nouă de Iunie 2017, deoarece schimbarea necesară pentru conectarea cu pompa Combo a fost introdusă începând de atunci. 
* O listă de telefoane compatibile poate fi găsită în documentul [telefoane AAPS](https://docs.google.com/spreadsheets/d/1gZAsN6f0gv6tkgy9EBsYl0BQNhna0RDqA9QGycAqCQc/edit).
* Atenție la faptul că aceasta nu este o listă completă și reflectă doar experiența avută de utilizator în folosire. Vă încurajăm să scrieți și experiența pe care o aveți dumneavoastră, cu scopul de a ajuta și alte persoane în luarea unei decizii (toate aceste proiecte sunt despre a vă aduce propria contribuție la binele comunității).
* Be aware that while Android 8.1 allows communicating with the Combo, there are still issues with AAPS on 8.1.
* For advanced users, it is possible to perform the pairing on a rooted phone and transfer it to another rooted phone to use with ruffy/AAPS, which must also be rooted. This allows using phones with Android < 8.1 but has not been widely tested: https://github.com/gregorybel/combo-pairing/blob/master/README.md

## Limitări

* Bolusul extins și bolusul multiwave nu sunt suportate (vedeți [Carbohidrați extinși](../Usage/Extended-Carbs.rst) ca înlocuitor).
* Doar un singur profil bazal este suportat.
* Setting a basal profile other than 1 on the pump or delivering extended boluses or multiwave boluses from the pump interferes with TBRs and forces the loop into low-suspend only mode for 6 hours as the the loop can't run safely under these conditions.
* It's currently not possible to set the time and date on the pump, so [daylight saving time changes](../Usage/Timezone-traveling#accu-chek-combo) have to be performed manually (you may disable the phone's automatic clock update in the evening and change it back in the morning together with the pump clock to avoid an alarm during the night).
* În prezent sunt suportate doar rate bazale în intervalul 0.05 până la 10 U/o. This also applies when modifying a profile, e.g. when increasing to 200%, the highest basal rate must not exceed 5 U/h since it will be doubled. Similar, când se reduce cu 50%, cea mai mică rată a bazalei trebuie să fie cel puțin 0.10U/o.
* If the loop requests a running TBR to be cancelled the Combo will set a TBR of 90% or 110% for 15 minutes instead. This is because cancelling a TBR causes an alert on the pump which causes a lot of vibrations.
* Occasionally (every couple of days or so) AAPS might fail to automatically cancel a TBR CANCELLED alert, which the user then needs to deal with (by pressing the refresh button in AAPS to transfer the warning to AAPS or confirming the alert on the pump).
* Bluetooth connection stability varies with different phones, causing "pump unreachable" alerts, where no connection to the pump is established anymore. 
* If that error occurs, make sure Bluetooth is enabled, press the Refresh button in the Combo tab to see if this was caused by an intermitted issue and if still no connection is established, reboot the phone which should usually fix this. 
* There is another issue were a restart doesn't help but a button on the pump must be pressed (which resets the pump's Bluetooth), before the pump accepts connections from the phone again. 
* There is very little that can be done to remedy either of those issues at this point. So if you see those errors frequently your only option at this time is to get another phone that's known to work well with AndroidAPS and the Combo (see above).
* Issuing a bolus from the pump will not always be detected in time (checked for whenever AAPS connects to the pump), and might take up to 20 minutes in the worst case. 
* Bolusurile din pompă sunt întotdeauna verificate înainte de a se seta o RBT mărită sau de a se livra un bolus de către AAPS, dar datorită limitărilor AAPS, va fi refuzată administrarea RBT/bolusului dacă a fost calculat pe baza unor premise false. (-> Nu bolusați din pompă! See chapter [Usage](#usage) below)
* Setarea unei RBT în pompă ar trebui evitată, deoarece doar bucla ar trebuie să ia astfel de decizii și să facă astfel de acțiuni - ar trebui să fie singura care controlează RBT-urile. Detectarea unei RBT noi în pompă durează până la 20 de minute și efectul RBT-ului va fi luat în calcul doar începând cu momentul detecției, astfel că în cazul cel mai rău pot exista 20 de minute a unei RBT a cărei valoare să nu se reflecte în IOB. 

## Instalare

* Configurați pompa folosind software-ul 360 config software. 
* Dacă nu aveți acest software, contactați linia telefonică de suport Accu-Chek. De obicei, aceștia vor trimite către utilizatorii înregistrați un CD conținând software-ul "360° Pump Configuration Software" și un dispozitiv de conectare USB-infraroșu SmartPix (de asemenea, se poate folosi și dispozitivul Realtyme).
* **Required settings** (marked green in screenshots):
    
    * Set/leave the menu configuration as "Standard", this will show only the supported menus/actions on the pump and hide those which are unsupported (extended/multiwave bolus, multiple basal rates), which cause the loop functionality to be restricted when used because it's not possible to run the loop in a safe manner when used.
    * Verificați că *Quick Info Text* este denumit exact "QUICK INFO" (fără ghilimele; se găsește la *Opțiuni pompă de insulină*).
    * Setați RBT *Ajustare maximă* la 500%
    * Dezactivați *Semnalizați terminarea Ratei Bazale Temporare*
    * Setați RBT *Incrementarea duratei* la 15 min
    * Activați Bluetooth-ul

* **Recommended settings** (marked blue in screenshots)
    
    * Stabiliți alarma de cartuș pe terminate așa cum considerați necesar
    * Configurați un bolus maxim potrivit indicațiilor dumneavoastră terapeutice pentru a vă proteja de o eventuală eroare posibilă în software
    * În mod similar, configurați o durată maximă a RBT ca un mijloc de protecție. Allow at least 3 hours, since the option to disconnect the pump for 3 hours sets a 0% for 3 hours.
    * Activați opțiunea de blocare a tastelor pompei, pentru prevenirea bolusării folosind pompa, mai ales when the pump was used before and quick bolusing was a habit.
    * Stabiliți un interval minim de 5.5, respectiv 5 pentru timpul după care ecranul să se stingă automat sau meniurile să se stingă automat. This allows the AAPS to recover more quickly from error situations and reduces the amount of vibrations that can occur during such errors

![Captură de ecran al meniului setărilor de utilizator](../images/combo/combo-menu-settings.png)

![Captură de ecran a setărilor RBT](../images/combo/combo-tbr-settings.png)

![Captură de ecran al setărilor de bolus](../images/combo/combo-bolus-settings.png)

![Captură de ecran al setărilor cartușului de insulină](../images/combo/combo-insulin-settings.png)

* Install AndroidAPS as described in the [AndroidAPS docs](../Installing-AndroidAPS/Building-APK.md).
* Make sure to read the docs to understand how to setup AndroidAPS.
* Select the **MDI plugin** in AndroidAPS, not the Combo plugin at this point to avoid the Combo plugin from interfering with ruffy during the pairing process.
* Clone [ruffy](https://github.com/MilosKozak/ruffy) from github via git.
* Instalați Ruffy și folosiți-o pentru împerecherea cu pompa.
    
    * În cazul în care împerecherea nu funcționează după încercări multiple, puteți schimba branch-ul cu `pairing`, împerecheați cu pompa și apoi reveniți la branch-ul original.
    * Note that the pairing processing is somewhat fragile (but only has to be done once) and may need a few attempts; quickly acknowledge prompts and when starting over, remove the pump device from the Bluetooth settings beforehand. 
    * Another option to try is to go to the Bluetooth menu after initiating the pairing process (this keeps the phone's Bluetooth discoverable as long as the menu is displayed) and switch back to ruffy after confirming the pairing on the pump, when the pump displays the authorization code.
    * Dacă totuși nu reușiti să duceți la bun sfârșit împerecherea cu pompa (să spunem după 10 încercări), așteptați până la 10 secunde înainte de a confirma împerecherea cu pompa (atunci când numele telefonului este afișat pe ecranul pompei). 
    * Dacă ați configurat ca meniul pompei să se stingă după 5 secunde, va fi necesar să măriți din nou acest interval. Câțiva utilizatori au raportat faptul că această setare a fost necesară. 
    * Ca o ultimă soluție, puteți încerca să vă mutați într-o altă încăpere pentru a evita eventualele interferențe radio locale. Cel puțin un utilizator a reușit să treacă cu succes peste etapa de împerechere cu pompa doar schimbând camera în care încerca acest lucru.

* Atunci când AAPS folosește ruffy, aplicația ruffy nu mai este disponibilă utilizatorului. The easiest way is to just reboot the phone after the pairing process and let AAPS start ruffy in the background.

* If the pump is completely new, you need to **do one bolus on the pump**, so the pump creates a first history entry.
* Before enabling the Combo plugin in AAPS make sure your profile is set up correctly and activated(!) and your basal profile is up to date as AAPS will sync the basal profile to the pump.
* Then activate the [Combo plugin](../Configuration/Config-Builder#pump). 
* Press the *Refresh* button on the Combo tab to initialize the pump.
* Pentru verificarea instalării, având pompa **deconectată de pacient (!!!)**, folosiți AAPS pentru a seta o RBT de 500% pentru 15 minute și administrați un bolus.
* Pompa ar trebui să aibă acum un RBT activ și să afișeze bolusul în istoric. AAPS ar trebui, de asemenea, să afișeze RBT-ul activ și bolusul livrat.

## Why does pairing with the pump not work with the app "ruffy"?

Există câteva cauze posiblie. Încercați următorii pași:

1. Introduceți o **baterie nouă și nefolosită** în pompă. Citiți secțiunea referitoare la baterii pentru mai multe detalii. Asigurați-vă că pompa se află foarte aproape de telefon.

![Combo trebuie să fie poziționat foarte aproape de telefon](../images/Combo_next_to_Phone.png)

2. Opriți sau îndepărtați orice alt dispozitiv bluetooth astfel încât acestea să nu poată să influențeze procesul de împerechere, când acesta este în desfășurare. Orice altă comunicare în spectrul bluetooth sau cerere de stabilire a unei conexiuni poate interfera cu procesul de împerechere.
3. Delete already connected devices in the Bluetooth menu of the pump: **BLUETOOTH SETTINGS / CONNECTION / REMOVE** until **NO DEVICE** is shown.
4. Delete a pump already connected to the phone via Bluetooth: Under Settings / Bluetooth, remove the paired device "**SpiritCombo**"
5. Asigurați-vă că AAPS nu rulează bucla în fundal. Disable Loop in AAPS.
6. Acum porniți ruffy pe telefon. S-ar putea să trebuie să apăsați Reset! și să ștergeți o eventuală conexiune veche. Apoi apăsați Connect!.
7. În meniul Bluetooth al pompei, mergeți la **ADĂUGAȚI DISPOZITIV / ADĂUGAȚI CONEXIUNE NOUĂ**". Press *CONNECT!**
    
    * Step 6 and 7 have to be done in a short timing.

8. Acum pompa ar trebui să afișeze numele bluetooth al telefonului pentru a putea fi selectat pentru împerechere. Here it is important to wait at least 5s before you hit the select button on Pump. Otherwise the Pump will not send the Pairing request to the Phone properly.

* If Combo Pump is set to 5s Screen timeout, you may test it with 40s (original setting). From experience the time between pump is showing up in phone until select phone is around 5-10s. In many other cases pairing just times out without successfully Pair. 
* Nu uitați să stabiliți timpul de stingere al ecranului la 5 secunde, după ce ați reușit împerecherea pompei cu telefonul, pentru a respecta cerințele AAPS.
* If the pump does not show the phone as a pairing device at all, your phone's Bluetooth stack is probably not compatible with the pump. Make sure you are running a new **LineageOS ≥ 14.1** or **Android ≥ 8.1 (Oreo)**. If possible, try another smartphone. Puteți găsi o listă de telefoane care au reușit împerecherea cu pompa la \[AAPS Phones\] (https://docs.google.com/spreadsheets/d/1gZAsN6f0gv6tkgy9EBsYl0BQNhna0RDqA9QGycAqCQc/edit). 

9. În continuare, pompa ar trebui să afișeze un cod de securitate format din 10 numere. Iar Ruffy, un ecran în care să scrieți aceste numere. Deci introduceți numerele afișate de pompă în Ruffy și asta ar trebui să fie totul.
10. Reporniți telefonul.
11. Acum puteți reporni bucla în AAPS.

## Folosire

* Reamintiți-vă că acesta nu este un produs, mai ales in the beginning the user needs to monitor and understand the system, its limitations and how it can fail. 
* It is strongly advised NOT to use this system when the person using it is not able to fully understand the system.
* Read the OpenAPS documentation https://openaps.org to understand the loop algorithm AndroidAPS is based upon.
* Read the [AAPS docs](../index.rst) to learn about and understand AndroidAPS.
* Această aplicație folosește aceeași funcționalitate pe care o asigură glucometrul ce vine odată cu pompa Combo.
* Acest glucometru permite să clonați ecranul pompei și transmite apăsările butoanelor către pompă. 
* The connection to the pump and this forwarding is what the ruffy app does. 
* A 'scripter' components reads the screen and automates entering boluses, TBRs etc and making sure inputs are processed correctly.
* AAPS interacționează cu scriptul pentru a implementa comenzile pe care le generează bucla și pentru a administra bolusuri.
* This mode has some restrictions: it's comparatively slow (but well fast enough for what it is used for) and setting a TBR or giving a bolus causes the pump to vibrate.
* The integration of the Combo with AndroidAPS is designed with the assumption that all inputs are made via AndroidAPS. Boluses entered on the pump directly will be detected by AAPS, but it can take up to 20 min before AndroidAPS becomes aware of such a bolus. 
* Reading boluses delivered directly on the pump is a safety feature and not meant to be regularly used (the loop requires knowledge of carbs consumed, which can't be entered on the pump, which is another reason why **all inputs should be done in AndroidAPS**). 
* Nu stabiliți sau anulați o RBT direct în pompă. Bucla presupune că are controlul total asupra RBT și nu poate genera comenzi corect altfel, deoarece nu poate determina cu precizie timpul la care este pornit RBT-ul setat de utilizator direct în pompă.
* Primul profil bazal al pompei este citit de către aplicație la pornirea acesteia și este updatat de către AAPS.
* The basal rate should not be manually changed on the pump, but will be detected and corrected as a safety measure (don't rely on safety measures by default, this is meant to detect an unintended change on the pump).
* Se recomandă să activați blocarea tastelor pompei, pentru a preveni bolusarea directă, mai ales when the pump was used before and using the "quick bolus" feature was a habit.
* Also, with keylock enabled, accidentally pressing a key will NOT interrupt active communication between AAPS and pump.
* When a BOLUS/TBR CANCELLED alert starts on the pump during bolusing or setting a TBR, this is caused by a disconnect between pump and phone, which happens from time to time. AAPS will try to reconnect and confirm the alert and then retry the last action (**boluses are NOT retried** for safety reasons). 
* Prin urmare, o astfel de alarmă poate fi ignorată deoarece AAPS o va confirma automat, de obicei în termen de 30s (anularea acesteia nu este o problemă, dar va conduce către acţiunea activă curentă și va trebui să aşteptați până când ecranul pompei se va opri înainte de a se putea reconecta la pompă). 
* If the pump's alarm continues, automatic confirmation failed, in which case the user needs to confirm the alarm manually.
* When a low cartridge or low battery alarm is raised during a bolus, they are confirmed and shown as a notification in AAPS. 
* If they occur while no connection is open to the pump, going to the Combo tab and hitting the Refresh button will take over those alerts by confirming them and show a notification in AAPS.
* When AAPS fails to confirm a TBR CANCELLED alert, or one is raised for a different reason, hitting Refresh in the Combo tab establishes a connection, confirms the alert and shows a notification for it in AAPS. This can safely be done, since those alerts are benign - an appropriate TBR will be set again during the next loop iteration.
* For all other alerts raised by the pump: connecting to the pump will show the alert message in the Combo tab, e.g. "State: E4: Occlusion" as well as showing a notification on the main screen.
* O eroare va genera o notificare urgentă. 
* AAPS never confirms serious errors on the pump, but let's the pump vibrate and ring to make sure the user is informed of a critical situation that needs action.
* After pairing, ruffy should not be used directly (AAPS will start in the background as needed), since using ruffy at AAPS at the same time is not supported.
* If AAPS crashes (or is stopped from the debugger) while AAPS and the pump were communicating (using ruffy), it might be necessary to force close ruffy. Repornirea AAPS va duce și la repornirea Ruffy.
* Restarting the phone is also an easy way to resolve this if you don't know how to force kill an app.
* Don't press any buttons on the pump while AAPS communicates with the pump (Bluetooth logo is shown on the pump).