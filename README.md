# What is SecondDesigner?
SecondDesigner is an all-in-one framework for games or simulations that use procedurally generated worlds or scenarios.

# Examples
Create a map filled with a random combination of Ocean and Land tiles:

config.json:
```
{
  "map" : {
    "dim": {
      "x": 100,
      "y": 100
    },
    "gen": {
      "method" : "rand"
    }
  },
  "tile": {
    "tilesize" : 1,
    "biomes" : [
      "ocean",
      "land"
    ]
  }
}
```
example.py:
```
from sd import StaticEnviroment, Ruleset
s = StaticEnviroment()
r = Ruleset.buildNewRuleset("config.json")
s.loadRuleset(r)
s.renderMap()
a = s.map.asArray()
for i in a:
  print("".join(i))
```

If you want to make it so that land tiles form near each other (like islands), you could change config.json to this:
```
{
  "map" : {
    "dim": {
      "x": 100,
      "y": 100
    },
    "gen": {
      "method" : "rand",
      "groupingbias" : {
        "land": {
          "tiles" : [land],
          "bias" : 20
        }
      }
    }
  },
  "tile": {
    "tilesize" : 1,
    "biomes" : [
      "ocean",
      "land"
    ]
  }
}
```
This gives the Land biome a "grouping bias" value of 20, meaning that there is an additional 20% of a land tile being randomly placed, but ONLY if the tile being generated is adjacent to a previously generated land tile.

Note: This project is very early in development. Feel free to contribute or ask questions!
