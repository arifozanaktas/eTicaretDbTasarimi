## eTicaretDbTasarimi
#eTicaret Database Projesindeki SQL Tasarımı

Bir e-ticaret sitesinin ürün, sepet, ödeme, kargo, satıcı ve kullanıcı gibi başlıklarını içeren kısa fakat detaylı bir tasarımını gerçekleştirdim. 
Detaylarını part part açıklayacağım.

![kapak](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/211d0e7b-a86c-4fbb-b7fe-b4c5b5999330)

---
*Users table ı kullanıcılar hakkında detaylı bilgiler içermektedir.

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
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/24d0e1d7-67b3-404c-bb9b-c5a66a04f832)

---
