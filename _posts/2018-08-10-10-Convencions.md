---
layout: post # Sustituye el layout si lo usas uno diferente
title: 10 Convencions # Nombre generado automáticamente
---

És important tenir en compte les convencions.

- Model - Singular amb CamelCase
- Tabla - Plural amb underscores

|------|--------|
Model/Class | Table/Schema
Article | articles
LineItem | line_items
Deer | deers
Moues | mice
Person | people

- Primary keys: per defecte la columna id
- Foreign keys: singularized_table_name_id

Atributs opcionals:

- created_at: data en la qual va ser creada
- update_at: data de l'última actualització de l'element

Font: [Curs de Ruby](https://www.youtube.com/watch?v=DcS0gAosMck)

