---
layout: post
title: 03 Erb i assets
date: 2017-06-02 dv 21:27
description: Extensió i carpeta de recursos
keywords: erb assets
coments: true
---

Partim de l'arxiu `app/views/welcome/index.html.erb` on hem direccionat l'inici de Rails.

El nom de l'arxiu és `index.html.erb` amb aquesta extensió `.erb`, la qual l'ha colocat Rails per defecte.

El que ofereix aquesta extensió és accés a Ruby dins de la vista, `view`.

### Etiquetes ####

`<%  %>` aquesta serveix per a imprimir coses.
`<%=  %>` aquesta avalua el codi i l'imprimeix dins de la pàgina web.

Exemple:

```ruby
<% [1,2,3,4].each do |number| %>
    <p>Número: <%= number%></p>
<%end%>
```

Output

```
Número: 1

Número: 2

Número: 3

Número: 4
```

Això seria com un cicle `for` en altres llenguatges.

Si ara incorporem un `=` al principi de la llista:

```ruby
<%= [1,2,3,4].each do |number| %>
    <p>Número: <%= number%></p>
<%end%>
```

Output

```
Número: 1

Número: 2

Número: 3

Número: 4

[1, 2, 3, 4] 
```

No sols imprimeix la les iteracions sinó també la llista.

A més podem fer altres operacions:

```ruby
<%= [1,2,3,4].each do |number| %>
    <p>Número: <%= number * 2 %></p>
<%end%>
```

Output

```
Número: 2

Número: 4

Número: 6

Número: 8
```

Ací podem posar tot el que siga vàlid en Ruby.

```ruby
<%= [1,2,3,4].each do |number| %>
    <p>Número: <%= number * 2 %></p>
<%end%>
<% mundo = "Uriel" %>
<%= "Hola #{mundo}" %>
```

Output

```
Número: 2

Número: 4

Número: 6

Número: 8

Hola Uriel 
```

Tots els recursos van a la carpeta `app/assets`. En la carpeta `app/assets/stylesheets` cal posar tots els arxius d'estils necessaris.

Ruby col·loca dins l'arxiu `applications.css` una sentència anomenada `require_tree`, la qual va a afegir totes les fulles d'estil que trobe a la carpeta `stylesheets`.

Per això anem la web [http://flexboxgrid.com/](http://flexboxgrid.com/) i baixem aquest full d'estils. El guardem a la carpeta `app/assets/stylesheets/` amb el nom `flexboxgrid.css`.

