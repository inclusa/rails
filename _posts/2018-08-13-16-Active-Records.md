---
layout: post # Sustituye el layout si lo usas uno diferente
title: 16 Active Records # Nombre generado automáticamente
---

**Rais Active Record** és un **Object/Relational Mapping (ORM)**, és una capa de relació. Relaciona:

- Mapes de taules amb classes.
- Mapes de files amb objectes.
- Mapes de columes amb atributs d'objectes.

Ruby és el programa que manipula la base de dades. El mètode Ruby genera automàticament camps de noms de la base de dades.

Cada objecte de l'**Active Record** és un **CRUD** (Create - Read - Update - Delete) mètode d'accés per a la base de dades. Esta estragegia permet dissenys simples per enviar simples mapes entre les taules de la base de dades i els objectes d'aplicacions.

# Transladant a Model de Domini dins d'SQL

Traduir un model de domini a SQL és generalment senzill, sempre que recordeu que heu d'escriure SQL compatible amb Rails. En termes pràctics, heu de seguir certes regles:

- Cada entitat (com ara llibre) obté una taula a la base de dades que porta el nom, però en plural (llibres).
- Cada taula de coincidència d'entitats d'aquest tipus té un camp anomenat id, que conté un enter únic per a cada registre inserit a la taula.
- Entitat entitat x i entitat y, si l'entitat pertany a l'entitat x, llavors la taula y té un camp anomenat x_id.
- La major part dels camps de qualsevol taula emmagatzemen els valors de les propietats simples d'aquesta entitat (qualsevol cosa que sigui un número o una cadena).

# Creant Arxius Active Record (Models)

Per a crear l'arxiu **Active Record** per a les nostres entitats per a l'aplicació de llibreria, introduirem aquest dos models `Book` i `Subject`:

```ruby
rails g model Book
rails g model Subject
```

Així, comptem que el generador crearà models anomenats `Book` i `Subject` en la pila d'instància de `books` i `subjects`. Els crearà començant per **majúscula** i usant la forma **singular**. Aquest és el paradigma que seguirà Rails cada vegada per a crear el model.

Quan utilitzeu l'eina de generació, Rails crea un model d'arxiu que manté tots els mètodes únics del model i a les regles que defineix, un fitxer de prova de la unitat per a dur a terme un desenvolupment basat en proves, un fitxer de dades d'exemple (anomenat fixtures) que s'utilitzarà amb les proves unitàries i una migració de Rails que facilita la creació de taules i columnes de bases de dades.

A banda de crear molts altres arxius i directoris, aquest crearà uns arxius anomenats **book.rb** i **subject.rb**, els quals contenen un esquelet definit en el directori **app/models**.

El contingut dels arxius és el següent:

book.rb

```ruby
class Book < ActiveRecord::Base
end
```


```ruby
class Subject < ActiveRecord::Base
end
```

# Creant Associacions entre Models

Quan tens més d'un model en les teues aplicacions de Rails, necessitaràs crear connexions entre aquests models. Pots fer això via associacions. **Active Record** suporta tres tipus d'associacions:

- **Un-a-Un**: Existeix una relació d'un a un quan un element té exactament un d'un altre element. Per exemple, una persona té exactament un aniversari o un gos té exactament un propietari.
- **un-a-molts**: Existeix una relació d'un a un quan un sol objecte pot ser membre de molts altres objectes. Per exemple, un tema pot tenir molts llibres.
- **Molts-a-Molts**: Existeix una relació de molts a molts quan el primer objecte està relacionat amb un o més d'un segon objecte i el segon objecte està relacionat amb un o molts dels primers objectes.

Indicarem estes associacions afegint declaracions a estos models:

- **has_one**: té un
- **has_many**: té molts
- **belongs_to**: pertany a
- **has_and_belongs_to_many**: una pertany a molts

Ara, necessites dir Rails que quines relacions vols establir entre la llibreria del dades del sistema. Per fer-ho cal modificar `book.rb` i `subject.rb` així:

```ruby
class Book < ActiveRecord::Base
    belongs_to :subject
end
```

Hem d'usar el nom en **singular** (Book), perquè `Book` pot pertànyer a un isol `subject`.

```ruby
class Subject < ActiveRecord::Base
    belongs_to :books
end
```

Hem utilitzat el **plural** perquè una `Subject` pot tenir múltiples `books`.

# Implementant Validacions sobre Models

La implementació de validacions es fa en un model Rails. Les dades estan dins de la base de dades que està definida en el actual model Rails, de manera que només té sentit definir quines dades vàlides impliquen a la mateixa ubicació.

Les validacions són:

- El valor del camp de `títol` **no hauria de ser NULL**.
- El valor del camp del `format` ha de ser **numèric**.

Cal obir `book.rb` en el subdirectori `app/model` i establir les validacions:

```ruby
class Book < ActiveRecord::Base
   belongs_to :subject
   validates_presence_of :title
   validates_numericality_of :price, :message=>"Error Message"
end
```

Explicació:

- `validates_presence_of`: protegeix els camps `NOT NULL` contra l'entrada de l'usuari que falta.
- `validates_numericality_of`: impedeix que l'usuari introduisca dades no-numèriques.`

Font: [ActiveRedord](https://www.tutorialspoint.com/ruby-on-rails/rails-active-records.htm)
