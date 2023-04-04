## Folder Data
File DataContext.cs
```
using Main.Models;
using Microsoft.EntityFrameworkCore;

namespace Main.Data
{
    public class DataContext : DbContext
    {
        public DataContext(DbContextOptions<DataContext> options) : base(options) { }

        public DbSet<SuperHero> SuperHeroes { get; set; }
    }
}
```
