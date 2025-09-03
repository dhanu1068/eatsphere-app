# 🍴 Eatsphere Backend

**Project Overview**

***Eatsphere*** is a ***full-stack food delivery web application*** developed using ***Java Servlets, JDBC, JSP, HTML, CSS, and JavaScript.***
The platform provides a seamless experience for both customers and restaurants,covering the entire workflow of browsing restaurants, exploring menus, placing orders, and tracking them in real time.

For customers, Eatsphere offers features such as secure registration and login, restaurant discovery, menu browsing, cart management, order placement, and order history tracking. This ensures that users can easily place food orders online while keeping a record of past purchases for convenience.
## 👥 For Users  

- Register and log in securely  
- Browse restaurants and view available menus  
- Add items to cart and place food orders online  
- Orders are stored in the database with details (payment mode, total bill, and delivery status)  
- View order history for easy tracking and reordering  


## 🏢 For Restaurants/Admins  

- Manage restaurant profiles  
- Add, update, or remove menu items  
- Track and manage incoming customer orders  
- Ensure smooth coordination between restaurants and customers  


## 🔗 Application Integration  

- **Backend:** Java Servlets + JDBC for handling requests and database operations  
- **Frontend:** JSP pages, HTML, CSS, and JavaScript for dynamic and responsive user interfaces  
- **Database:** MySQL for persistent storage of users, restaurants, menus, and orders  

Eatsphere is designed as a **mini-version of popular apps like Zomato or Swiggy**, showcasing how real-world food delivery systems work.  


A **Food Delivery Application** built using **JDBC + Servlets**.

**Create Database & Tables**
Run the following queries in your MySQL (or compatible) database: 

CREATE TABLE `foodapp`.`user` (
  `userId` INT NOT NULL AUTO_INCREMENT,
  `userName` VARCHAR(45) NULL,
  `email` VARCHAR(45) NOT NULL,
  `phoneNumber` VARCHAR(45) NULL,
  `password` VARCHAR(45) NOT NULL,
  `address` VARCHAR(45) NULL,
  `createdDate` DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `lastLogin` DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`userId`));


CREATE TABLE `foodapp`.`restaurant` (
  `restaurantId` INT NOT NULL AUTO_INCREMENT,
  `restaurantName` VARCHAR(45) NOT NULL,
  `deliveryTime` DATETIME NOT NULL,
  `cuisineType` VARCHAR(45) NOT NULL,
  `address` VARCHAR(45) NOT NULL,
  `ratings` FLOAT NULL,
  `isActive` VARCHAR(45) NOT NULL,
  `adminId` INT NULL,
  `imgPath` VARCHAR(45) NULL,
  PRIMARY KEY (`restaurantId`));

CREATE TABLE `foodapp`.`menu` (
  `menuId` INT NOT NULL AUTO_INCREMENT,
  `restaurantId` INT NOT NULL,
  `menuName` VARCHAR(45) NOT NULL,
  `price` FLOAT NOT NULL,
  `description` VARCHAR(205) NOT NULL,
  `isAvailable` VARCHAR(45) NOT NULL,
  `imgPath` VARCHAR(45) NULL,
  PRIMARY KEY (`menuId`),
  INDEX `fk1_idx` (`restaurantId` ASC) VISIBLE,
  CONSTRAINT `fk1`
    FOREIGN KEY (`restaurantId`)
    REFERENCES `foodapp`.`restaurant` (`restaurantId`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION);


CREATE TABLE `foodapp`.`ordertable` (
  `orderId` INT NOT NULL AUTO_INCREMENT,
  `restaurantId` INT NOT NULL,
  `userId` INT NOT NULL,
  `orderDate` DATE NOT NULL,
  `totalAmount` FLOAT NOT NULL,
  `status` VARCHAR(45) NOT NULL,
  `paymentMode` VARCHAR(45) NOT NULL,
  PRIMARY KEY (`orderId`),
  INDEX `fk2_idx` (`userId` ASC) VISIBLE,
  INDEX `fk3_idx` (`restaurantId` ASC) VISIBLE,
  CONSTRAINT `fk2`
    FOREIGN KEY (`userId`)
    REFERENCES `foodapp`.`user` (`userId`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk3`
    FOREIGN KEY (`restaurantId`)
    REFERENCES `foodapp`.`restaurant` (`restaurantId`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION);


CREATE TABLE `foodapp`.`orderitem` (
  `orderItemId` INT NOT NULL AUTO_INCREMENT,
  `orderId` INT NOT NULL,
  `menuId` INT NOT NULL,
  `quantity` INT NOT NULL,
  `subTotal` FLOAT NOT NULL,
  PRIMARY KEY (`orderItemId`),
  INDEX `fk4_idx` (`menuId` ASC) VISIBLE,
  INDEX `fk5_idx` (`orderId` ASC) VISIBLE,
  CONSTRAINT `fk4`
    FOREIGN KEY (`menuId`)
    REFERENCES `foodapp`.`menu` (`menuId`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk5`
    FOREIGN KEY (`orderId`)
    REFERENCES `foodapp`.`ordertable` (`orderId`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION);

CREATE TABLE `foodapp`.`orderhistory` (
  `orderHistoryId` INT NOT NULL AUTO_INCREMENT,
  `orderId` INT NOT NULL,
  `userId` INT NOT NULL,
  `orderDate` DATETIME NOT NULL,
  `totalAmount` FLOAT NOT NULL,
  `status` VARCHAR(45) NULL,
  PRIMARY KEY (`orderHistoryId`),
  INDEX `fk6_idx` (`orderId` ASC) VISIBLE,
  INDEX `fk7_idx` (`userId` ASC) VISIBLE,
  CONSTRAINT `fk6`
    FOREIGN KEY (`orderId`)
    REFERENCES `foodapp`.`ordertable` (`orderId`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk7`
    FOREIGN KEY (`userId`)
    REFERENCES `foodapp`.`user` (`userId`)
    ON DELETE NO ACTION ON UPDATE NO ACTION); 
## 🏃 Run the Project  

- Import the project into **Eclipse**  
- Configure **DBConnection.java** with your database username & password  
- Start your server (**Apache Tomcat**)  
- Access the homepage at 👉 [http://localhost:8443/FoodApp/](http://localhost:8443/FoodApp/)

 **Project Homepage**
 When you run the project, the homepage looks like this:
![Home](https://github.com/user-attachments/assets/6322d715-ec92-40bd-b46e-8180f68b662a)
![resturants](https://github.com/user-attachments/assets/154d2c0e-a2e8-4be0-999f-1c74882aa622)
and Menu like this
  ![menu](https://github.com/user-attachments/assets/37bdb0ea-0696-4054-92eb-da1cfa02815e)

🛠 **Tech Stack**
   - Java Servlets
   - JDBC
   - MySQL
   - JSP (for views)
   - Tomcat

