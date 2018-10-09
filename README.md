# Linq 101

https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/linq/introduction-to-linq-queries

## Query
The query expression contains three clauses: 
* from
* where
* select
```
var numbers = new[] { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

var oddNumberQry = from it in numbers
                    where it % 2 == 0
                    select it;

foreach (var item in oddNumberQry)
{
    System.Console.WriteLine(item);
}
```
Shorthand version
```
var qry = numbers.Where(it => it % 2 == 0);
```

## Execution
**Deferred Execution**  
The query variable itself only stores the query commands.
```
int counter = 1;
var oddNumberQry = from it in numbers
                    where it % 2 == 0
                    let somthing = counter++
                    select it;
```

**Immediate Execution**  
Examples of such queries are `Count`, `Max`, `Average`, `ToList`, and `First`  
These execute without an explicit foreach statement because the query itself must use foreach in order to return a result.
```
var oddSummation = oddNumberQry.Sum();
```

## Data Transformations
```
public class Student
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```
```
var oddStudentQry = from it in numbers
                    where it % 2 == 0
                    select new Student
                    {
                        Id = it,
                        Name = it.ToString()
                    };

foreach (var item in oddStudentQry)
{
    System.Console.WriteLine($"Id: {item.Id}, Name: {item.Name}");
}
```
Shorthand version
```
var qry = numbers
                .Where(it => it % 2 == 0)
                .Select(it => new Student
                {
                    Id = it,
                    Name = it.ToString()
                });
```
