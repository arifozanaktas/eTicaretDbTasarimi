## eTicaretDbTasarimi
#eTicaret Database Projesindeki SQL Tasarımı

Bir e-ticaret sitesinin ürün, sepet, ödeme, kargo, satıcı ve kullanıcı gibi başlıklarını içeren kısa fakat detaylı bir tasarımını gerçekleştirdim. 
Detaylarını part part açıklayacağım.

![kapak](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/211d0e7b-a86c-4fbb-b7fe-b4c5b5999330)

---
*UsersAddresses table ı kullanıcıların iletişim ve kargo bilgileri hakkında detaylar içermektedir. 
Adres bilgileri Türkiye şartlarına uyarlanarak zorunlu alanlar düzenlenecek şeklinde tasarlanmıştır.

```tSQL
CREATE TABLE [dbo].[UserAddresses](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[UserId] [int] NOT NULL,
	[City] [varchar](150) NOT NULL,
	[Town] [varchar](150) NULL,
	[Street] [varchar](150) NULL,
	[ZipCode] [varchar](50) NULL,
	[Address] [varchar](550) NOT NULL,
	[PhoneNumber] [varchar](50) NULL,
	[Name] [varchar](50) NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
```
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/1d8ba5fc-4371-4902-ac20-b03706626072)


---
*Users table ı kullanıcılar hakkında detaylı bilgiler içermektedir. Telefon numarası ve Update tarihi boş bırakılabilir şeklinde tasarlanmıştır.

```tSQL
CREATE TABLE [dbo].[Users](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [varchar](250) NOT NULL,
	[Email] [varchar](250) NOT NULL,
	[PhoneNumber] [varchar](50) NULL,
	[PasswordHash] [varbinary](max) NOT NULL,
	[PasswordSalt] [varbinary](max) NOT NULL,
	[IsActive] [bit] NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
```
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/7702e53d-83f8-45b5-a5a8-7cd0acaab46d)

---
*Tickets table ı kullanıcı ve satıcının iletişime geçebilmesi hakkında bilgiler içermektedir. Kullanımda olan 'Satıcıya soru sor' butonu amacıyla tasarlanmıştır.
```tSQL
CREATE TABLE [dbo].[Tickets](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[SellerId] [int] NOT NULL,
	[UserId] [int] NOT NULL,
	[Subject] [varchar](150) NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
```
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/78e675b0-cb31-476b-89af-763bde0ea68d)

---


*TicketsDetails table ı kullanıcı ve satıcının iletişime geçtikten sonraki diğer kullanıcıların bu iletişimi gördüğü ekran hakkında bilgiler içermektedir. Kullanımda olan 'Satıcıya sorulan sorular' ekranı amacıyla tasarlanmıştır.
```tSQL
CREATE TABLE [dbo].[TicketDetails](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[TicketId] [int] NOT NULL,
	[SellerId] [int] NULL,
	[UserId] [int] NULL,
	[Content] [varchar](250) NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
```
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/93ccd7f4-11ee-4c6c-824c-ef276df58262)

---


*TaxDepartments table ı satıcının hangi Vergi Dairelerine bağlı olduğu hakkında bilgiler içermektedir. 
```tSQL
CREATE TABLE [dbo].[TaxDepartments](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[City] [varchar](150) NOT NULL,
	[Town] [varchar](150) NOT NULL,
	[Code] [int] NOT NULL,
	[Name] [varchar](150) NOT NULL,
```
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/1ba58944-de71-40de-b525-e2e872d5629d)


---


*ShoppingCarts table ı kullanıcının sepeti hakkında bilgiler içermektedir. 
```tSQL
CREATE TABLE [dbo].[ShoppingCarts](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[UserId] [int] NOT NULL,
	[ProductFieldId] [int] NOT NULL,
	[Stock] [decimal](18, 2) NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
```
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/d310c95a-1c47-4bc2-9a81-85d9401ab267)

---


*SellerTitles table ı satıcının sitede görünecek kullanıcı adı hakkında bilgiler içermektedir. 
```tSQL
CREATE TABLE [dbo].[SellerTitles](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Title] [varchar](50) NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
	[SellerId] [int] NOT NULL,
```
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/7ffc3b23-84a1-471d-acfa-b24f1a949fc1)

---


*Sellers table ı satıcının sitede hizmet verebilmesi için gerekli bilgileri içermektedir. 
```tSQL
CREATE TABLE [dbo].[Sellers](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [varchar](350) NOT NULL,
	[Address] [varchar](max) NOT NULL,
	[TaxIdentityNumber] [char](10) NOT NULL,
	[IdentityNumber] [char](11) NULL,
	[TaxDepartmentId] [int] NOT NULL,
	[WebSite] [varchar](max) NULL,
	[PhoneNumber] [varchar](20) NOT NULL,
	[Email] [varchar](500) NOT NULL,
	[UserName] [varchar](150) NOT NULL,
	[PasswordHash] [varbinary](max) NOT NULL,
	[PasswordSalt] [varbinary](max) NOT NULL,
	[IsConfirm] [bit] NOT NULL,
	[ConfirmCode] [int] NOT NULL,
	[ConfirmCodeSendDate] [datetime] NOT NULL,
	[ChangePasswordCode] [int] NULL,
	[ChangePasswordCodeSendDate] [datetime] NULL,
	[ChangePasswordIsCompleted] [bit] NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
	[AverageRating] [decimal](3, 2) NOT NULL,
	[IsActive] [bit] NOT NULL,
```
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/d1b81dc0-4a68-4704-96a3-6590f6eb7aa1)

---


*ProductSelections table ı satılacak ürünlerin üst kategorileri ile bağlantı sağladığımız tabledır ve Product table ı ile bağlantılı çalışır. 
```tSQL
CREATE TABLE [dbo].[ProductSelections](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [varchar](150) NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
	[ProductId] [int] NOT NULL,
	[MainProductSelectionId] [int] NULL,
```
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/34e4d108-d576-4263-a8cc-d896c551219e)

---


*ProductSelections table ı satılacak ürünlerin üst kategorileri ile bağlantı sağladığımız tabledır ve Product table ı ile bağlantılı çalışır. 
```tSQL
CREATE TABLE [dbo].[Products](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [varchar](255) NOT NULL,
	[OverrangeRating] [decimal](3, 2) NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
	[SellerId] [int] NOT NULL,
```

