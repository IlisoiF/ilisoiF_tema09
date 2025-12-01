
1) Texturi cu transparență vs. fără transparență

Texturile cu transparență (PNG, TGA cu canal alfa) duc la zone transparente sau semi-transparente în obiectul randat atunci când blending-ul este activat.

Fără blending, pixelii transparenți apar ca negru sau altă culoare default.

Texturile fără transparență sunt tratate ca simple texturi RGB, fără efecte vizuale legate de opacitate.


2) Formate de imagine utilizabile în OpenGL

Orice format care poate fi încărcat prin biblioteca folosită pentru decodare (în OpenTK, de obicei System.Drawing sau ImageSharp).

Cele mai frecvente: PNG, JPG, BMP, TGA, plus DDS pentru texturi comprimate (DXT1, DXT5).

OpenGL nu impune un format anume; important este ca în cod imaginea să fie convertită în bitmap raw (RGB, RGBA).


3) Efectul modificării culorii obiectului texturat (RGB)

Culoarea obiectului acționează ca un factor de multiplicare pentru texelul texturii.

Dacă obiectul este colorat cu (1,1,1), textura rămâne neschimbată.

Dacă se reduce un canal (ex. R), textura devine mai albastră și verde, deoarece componenta roșie este atenuată.

Dacă luminozitatea obiectului este redusă global, textura apare mai întunecată.


4) Diferențe între scenă cu iluminare activată vs. dezactivată

Cu iluminarea activată: textura este afectată de lumină, umbre, atenuare, normal vectors; culorile devin mai realiste și respectă poziția surselor de lumină.

Cu iluminarea dezactivată: textura apare uniformă pe toată suprafața, fără zone mai luminoase sau mai întunecate; efectul este plat, fără profunzime.

În modul iluminare activat, calitatea normalelor din model devine esențială. În modul dezactivat, normalelor nu li se acordă importanță.
