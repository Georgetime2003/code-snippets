#### Connexió a una SGBD MySQL
Codi molt simple per veure les funcions bàsiques de connexió a un SGBD MySQL i  realitzar les operacioins d'INSERT i SELECT 
Els exemples estan contextualitzats a la BD rrhh.

**INSERT**
```python

import mysql.connector
import datetime

cnx = mysql.connector.connect(host='127.0.0.1',user='usuari',password='paraulapas', database='rrhh')
cursor = cnx.cursor()

avui = datetime.datetime.now().date()
#dema = datetime.now().date() + timedelta(days=1)
#date(1977, 6, 14)

stm_insert_empleat = ("INSERT INTO empleats "
            "(empleat_id, nom,cognoms,email,data_contractacio,feina_codi,salari) "
            "VALUES (%s, %s, %s, %s, %s, %s, %s)")
dades_empleat = (500,'Geert', 'Vanderkelen','gvanderkelen@sapalomera.cat', tomorrow, 'IT_PROG',77.99)

# Executem l'INSERT
cursor.execute(insert_empleat, data_employee)
# Si la taula tenia un valor autoincremental aquest es pot recollir mitjançant lastrowid o _last_insert_id.
empleat_id = cursor.lastrowid    
print(cursor._last_insert_id)

# Ens assegurem de realitzar un commit a la BD
cnx.commit()
#allibarem recursos
cursor.close()
cnx.close()
```

**SELECT/QUERY**
```python

import mysql.connector
import datetime

cnx = mysql.connector.connect(host='127.0.0.1',user='usuari',password='paraulapas', database='rrhh')
cursor = cnx.cursor()

query = ("SELECT empleat_id,nom,cognoms,data_contractacio 
         "   FROM empleats "
         "WHERE data_contractacio BETWEEN %s AND %s")

inici = datetime.date(1990, 1, 1)
fi = datetime.date(2016, 12, 31)

cursor.execute(query, (inici, fi))

for (e_id, e_nom, e_cognoms, e_data_contractacio) in cursor:
    print("{} - {}, {} va ser contractat el {:%d %b %Y}".format(e_id,e_nom,e_cognoms,e_data_contractacio))

cursor.close()
cnx.close()
    
```
