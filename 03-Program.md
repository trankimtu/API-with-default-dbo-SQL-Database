## Root folder
File Program.cs
```
global using Main.Data;
global using Microsoft.EntityFrameworkCore;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.

builder.Services.AddControllers();
builder.Services.AddDbContext<DataContext>(options =>
{
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection"));
});
// Learn more about configuring Swagger/OpenAPI at https://aka.ms/aspnetcore/swashbuckle
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```
## Explain the code

```
builder.Services.AddDbContext<DataContext>(options =>
```
This line of code registers a database context with the dependency injection container. In this case, the database context being registered is ```DataContext```.<br>

The ```builder``` object is an instance of the ```WebHostBuilder``` or ```HostBuilder``` class, which is typically used to configure and launch an ASP.NET Core application. The ```Services``` property of the ```builder``` object is an instance of ```IServiceCollection```, which is used to register services that the application will use.<br>

The ```AddDbContext``` method is an extension method on ```IServiceCollection``` that is provided by the ```Microsoft.EntityFrameworkCore``` package. It allows us to register a database context with the dependency injection container.<br>

The first argument to ```AddDbContext``` is the type of database context that we want to register (```DataContext``` in this case). The second argument is a callback function that configures the database context options.<br>

The ```options``` parameter in the callback function is an instance of ```DbContextOptionsBuilder<DataContext>```, which allows us to configure options for the ```DataContext```.<br>

So in summary, this line of code is registering ```DataContext``` as a service in the application's dependency injection container and providing a callback function to configure its options.<br>
