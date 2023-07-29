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
