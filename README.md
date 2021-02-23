# .Net_Linq

LINQ => Language-Integrated Query
* Se trata de un conjunto de tecnologías para poder expresar en lenguaje c# consultas desde diferentes orígenes de datos.
* Más información aquí: https://docs.microsoft.com/es-es/dotnet/csharp/tutorials/working-with-linq

# Struct

Todas las operaciones de consulta LINQ constan de tres acciones distintas: <br>
1.- Obtener el origen de datos. <br>
2.- Crear la consulta. <br>
3.- Ejecutar la consulta. <br>

https://docs.microsoft.com/es-es/dotnet/csharp/programming-guide/concepts/linq/introduction-to-linq-queries

```
   class IntroToLINQ
{
    static void Main()
    {
        // The Three Parts of a LINQ Query:
        // 1. Data source.
        int[] numbers = new int[7] { 0, 1, 2, 3, 4, 5, 6 };

        // 2. Query creation.
        // numQuery is an IEnumerable<int>
        var numQuery =
            from num in numbers
            where (num % 2) == 0
            select num;     
            
        //Otra forma de hacer la consulta
            var query = numbers.Where(num => num % 2 == 0);    
         
        // 3. Query execution.
        foreach (int num in numQuery)
        {
            Console.Write("{0,1} ", num);
        }
    }
}
```


### from, where y select 

La cláusula from especifica el origen de datos, la cláusula where aplica el filtro y la cláusula select especifica el tipo de los elementos devueltos. 


 
 ### Ordering
 
 ```
  // utilizando el lenguaje de consultas de Linq:
            var conLenguajeDeConsultas = from producto in _productos
                                         orderby producto.Precio descending // si quisiera ordenar de forma ascendente usamos el keyword 'ascending'
                                         select producto;

            
// utilizando el lenguaje de consultas de Linq:
            var conMetodos = _productos.OrderByDescending(producto => producto.Precio); // si quisiera ordenar de forma ascendente usamos el método 'OrderBy()'
```
 
# Data transformation

documentacion: https://docs.microsoft.com/es-es/dotnet/csharp/programming-guide/concepts/linq/type-relationships-in-linq-query-operations

# Examples 

### FindAsync

```
 var usuario =  _context.Usuarios.FindAsync(id);

```


### FirstOrDefault

```
var usuario =  _context.Usuarios.FirstOrDefaultAsync(m => m.Id == id);
```

### Multiple Where

```
 var funciones = _context.Funciones.Where(f => f.Pelicula.PeliculaId == model.PeliculaId)
                                               .Where(f => f.ButacasDisponibles >= model.cantButacas)
                                               .Where(f => f.Fecha >= DateTime.Today && f.Fecha < model.Fecha)
                                               .Where(f => f.Confirmada == true)
                                               .Select(p => new MostrarFuncionesVM() 
                                               { FuncionId = p.FuncionId,
                                                 Fecha = p.Fecha, 
                                                 Hora = p.Hora, 
                                                 cantButacas = model.cantButacas, 
                                                 Titulo = p.Pelicula.Titulo,
                                                 Sala = p.Sala.Numero, 
                                                 tipoSala = p.Sala.TipoSala.Nombre 
                                               });
```

### Multiple Include

```
reservas = _context.Reservas.Include(r => r.Cliente).Include(r => r.Funcion).Include(r => r.Funcion.Pelicula).ToList();
```

### Using navigational properties

```
var pelicula = await _context.Peliculas.Include(p => p.Genero).FirstOrDefaultAsync(m => m.PeliculaId == id);
```
