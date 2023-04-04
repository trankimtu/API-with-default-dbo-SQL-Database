## Controllers folder
File SuperHeroController.cs
```
using Azure.Core;
using Main.Models;
using Microsoft.AspNetCore.Components.Web.Virtualization;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;

namespace Main.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class SuperHeroController : ControllerBase
    {
       
        // DB envolve
        private readonly DataContext _context;
        public SuperHeroController(DataContext context)
        {
            _context = context;
        }
        //====================================================================
        // Get whole list of SuperHero
        [HttpGet]
        public async Task<ActionResult<List<SuperHero>>> Get()
        {
            return Ok(await _context.SuperHeroes.ToListAsync()); // Ok: 200, BadRequest: 400, NotFound: 404
        }


        //====================================================================
        // Get superhero by Id
        // [HttpGet]
        // [Route("{id}")]
        [HttpGet("{id}")]
        public async Task<ActionResult<SuperHero>> Get(int id)
        {
            // var hero = heroes[id];
            var hero = await _context.SuperHeroes.FindAsync(id);
            if (hero == null)
            {
                return NoContent();
            }
            return Ok(hero); // Ok: 200, BadRequest: 400, NotFound: 404
        }


        //====================================================================
        [HttpPost]
        public async Task<ActionResult<List<SuperHero>>> AddHero(SuperHero hero)
        {
            _context.SuperHeroes.Add(hero); //change table
            await _context.SaveChangesAsync(); // Save table
            return Ok(await _context.SuperHeroes.ToListAsync()); 
        }


        //====================================================================
        [HttpPut]
        public async Task<ActionResult<SuperHero>> UpdateHero( SuperHero request)
        {
            var hero = await _context.SuperHeroes.FindAsync(request.Id);
            if (hero == null)
            {
                return NotFound("Hero is not found.");
            }

            hero.Name = request.Name;
            hero.FirstName = request.FirstName ;
            hero.LastName = request.LastName ;
            hero.Place = request.Place;
            await _context.SaveChangesAsync(); // Save table
            return Ok(await _context.SuperHeroes.ToListAsync()); // Ok: 200, BadRequest: 400, NotFound: 404
        }


        //====================================================================
        [HttpDelete("{id}")]
        public async Task<ActionResult<SuperHero>> Delete(int id)
        {
            var hero = await _context.SuperHeroes.FindAsync(id);
            if (hero == null)
            {
                return BadRequest("Hero is not found.");
            }

            _context.SuperHeroes.Remove(hero);
            await _context.SaveChangesAsync(); // Save table
            return Ok(await _context.SuperHeroes.ToListAsync()); // Ok: 200, BadRequest: 400, NotFound: 404
        }
    }
}

```
