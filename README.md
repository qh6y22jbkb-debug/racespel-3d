# VELOX 3D — circuitracer

Het hele spel zit in één bestand: `index.html`. Three.js 0.160.0 komt via een CDN (cdn.jsdelivr.net). Er is geen build-stap.
Alle auto's, merken, circuits en sponsors zijn verzonnen.

## Besturing

**Toetsenbord**

| Toets | Actie |
|---|---|
| ↑ / W | Gas |
| ↓ / S | Remmen. Als je stilstaat en blijft drukken, rijd je achteruit |
| ← → / A D | Sturen. Bij hoge snelheid stuur je minder ver |
| Spatie | Handrem (om te driften) |
| Shift | Nitro |
| C | Camera wisselen: achtervolging, motorkap, cockpit, ver weg |
| R | Auto terugzetten op de baan |
| Q / E | Schakelen, alleen als je in de race-instellingen "Handmatig" kiest |
| Esc / P | Pauze |
| F | Fps-teller aan/uit |

**Gamepad:** RT gas · LT rem · linkerstick sturen · A nitro · X handrem · Y camera · LB/RB schakelen · Back reset · Start pauze.

**Telefoon/tablet:** houd het scherm liggend. Links zitten ◀ ▶, HANDREM en CAMERA, rechts GAS, REM en NITRO.
In Instellingen → "Sturen mobiel" kies je **Kantelen (gyro)**: dan stuur je door de telefoon als een stuur te draaien.

**Tips**
- Nitro laad je op door te driften, in de slipstroom van een andere auto te rijden, schoon over het asfalt te rijden en door een ronde af te maken.
- Gras en grind geven minder grip en remmen je af. De Ravik R4 (rally) heeft daar het minst last van.
- Bij regen heb je minder grip en remmen de AI-rijders eerder.
- Geef je gas voordat het startlicht uitgaat, dan krijg je 5 seconden straf.
- Rijhulp (Instellingen): *Licht* is de standaard. *Uit* is voor gevorderde spelers, *Sterk* is handig voor kinderen.

## Modi
- **Snelle race**: 3 tot 5 ronden tegen 7 AI-rijders, met de niveaus makkelijk, normaal en moeilijk. Na de finish volgt een tv-herhaling, daarna het podium en de uitslag.
- **Tijdrit**: je rijdt alleen. Je beste ronde rijdt daarna mee als blauwe ghost. Stoppen doe je via pauze → "Naar hoofdmenu".
- **Kampioenschap**: drie races (Alpenring Valdoro, Neon Haven, Kaap Solara). Je krijgt punten volgens 10-8-6-5-4-3-2-1.

Records, ghosts en garage-keuzes worden bewaard in de browser (localStorage).

## Testen op je eigen computer
Dubbelklikken op `index.html` werkt niet, want browsers blokkeren ES-modules via `file://`. Start in deze map een mini-server:

```bash
python3 -m http.server 8000
```

Open daarna http://localhost:8000.

## Uploaden en hosten
1. Zet `index.html` op een webhost, bijvoorbeeld als `racespel/index.html`. Meer bestanden zijn niet nodig.
2. Gebruik https. Dan werken volledig scherm, de bewegingssensor (gyro) en geluid op mobiel het best.
3. Opties die gratis zijn: GitHub Pages, Netlify (map erin slepen) of Cloudflare Pages.
4. **meester-jop.nl** heeft een strenge CSP: geen CDN en geen inline scripts. Daar werkt dit bestand niet zomaar.
   Het moet dan eerst gebundeld worden (Three.js lokaal, script in een apart .js-bestand), net zoals bij Voetbalwereld.

## Zo maak je het nog realistischer
- **Echte 3D-automodellen (GLB/glTF)**: laad ze met `GLTFLoader`, eventueel met DRACO-compressie. Gebruik alleen modellen met een vrije licentie (bijvoorbeeld CC0) en zonder echte merken.
- **HDRI-omgevingen**: een `.hdr`-bestand van bijvoorbeeld Poly Haven (CC0) via `RGBELoader` maakt de lucht en de reflecties veel echter dan de procedurele lucht.
- **Foto-texturen (PBR)**: asfalt, gras, grind en beton met kleur-, normal-, roughness- en AO-maps (bijvoorbeeld van ambientCG, CC0), in plaats van de canvas-texturen.
- **Echte motorgeluiden**: opnames per toerental (samples) met crossfades zijn beter dan de synthesizer.
- **Betere schaduwen en licht**: cascaded shadow maps, SSAO (ambient occlusion) en lichtvlekken (lightmaps) die vooraf berekend zijn voor het circuit.
- **Reflecties op natte weg**: screen-space reflections of een `Reflector` voor plassen.
- **Fysica**: een volledig bandenmodel (Pacejka per wiel) met vering per wiel, bijvoorbeeld met Rapier of cannon-es (RaycastVehicle).
- **Circuits uit echte hoogtedata**: een heightmap voor het terrein en een spline-editor voor nieuwe banen.
- **Meer publiek en details**: geanimeerde mensen, marshals met vlaggen, pitstraat met monteurs, vogels en geanimeerde vlaggen.
