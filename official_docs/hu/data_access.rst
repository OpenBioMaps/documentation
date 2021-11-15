Adatelérés
**********

Adatelérési lehetőségek
=======================

  * Fájl letöltés
    
      Támogatott formátumok: 
        
        - Egyszerű szöveges állományok: csv, json
        
        - Kép fájlok kivitele: egyesével, vagy tömegesen
        
        - Táblázatkezelő formátumok: ods (Libreoffice), xls (Excel), xlsx (Excel)
        
        - Térbeli formátumok: Esri shape (.shp, .dbf, .cpg, .prj, .shx együttesen), gpx (GPS adatformátum (xml)), sqlite
        

  * Webes lekérdezés
  
    - Szöveges szűréssel leválogatás
    
    - Térbeli lekérdezéssel leválogatás

  * Külső alkalmazások
    
    * API felület használata (pl.: R-csomag)
    
    * SQL kapcsolat használata (pl.: QGIS)


Adathozzáférés szabályozása
===========================

A projekt alapításakor meghatározott legalacsonybb színtű szabályozás a

local_vars.php.inc

fájlban van:

.. code-block:: php

   define('ACC_LEVEL','group'); // lehet az  értéke 'public' vagy 'login'
   define('MOD_LEVEL','group');


Amennyiben az adatmegtekintési/letöltési és módosítási szintek érteke "group", akkor további szabályozási lehetőségeink

_rules tábla használatával lesznek

A _rules táblánk egy-egy kapcsolatban van az minden szabályozni kívánt adattáblánkkal az obm_id - row_id idegenkulcs beállításával.
Azok az adatsorok amelyekre nincs _rules bejegyzés csak projekt gazdáknak érhető el (az ACC_LEVEL='group' esetén).

A _rules tábla működése a [projekt adminisztráció] -> [függvények] menüben található: [Hozzáférési szabályok elkészítése]

Itt lehet a trigger függvényt létrehozni és módosítani, illetve a triggert engedélyezni vagy letiltani ami minden rekord hozzáadás, módosítás és törlés után automatikusan frissíti a _rules táblánkat.

Az egyes adatsorok hozzáférése egyedileg is meghatározható amennyiben a csoport írás és olvasás mezőkben csoportokat adunk hozzá. Ezt a _rules trigger meg tudja automatikusan csinálni a feltöltő űrlapok adathozzárendelési beállítása alapján, amely értékek a system.uploadings táblában kerülnek beírásra a feltöltő űrlapok beállítása alapján.

A _rules tábla kézzel is újra generálható:
 - egyrészt egyszerre, csoportbeállítások nélkül:

.. code-block:: sql

   DELETE FROM abc_rules WHERE data_table='abc';
   INSERT INTO abc_rules (row_id,sensitivity,data_table) SELECT obm_id,'sensitive','abc' FROM abc
..

- vagy soronkénti csoportbeállítással is:

.. code-block:: sql

   DELETE FROM abc_rules WHERE data_table='abc';
   INSERT INTO abc_rules (row_id,sensitivity,data_table,read,write) 
      SELECT obm_id, 'sensitive', 'abc', s.group, s.owner 
      FROM abc a LEFT JOIN system.uploadings s ON (s.id = a.obm_uploading_id)

