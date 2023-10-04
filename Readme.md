Esse projeto se refere aos dados de uma empresa que produz bicicletas. 

1. Escolhi a plataforma Google CLoud.

2. Modelagem conceitual elaborei pelo SQL Server

3. Importação dos dados foi realizada pelas tarefas do Management Studio.

4.	Desenvolvimento de SCRIPT para análise de dados foram realizados somente utilizando as tarefas para importar os arquivos que já geraram as  tabelas, somente realizei a modelagem dos diagramas.

Análise de dados
Com base na solução implantada responda aos seguintes questionamentos:
1.	Escreva uma query que retorna a quantidade de linhas na tabela Sales.SalesOrderDetail pelo campo SalesOrderID, desde que tenham pelo menos três linhas de detalhes.
Resposta: SELECT SalesOrderID, 
COUNT(*)
FROM [importCSV].[dbo].[Sales.SalesOrderDetail]
GROUP BY SalesOrderID
HAVING COUNT (SalesOrderID) <= 3

2.	Escreva uma query que ligue as tabelas Sales.SalesOrderDetail, Sales.SpecialOfferProduct e Production.Product e retorne os 3 produtos (Name) mais vendidos (pela soma de OrderQty), agrupados pelo número de dias para manufatura (DaysToManufacture).
Resposta: SELECT 
A.SalesOrderID,
B.SpecialOfferID,
C.Productid
  FROM [importCSV].[dbo].[Sales.SalesOrderDetail] a
  LEFT JOIN [importCSV].[dbo].[Sales.SpecialOfferProduct] B ON B.SpecialOfferID = A.SalesOrderID
  LEFT JOIN [importCSV].[dbo].[Production.Product ] C ON C.Productid = b.ProductID


3.	Escreva uma query ligando as tabelas Person.Person, Sales.Customer e Sales.SalesOrderHeader de forma a obter uma lista de nomes de clientes e uma contagem de pedidos efetuados.
Resposta: SELECT *
  FROM [importCSV].[dbo].[Person.Person] a
 LEFT JOIN [importCSV].[dbo].[Sales.Customer] b on b.PersonID = a.[ID de entidade comercial]
 LEFT JOIN [importCSV].[dbo].[Sales.SalesOrderHeader] c on c.SalesOrderID = b.CustomerID

4.	Escreva uma query usando as tabelas Sales.SalesOrderHeader, Sales.SalesOrderDetail e Production.Product, de forma a obter a soma total de produtos (OrderQty) por ProductID e OrderDate.
Resposta: SELECT c.ProductID, 
       c.Name,
       sum(OrderQty),
       b.OrderDate,  
       sum(OrderQty)
FROM [importCSV].[dbo].[Sales.SalesOrderDetail] a
INNER JOIN [importCSV].[dbo].[Sales.SalesOrderHeader] b ON b.SalesOrderID  = a.SalesOrderID
INNER JOIN [importCSV].[dbo].[Production.Product] c ON c.ProductID = a.ProductID 
GROUP BY a.ProductID, b.OrderDate
ORDER BY b.OrderDateINNER JOIN [importCSV].[dbo].Production.Products c ON c.ProductID = a.ProductID 
GROUP BY a.ProductID, b.OrderDate
ORDER BY b.OrderDate

5.	Escreva uma query mostrando os campos SalesOrderID, OrderDate e TotalDue da tabela Sales.SalesOrderHeader. Obtenha apenas as linhas onde a ordem tenha sido feita durante o mês de setembro/2011 e o total devido esteja acima de 1.000. Ordene pelo total devido decrescente.
Resposta: SELECT SalesOrderID,
OrderDate,
TotalDue
FROM [importCSV].[dbo].[Sales.SalesOrderHeader]
WHERE OrderDate BETWEEN '2011-09-01 00:00:00' and '2011-09-30 00:00:00'and TotalDue > 1000
ORDER BY TotalDue desc

