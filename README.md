import requests
import pandas as pd

Pokemon_Lista = []

for N_Pokemon in range(1,152):

  url = f"https://pokeapi.co/api/v2/pokemon-form/{N_Pokemon}/"

  response = requests.get(url)
  data = response.json()

  url = f"https://pokeapi.co/api/v2/pokemon/{data['name']}/"

  response = requests.get(url)
  data = response.json()

  Pokemon_Lista.append({
  "N° Pokedex" : data["game_indices"][4]["game_index"],
  "Pokemon" : data['name'],
  "Peso" : data['weight'],
  "Altura" : data['height'],
  "Exp. Base" : data['base_experience'],
  "Habilidade" : data["abilities"][0]["ability"]["name"]
  })


df = pd.DataFrame(Pokemon_Lista)
df.sort_values(by='Peso', ascending=False).head(10)
