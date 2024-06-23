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
![Right](https://github.com/evaveryasova/Calculator/blob/main/images/right.png)

Сложение в swagger
![Swork+](https://github.com/evaveryasova/Calculator/blob/main/images/image1.png)
![Swork+](https://github.com/evaveryasova/Calculator/blob/main/images/image2.png)

Вычитание в swagger
![Swork-]( https://github.com/evaveryasova/Calculator/blob/main/images/image3.png)
![Swork-](https://github.com/evaveryasova/Calculator/blob/main/images/image4.png)

## _**Задание №3 - Создание тестов**_

Изменения в pom.xml

```
<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
		<!-- Swagger Dependency-->
		<dependency>
			<groupId>org.springdoc</groupId>
			<artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
			<version>2.0.2</version>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-test</artifactId>
		</dependency>
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-test-autoconfigure</artifactId>
		</dependency>
		<dependency>
			<groupId>org.testng</groupId>
			<artifactId>testng</artifactId>
			<version>RELEASE</version>
			<scope>compile</scope>
		</dependency>
	</dependencies>
```
Код тестов

```
package ru.neoflex.practice;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.test.web.servlet.MockMvc;
import ru.neoflex.practice.controller.CalcController;

import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

@WebMvcTest(CalcController.class)
public class CalcControllerTest {

	@Autowired
	private MockMvc mockMvc;

	@Test
	public void testPlus() throws Exception {
		mockMvc.perform(get("/calc/plus/5/3"))
				.andExpect(status().isOk())
				.andExpect(content().string("8"));
	}

	@Test
	public void testMinus() throws Exception {
		mockMvc.perform(get("/calc/minus/5/3"))
				.andExpect(status().isOk())
				.andExpect(content().string("2"));
	}
}

```



