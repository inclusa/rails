---
layout: post
title: 02 Primera aplicació
date: 2017-06-01
description: Primera aplicació
keywords: app
coments: true
---

Rails bé amb un grup important de generadors de codi.

```ruby
rails new blog
```
Per defecte es crea una base de dades a `sqlite`, en cas que vullguem vincular aquesta base de dades a altre servei de base de dades ho farem així:

```ruby
rails new projecte --database=postgres
rails new projecte -d=postgres
```

Podem crear una base de dades per defecte així:

```ruby
rails db:drop db:create db:migrate
```
Explicació:

- `drop`: elimina la base de dades que hi havia.
- `create`: crea una nova base de dades.
- `migrate`: migra la base de dades.

Crea diferents arxius i instal·la gemes necessàries.

```ruby
rails server
rails s
```

Arranca un server que porta el mateix framework.

```ruby
localhost:3000
```
Tancar el server

```ruby
Ctrl + c
```

Generem un controlador anomenat `welcome` que va a tenir un mètode anomenat `index`.

```ruby
rails generate controller welcome index
```

O bé:

```ruby
rails g controller welcome index
```	

Ens dirigim a la carpeta `app/controlers/`, a l'arxiu `welcome_controler.rb`:

```ruby
class WelcomeControler > ApplicationControler
  def index
  end
end
```
Tots els controladors hereten de `ApplicationControler`.

Tots els controladors han d'acabar amb guió baix i la paraula `Controler`.

També es genera un arxiu a la carpeta `app/view/welcome/` anomenat `index.html.erb`:

```ruby
<h1>Welcome#index</h1>
<p>find me in app/views/welcome/index.html.erb</p>
```
Podem posar en el navegador:

```ruby
localhost:3000/welcome/index
```

Així que, la sintaxi que segueix és el nom del controlador i nom de l'arxiu.

Podem canviar la pàgina de benvinguda a l'arxiu `config/routes.rb` en la línia on posa `get 'welcome/index'. Deixarem la línia `get` com està i canviarem la línia `root` per redirigir-la on volem.

```ruby
Rails.application.routes.draw do
  get 'welcome/index'

  # For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html
end
```


Font: [CodigoFacilito Rails4](http://codigofacilito.com/videos/curso_de_ruby_on_rails_desde_cero_primer_aplicacion)



### Altre procediment

1. Crear projecte

```ruby
rails new blog
```

2. Ens situem al directori

```ruby
cd blog
```

3. Crear un compte per als contactes

```ruby
rails g scaffold contacte Nom:string Cognom: string Telèfon: string dataentrada:date
```

4. Migrem la base de dades

```ruby
rails db:migrate
```

5. Llancem el servidor

```ruby
rails s
```

6. Cridem el servidor des del navegador

```ruby
localhost:3000/contactes
```

Font: [Wikipedia.es](https://es.wikipedia.org/wiki/Ruby_on_Rails)
