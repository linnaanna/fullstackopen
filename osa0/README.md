title 0.4: Uusi muistiinpano

selain->palvelin: HTTP POST https://studies.cs.helsinki.fi/exampleapp/new_note

note over selain:
selain lähettää napin painalluksella palvelimelle POST-pyynnön,
jossa mukana bodynä tekstikentän sisältämä data sekä aikaleima
end note

palvelin-->selain: HTTP statuskoodi 302

note over palvelin:
palvelimella on koodia, joka huolehtii POST pyynnöstä. Se luo uutta muistiinpanoa 
vastaavan olion ja laittaa sen muistiinpanot sisältävään taulukkoon.
palvelin palauttaa vastauksena statuskoodin 302 eli uudelleenohjauspyynnön, joka
kehottaa selainta tekemään uuden GET pyynnön osoitteeseen notes
end note

selain->palvelin: HTTP GET https://studies.cs.helsinki.fi/exampleapp/notes
palvelin-->selain: HTML-koodi
selain->palvelin: HTTP GET https://studies.cs.helsinki.fi/exampleapp/main.css
palvelin-->selain: main.css
selain->palvelin: HTTP GET https://studies.cs.helsinki.fi/exampleapp/main.js
palvelin-->selain: main.js

note over selain:
selain alkaa suorittaa js-koodia
joka pyytää JSON-datan palvelimelta
end note

selain->palvelin: HTTP GET https://studies.cs.helsinki.fi/exampleapp/data.json
palvelin-->selain: [{ content: "HTML on helppoa", date: "2019-01-01" }, ...]

note over selain:
selain suorittaa tapahtumankäsittelijän
joka renderöi muistiinpanot näytölle ml. uuden muistiinpanon
end note

-----------------------------------------------
title 0.5: Single Page App

selain->palvelin: HTTP GET https://studies.cs.helsinki.fi/exampleapp/spa
palvelin-->selain: HTML-koodi
selain->palvelin: HTTP GET https://studies.cs.helsinki.fi/exampleapp/main.css
palvelin-->selain: main.css
selain->palvelin: HTTP GET https://studies.cs.helsinki.fi/exampleapp/spa.js
palvelin-->selain: spa.js

note over selain:
selain alkaa suorittaa js-koodia
joka pyytää JSON-datan palvelimelta
end note

selain->palvelin: HTTP GET https://studies.cs.helsinki.fi/exampleapp/data.json
palvelin-->selain: [{"content":"new note","date":"2022-10-31T19:16:44.328Z"}, ...]

note over selain:
selain suorittaa tapahtumankäsittelijän
joka renderöi muistiinpanot näytölle
end note

--------------------------------------------------
title 0.6: Uusi muistiinpano

selain->palvelin: HTTP POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa

note over selain:
Koodi luo muistiinpanon, lisää sen muistiinpanojen listalle, 
renderöi muistiinpanojen listan uudelleen ja lähettää POST-pyynnössä uuden 
muistiinpanon palvelimelle JSON-muodossa. 
end note

palvelin-->selain: HTTP statuskoodi 201 eli 'created'

note over palvelin
palvelin ei pyydä uudelleenohjausta.Selain pysyy samalla sivulla 
ja muita HTTP-pyyntöjä ei suoriteta.
end note