SAMSON Hospital — мобильное рабочее место врача для legacy-МИС
О конфиденциальности
SAMSON Hospital — внутреннее медицинское приложение для работы в закрытом контуре. В публичном репозитории размещены только обезличенные материалы портфолио и техническая документация. Исходный production-код, учетные данные, реальные данные пациентов и параметры развертывания не публикуются.

SAMSON Hospital — Android-приложение для врачей стационара, интегрированное с действующей настольной медицинской информационной системой. Основная задача проекта — перенести ключевые клинические сценарии на мобильное устройство без изменения базовой схемы БД МИС.
Реализованные сценарии
- работа со списком пациентов отделения;
- создание и просмотр дневников;
- локальные офлайн-черновики дневников;
- просмотр анализов и создание направлений;
- диагностика и направления на исследования;
- лечение и листы назначений;
- клинические мероприятия и документы;
- динамические формы, формируемые из метаданных МИС.
Моя роль на проекте
Full-cycle разработка:
- Android-клиент на Kotlin / Jetpack Compose;
- Django REST API;
- анализ legacy-схемы MySQL / MariaDB;
- динамическое построение форм по ActionType / ActionPropertyType;
- совместимая запись в структуры существующей МИС;
- UX/UI для работы врача на планшете и телефоне;
- локальное хранение черновиков и пользовательского состояния на устройстве;
- диагностика интеграции, логирование и отладка;
- пользовательская и developer-документация.
Архитектура
```mermaid
flowchart LR
    A[Android\nKotlin + Jetpack Compose]
    B[Django REST API\nинтеграционный адаптер]
    C[(Legacy MIS\nMySQL / MariaDB)]
    D[Внутренние файловые сервисы]
    E[(Память устройства\nчерновики + UI state)]

    A <-->|REST / JSON| B
    B <--> C
    B <--> D
    A <--> E
```
Главный архитектурный принцип: мобильное приложение не создает отдельную медицинскую модель данных и не меняет базовую схему МИС. Backend интерпретирует существующие метаданные и формирует стабильный REST-контракт для Android-клиента.
UX/UI и офлайн
Интерфейс проектировался под рабочие сценарии медицинского учреждения:
- Material 3 и Jetpack Compose;
- работа на планшетах и телефонах;
- настройка темы и размера текста;
- компактная навигация вокруг пациента;
- локальные шаблоны и избранное;
- сохранение черновиков дневников в памяти устройства;
- продолжение работы с черновиком после восстановления соединения.
Скриншоты
Все изображения обезличены.
<img width="311" height="656" alt="image" src="https://github.com/user-attachments/assets/969d76d0-cbd8-4681-b7d0-4037f44d66b1" />
Основное меню приложения
<img width="296" height="644" alt="image" src="https://github.com/user-attachments/assets/1d04713d-a98e-4bf7-aa64-22f33693d40a" />
Меню пациента	
<img width="296" height="440" alt="image" src="https://github.com/user-attachments/assets/1a1df48b-b784-44ed-9d27-948ee87f8f45" />
Типы дневников и локальные черновики
<img width="296" height="328" alt="image" src="https://github.com/user-attachments/assets/86175baf-c4da-4faf-b4ff-454a91b972cf" />	
Динамическая форма дневника	
<img width="298" height="438" alt="image" src="https://github.com/user-attachments/assets/b9a45639-b76f-42be-9dd9-5d4414cf5dfe" />
<img width="298" height="438" alt="image" src="https://github.com/user-attachments/assets/57d1e4b6-55cd-476d-abff-a840dedb26fd" />
Результаты лабораторных исследований
<img width="294" height="451" alt="image" src="https://github.com/user-attachments/assets/24ce3887-62dd-4907-9444-e5bdb8ee2455" />
История диагностики
<img width="298" height="361" alt="image" src="https://github.com/user-attachments/assets/1821dfcd-4b34-443c-9506-7dbb5a7811a5" />
Лечение и назначения
<img width="290" height="531" alt="image" src="https://github.com/user-attachments/assets/fc80b403-4584-4083-ba2d-97f6eb9dd9c5" />
Клинические мероприятия
<img width="256" height="463" alt="image" src="https://github.com/user-attachments/assets/dcaded92-5533-4ad7-94b6-18a9287abe17" />
Динамическое разделение полей направления и результата

При создании направления приложение разрешает ввод параметров, относящихся к назначению, и отдельно блокирует поля, которые должны заполняться только после выполнения исследования.
Стек
- Android: Kotlin, Jetpack Compose, Material 3, Navigation Compose, Retrofit, OkHttp, Coroutines, JVM 17
- Backend: Python, Django, Django REST Framework, REST/JSON
- БД: MySQL / MariaDB
- Инфраструктура: CentOS, RED OS, Astra Linux
- Инструменты: Git, Postman, Insomnia
Документы
- [Презентация проекта (PDF)](docs/SAMSON_Hospital_Portfolio_2026.pdf)
- [Презентация проекта (PPTX)](docs/SAMSON_Hospital_Portfolio_2026.pptx)
- [Инструкция пользователя](docs/SAMSON_Hospital_User_Guide_2026.docx)
- [Developer Guide (DOCX)](docs/SAMSON_Hospital_Developer_Guide_2026.docx)
- [Developer Guide (Markdown)](docs/SAMSON_Hospital_Developer_Guide_2026.md)
Состав публичного репозитория
Репозиторий предназначен для портфолио и демонстрирует архитектуру, UX/UI, интеграционные решения и техническую документацию проекта. Production-код и медицинские данные не публикуются.
