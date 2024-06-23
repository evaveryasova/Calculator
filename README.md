# Практика "Создание клиент-серверного приложения"

Сначала конфигурируем проект на https://start.spring.io/
![spring](https://github.com/evaveryasova/Calculator/blob/main/images/spring.png)

## _**Задание №1 - Создание контроллера**_

В папке src/main/java/ru/neoflex/practice создаю папку controller. В папке controller создаем файл CalcController.java
Над классом указываем аннотацию @RestController
Создаем два public метода с аннотациями @GetMapping("/plus/{a}/{b}") и @GetMapping("minus/{a}/{b}", которые принимают по два аргумента, типа Integer, а возвращают их сумму/разность. Перед каждым аргументом необходимо поставить @PathVariable.

```
package ru.neoflex.practice.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class CalcController {

    @GetMapping("/plus/{a}/{b}")
    public Integer plus (@PathVariable("a") Integer a, @PathVariable("b") Integer b){
        return a+b;
    }
    @GetMapping("/minus/{a}/{b}")
    public Integer minus (@PathVariable("a") Integer a, @PathVariable("b") Integer b){
        return a-b;
    }
}
```
Запускаем сервис, по зеленой кнопке сверху справа в окне Intellij IDEA <br>
Тестируем своё приложение по адресу http://localhost:8080/<адрес_и_параметры_для_2х_созданных_АПИ> <br>

Сложение
  ![plus](https://github.com/evaveryasova/Calculator/blob/main/images/plus.png)
  
Вычитание
  ![minus](https://github.com/evaveryasova/Calculator/blob/main/images/minus.png)

## _**Задание №2 - Подключение Swagger 3.0.0**_
Добавим в pom.xml зависимость

```
<dependency>
			<groupId>org.springdoc</groupId>
			<artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
			<version>3.0.0</version>
</dependency>
```
Тестируем своё приложение по адресу http://localhost:8080/swagger-ui/index.html
Результат ссылки
![Right](https://github.com/KseniyaVinevskaya/CalculatorJava/blob/main/images/image3.png)<br>
Сложение в swagger<br>
![Swork+](https://github.com/KseniyaVinevskaya/CalculatorJava/blob/main/images/image4.png)<br>
Вычитание в swagger<br>
![Swork-](https://github.com/KseniyaVinevskaya/CalculatorJava/blob/main/images/image5.png)<br>

1) Конфигурация проекта: 
2) Результат ссылки http://localhost:8080/plus/10/3: 
3) Результат ссылки http://localhost:8080/minus/10/3: 
4) Результат ссылки http://localhost:8080/swagger-ui/index.html: 
  1. https://github.com/evaveryasova/Calculator/blob/main/images/image1.png
  2. https://github.com/evaveryasova/Calculator/blob/main/images/image2.png
  3. https://github.com/evaveryasova/Calculator/blob/main/images/image3.png
  4. https://github.com/evaveryasova/Calculator/blob/main/images/image4.png
