Adatfeltöltés munkafolyamat
***************************

Adatfeltöltési lehetőségek
==========================

  * Fájl feltöltés
    
      Támogatott formátumok: 
        
        - Egyszerű szöveges állományok: csv, dsv, tsv, json
        
        - Kép fájlok: jpg, tiff (Exif oszlopok kerülnek kiolvasásra)
        
        - Táblázatkezelő formátumok: ods (Libreoffice), xls (Excel), xlsx (Excel)
        
        - Térbeli formátumok: Esri shape (.shp, .dbf, .cpg, .prj, .shx együttesen), gpx (GPS adatformátum (xml)), sqlite
        
        - Genetikai adatfájlok: fasta
      
      Bármilyen itt felsorolt fájl importálható URL cím megadasával is (egyszerű GET lekérdezés)  
        

  * Webes űrlap

  * Külső alkalmazások
    
    * API felület használata (pl.: mobil alkalmazás, R-csomag)
    
    * SQL kapcsolat használata (pl.: QGIS)


Adat exportálás a feltöltési folyamatból
========================================

Az adatfeltöltési folyamat során és a megszakított feltöltések elmentett állapotából lehetőség van az adatok kiexportálására egy CSV fájlba.

Adatfeltöltés megszakítása
==========================

Az adatfeltöltés folyamatát a webes felületen bármikor meg lehet szakítani. Két percenként automatikusan mentés készül, de feleső menü sávban található mentés gombbal bármikor készíthetünk mentést. 

Az elmenett feltöltések a profil oldalon található "felfüggesztett adatfeltöltések" listából kiválasztva visszatölthetőek.

A befejezett feltöltések a listából autómatikusan kitörlődnek.
