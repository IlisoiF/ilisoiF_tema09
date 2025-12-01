1. Observații privind texturarea în OpenTK_winforms_z03

Aplicația încarcă textura în GPU folosind GL.GenTexture, GL.BindTexture și setările standard de filtrare și wrapping.

Coordonatele de textură sunt predefinite în structurile de date ale obiectelor 3D.

La testarea celor două tipuri de obiecte 3D, textura este mapată în funcție de modul în care fiecare obiect își definește coordonatele UV. Obiectele cu UV-uri bine definite afișează textura corect; cele fără mapare completă pot prezenta întinderi sau zone deformate.


2. Stocarea și încărcarea vertecșilor

Vertecii sunt stocați într-o structură ce include poziția, normalul și coordonata de textură.

Lista de vertecși este transferată în GPU prin VBO (Vertex Buffer Object) și organizată printr-un VAO (Vertex Array Object).

În aplicație, fiecare obiect are o listă proprie de vertecși și indici, încărcate la inițializare, apoi utilizate direct în momentul randării.


3. Modificarea aplicației pentru texturare pe obiecte volumetrice sau suprafețe non-rectangulare

Pe obiecte volumetrice (sferă, cilindru, tor), rezultatul depinde de modul în care sunt generate coordonatele UV. Dacă sunt corect generate (de tip "unwrap"), textura se aplică natural pe întreaga suprafață.

Pe forme neregulate sau neplanare apar adesea distorsiuni, suprapuneri sau cusături vizibile dacă UV-urile nu sunt distribuite uniform.

Obiectele definite procedural, fără UV-uri explicite, necesită generarea lor manuală; altfel textura va apărea nealiniată sau repetată haotic.


6. Răspunsuri la întrebări

a) Texturi cu transparență vs. fără transparență

Texturile cu transparență (PNG, TGA cu canal alfa) duc la zone transparente sau semi-transparente în obiectul randat atunci când blending-ul este activat.

Fără blending, pixelii transparenți apar ca negru sau altă culoare default.

Texturile fără transparență sunt tratate ca simple texturi RGB, fără efecte vizuale legate de opacitate.

b) Formate de imagine utilizabile în OpenGL

Orice format care poate fi încărcat prin biblioteca folosită pentru decodare (în OpenTK, de obicei System.Drawing sau ImageSharp).

Cele mai frecvente: PNG, JPG, BMP, TGA, plus DDS pentru texturi comprimate (DXT1, DXT5).

OpenGL nu impune un format anume; important este ca în cod imaginea să fie convertită în bitmap raw (RGB, RGBA).

c) Efectul modificării culorii obiectului texturat (RGB)

Culoarea obiectului acționează ca un factor de multiplicare pentru texelul texturii.

Dacă obiectul este colorat cu (1,1,1), textura rămâne neschimbată.

Dacă se reduce un canal (ex. R), textura devine mai albastră și verde, deoarece componenta roșie este atenuată.

Dacă luminozitatea obiectului este redusă global, textura apare mai întunecată.

d) Diferențe între scenă cu iluminare activată vs. dezactivată

Cu iluminarea activată: textura este afectată de lumină, umbre, atenuare, normal vectors; culorile devin mai realiste și respectă poziția surselor de lumină.

Cu iluminarea dezactivată: textura apare uniformă pe toată suprafața, fără zone mai luminoase sau mai întunecate; efectul este plat, fără profunzime.

În modul iluminare activat, calitatea normalelor din model devine esențială. În modul dezactivat, normalelor nu li se acordă importanță.
