# Modèle de la base de données de CML

1. Tale role

```
CREATE TABLE role (
    id SERIAL PRIMARY KEY,
    role_name VARCHAR(100) NOT NULL,
    create_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    update_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

```

2. Table members

```
CREATE TABLE members (
id SERIAL PRIMARY KEY,
name VARCHAR(100) NOT NULL,
first_name VARCHAR(100) NOT NULL,
email VARCHAR(150) NOT NULL UNIQUE,
password VARCHAR(255) NOT NULL,
phone_number BIGINT NOT NULL,
address TEXT,
role_id INT REFERENCES role(id) ON DELETE SET NULL,
create_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
update_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

```

3. Table location

```
CREATE TABLE location (
id SERIAL PRIMARY KEY,                 -- Identifiant unique auto-incrémenté
location_name VARCHAR(100) NOT NULL,   -- Nom de l'emplacement
description TEXT,                      -- Description de l'emplacement
create_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,   -- Date de création
update_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP    -- Date de mise à jour
);
```

4. Table materials

```
CREATE TABLE materials (
id SERIAL PRIMARY KEY,                 -- Identifiant unique auto-incrémenté
material_name VARCHAR(100) NOT NULL,   -- Nom du matériel
first_name VARCHAR(100),               -- Prénom associé (si applicable)
description TEXT,                      -- Description du matériel
status VARCHAR(50),                    -- Statut du matériel (ex. : "Disponible", "En maintenance")
value DECIMAL(10, 2),                  -- Valeur du matériel
location_id INT REFERENCES location(id) ON DELETE SET NULL, -- Référence vers l'emplacement
member_id INT REFERENCES members(id) ON DELETE SET NULL,    -- Référence vers le membre responsable
date_enter DATE,                       -- Date d'entrée du matériel
date_out DATE,                         -- Date de sortie (si applicable)
create_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, -- Date de création
update_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP  -- Date de mise à jour
);

```

5. Table mouvement_type

```
CREATE TABLE mouvement_type (
id SERIAL PRIMARY KEY,
mouvement_type_name VARCHAR(50) NOT NULL,
description TEXT,
create_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, -- Date de création
update_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP  -- Date de mise à jour
);

```

6. Table mouvement_material

```

CREATE TABLE material_mouvement (
id SERIAL PRIMARY KEY, -- Identifiant unique auto-incrémenté
material_id INT REFERENCES materials(id) ON DELETE CASCADE, -- Matériel déplacé
location_origin_id INT REFERENCES location(id) ON DELETE SET NULL, -- Emplacement d'origine
location_destination_id INT REFERENCES location(id) ON DELETE SET NULL, -- Emplacement de destination
mouvement_type_id INT REFERENCES mouvement_type(id) ON DELETE SET NULL, -- Type de mouvement (ex : "Entrée", "Sortie")
mouvement_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP, -- Date du mouvement
comment TEXT, -- Commentaires supplémentaires
member_id INT REFERENCES members(id) ON DELETE SET NULL, -- Membre responsable du mouvement
create_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, -- Date de création
update_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP -- Date de mise à jour
);

```

7. Table maintenance

```

CREATE TABLE maintenance (
id SERIAL PRIMARY KEY, -- Identifiant unique auto-incrémenté
material_id INT REFERENCES materials(id) ON DELETE CASCADE, -- Référence au matériel concerné
description TEXT, -- Description de la maintenance
cost DECIMAL(10, 2), -- Coût de la maintenance
member_id INT REFERENCES members(id) ON DELETE SET NULL, -- Référence au membre responsable
date TIMESTAMP DEFAULT CURRENT_TIMESTAMP, -- Date de la maintenance
create_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, -- Date de création
update_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP -- Date de mise à jour
);

```

8. Table cult_program

```

CREATE TABLE cult_program (
id SERIAL PRIMARY KEY, -- Identifiant unique auto-incrémenté
day VARCHAR(20) NOT NULL, -- Jour du programme (par exemple, "Dimanche")
hour TIME NOT NULL, -- Heure du programme
create_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, -- Date de création
update_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP -- Date de mise à jour
);

```
