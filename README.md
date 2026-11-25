# oop-workshop
OOP Projekt 1. semester (Øvelsesprojekt)


### Krav

### Funktionelle krav
#### Indhold
Programmet skal understøtte
- E-Books
- Movies
- Songs
- Video-games
- Apps
- Podcasts
- Images

For hver type skal programmet gemme metadata

#### Udlån
Brugere skal kunne låne alle typer af medie i biblioteket
Brugere som har lånt mediet skal kunne give en bedømmelse

#### Brugere
Der skal forskellige typer af brugere
- Borrower
- Employee
- Admin
Ved opstart skal programmet bede om at man angiver hvilken bruger man er
Programmet skal gemme oplysninger om navn, alder, cpr nummer. 

I første omgang er verificering ikke nødvendigt, men programmet skal bare spørge om hvilken brugertype personen er.


Borrower:
Skal kunne interergere med samlingen af medier ved at liste items efter type, vælge og se detaljer om item, rate item og udføre de aktioner som høre til det medie de vælger

Employee:
Skal kunne administrere samlingen ved at tilføje eller fjerne medie

Admin:
Skal have alle rettigheder som employee, men kan også manage, borrowers og emplyees. Manegement dækker viewing, creating, deleting og updating personlig information om brugere

### Ikke funktionelle krav

Systemet skal designes så det kan udvides med nye medietyper og lign uden stort besvær

Ugyldige handlinger må ikke kunne crashe programmet

Det skal være konsolbaseret der guider brugeren tydeligt


### 2. Verb noun analyse af programspecifikation

| Navneord                                                                                                 | Udsagnsord                                                                                                                      |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **E-books**<br><br>Title<br>Author<br>Language<br>Number of pages<br>Year of publication<br>ISBN<br><br> | View<br>Download<br>Read                                                                                                        |
| **Movies**<br><br>Title<br>Director<br>Genres<br>Release year<br>Language<br>Duration                    | Watch<br>Download                                                                                                               |
| **Songs**<br><br>Title<br>Composer<br>Singer<br>Genre<br>File type<br>Duration<br>Language               | Play<br>download                                                                                                                |
| **Video-games**<br><br>Title<br>Genre<br>Publisher<br>Release year<br>Supported platforms                | Download<br>Play<br>Complete                                                                                                    |
| **Apps**<br><br>Title<br>Version<br>Publisher<br>Supported platforms<br>File Size<br>                    | Download<br>Execute                                                                                                             |
| **Podcasts**<br><br>Title<br>Release year<br>Hosts<br>Guests<br>Episode number<br>Language               | Download<br>Listen<br>Complete                                                                                                  |
| **Images**<br><br>Title<br>Resolution<br>File format<br>File Size<br>Date taken                          | Download<br>Display<br>                                                                                                         |
| **Users**<br><br>Name<br>Age<br>CPR<br>                                                                  | Borrow<br><br>**If borrowed:**<br>Rate item                                                                                     |
| **Borrower**                                                                                             | Sort by type<br>Select media<br>View Media details<br>Rating items<br>Perform action for each type                              |
| **Emplyee**                                                                                              | Add item<br>Remove Item                                                                                                         |
| **Admin**                                                                                                | Add item<br>Remove item<br><br>Manage borrowers and employees:<br>View, Create, Delete and Update Personal information of users |
| **Collection**                                                                                           |                                                                                                                                 |


### 3. CRC kort som matcher verb noun analyse og krav

| Class      | Responsabilities                                                                                 | Collaborators                                          |
| ---------- | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------ |
| Media      | Titel<br>Review<br>Borrowed<br><br>Download<br>Borrow<br>Rate<br><br>                            | IDownloadable<br>IRateable<br>IBorrowable<br>IViewable |
| EBook      | Author<br>Language<br>Number of pages<br>Year of publication<br>ISBN<br><br>View<br>Read<br>     | Media<br>IReadable                                     |
| Borrower   | <br><br>Sort<br>Select<br>View<br>Perform action                                                 | User<br><br>Collection<br>                             |
| User       | Name<br>Age<br>CPR<br><br>Borrow<br>Rate                                                         | Media<br><br>                                          |
| Collection | List of media<br>List of users<br><br>Sort<br>Borrow<br>Add<br>Remove                            | User<br>Media                                          |
| Employee   | <br>Add<br>Remove                                                                                | User<br><br>Collection                                 |
| Admin      | <br>Manage                                                                                       | Employee<br>User<br><br>Collection<br>Employee<br>User |
| Movie      | Title<br>Director<br>Genres<br>Release year<br>Language<br>Duration<br><br>Watch<br>             | Media<br>IWatchable                                    |
| Song       | Title<br>Composer<br>Singer<br>Genre<br>File type<br>Duration<br>Language<br><br>Play<br>        | IPlayable<br>Media                                     |
| Video-game | Title<br>Genre<br>Publisher<br>Release year<br>Supported platforms<br><br>Play<br>Complete       | IPlayable<br>ICompleteable<br>Media                    |
| App        | Title<br>Version<br>Publisher<br>Supported platforms<br>File Size<br><br>Execute                 | IExecuteable<br>Media                                  |
| Podcast    | Title<br>Release year<br>Hosts<br>Guests<br>Episode number<br>Language<br><br>Listen<br>Complete | IListenable<br>ICompleteable<br>Media                  |
| Image      | Title<br>Resolution<br>File format<br>File Size<br>Date taken<br><br>View                        | IViewable<br>Media                                     |

#### Interfaces

| Name          | Methods  |
| ------------- | -------- |
| IPlayable     | play     |
| IDownloadable | download |
| IRateable     | rate     |
| IReadable     | read     |
| IWatchable    | watch    |
| ICompletable  | complete |
| IExecutable   | execute  |
| IViewable     | view     |
| IBorrowable   | borrow   |
| IListenable   | listen   |


### 4. UML diagram

```mermaid
classDiagram

class Media {
	<<abstract>>
		+string title
		+double review
		+bool isBorrowed
		
		+Download() void
		+Borrow() void
		+Rate(int rating) void
		+View() void
}

class User {
	<<abstract>>
		+string name
		+int age
		+string CPR
		
		+Borrow(Media media) void
		+Rate(int rating) void
}

class Borrower {
		+Sort() void
		+Select(Media media) void
		+View(Media media) void
		+PerformAction() void
}

class Employee {
		+Add(Media media) void
		+Remove(Media media) void
}

class Admin {
		+View() void
		+Create() void
		+Delete() void
		
		+UpdatePersonalInfo() void
}

class Collection {
		+List ~Media~ mediaList
		+List ~User~ userList
		+Sort() void
		+Borrow() void
		+Add(Media media) void
		+Remove(Media media) void
}

class EBook {
		+string auther
		+string language
		+int numberOfPages
		+int yearOfPublication
		+string ISBN
		
		+View() void
		+Read() void
}

class Movie {
		+string director
		+string genre
		+int releaseYear
		+string language
		+double duration
		
		+Watch() void
}

class Song {
		+string composer
		+string singer
		+string genre
		+string filetype
		+double duration
		+string language
		
		+Play() void
}

class VideoGame {
		+string genre
		+string publisher
		+int releaseYear
		+string supportedPlatforms
		
		+Play() void
		+Complete() void
}

class App {
		+string version
		+string publisher
		+string suppoortedPlatforms
		+double fileSize
		
		+Execute() void
}

class Podcast {
		+int releaseYear
		+string hosts
		+string guests
		+int episodeNumber
		+string language
		
		+Listen() void
		+Complete() void
}

class Image {
		+string resolution
		+string fileFormat
		+double fileSize
		+DateTime dateTaken
		
		+View() void
}


class IPlayable {
		<<interface>>
		+Play() void
}

class IDownloadable { 
		<<interface>>
		+Download() void
}

class IRateable {
		<<interface>>
		+Rate(int rating) void
}

class IReadable {
		<<interface>>
		+Read() void
}

class IWatchable {
		<<interface>>
		+Watch() void
}

class ICompleteable {
		<<interface>>
		+Complete() void
}

class IExecutable {
		<<interface>>
		+Excecute() void
}

class IViewable {
		<<interface>>
		+View() void
}

class IBorrowable {
		<<interface>>
		+Borrow() void
}

class IListenable {
		<<interface>>
		+Listen() void
}


Media<|--EBook
Media<|--Movie
Media<|--Song
Media<|--VideoGame
Media<|--App
Media<|--Podcast
Media<|--Image
Media<--Collection

User<|--Borrower
User<|--Employee
Employee<|--Admin

IDownloadable<|..Media
IRateable<|..Media
IBorrowable<|..Media
IViewable<|..Media
IReadable<|..EBook
IWatchable<|..Movie
IPlayable<|..Song
IPlayable<|..VideoGame
ICompleteable<|..VideoGame
IExecutable<|..App
IListenable<|..Podcast
ICompleteable<|..Podcast
IViewable<|..Image


```





