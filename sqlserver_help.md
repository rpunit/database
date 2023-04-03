# database

## delete duplicate rows from table without primary key

```
DELETE FROM dbo.duplicateTest
INSERT INTO dbo.duplicateTest VALUES(1, 'Bob','Smith') 
INSERT INTO dbo.duplicateTest VALUES(2, 'Dave','Jones') 
INSERT INTO dbo.duplicateTest VALUES(3, 'Karen','White') 
INSERT INTO dbo.duplicateTest VALUES(1, 'Bob','Smith')
INSERT INTO dbo.duplicateTest VALUES(1, 'Bob','Smith')	

SELECT * FROM dbo.duplicateTest; 

with temp(rank1,id ,fname,lname)
as (
   select row_number() over ( partition by ID, FirstName, LastName order by ID, FirstName, LastName ) , * 
   from duplicateTest
)
delete from temp where rank1 > 1;

SELECT * FROM dbo.duplicateTest;

```
