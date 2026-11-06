# MazatleraOT Client (CrystalOTC, preparado para MazatleraOT)

Cliente basado en CrystalOTC (Jattartajjar/CrystalOTC, commit 6b57ea7, main).
Trabajado en el VPS en /home/benny/CrystalOTC (NO en mazatleraot, solo se mandara el zip final).

## Version: a que llega
- CrystalOTC original es protocolo **15.30** (1530): README, init.lua
  original con protocol = 1530, assets en data/things/1530/.
- Este cliente, preparado para MazatleraOT, esta configurado a protocolo
  **1525**.
- 1525 se anadio a getSupportedClients() en modules/gamelib/game.lua
  (la lista llegaba hasta 1521). El codigo ya tenia ramas para 15.25
  (>=1520, crosshair, dust u8, etc.) y el techo setLastSupportedVersion(1530)
  lo permite. No esta probado en juego todavia con 1525.
- OJO: el server MazatleraOT actual sigue en 1511 (CLIENT_VERSION = 1511).
  Cliente 1525 y server 1511 no se conectan entre si; el server tambien
  tendra que subirse a 1525, o el cliente es para cuando eso pase.

## Que se cambio para MazatleraOT (init.lua)
- Nombre: MazatleraOT / mazatleraot / MazatleraOT
- Login: https://mazatleraot.com/login.php, port 443, protocol 1525, httpLogin = true
- Techo de version: setLastSupportedVersion(1530) se deja, permite 1525
  y una futura subida a 15.30.
- Website en entergame.otmod: https://mazatleraot.com

## Assets que FALTAN (no vienen en el repo)
- Assets 1525 INSTALADOS (2026-11-06): data/things/1525/ con 6,031
  archivos de zimbadev/gameclient release 15.25.3a4a52 (appearances,
  catalog-content.json, staticdata, staticmapdata, 4,927 sprites,
  minimap y satellite). Verificado: los 4,933 archivos del catalogo
  estan todos presentes, faltan 0.
  - Para 1530 (original): data/things/1530/ + 1530_mapview/, del Google
    Drive del README de CrystalOTC (no instalados).
- Sin assets el cliente no carga el mapa/sprites y da error
  "Things are not loaded". No trae data/things/1525_mapview/ (solo
  afecta la vista de mapa de la Cyclopedia, no el juego).

## Como compilar (Windows, lo que necesita el cliente)
- Visual Studio 2022 (v143), vcpkg con VCPKG_ROOT.
- msbuild vc18\otclient.vcxproj /p:Configuration=DirectX /p:Platform=x64
- Sale CrystalOTC.exe en la raiz (renombrar a MazatleraOT.exe si se quiere).
- Renderer: renderBackend = vulkan o gl en config.ini.
- Vulkan es solo Windows; en Linux usa OpenGL (CMake/Dockerfile en el repo).

## Server
- MazatleraOT: mazatleraot.com, juego 7171/7172, web https://mazatleraot.com/
- Si el server se sube a 15.30 en el futuro, cambiar protocol = 1530 en
  init.lua y poner assets data/things/1530/.

## Zip de prueba Windows (2026-11-06)
- Compilado Windows SI existe: CrystalOTC-windows.zip, release "latest"
  de Jattartajjar/CrystalOTC, 2026-08-17, commit cccab80, 576 MB, con
  CrystalOTC.exe + init.lua + data + modules + mods. NO trae assets.
- Zip de prueba armado en /home/benny/MazatleraOT-1525-test.zip:
  ese exe precompilado + archivos MazatleraOT de este repo (init.lua
  1525/tibiaserver, game.lua con 1525, entergame) + data/things/1525/.
  No hace falta compilar para probar; para compilar desde cero hace
  falta VS2022 + vcpkg en Windows.
- OJO: server MazatleraOT sigue en 1511, cliente 1525 no entrara al
  juego hasta que el server suba a 1525.
