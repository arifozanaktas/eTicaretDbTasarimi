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


*Products table ı satılacak ürünleri ile satıcının bağlantısını sağladığımız tabledır. 
```tSQL
CREATE TABLE [dbo].[Products](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [varchar](255) NOT NULL,
	[OverrangeRating] [decimal](3, 2) NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
	[SellerId] [int] NOT NULL,
```
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/e059141d-296d-472a-9fae-d92d5144a3e4)

---


*ProductFields table ı satılacak ürünlerin renk,ölçü gibi detaylarının seçilip stok,ilk açılıştaki görseli ve fiyat gibi bilgilerin kullanıcıya aktarıldığı tabledır. 
```tSQL
CREATE TABLE [dbo].[ProductFields](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [varchar](150) NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
	[ProductSelectionId] [int] NOT NULL,
	[MainImageUrl] [varchar](max) NULL,
	[MainProductFieldId] [int] NULL,
	[IsActive] [bit] NOT NULL,
	[Price] [money] NULL,
	[SellingPrice] [money] NULL,
	[Stock] [decimal](18, 2) NULL,
	[IsVatInclude] [bit] NOT NULL,
```
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/b342d949-44fa-4b60-8e41-ae8483e89237)

---


*ProductFieldImageUrls table ı satılacak ürünlerin renk,ölçü gibi detaylarının seçildikten sonraki görsellerinin kullanıcıya aktarıldığı tabledır. 
```tSQL
CREATE TABLE [dbo].[ProductFieldImageUrls](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[ImageUrl] [varchar](max) NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
	[ProductFieldId] [int] NOT NULL,
```
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/26a1c4a0-dc1f-49d4-ac9b-3169ab7949e6)


---


*ProductFieldCategoryFields table ı satılacak ürünlerin seçilebilecek kategoriler ile bağlantı kurmasını sağlayan tabledır. 
```tSQL
CREATE TABLE [dbo].[ProductFieldCategoryFields](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[ProductFieldId] [int] NOT NULL,
	[CategoryFieldId] [int] NOT NULL,
	[Value] [varchar](250) NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
```
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/44053470-9deb-4925-8f20-c3003d59f880)

---


*PaymentDetails table ı satılacak ürünlerin seçilebilecek kategoriler ile bağlantı kurmasını sağlayan tabledır. 
```tSQL
CREATE TABLE [dbo].[PaymentDetails](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[OrderId] [int] NOT NULL,
	[PaymentPrice] [money] NOT NULL,
	[PaymentType] [varchar](150) NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
	[KKPaymentConfirmId] [int] NULL,
	[BankName] [varchar](150) NULL,
	[IsCompleted] [bit] NOT NULL,
	[CompletedDate] [datetime] NULL,
	[Description] [varchar](250) NULL,
```
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/e3111452-382b-4caa-bbe2-943aa35cd0fa)

---


*OrderStatuses table ı satılacak ürünlerin seçilebilecek kategoriler ile bağlantı kurmasını sağlayan tabledır. 
```tSQL
CREATE TABLE [dbo].[OrderStatuses](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [varchar](100) NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
	[IsActive] [bit] NOT NULL,
```

![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/3f438fc5-b09c-4b14-9135-ec3898025428)

---


*Orders table ı satılacak ürünlerin seçilebilecek kategoriler ile bağlantı kurmasını sağlayan tabledır. 
```tSQL
CREATE TABLE [dbo].[Orders](
	[Id] [int] NOT NULL,
	[UserId] [int] NOT NULL,
	[ProductFieldId] [int] NOT NULL,
	[SellingPrice] [money] NOT NULL,
	[Stock] [decimal](18, 2) NOT NULL,
	[UserAddressId] [int] NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
	[OrderStatusId] [int] NOT NULL,
	[CargoTracingNumber] [varchar](150) NULL,
```

![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/4c7ebaae-2fd7-4385-b74e-b6ad969920bc)

---


*Invoices table ı satılacak ürünlerin seçilebilecek kategoriler ile bağlantı kurmasını sağlayan tabledır. 
```tSQL
CREATE TABLE [dbo].[Invoices](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[OrderId] [int] NOT NULL,
	[InvoiceNumber] [varchar](16) NOT NULL,
	[Date] [datetime] NOT NULL,
	[DeliveryDate] [datetime] NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
	[Discount] [money] NOT NULL,
```
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/d1b541ed-f9db-42ab-b9fa-e2a3ecbf1f64)

---


*Comments table ı satılacak ürünlerin seçilebilecek kategoriler ile bağlantı kurmasını sağlayan tabledır. 
```tSQL
CREATE TABLE [dbo].[Comments](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[OrderId] [int] NOT NULL,
	[Rating] [int] NOT NULL,
	[Comment] [varchar](250) NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
```

![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/2e7e976a-5814-4614-85cd-ee601bd82750)

---


*CommentLikes table ı satılacak ürünlerin seçilebilecek kategoriler ile bağlantı kurmasını sağlayan tabledır. 
```tSQL
CREATE TABLE [dbo].[CommentLikes](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[UserId] [int] NOT NULL,
	[CommentId] [int] NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
```
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/e82a7ccd-dc30-4223-87c8-a0eca8cbf077)

---


*CommentImageUrls table ı satılacak ürünlerin seçilebilecek kategoriler ile bağlantı kurmasını sağlayan tabledır. 
```tSQL
CREATE TABLE [dbo].[CommentImageUrls](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[CommentId] [int] NOT NULL,
	[ImageUrl] [varchar](max) NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
```
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/76224a98-197d-4dd8-bd7f-2fc12aba0199)

---


*CategoryFields table ı satılacak ürünlerin seçilebilecek kategoriler ile bağlantı kurmasını sağlayan tabledır. 
```tSQL
CREATE TABLE [dbo].[CategoryFields](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [varchar](150) NOT NULL,
	[CategoryId] [int] NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
```

![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/4c77db8f-011f-493b-864f-306762696e2f)


---


*CategoryEquivalents table ı satılacak ürünlerin seçilebilecek kategoriler ile bağlantı kurmasını sağlayan tabledır. 
```tSQL
CREATE TABLE [dbo].[CategoryEquivalents](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[CategoryId] [int] NOT NULL,
	[EquivalentId] [int] NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
```

![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/94dc35f5-cb73-47a9-b52e-ad351c22329e)

---


*Categories table ı satılacak ürünlerin seçilebilecek kategoriler ile bağlantı kurmasını sağlayan tabledır. 
```tSQL
CREATE TABLE [dbo].[Categories](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [varchar](250) NOT NULL,
	[IsActive] [bit] NOT NULL,
	[MainCategoryId] [int] NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
	[Path] [varchar](max) NULL,
	[VatRate] [int] NOT NULL,
```
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/a54f51c9-66fd-4575-bf8b-09186f2d6f4e)
