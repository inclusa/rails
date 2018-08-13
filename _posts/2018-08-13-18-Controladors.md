---
layout: post # Sustituye el layout si lo usas uno diferente
title: 18 Controladors # Nombre generado automáticamente
---

Els controladors de Rails són el centre lògic de la teua aplicació. Coordina les interaccions entre l'usuari, les vistes i el model. A més té altres serveis:

- És responsable d'enrutar les respostes externes a les accions internet. A més utilitza URLs molt bé.
- Gestiona la caché, amb la qual pot donar ordres a efectives per a l'arranc de les aplicacions.
- Gestiona els mòduls d'ajuda, amb els quals s'extenen les capacitats de les plantilles de les vistes sense tornar a generar aquest codi.
- Gestiona sesions, dóna usuaris la impressió d'interaccionar amb les aplicacions.

El procés de cració d'un controlador és molt fàcil, i és similar al procés en el què hem creat el model. Es fa així:

```ruby
rails generate controller Book
```

Al tant, utililitzem la paraula `Book` en **majúscula** i en **singular**. Aquest és el procediment per a crear controladors.

Es creen a aquesta ruta `àpp/controllers/book_controller.rb`.

Podem observar el seu contingut:

```ruby
class BookController < ApplicationController
end
```

