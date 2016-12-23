# Az OpenBioMaps Gekko kiadás telepítése és első indítása (Windows 10 Pro 64bit)


## Fő lépések:

1. Telepítsd a Virtualbox aktuális kiadását.
2. Telepítsd a kiegészítő csomagot, és végezd el a szükséges beállításokat.
3. Importáljad a letöltött virtuális gépet.
4. Indítsd el a Gekko kiadást és jelentkezz be.

A [VirtualBox](http://virtualbox.org/) egy ingyenesen használható virtuális számítógép, amely Linux, OS X és Windows gépeken is futtatható. Ennek a szoftvernek a segítségével tudod elindítani az OBM Gekko kiadását.

A [VirtualBox](http://download.virtualbox.org/virtualbox/5.1.4/VirtualBox-5.1.4-110228-Win.exe) és a telepítés után szükséges [kiegészítő
csomag](http://download.virtualbox.org/virtualbox/5.1.4/Oracle_VM_VirtualBox_Extension_Pack-5.1.4-110228.vbox-extpack) a [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads) oldalról tölthető le.

Letöltés után indítsd el a telepítőcsomagot, amely egy varázsló segítségével vezet végig a telepítési folyamaton:
![alt text][fig1]
![alt text][fig2]
![alt text][fig3]

Kiválaszthatod, hogy akarsz-e az Asztalon, illetve a Gyorsindító eszköztárban parancsikont elhelyezni, illetve fájltársításokat állíthatsz be.
![alt text][fig4]

A telepítő figyelmeztet, hogy a hálózati kapcsolatod a telepítés folyamán meg fog szakadni.
Amennyiben a hálózaton keresztül végzel valamilyen tevékenységet, fejezd azt be, mentsd el a munkádat.
![alt text][fig5]
![alt text][fig6]
![alt text][fig7]
![alt text][fig8]

Az USB eszközszoftvert is telepítsd!
![alt text][fig9]

A telepítés befejezése után indítsd el a VirtualBoxot, a kiegészítő csomag telepítéséhez és a beállításokhoz.
![alt text][fig10]

A főablakban először ez a kép fogad.
![alt text][fig11]

A fájl menüben válaszd ki a Beállítások menüpontot (Ctrl+G)
![alt text][fig12]

Válaszd a Kiterjesztők lapot, és nyisd meg a letöltött kiterjesztőcsomagot a Megnyitás gombra kattintva.
![alt text][fig13]

Navigáljunk a letöltött csomagra, valami hasonlót fogsz látni. Nyisd meg ezt a csomagot.
![alt text][fig14]

A Telepítés gombra kattintva indítsd el a folyamatot.
![alt text][fig15]

A folyamat elindításához el kell fogadni a licensz megállapodást.
![alt text][fig16]

A folyamat elindul.
![alt text][fig17]

Ha szerencsésen végigfutott a telepítés, a végén az OK gombra kattintva visszatérsz a Beállításokhoz, ahol a Kiterjesztők lapon láthatod, hogy aktív az Extension Pack.
Ezután a hálózati adaptereket kell beállítani azért, hogy a virtuális gép megfelelően működhessen. Ehhez a Hálózati és megosztási központ Adapterbeállításihoz kell eljutnod.
![alt text][fig18]

A Rendszertálca hálózat ikonján jobb egérgombra kattintva felugrik a fenti menü, ahonnan a Hálózati és megosztási központot kell megnyitnod.
![alt text][fig19]

Itt az ablak bal oldalán fent találod az Adapterbeállításokat.
![alt text][fig20]

Jobb egérgombbal kattints a Virtualbox Host-Only Network ikonra, és nyisd meg a Tulajdonságok menüpontot.
![alt text][fig21]

A VirtualBox NDIS6 Bridged Networking Driver elem elől vedd ki, majd rakd vissza a pipát (ha nem volt benne a pipa, rakd be)!
Ezután lépj ki a VirtualBox alkalmazásból, mentsd el minden munkádat, és indítsd újra a számítógépet!
Újraindítás után importálnod kell a letöltött virtuális gépet! A Gekko legújabb kiadást
a [http://openbiomaps.org/downloads/virtual-image/](http://openbiomaps.org/downloads/virtual-image/) oldalon találod meg.
![alt text][fig22]

A virtuális gép importálásához a VirtulaBox elindítása után a Fájl menü Gép importálása (Ctrl + I) menüpontot kell kiválasztanod!
![alt text][fig23]

A fenti ablakban a Megnyitás gombra kattintva navigálj a letöltött OpenBioMaps.ova nevű fájlra és fogadd el azt!
![alt text][fig24]

A felbukkanó ablakban láthatod az importálni kívánt gép tulajdonságait. Kattints az Importálás gombra.
![alt text][fig25]
![alt text][fig26]

A pár perces folyamat végén, ha az sikeres, indíthatod majd az OpenBioMaps virtuális szervert.
![alt text][fig27]

Az indításhoz a VirtualBox főablakban jelöld ki a gépet és kattints a Start gombra. Ha a rendszerünk elindult egy ilyen konzol kép fog fogadni bennünket a VirtualBox ablakban:
![alt text][fig28]

A sikeres importálás és beállítások elvégzése után a gazda gépen (Windows) létrejön egy virtuális hálózati csatoló a 192.168.56.1 ip címmel. Ezt egy két gépes hálózatként kell elképzelni ami virtuális gépünkben a 192.168.56.101 címet kapja, azaz a gazdagép felől ezen utóbbi címen lehet elérni a Gekko-t.   A z OBM gekko webes felületet a gazdagépen futó böngészőből a  [http://192.168.56.101/biomaps/projects/template/](http://192.168.56.101/biomaps/projects/template/) címen érheted el. Itt kezdheted el a munkát a saját OpenBioMaps szervereden!
További hálózati elérési lehetőség az SSH használata. Windows alatt például a [putty](http://www.putty.org) alkalmazás használható erre. SSH-val a gekko@192.168.56.101 címet kell megadni a gazdagépen a Gekko eléréséhez.
A Gekko Debian Linux rendszerbe bejelentkezve az adatbázis és az OBM rendszer működésének mélyebb rétegeit érheted el. Ezekről a lehetőségekről olvasd el fejlesztői és kezelői dokumentációkat, ill. a Debian Linux, Apache2, Mapserver és PostgreSQL kézikönyveket.
A postgresql adatbázis kezeléséhez telepítettük a phppgadmin webes postgresql kliens programot. Ezt a [http://192.168.56.101/phppgadmin](http://192.168.56.101/phppgadmin) címen tudod elérni. A gisadmin felhasználó rendszergazdai joggal rendelkezik. Ezzel a felhasználóval bejelentkezve lehet alapvető beállításokat módosítani.

A szükséges felhasználónevek és jelszavak az első használathoz:
Webes felületen történő bejelentkezés:
felhasználónév: gekko@openbiomaps.org	jelszó: 12345

PostgreSQL
felhasználónév: gisadmin		  jelszó: FeZaiw4e
felhasználónév:biomapsadmin		jelszó: De8Eilu6
felhasználónév:template_admin	jelszó: MaeS2dai

OBM vendég (Debian Linux) operációs rendszer
felhasználónév: gekko	  jelszó: gekko
felhasználónév: root		jelszó: gekko

Ha nem csak saját magad használod a rendszered, 
a jelszavakat változtasd meg!!!

További információkat a rendszer konfigurálásáról itt találhatsz:
http://openbiomaps.org/obwiki

A dokumentációt Ferenc Attila (ferenca@bnpi.hu) készítette 2016. augusztus 26-án. 

Módosítások:
Bán Miklós (banm@vocs.unideb.hu) 2016.augusztus 27, december.23.


[fig1]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig1.png
[fig2]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig2.png
[fig3]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig3.png
[fig4]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig4.png
[fig5]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig5.png
[fig6]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig6.png
[fig7]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig7.png
[fig8]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig8.png
[fig9]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig9.png
[fig10]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig10.png
[fig11]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig11.png
[fig12]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig12.png
[fig13]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig13.png
[fig14]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig14.png
[fig15]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig15.png
[fig16]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig16.png
[fig17]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig17.png
[fig18]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig18.png
[fig19]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig19.png
[fig20]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig20.png
[fig21]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig21.png
[fig22]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig22.png
[fig23]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig23.png
[fig24]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig24.png
[fig25]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig25.png
[fig26]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig26.png
[fig27]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig27.png
[fig28]: https://github.com/OpenBioMaps/documentation/blob/master/images/fig28.png
