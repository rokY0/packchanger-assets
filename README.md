# packchanger-assets

Contenuti di [PackChanger](https://github.com/rokY0/packchanger-app):
i pack, le loro anteprime e i testi che compaiono nell'app.

**Questo repository deve restare PUBBLICO**: l'app scarica i file da
`raw.githubusercontent.com`, che senza autenticazione serve solo repo
pubblici. Sono asset di gioco, non dati sensibili — e' il codice che ha
senso tenere privato.

## Come e' organizzato

Una cartella per categoria, e dentro **una cartella per ogni pack**:

```
tracers/
└── red/
    ├── pack.zip        il file che viene installato
    ├── preview.png     l'immagine mostrata sulla card
    └── info.json       nome, descrizione, autore
```

Il nome dei file non conta (`red.zip`, `pack.zip`, `Red Tracers v2.zip`
vanno bene uguale): vengono riconosciuti dall'estensione. Conta la
**cartella**: una cartella = un pack.

## Aggiungere un pack

1. Crea la cartella: `tracers/red/`
2. Mettici dentro il pack (`.zip`, `.rar`, `.7z`, `.rpf`, `.dat`, ...)
3. Aggiungi un'immagine di anteprima (`.png` o `.jpg`)
4. Crea `info.json`:

```json
{
  "nome": "Red Tracers",
  "descrizione": "proiettili traccianti rossi",
  "autore": "nome dell'autore"
}
```

5. Rigenera il manifest e pubblica:

```bash
python ../packchanger-app/tools/build_manifest.py .
git add .
git commit -m "Aggiunto Red Tracers"
git push
```

Chi usa l'app lo vede al riavvio, o subito con **Aggiorna ora** in Home.
Nessuno deve reinstallare niente.

## Regole per categoria

| Categoria | Cosa deve contenere il pack |
|---|---|
| Mod Grafica (citizen) (`grafica`) | archivio con i file da versare in `citizen/` |
| Sound Arma (`weapon-sounds`) | archivio dei suoni (+ un `.wav` breve per l'anteprima) |
| Blood-FX (`blood-fx`) | un archivio contenente `bloodfx.dat` |
| Vegetation (`vegetation`) | archivio con i file da versare in `mods/` |
| Tracer (`tracers`) | archivio con i file da versare in `mods/` |

**Blood-FX**: l'archivio deve contenere un file `bloodfx.dat`, altrimenti
l'app rifiuta l'installazione (e' la protezione che evita di rompere
FiveM). `build_manifest.py` te lo segnala prima che tu faccia push.

**Sound Arma**: se aggiungi anche un breve file `.wav`, diventa
l'anteprima ascoltabile dentro l'app. I formati veri dei sound pack
(`.awc`, `.rpf`) nessun player di sistema sa aprirli, quindi senza un WAV
il pulsante "Ascolta" resta spento.

## Anteprime

Immagini quadrate, almeno 256x256. Vengono ridimensionate a 104x104
nell'app, quindi non serve che siano grandi: file leggeri = download piu'
rapidi per chi usa il programma.

## Non modificare manifest.json a mano

E' **generato** da `build_manifest.py`. Ogni modifica manuale viene persa
alla rigenerazione successiva: per cambiare nome o descrizione di un pack,
modifica il suo `info.json`.
