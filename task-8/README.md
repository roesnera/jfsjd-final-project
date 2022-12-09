# Task 8: Database Connection with Spring Data JPA

## Description

For this task, we'll implement the backend of our web application using Spring Boot with Java.

## Walkthrough

### Step 1: Creating the base project

> #### Useful Resources for this step
>
> - [Spring Initializr](https://start.spring.io/)

In this step, we'll generate a Spring Boot project using the [spring initializr](https://start.spring.io/)

1. Go to the [spring initializr](https://start.spring.io/) and generate a new project with the following configuration:
   - Project: Maven Project
   - Language: Java
   - Dependencies: Spring Web, Spring Data JPA (SQL), and the MySQL Driver
   - Project Metadata: use meaningful names that describe your project, use Jar for packaging and select the Java version installed on your computer.
     <img src="./img/SpringInit.png">
2. Click on Generate.
   ([Here](https://start.spring.io/#!type=maven-project&language=java&platformVersion=3.0.0&packaging=jar&jvmVersion=19&groupId=com.example&artifactId=itemsAPI&name=itemsAPI&description=Demo%20project%20for%20Spring%20Boot&packageName=com.example.itemsAPI&dependencies=web,data-jpa,mysql) is a pre-initialized project link)
3. Create a new repo on Github for the backend and upload the generated code.

### Step 2: Database Connection with Spring Data JPA

> #### Useful Resources for this step
>
> - [Spring Data Reference Documentation](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.introduction)
> - [Accesing data with MySQL](https://spring.io/guides/gs/accessing-data-mysql/)

In this step, we'll connect the Spring Boot project with the MySQL database created on [task 7](https://github.com/generation-org/jfsjd-final-project/tree/main/task-7).


1. Add the following properties to the src/main/resources/application.properties:

   ```yaml
      ## the username of the user I created in the MySQL workbench
      spring.datasource.username=aaroe
      ## the password for that user
      spring.datasource.password=myPassword
      ## "item" here refers to the name of the database I created
      spring.datasource.url=jdbc:mysql://${MYSQL_HOST:localhost}:3306/item
      ## the remaining lines should be the same for everyone
      spring.jpa.hibernate.ddl-auto=update
      spring.jpa.show-sql=true
      spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
   ```

#### Test Your Code!

> Now is a good chance to test your code, run your Application main method to start the server.
>
> **Expected Result**
> Your application should start and connect with your database, no error should be displayed on the console.

### Step 3: Interacting with the Database from your Spring Boot Project

1. Create new package called `repository.entity` and define the @Entity Model class:

   ```java
       package org.generation.ItemsAPI.repository.entity;

       import jakarta.persistence.Entity;
       import jakarta.persistence.GeneratedValue;
       import jakarta.persistence.GenerationType;
       import jakarta.persistence.Id;

       @Entity
       public class Item
       {
           @Id
           @GeneratedValue(strategy= GenerationType.AUTO)
           private Integer id;

           private String name;

           private String description;

           private String imageUrl;

           public Integer getId()
           {
               return id;
           }

           public void setId( Integer id )
           {
               this.id = id;
           }

           public String getName()
           {
               return name;
           }

           public void setName( String name )
           {
               this.name = name;
           }

           public String getDescription()
           {
               return description;
           }

           public void setDescription( String description )
           {
               this.description = description;
           }

           public String getImageUrl()
           {
               return imageUrl;
           }

           public void setImageUrl( String imageUrl )
           {
               this.imageUrl = imageUrl;
           }
       }
   ```

2. Create your repository interface to access the `Item` entity data under the repository package:

   For example:

   ```java
    package org.generation.ItemsAPI.repository;

    import org.generation.ItemsAPI.repository.entity.Item;
    import org.springframework.data.jpa.repository.JpaRepository;

    // This will be AUTO IMPLEMENTED by Spring into a Bean called itemRepository
    // CRUD refers Create, Read, Update, Delete
    public interface ItemRepository extends JpaRepository<Item, Integer>
    {
    }
   ```

3. Create a REST Controller to test your code inside a new package `controller` called ItemController:

   ```java
   @RestController
   @RequestMapping("/item")
   public class ItemController{

       final ItemRepository itemRepository;


       public ItemController(@Autowired ItemRepository itemRepository )
       {
           this.itemRepository = itemRepository;
       }

       @GetMapping
       public Iterable<Item> getItems(){
           return itemRepository.findAll();
       }
   }

   ```

> #### Test Your Code!
>
> Now is a good chance to test your code, start your application and open `http://localhost:8080/item` on your browser.
>
> **Expected Result**
> You should see the list of items stored on your MySQL database:
>
> ```json
> [
>   {
>     "id": 1,
>     "name": "Chips",
>     "description": "Sour Cream and Onion",
>     "imageUrl": "https://images-na.ssl-images-amazon.com/images/I/81EUE1oZURL._SL1500_.jpg"
>   }
> ]
> ```

## Example

Stuck? Check out the provided example in the [example/](example/) folder
