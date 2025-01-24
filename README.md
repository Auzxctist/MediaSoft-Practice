# MediaSoft-Practice
Выполнил Алексей Калентьев ИСдо-34
# Задание 3
- https://www.figma.com/design/cmewuQ6vDBKLCwMbqNLAU0/%D0%9F%D1%80%D0%BE%D1%82%D0%BE%D1%82%D0%B8%D0%BF?node-id=0-1&p=f&t=JVcTN6DZHxrVYUkO-0
# Задание 4
# Основной сценарий:
1. Пользователь выбирает заказ из списка своих заказов.
2. Интерфейс открывает экран редактирования заказа, где отображаются:
- Список товаров, добавленных в заказ.
- Возможность изменения количества каждого товара.
- Общая сумма заказа.
3. Пользователь может:
- Добавить новые товары (открывается общий каталог).
- Удалить товары из заказа.
- Изменить количество товаров.
4. После изменений пользователь нажимает кнопку "Сохранить", и обновленные данные отправляются на сервер.
5. Сервер обновляет данные заказа в базе и возвращает подтверждение успешного обновления.
6. Пользователь видит уведомление об успешном обновлении.
  
# Исключительные сценарии:
1. Если товар недоступен для добавления, пользователь получает сообщение: "Товар недоступен для заказа."
2. Если сервер недоступен, пользователь получает сообщение: "Произошла ошибка. Попробуйте позже."

# Задание 5
1. Вывести покупателей с количеством осуществленных покупок -
SELECT 
    Покупатели.Имя, 
    Покупатели.Фамилия, 
    COUNT(Покупки.Идентификатор) AS Количество_покупок
FROM 
    Покупатели
LEFT JOIN 
    Покупки 
ON 
    Покупатели.Идентификатор = Покупки.Ключ_покупателя
GROUP BY 
    Покупатели.Идентификатор, 
    Покупатели.Имя, 
    Покупатели.Фамилия;
   
2. Общая стоимость товаров для каждого покупателя, отсортированная в порядке убывания -
SELECT 
    Покупатели.Имя, 
    Покупатели.Фамилия, 
    SUM(Покупки.Сумма) AS Общая_стоимость
FROM 
    Покупатели
LEFT JOIN 
    Покупки 
ON 
    Покупатели.Идентификатор = Покупки.Ключ_покупателя
GROUP BY 
    Покупатели.Идентификатор, 
    Покупатели.Имя, 
    Покупатели.Фамилия
ORDER BY 
    Общая_стоимость DESC;

3. Получить покупателей, купивших только один товар -
SELECT 
    Покупатели.Имя, 
    Покупатели.Фамилия
FROM 
    Покупатели
JOIN 
    Покупки 
ON 
    Покупатели.Идентификатор = Покупки.Ключ_покупателя
GROUP BY 
    Покупатели.Идентификатор, 
    Покупатели.Имя, 
    Покупатели.Фамилия
HAVING 
    COUNT(Покупки.Идентификатор) = 1;
