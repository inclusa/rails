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

```ruby
def show
    @book = Book.find(params[:id])
end
```
El mètode `show` de `@book = Book.findparams[:id]` crida **Rails** per buscar un sol llibre el qual té definit l'`ìd`en els `params[:id]`.

Els paràmetres objecte estan continguts en eixes

Els paràmetres objete són un contenidor que permet passar valors entre trucades de mètode. Per exemple, quan es troba a la pàgina anomenada pel mètode de la llista, podeu fer clic a un enllaç per a un llibre específic i passar l'`id`  d'aquest llibre a través de l'objecte params perquè el programa pugui trobar el llibre específic.

# Implementant el nou mètode

El nou mètode permet a Rails saber que crearà un nou objecte. Per tant, afegiu el codi següent en aquest mètode.

```ruby
def new
    @book = Book.new
    @subjects = Subjects.all
end
```

El mètode anterior es dirà quan mostrarà una pàgina a l'usuari per fer-se càrrec de l'usuari. Aquí la segona línia agafa tots els temes de la base de dades i els posa en una matriu anomenada `@subjects`.

# Implementant el mètode creat

Un cop hagueu introduït l'usuari amb un formulari HTML, és hora de crear un registre a la base de dades. Per aconseguir-ho, editeu el mètode create a `book_controller.rb` per fer coincidir el següent:

```ruby
def create
   @book = Book.new(book_params)

   if @book.save
      redirect_to :action => 'list'
   else
      @subjects = Subject.all
      render :action => 'new'
   end

end

def book_params
   params.require(:books).permit(:title, :price, :subject_id, :description)
end
```

La primera línia crea una nova variable d'instància anomenada `@book` que conté un objecte `Book` construït a partir de les dades, l'usuari ha enviat. El mètode `book_params` s'utilitza per recollir tots els camps de l'objecte `:books`. Les dades es van passar del nou mètode per crear l'ús dels paràmetres de l'objecte.

La següent línia és una instrucció condicional que redirigeix l'usuari al mètode de llista si l'objecte es guarda correctament a la base de dades. Si no es guarda, l'usuari s'envia de nou al nou mètode. El mètode `redirect_to` és similar a realitzar una actualització meta en una pàgina web: automàticament us envia a la vostra destinació sense cap interacció de l'usuari.

A continuació, `@subjects = Subject.all` és obligatori en cas que no deseu dades amb èxit i esdevingui un cas semblant a l'opció nova.

# Implementant el mètode update

Aquest mètode es crida després del mètode d'edició, quan l'usuari modifica les dades i vol actualitzar els canvis a la base de dades. El mètode d'actualització és similar al mètode de creació i s'utilitzarà per actualitzar llibres existents a la base de dades.

```ruby
def update
   @book = Book.find(params[:id])

   if @book.update_attributes(book_param)
      redirect_to :action => 'show', :id => @book
   else
      @subjects = Subject.all
      render :action => 'edit'
   end

end

def book_param
   params.require(:book).permit(:title, :price, :subject_id, :description)
end
```

El mètode `update_attributes` és similar al mètode guardat usat per crear, però en lloc de crear una nova fila a la base de dades, sobreescriu els atributs de la fila existent.

A continuació, `@subjects = Subject.all` és necessària la línia en cas que no guardi correctament les dades, es torna similar a l'opció d'edició.

# Implementant el mètode delete

Si voleu eliminar un registre de la base de dades, usareu aquest mètode. Implementeu aquest mètode de la manera següent.

```ruby
def delete
   Book.find(params[:id]).destroy
   redirect_to :action => 'list'
end
```

La primera línia troba la classificació basada en el paràmetre passat a través dels paràmetres de l'objecte i, a continuació, el suprimeix utilitzant el mètode de destrucció. La segona línia redirigeix l'usuari al mètode de la llista usant una trucada redirigida.

# Mètodes adicionals per visualizar Subjects

Assumeixi que voleu proporcionar una facilitat als seus usuaris per explorar tots els llibres en funció d'un tema determinat. Per tant, podeu crear un mètode dins de `book_controller.rb` per mostrar tots els temes. Assumeixi que el nom del mètode és `show_subjects`.

```ruby
def show_subjects
   @subject = Subject.find(params[:id])
end
```

Finalment l'arxiu `book_controller.rb` es vorà així:

```ruby
class BooksController < ApplicationController

   def list
      @books = Book.all
   end

   def show
      @book = Book.find(params[:id])
   end
  
   def new
      @book = Book.new
      @subjects = Subject.all
   end

   def book_params
      params.require(:books).permit(:title, :price, :subject_id, :description)
   end

   def create
      @book = Book.new(book_params)

      if @book.save
         redirect_to :action => 'list'
      else
         @subjects = Subject.all
         render :action => 'new'
      end
   end
   
   def edit
      @book = Book.find(params[:id])
      @subjects = Subject.all
   end
   
   def book_param
      params.require(:book).permit(:title, :price, :subject_id, :description)
   end
   
   def update
      @book = Book.find(params[:id])
      
      if @book.update_attributes(book_param)
         redirect_to :action => 'show', :id => @book
      else
         @subjects = Subject.all
         render :action => 'edit'
      end
   end
   
   def delete
      Book.find(params[:id]).destroy
      redirect_to :action => 'list'
   end
   
   def show_subjects
      @subject = Subject.find(params[:id])
   end

end
```



Font: [Controladors](https://www.tutorialspoint.com/ruby-on-rails/rails-controllers.htm)
