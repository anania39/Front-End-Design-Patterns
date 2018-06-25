# დიზაინ პატერნები და მათი გამოყენება

##### როგორ ვწეროთ უკეთესი კოდი დიზაინ პატერნების დახმარებით

_Bachelors thesis in Computer Sciences. Supervisor: Nino Kiviladze_

## <a name='TOC'>სარჩევი</a>

1.  [რეზიუმე](#abstract)
1.  [შესავალი](#introduction)
1.  [თავი 1: ლიტერატურის მიმოხილვა](#literature_review)
    - [მიმოხილვა](#review_1)
    - [დიზაინ პატერნების სიტორია](#history)
    - [რა არის პატერნი?](#what_is_pattern)
    - [ჩვენ ყოველდღე ვიყენებთ პატერნებს](#everyday_pattern)
    - [Proto-პატერნების ისტორია და "3 წესი"](#proto_patterns)
    - [დიზაინ პატერნების სტრუქტურა](#pattern_structure)
    - [ანტი პატერნები](#anti_patterns)
    - [დიზაინ პატერნების კატეგორიები](#pattern_categories)
      - [Creational კატეგორიის დიზაინ პატერნები](#creational)
      - [Structural კატეგორიის დიზაინ პატერნები](#structural)
      - [Behavioral კატეგორიის დიზაინ პატერნები](#behavioral)
1.  [თავი 2: დიზაინ პატერნები რეალურ პროგრამირებაში](#patterns_in_real)
    - [მიმოხილვა](#review_2)
    - [Round-Trip ინჟინერია VS Single-Page აპლიკაციები](#round_trip_vs_spa)
      - [Round-Trip ინჟინერია](#round_trip_engineering)
      - [Single-Page აპლიკაციები](#spa)
      - [როგორ მუშაობს SPA?](#how_spa_works)
1.  [თავი 3: დიზაინ პატერნები ფრონტ-ენდ ინჟინერიაში](#patterns_in_front_end)
    - [მიმოხილვა](#review_3)
    - [Front-End Framework-ები და დიზაინ პატერნები](#front_end_frameworks)
      - [Angular 2+ დიზაინ პატერნები](#angular_patterns)
    - [Javascript დიზაინ პატერნები](#javascript_patterns)
      - [Constructor პატერნი](#constructor_pattern)
      - [Module პატერნი](#module_pattern)
      - [Singleton პატერნი](#singleton_pattern)
      - [Observer პატერნი](#cobserver_pattern)
      - [Facade პატერნი](#facade_pattern)
      - [Decorator პატერნი](#decorator_pattern)
1.  [შეჯამება](#summarize)

## <a name='abstract'>რეზიუმე</a>

პროგრამირება სულ უფრო და უფრო პოპულარული და მოთხოვნადი ხდება დროთა განმავლობაში. ეს უმეტესწილად განპირობებული არსებული ტექნიკის დამოკიდებულებაზე კომპიუტერულ მეცნიერებასა და პროგრამირებაზე ამან რა თქმა უნდა დახვეწა მიდგომები და სტანდარტები კონკრეტულ პროგრამირების ენებში.

დღესდღეობით პროგრამირება არ მოიცავს ერთი ადამიანის ჩართულობას, პირიქით ერთ პროექტზე შესაძლებელია ათობით და ასობით პროგრამისტი მუშაობდეს. ხოლო პროექტის ჯანსაღი განვითარებისთვის საჭიროა პროგრამისტები მუშაობდნენ ერთად შემუშავებული სტანდარტებით და ნებისმიერი სახის პროგრამულ უზრუნველყოფაზე ჰქონდეთ ისეთი გამოსავალი, რომელიც შემდგომში ხელს არ შეუშლის ახალი ფუნქციონალის დამატებას.

ასევე, ნებისმიერი პროგრამული უზრუნველყოფის შექმნისას, აუცილებელია სწორი და ჩამოყალიბებული არქიტექტურის შემუშავება, რომელიც პროდუქტს გახდის უფრო მოქნილს, გამოყენებადს და გამართულს შემდგომი განვითარებისთვის.

## <a name='introduction'>შესავალი</a>

ამ თეზისში შეფასებული იქნება დიზაინ პატერნები კონკრეტული პროგრამული ენებიდან ასევე ამ პატერნების პრაქტიკული ღირებულება ობიექტზე ორიენტირებულ გარემოში. ასევე განხილული იქნება რა გავლენას ახდენს ე.წ. “Gang of Four(GOF)”-ის სახელით ცნობილი დიზაინ პატერნები ჯავასკრიპტის ერთ-ერთ თანამედროვე ფრეიმვორკზე - Angular-ზე. კვლევა ფოკუსირებული იქნება დიზაინ პატერნების გამოყენების უპირატესობების გამოვლენაზე და ამა თუ იმ პროგრამული ენის მახასიათებლებთან დიზაინ პატერნების შესაძლო კომბინაციების აღმოჩენაზე.

შემდეგი თავი დეტალურად აღწერს პრობლემის არსს და ასევე ნაშრომის მიზანს.

**Problem Statement**

პროგრამირების დროს საკმაოდ რთულია დაიცვა სტანდარტები და წერო ისე, რომ კოდი ყველასათვის გასაგები იყოს. ან თუნდაც შეიმუშავო პრობლემის გადაჭრის ისეთი ხერხი, რომ მან ხელი შეუშალოს და შეაფერხოს ახალი ფუნქციონალის ჩამატება. ამ დროს ხდება ისეთი გამოსავლის მოძებნა, რომელიც არც თუ ისე მართებული და საზოგადოდ მიღებულია.

ნაშრომის მიზანია გამოვიკვლიოთ ზემოთ არსებული პრობლემის მოგვარების ოპტიმალური და საუკეთესო გზა. კერძოდ, განვიხილოთ მიდგომა, რომელსაც Design Patterns ჰქვია. იგი გვთავაზობს საზოგადოდ შექმნილ და არსებულ პრობლემებზე საუკეთესო გამოსავალს და სწორ მიმართულებას. ამასთანავე ნაშრომში განხილულია თანამედროვე და მოწინავე პროგრამული ბიბლიოთეკები და ფრეიმვორკები, რომლებიც მასიურად იყენებენ ამ მიდგომას და ჩაშლილია დეტალურად თითოეული დიზაინ პატერნი, რომელიც გამოყენებულია ამ ბიბლიოთეკებსა თუ პროგრამულ ენებში.

## <a name='literature_review'>თავი 1: ლიტერატურის მიმოხილვა</a>

### <a name='review_1'>მიმოხილვა</a>

ნაშრომის ამ თავში განხილული იქნება “დიზაინ პატერნების” მნიშვნელობა, მისი შემუშავებისა და გამოყენების ისტორია, ასევე უფრო დეტალურად იქნება მოწოდებული თუ რა არის ის უფრო დეტალურად და რას გულისხმობს მისი გამოყენება

### <a name='history'>დიზაინ პატერნების ისტორია</a>

ერთ-ერთი უმნიშვნელოვანესი ასპექტი მართვადი კოდის(maintainable code) წერისა არის ის, რომ შენიშნო განმეორებადი თემები(recurring themes) კოდში და დააოპტიმიზირო ისინი. ეს არის ის სფერო, სადაც დიზაინ პატერნებს შეუძლია დაამტკიცოს მისი ფასდაუდებლობა.

დიზაინ პატერნებს შეგვიძლია მივაკვლიოთ ადრეულ წარსულში მოღვაწე არქიტექტორის - ქრისტოფერ ალექსანდერის(Christopher Alexander) ნამუშევრებში. ის ხშირად წერდა პუბლიკაციებს მისი გამოცდილების შესახებ დიზაინის საკითხების გადაწყვეტაში და როგორ უკავშირდებოდნენ ისინი შენობებსა და ქალაქებს. ერთ დღეს მან აღმოაჩინა, რომ რაც უფრო და უფრო მეტ დროს უთმობდა დიზაინებზე მუშაობას, გარკვეული დიზაინის კონსტრუქციები აშკარა ოპტიმალური ეფექტისკენ მიყავდა.

სარა იშიკასთან(Sara Ishikawa) და მიურეი სილვერსტთან(Murray Silverstein) თანამშრომლობით ალექსანდრემ წარმოადგინა პატერნის(შაბლონის) ენა, რომელიც დაეხმარებოდა ნებისმიერ მსურველს, ვისაც სურდა შეექმნა ნებისმიერი მასშტაბების დიზაინი არქიტექტურაში. იგი წიგნად გამოვიდა 1977 წელს სახელით “A Pattern Language”.

დაახლოებით 30 წლის წინ პროგრამული უზრუნველყოფის ინჟინრებმა(software engineers) დაიწყეს იმ პრინციპების გათვალისწინება და ხმარება, რაც ალექსანდერმა დაწერა თავის პირველ დოკუმენტაციაში დიზაინ პატერნებთან დაკავშირებით,რომელიც უნდა ყოფილიყო სახელმძღვანელო დამწყები დეველოპერებისთვის, რომელთაც სურდათ განევითარებინათ თავიანთი კოდის წერის უნარები.

მნიშვნელოვანია აღინიშნოს, რომ დიზაინის ნიმუშების მიღმა არსებული კონცეფციები პრაქტიკულად შემოფარგლული იყო პროგრამირების ინდუსტრიაში მისივე დასაწყისიდან,თუმცა ნაკლებად ფორმალური ფორმით.

ერთ-ერთი პირველი და ალბათ ყველაზე ღირებული წიგნი, რომელიც დიზაინ პატერნებზე დაიბეჭდა, იყო 1995 წელს დაწერილი წიგნი სახელად “Design Patterns: Elements Of Reusable Object-Oriented Software”. იგი დაწერა 4-მა მეცნიერმა: Erich Gamma, Richard Helm, Ralph Johnson და John Vlissides-მა, რომლებიც ცნობილი გახდნენ როგორც “Gang of Four (GoF)”, რაც ქართულად ითარგმნება როგორც “ოთხთა ბანდა”.

GoF-ის პუბლიკაცია დღემდე ძლიერ ინსტრუმენტად ითვლება დიზაინ პატერნების კონცეფციის ღრმად ჩამოყალიბებასა და დიდი რაოდენობიით დეველოპმენტის ტექნიკისა და პრობლემების აღწერით. ასევე იგი გვთავაზობს საზოგადოდ გავრცელებულ 23 ობიექტზე-ორიენტირებული დიზაინ პატერნის დეტალურ აღწერას. ამ ნაშრომის შემდგომ თავებში უფრო დეტალურად იქნება განხილული ზემოთ ხსენებული დიზაინ პატერნების ძირითადი წარმომადგენლები.
