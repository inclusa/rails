---
layout: post
title: 05 Bases de dades i migracions
date: 2017-06-05 dl 04:09
description: Bases de dades i migracions
keywords: database, migrations
coments: true
---

Rails 05 Bases de dades i migracions 				       :NOTE:

Per defecte obrim l'arxiu `config/database.yml` **Ruby on Rails** utilitza **sqlite**.

- `default:` => `adater: sqlite3`, utiliza esta base de datos.
- `development:` => `database: db/development.sqlite3`.
- `test:` => `database: db/test.sqlite3`.
- `production:` => `database: db/test.sqlite3`.

Cada vegada que executem el comandament `rake` las base de dades de `test` es ba a borrar. Aquesta és la raó per la qual **mai al nomenar de la mateixa forma totes les bases de dades**. Cada base de dades ha de tenir un nom diferent.

En cas de voler utilizar altra base de dades, per exemple, `mysql2` caldrà comentar la gema `gem 'sqlite3'` i escriure `gem 'mysql2'`. En cas de voler córrer-lo en **Heroku** caldrà posar `gem 'postgresql'`, ja que és la base de dades que utilitza.

Si finalment fem el canvi cal córrer aquest comandament `bundle install`.

Si es vol utilizar `msql2` cal canvia la configuració de l'arxiu  `config/database.yml`.

Configurem la base de dades per defecte, per a **mysql2**.

 ATENCIÓ: no canviar de la configuració a partir d'ací si el que volem és deixar convigurat `sqlite3`.

```
development:
  adapter: mysql2
  username: root
  password:
  host: localhost
  port: 3306
  database: blog
  pool: 5
  timeout: 5000
```

Ara iniciem el servidor per veure que no hi ha error:

```
rails s
```

Ens dóna un error perquè no hem creat la base de dades.

La creem amb el comandament:

```
rake db:create
```

Li anem a dir a Rails **sols vas a instal·lar sqlite3 quan tingues l'entorn de desenvolupament `test`**.

Per fer això cal anar a l'arxiu `Gemfile` i posar aquest codi en la abans de la línia on veiem la paraula group:

**Codi modificat per configurar `mysql2`**.

```
group: test do
  gem 'sqlite3'
end
```

Rails té tres entors:

- **test**: quan tenim tests automàtics per provar l'aplicació.
- **desenvolupament**: quan estem desenvolupant l'aplicació.
- **producció**: entorn real.

Tornem a alçar el server:

```
rails s
```

Esperem un error: `PendingMigrationError`, també ens diu com solucionar-ho.

Les migracions es troben a la carpeta `db/migrate/` allí trobarem un arxiu que començarà per la data en la qual s'ha fet la migració, on Ruby està creant la taula.

Quan hem vist tot això hem de tornar a `sqlite3`, aleshores borrarem el codi incorporat abans. Bàsicament no tocarem la configuració que ve per defecte.

### Les migracions

Les migracions són arxius que s'encarreguen de fer modificacions a la base de dades, ja siga agregar taules, crear camps, agregar index, borrar taules, borrar camps, etc., tot es fa a través de les migracions, no directament en la base de dades.

Les migracions es comporten com en una espècie de **pila**, una **pila** és una estructura en el què l'últim arxiu que agregues és el primer que traus.

Per executar la migració cal córrer el comandament:

```ruby
rake db:migrate
```

En aquest cas el que fa és crear el que està en el mètode `change` que serà crear la tabla `articles`.

Tornem a córrer el servidor:

```
rails s
```

Si actualitzem la pàgina no ens donen errades.

Així, ja està creada la base de dades.

Si ens equivoquem amb la taula o algun mètode existeix un comandament anomenat `rollback`:

```ruby
rake db:rollback
```

Aquest mètode fa l'invers del mètode `change_table`, que és `role_table`.

Caldria fer:

```ruby
rake db:up
rake db: migrate
```

Aquesta és la part que anomenàvem com una **pila**.

L'última migració que es va executar és l'última que es va a revertir quan nosaltres fem `rollback`. Seria com desfer o anar cap enrere en totes les migracions. Això ens permet fer canvis a la base de dades de manera molt sencilla.

Al mateix temps que passa això es crea un arxiu dins de la carpeta `db/migrate`, anomenat `schema.rb`. Aquest arxiu guarda l'esquema de la nostra base de dades.

Podem obrir la cònsola de Rails, és una cònsola especial on podem executar mètodes.

```ruby
rails console
```

Allí teclegem:

```ruby
irb(main):001:B> Article.all
```

Ens torna informació buida perquè no tenim cap artícle.

Font: [Código Facilito](http://codigofacilito.com/videos/bases_de_datos_y_migraciones_curso_ruby_on_rails_desde_cero)

