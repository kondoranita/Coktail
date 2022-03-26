# „COCKTAILS” ANDROID ALKALMAZÁS

## 1. Alkalmazás célja

A TheCocktailDB (https://www.thecocktaildb.com/api.php) oldal által biztosított **Koktélok** - Android alkalmazásban történő – **megjelenítése**, a Themoviedb.org Rest API-hoz történő csatlakozásával.

A wikipedia szerint: _„A **koktél** olyan ital, melyet alkoholos italok és egyéb összetevők, például ízesített szirupok, gyümölcslé, szódavíz, tej, tejszín, méz, cukor és/vagy fűszernövények (például mentalevél) összekeverésével állítanak elő. Bár jobbára szeszes italt jelöl, léteznek alkoholmentes koktélok is. A koktél eredete nem tisztázott, és a nevének jelentéséről is számos elmélet született. A világ legnépszerűbb koktéljai közé tartozik a Piña Colada, a Bloody Mary, a Mai Tai, a Mojito, az Aperol Spritz, a Margarita, a Martini, a Manhattan, a Daiquiri, a Whiskey Sour vagy a Negroni. A legnépszerűbb koktélok listáját évek óta az Old Fashioned vezeti.”_

Az app a **finom italok/koktélok receptjeit jeleníti meg**, amelyek lépésről lépésre tartalmazzák az elkészítésüket. Minden recept:
* képpel, 
* összetevőkkel, 
* és részletes előkészítési utasításokkal rendelkezik, 
* továbbá az ital szervírozásához szükséges pohár javaslatot is tartalmaz;
így könnyedén elkészíthetőek az italok. Lehetőség van a kedvenc koktélok kiemelten történő kezelésére is.
Illetve új koktélok hozzáadásához a belső adatbázisba. 

## 2. Felhasználó által elérhető funkciók leírása

Az alkalmazás felhasználói felületét, annak megvalósítását az **alábbi UI vezérlők biztosítják**.
* alkalmazásunk UI mappájának szerkezete (add – hozzáadás, details – részletek, favorites – kedvencek, home – nyitóoldal, search – keresés almappák szerint):

![1](https://user-images.githubusercontent.com/83447486/160257424-f5c31955-176e-4267-9c20-bb25dc9b79ff.png)

### 2.1. Alkalmazás belépési pontja – 1 db Activity

Az alkalmazásunknak **egy - Activity példánnyal – biztosított belépési pontja** van. Komplex alkalmazások esetében már több felület megjelenítése célszerű, viszont jelen alkalmazásunk esetében ezt több Fragment-tel oldottuk meg. Az alkalmazásindítónkban megjelenő **egy Activity komponens** saját életciklussal rendelkezik, mely **biztosítja az ablakot: amiben a felhasználói felület megjelenítésre kerül** - jelen esetben a - teljes képernyő vertikális kitöltésével, mely tartalmaz:
* fragment konténert: ahol az alkalmazás 4 fő Fragmentje jelenik meg;
* továbbá alul egy alsó menüsávot: ahonnan elérhetősége biztosított a következő fő funkcióknak: főoldal, keresés, koktél/ital hozzáadás, kedvencek.

### 2.2. Főoldal – HomeFragment

![2](https://user-images.githubusercontent.com/83447486/160257425-17cdacea-fcac-4516-b126-08811551f804.png)

Nézet, **apiInterface, RetrofitClient, Drink meghívása, drinkList** létrehozása.
A **RecyclerView** és egy **for ciklus segítségével** megjelenítésre kerül itt a teljes koktél lista:
* a koktél képével 
* és megnevezésével.

**LoyoutManager** alkalmazásával sorba rakjuk a koktélokat, 2 oszlopban az alábbiak alkalmazásával:
![3](https://user-images.githubusercontent.com/83447486/160257427-2d0227ca-4f41-49b4-8108-1308f4f0dd82.png)

Egy adott koktélra kattintva az **alábbi Navigációs metódussal** Fragment váltásra kerül sor:
![4](https://user-images.githubusercontent.com/83447486/160257430-e51510aa-8c56-4cef-94cd-8ce345182dc2.png)

#### 2.2.1.DrinkDetailsFragment 
![5](https://user-images.githubusercontent.com/83447486/160257431-18ae5f35-e7d6-42d2-b642-68b9a7ecb7b8.png)

A koktél fényképén és megnevezésén túl itt **megjelenítésre kerülnek** - **TextView és ImageView alkalmazásával** - a koktélra vonatkozó következő információk: Kategória, Típus, Pohár, Elkészítés, Hozzávalók.

A koktél kép felületén található **FavoriteimageButton – szív ikon** - segítségével, az **alkalmazás adatbázisa** és az alábbi **Boolean függvény** alkalmazásával az **adott koktél kedvencek közé történő beszúrása valósulhat meg**:
![6](https://user-images.githubusercontent.com/83447486/160257432-b0737e57-89ae-4f66-a132-139974fdd8ec.png)

### 2.3. Keresés – SearchFragment
![7](https://user-images.githubusercontent.com/83447486/160257433-220bc9c4-2f4d-4d3d-bf14-94ca5ace64e6.png)

**Koktél név alapján történő keresés funkció** megvalósítása az alábbi boolean függvény alkalmazásával:
![8](https://user-images.githubusercontent.com/83447486/160257435-3b8a0479-404a-4329-af1e-7ebf9537c603.png)
 
Koktélra kattintva az **alábbi Navigációs metódussal** Fragment váltásra kerül sor:
![9](https://user-images.githubusercontent.com/83447486/160257436-9c100213-1cba-4df0-b0ba-093e2ae42531.png)
mely a **DrinkDetailsFragment-re** irányít.

![10](https://user-images.githubusercontent.com/83447486/160257437-34bba9ce-da6c-4bea-86bc-2324ebb895c6.png)

![11](https://user-images.githubusercontent.com/83447486/160257438-9cd10b0d-d87a-4bb6-a4ab-7e8f7b960920.png)

![12](https://user-images.githubusercontent.com/83447486/160257439-2fd6cad7-ccbb-416c-b88d-ee266a688e65.png)


#### 2.3.1.	DrinkDetailsFragment

Lásd. 2.2.1. pontban foglaltak.

### 2.4. Hozzáadás – AddFragment
![13](https://user-images.githubusercontent.com/83447486/160257440-cc8df788-bceb-42b2-a914-ba3fbb62da67.png)
![14](https://user-images.githubusercontent.com/83447486/160257441-adf29e79-2a64-4e2a-be84-b10752292620.png)


**Koktélok hozzáadás** funkció itt listáztatja ki a hozzáadott koktélokat, a jobb alsó sarokban található – úszó vagy repülő / **floatgomb** segítségével a **koktél hozzáadást** tudunk megvalósítani a gomb lenyomásával – AddCoctailsFragment - megjelenő adatlappal.
![15](https://user-images.githubusercontent.com/83447486/160257442-b19bd686-9640-4613-9b30-f76ee86630d0.png)


#### 2.4.1.	AddCoctailsFragment
![16](https://user-images.githubusercontent.com/83447486/160257443-926b2802-2845-4312-a590-45bea8758e47.png)

Az adatlap kitöltése céljából **string változók létrehozására került sor** a koktél Név, Kategória, Típus, Pohár, Hozzávaló, Mennyiség esetén.

Ahhoz, hogy **új koktélt hozzon létre** az adatbázisban szükséges minimum a név és egy hozzávaló megadása az alábbi függvény alkalmazásával:
![17](https://user-images.githubusercontent.com/83447486/160257444-61828080-0293-4664-b7a6-f7877dd2bd04.png)

**SaveNewRow** függvény elindítja az AppDatabas-t.
A fenti **Navigációs metódussal** Fragment váltásra kerül sor a mentés gombra történő kattintással, visszajutunk az AddFragment-hez.

![18](https://user-images.githubusercontent.com/83447486/160257445-8f80d069-8fb1-4f1c-835c-ad3e8bb506f8.png)

![19](https://user-images.githubusercontent.com/83447486/160257446-c3d1f6db-2cc4-48cb-a7b8-35534a5dca9c.png)

![20](https://user-images.githubusercontent.com/83447486/160257447-2f3ed88d-38a4-4cb1-b1e7-bfe0d7df8817.png)

![21](https://user-images.githubusercontent.com/83447486/160257415-751f2bc2-0488-446a-8db8-1ac768b4026e.png)



#### 2.4.2.	CoctailsDetailsFragment

![22](https://user-images.githubusercontent.com/83447486/160257416-37f46d87-8a56-4400-b169-449b420011a9.png)

Az AddFragment **Koktélok hozzáadás** funkciónál kilistázott koktélra kattintva jutunk ide, ahol koktél kép nélkül **TextView** segítségével megjelenítésre kerül a kategória, típus, pohár, hozzávalók, mennyiségek.

Ezen **koktél törlését is megtudjuk itt valósítani** az alábbiak alkalmazásával és az AddFragment-re történő lépéssel:
![23](https://user-images.githubusercontent.com/83447486/160257418-93292309-8f31-4b39-adbc-05705e3832ab.png)


### 2.5. Kedvencek – FavoriteFragment
![24](https://user-images.githubusercontent.com/83447486/160257420-dac36e03-adc4-41f3-90bc-fa68e5cc136b.png)

A Favorite Fragment tartalmazza a kedvencekbe berakott koktélokat.

A DrinkDetailsFragmentnél, a koktél kép felületén található **FavoriteimageButton – szív ikon** - segítségével, **FavoriteFragmentnél az adott koktél kedvencekbe történő besorolását tekinthetjük meg** az összes koktél szűrésével.

### 2.5.1. FavoritesDetailsFragment
![25](https://user-images.githubusercontent.com/83447486/160257422-294670f5-9af5-41fb-a54a-74eae33e2017.png)

A kilistázott koktélra kattintva megjelenítésre kerül a koktél képe, **TextView** segítségével pedig a kategória, típus, pohár, recept, hozzávalók, mennyiségek.

A koktél képen található - **kuka formájú - gomb/ikon megnyomásával törölhető** a koktél a kedvencekből.

## 3. Technológiák, projektre vonatkozó releváns információk

### 3.1. A következő technológiák, könyvtárak alkalmazására került sor:
* Retrofit,
* Android SDK,
* Git (verzióvezérlő rendszer)
* Room architecture compments 
* Glide

### 3.2. Projekt hierarchia:

![26](https://user-images.githubusercontent.com/83447486/160257423-330037c7-e5fe-4325-8648-978f37f03db4.png)

### 3.3. Alkalmazás azonosítója, verziószáma
* használt **SDK verziószám** (compileSdkVersion): **32**
* az alkalmazás **egyedi azonosító** (applicationId): **„com.larabel.coctails”**
* a **minimum API szint** (minSdkVersion): **27**
* az **alkalmazás verziószám** (versionCode): **1**

Az Android rendszerben meghatározott jogosultságokon kívül **saját jogosultság**, valamint az alkalmazás funkcionalitásához vagy megfelelő működéséhez **további szoftveres vagy hardveres erőforrás meghatározására nem került sor**.

## 4. Fejlesztési lehetőségek pl.:

### 4.1. Keresés – SearchFragment

Koktél név alapján történő **keresési funkció bővítése**: a Kategória, Típus, Pohár, Elkészítés, Hozzávalók stringek között.

### 4.2. CoctailsDetailsFragment

Az AddFragment **Koktélok hozzáadás** funkciónál kilistázott koktél esetén, ahol a koktél képpel történő megjelenítése.
