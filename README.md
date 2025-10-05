# CDN-Riot
CDN-Riot is a lightweight GitHub repository that automatically updates a data file containing information about all League of Legends champions every day.<br>
The file can be accessed directly via a GitHub raw URL and used in web or game-related projects that need up-to-date champion data.

## Accessing League of Legends Champion Information
https://raw.githubusercontent.com/megadoxs/cdn-riot/main/champions.json

## Example Usage
```javascript
fetch('https://raw.githubusercontent.com/megadoxs/cdn-riot/main/champions.json')
.then(response => response.json())
.then(data => {
  champions.map(champion => {
    champion.price = data[`${champion.id}`].price
    champion.releaseDate = data[`${champion.id}`].releaseDate
    champion.roles = data[`${champion.id}`].roles
    champion.positions = data[`${champion.id}`].positions
    champion.difficulty = data[`${champion.id}`].attributeRatings.difficulty
    champion.skins.forEach((skin, j) => {
      let index = data[`${champion.id}`].skins.findIndex(skin => skin.id == parseInt(champion.skins[j].id));
      if (index === -1)
        skin.price = 'Special'
      else {
        skin.price = data[`${champion.id}`].skins[index].cost;
        skin.set = data[`${champion.id}`].skins[index].set
        skin.releaseDate = data[`${champion.id}`].skins[index].release
        skin.rarity = data[`${champion.id}`].skins[index].rarity
        if (data[`${champion.id}`].skins[index].set.length > 0 && !skinLines.includes(data[`${champion.id}`].skins[index].set[0]))
          skinLines.push(data[`${champion.id}`].skins[index].set[0])
      }
    });
    return champion
  });
})
```

## Example Project
[Riot Characters Discoverer](https://github.com/megadoxs/Riot)
