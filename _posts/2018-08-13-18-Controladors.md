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

El controlador hereta de `ApplicationController`, el qual es altre arxiu de del directori de controladors: `application.rb`.

`ApplicationController` conté el codi que pot ser executat pels teus controladors i heratat per Rails `ActionController::base` class.

No necessites preocupar-te per `ApplicationController`

No necessiteu preocupar-vos per l'`ApplicationController` fins ara, així que només definirem uns quants mètodes en book_controller.rb. Segons el vostre requisit, podeu definir qualsevol quantitat de funcions en aquest fitxer.

Modifiqueu el fitxer per veure'l seguit i deseu els canvis. Tingueu en compte que us pertoca el nom que voleu donar a aquests mètodes, però és millor donar noms rellevants.

```ruby
class BookController < ApplicationController
   def list
   end

   def show
   end

   def new
   end

   def create
   end

   def edit
   end

   def update
   end

   def delete
   end

end
```

Ara implementarem tots els metods un per un.

# Implementant el mètode list

El mètode de llista us proporciona una llista de tots els llibres a la base de dades. Aquesta funcionalitat s'aconseguirà mitjançant les següents línies de codi. Editeu les línies següents al fitxer `book_controller.rb`.

```ruby
def list
    @books = Books.all
end
```

`@books = Book.all` en el mètode list li diu a Rails que busque llibres en la taula i en el magatzem en cada fila i cerque l'objecte instància `@books`.

# Implementant el mètode show

El mètode Show mostra només més detalls en un únic llibre. Aquesta funcionalitat s'aconseguirà mitjançant les següents línies de codi.

````ruby
def show
    @book = Book.find(params[:id])
end
```








Font: [Controladors](https://www.tutorialspoint.com/ruby-on-rails/rails-controllers.htm)
