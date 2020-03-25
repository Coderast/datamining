***URL***: https://www.kaggle.com/jessemostipak/hotel-booking-demand

## Описание:
Датасет представляет из себя данные о бронировке курортных и городских отелей с 2015 по 2017 года.

##### Есть следующие поля у записей (всего их 32):
* hotel - тип отеля - уникальных 2: Resort Hotel, City Hotel
* is_canceled - заказ был отменён - уникальных 2: 0(нет), 1(да)
* lead_time - время между бронировкой и прибытием в днях - int
* arrival_date_year, arrival_date_mounth, arrival_date_week_number, arrival_date_day_of_month - дата прибытия (год, месяц, номер недели, день месяца) При том месяц - строка
* adults - количество взрослых в номере
* children - количество детей в номере
* babies - количество грудничков в номере
* stays_in_weekend_nights - количество выходных в таймфрейме бронирования
* stays_in_week_nights - количество будних в таймфрейме бронирования
* meal - тип питания, SC,Undefined = не включено
* country - страна отеля
* market_segment - сегмент рынка
* distribution_channel - способ бронирования
* is_repeated_guest - от гостя, который ранее уже заказывал
* previous_cancellations - количество отменённых броней до того как гость остановился на данном выборе
* previous_bookings_not_canceled - количество не отменённых броней до того как гость остановился на данном выборе
* reserved_room_type - код типа комнаты, который был зарезервирован
* assigned_room_type - код типа комнаты, который в итоге был назначен
* booking_changes - количество исправления в брони после её публикации
* deposit_type - тип депозита - уникальных 3: No Deposit - нет депозита, Non Refund - есть депозит без возврата, Refundable - депозит с возвратом
* agent - ID агентства, через которое сделано бронирование
* company - ID компании, которая сделала бронирование
* days_in_waiting_list - количество дней бронирования между его созданием со стороны гостя и принятием со стороны отеля
* customer_type - тип гостя - уникальных 4: Contract, Transient, Transient-party, Group
* adr - коэфициент представляющий собой отношение суммы всех заявок на проживание к общему количеству ночей проживания
* required_car_parking_spaces - количество парковочных мест запрошенных гостем
* total_of_special_requests - количество дополнительных требования от гостя
* reservation_status - актуальный статус брони - уникальных 3: Canceled - закрыт пользователем, Check-Out - клиент был, но уже выселился, No-Show - клиент не зарегестрировался, но объяснил причину
* reservation_status_date - дата последнего изменения статуса

### Формулировка задачи:
Обучить модель, которая получая на вход данные сможет определять категорию того будет ли заказ отменён или нет.
Для тестовой выборки будут отброшены поля is_canceled и reservation_status

В ходе анализа данных для их подготовки поля были выделены в следующие группы:
#####  Оставить как есть:
hotel - 0/1
is_canceled - 0/1
lead_time - int
arrival_date_year - int
arrival_date_week_number - int
arrival_date_day_of_month - int
adults - int
children - int - 0.003% пропусков заменим на mean
babies - int
stays_in_weekend_nights - int
stays_in_week_nights - int
is_repeated_guest - 0/1
previous_cancellations - int
previous_bookings_not_canceled - int
booking_changes - int
days_in_waiting_list - int
adr - float
required_car_parking_spaces - int
total_of_special_requests - int
##### Заменить на число:
arrival_date_mounth - сохраняем порядок месяцев
meal - есть чёткая линейная градация от худшего к лучшему
deposit_type - аналогично с meal
##### Заменить на категорию (dummy кодирование):
country - 0.4% пропусков - заменим на mean
market_segment
distribution_channel
reserved_room_type (мы ничего не знаем о порядке типов комнат)
assigned_room_type (мы ничего не знаем о порядке типов комнат)
customer_type
reservation_status
##### Удалить:
agent - 333 unique на 103 050 - более 14% пропусков
company - более 94% пропусков
##### Другие преобразования:
reservation_status_date - записано в виде строки в формате YYYY-MM-DD, преобразуем в три int поля:
    reservation_status_date_year
    reservation_status_date_month
    reservation_status_date_day_of_month
