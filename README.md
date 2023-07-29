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
![image](https://github.com/arifozanaktas/eTicaretDbTasarimi/assets/139919845/1d8ba5fc-4371-4902-ac20-b03706626072)


---
