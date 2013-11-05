Systemutviklerskolen - Design Patterns workshopoppgaver C#

Oppsett
	� Ha installert Visual Studio 2012
	� Ha installert NuGet-extension
	
Ressurser
	� Visual studio prosjekt: <path>
	� A developer's guide to Dependency Injection using Unity 3 - http://msdn.microsoft.com/en-us/library/dn170416.aspx
	
Case
	Du er en del av et team som skal lage et kursh�ndteringssystem som en Windows Console Application. Dere har g�tt for en lagdelt struktur med Application (front-end), Business (forretningslogikk), Domain (domeneentiteter) og Data (dataaksess) som lag. Du har ansvaret for Application-, Business og Domain-lagene mens din kollega, Ola, har ansvaret for Data-laget. Dataaksess er planlagt � skje via en database men dere har ikke helt klart for dere noe db-skjema enn�. 
	
	Dere har v�rt igjennom en t�ff dag i g�r hvor deler av l�sningen ble raskt prototypet til en kundedemo p� neste fredag.
	
	Oppgave 1
	
		Det er dag 2 i prosjektet og prototypingen dere har gjort i g�r kveld skal omskrives til � implementere IoC med Dependency Injection (DI).
	
		a. Installer Unity via NuGet (pakkenavn: "Unity")
		b. Konfigurer Unity til � resolve IKursFactory til KursFactory
			i. Hint:
				1) var unityContainer = new UnityContainer();
				2) unityContainer.RegisterType<(IClassContract), (ConcreteType)>();
				3) var minKlasseInstans = unityContainer.Resolve<IClassContract>();
		
	Oppgave 2
	
		Det er dagen f�r demo. Datahenting foreg�r ved bruk av "repositories" i Data-laget. Alle "repositories" implementerer et interface som er kontrakten for operasjoner mot en datakilde. Kontrakten for kursrepository er IKursRepository.
		
		Ola p� teamet som er ansvarlig for databaseinteraksjon skal lage en klasse for henting av kurs kalt KursRepositorySql, men det ser ikke ut som om han rekker demofristen i morgen og du kommer ikke videre med utviklingen. P� demoen m� det vises en fungerende prototype av systemet, med data! 
		
		a. Implementer KursRespositoryFake slik at dere f�r vist data i applikasjonen.
			i. Hint:
				1) Bruk "private List<Kurs>" slik at du kan fake en databasetabell for kursene.
		b. Bruk DI og Unity til � sette opp IKursRepository til � resolve til KursRepositoryFake. Repositoryklassen som blir resolvet av Unity skal bli brukt som en "Singleton" av applikasjonen.
			i. Hint: L�r mer om Lifetime Managers her: http://msdn.microsoft.com/en-us/library/ff647854.aspx
			
			
	Oppgave 3
	
		Dere begynne � f� kontroll til demoen men f�ler at dere savner � forst� hva som skjer til hvilken tid i applikasjonen, og i hvilken rekkef�lge ting skjer. Derfor �nsker dere � implementere Trace-logging i metodekall. Dette finner dere ut kan gj�res ved hjelp av Interceptors i Unity. 
		
		a. Implementer LoggingInterceptionBehavior-klassen p� alle typene som er registrert i Unity-containeren
			i. Hint:
				1) NuGet-pakkenavn: "Unity.Interception"
			ii. Trace-output i Debug-vinduet i Visual Studio skal v�re p� formatet: 
				? Kaller metode <returtype> <metodenavn> - kl. <tid>
				og
				? Metode <returtype> <metodenavn> returnerte <returverdi> - kl. <tid>
