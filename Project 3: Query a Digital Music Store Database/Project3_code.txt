/*SamanhAlsaeed*/
/*Q1: What are the genre of the most purchased tracks ?*/

SELECT g.name,  COUNT(*)  number_purchases
FROM invoice i
JOIN invoiceLine il
ON i.InvoiceId = il.InvoiceId
JOIN Track t
ON il.TrackId = t.TrackId
JOIN Genre g
ON t.GenreId = g.GenreId

GROUP BY g.name
ORDER BY 2 DESC

/*Q2: Who is the Rock Artist of The Best Selling? (TOP FIVE)*/

SELECT ar.Name,  COUNT(*)  number_purchases
FROM invoice i
JOIN invoiceLine il
ON i.InvoiceId = il.InvoiceId
JOIN Track t
ON il.TrackId = t.TrackId
JOIN Genre g
ON t.GenreId = g.GenreId
JOIN Album al
ON t.AlbumId = al.AlbumId
JOIN Artist ar
ON al.ArtistId = ar.ArtistId

WHERE g.Name = 'Rock'

GROUP BY ar.name
ORDER BY 2 DESC
LIMIT 5

/*Q3: What Are the Least Sales Albums? */

SELECT  i.BillingCountry, COUNT(*) num_purchases
FROM Artist ar
JOIN Album al
ON ar.ArtistId = al.ArtistId
JOIN Track t
ON al.AlbumId = t.AlbumId
JOIN InvoiceLine il
ON t.TrackId = il.TrackId
JOIN Invoice i
ON il.InvoiceId = i.InvoiceId

WHERE ar.Name = 'U2'

GROUP BY 1
ORDER BY 2 DESC

/*Q4: Which Country Has The Greatest Sales of ‘U2’ ?  */

SELECT al.Title, al.AlbumId, COUNT(*) as num_purchases, SUM(i.total)  as Total_Revenue
FROM Album al
JOIN Track t
ON al.AlbumId = t.AlbumId
JOIN InvoiceLine il
ON t.TrackId = il.TrackId
JOIN invoice i
ON il.InvoiceId = i.InvoiceId


GROUP BY  1
HAVING Total_Revenue < 10 AND num_purchases < 5 /*to obtain the least purchased and less revenue albums, so we might stop supplying it*/
ORDER BY 4,3
