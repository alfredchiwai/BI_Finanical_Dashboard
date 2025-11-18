# BI_Finanical_Dashboard
Power BI Main Financial Dashboard
<img width="2050" height="1201" alt="image" src="https://github.com/user-attachments/assets/9f75de56-3d8d-43b2-b87f-5a38e69a1c32" />
Revenue Analysis
<img width="2026" height="1194" alt="image" src="https://github.com/user-attachments/assets/4f85bfd4-f0a0-4bca-b352-935a33e78a68" />


<details>
  <summary>SQL Code in Azure Data Studio</summary>
  CREATE VIEW vwGLTrans

--This view contains all the information required to create financial statements

AS

SELECT

--FactGLTran
gl.FactGLTranID,
gl.GLTranAmount,
gl.JournalID,
gl.GLTranDescription,
gl.GLTranDate,

--GL Accounts
acc.AlternateKey 'GLAcctNum',
acc.GLAcctName,
acc.Statement,
acc.Category,
acc.Subcategory,

--Stores
sto.AlternateKey 'StoreNum',
sto.StoreName,
sto.ManagerID,
sto.PreviousManagerID,
sto.ContactTel,
sto.AddressLine1,
sto.AddressLine2,
sto.ZipCode,

--Region
reg.AlternateKey 'RegionNum',
reg.RegionName,
reg.SalesRegionName,

--Last Refresh Date
CONVERT(datetime2, GETDATE() at time zone 'UTC' at time zone 'Central Standard Time') AS 'LastRefreshDate'

FROM FactGLTran AS gl
    INNER JOIN dimGLAcct AS acc ON gl.GLAcctID = acc.GLAcctID
    INNER JOIN dimStore AS sto ON gl.StoreID = sto.StoreID
    INNER JOIN dimRegion AS reg ON sto.RegionID = reg.RegionID
GO


  
</details>


