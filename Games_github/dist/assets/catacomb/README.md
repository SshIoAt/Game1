# Catacombe di Parigi — Tilemap

**Gioco:** (RE)VOLUTION — Survival top-down, Rivoluzione Francese  
**Formato:** Tiled JSON (v1.10)  
**Dimensioni:** 100×100 tiles × 16×16 px = 1600×1600 pixel totali  
**Tileset:** `../tiny-town/tilemap_packed.png` (192×176 px, 12×11 tiles)

## Layer

| Layer | Descrizione | Tile usati |
|-------|-------------|------------|
| `background` | Muri/vuoto scuro | Tile 123-124 (grigio molto scuro) |
| `floor` | Pavimento camminabile | Tile 49, 61, 77, 97, 108-110, 121 (pietra) |
| `walls` | Bordi murari con fisica | Tile 48, 51, 96, 99, 111 |
| `decor` | Decorazioni sparse | Tile 44-45, 56-57, 92-93, 105-106 |

## Zone della Mappa

```
[NORD]
  Ingresso (entrata dalle strade di Parigi)
      │
  ┌───┴───────────────────────────┐
  │  Ossario Ovest ── Ossario Est │
  │                               │
  │      NAVATA CENTRALE          │
  │                               │
  │  Camera di Tortura  ┤ Archivi │
  └───────────────┬───────────────┘
              Camera Rituale
                  │
         ┌────────┴──────────┐
         │  Anticamera       │
         │                   │
         │  ████████████     │
         │  █ PORTALE █      │  ← Zona Infernale
         │  █ INFERN. █      │
         │  ████████████     │
         └───────────────────┘
[SUD]
```

## Come usare in Phaser 3

```javascript
// Preload
this.load.tilemapTiledJSON('catacomb', '/assets/catacomb/catacomb.json');
this.load.image('tilemap_packed', '/assets/tiny-town/tilemap_packed.png');

// Create
const map = this.make.tilemap({ key: 'catacomb' });
const tiles = map.addTilesetImage('tilemap_packed', 'tilemap_packed');
const bgLayer    = map.createLayer('background', tiles, 0, 0);
const floorLayer = map.createLayer('floor',      tiles, 0, 0);
const wallLayer  = map.createLayer('walls',      tiles, 0, 0);
const decorLayer = map.createLayer('decor',      tiles, 0, 0);

// Aggiungere collisioni ai muri
wallLayer.setCollisionByExclusion([-1]);

// World bounds
this.physics.world.setBounds(0, 0, map.widthInPixels, map.heightInPixels);
this.cameras.main.setBounds(0, 0, map.widthInPixels, map.heightInPixels);
```

## Preview

Apri `/catacomb-preview.html` nel browser per visualizzare la mappa interattiva.

---
_Generato per il corso "Crea un videogame con PhaserJs e Typescript"_
