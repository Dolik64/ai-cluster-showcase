# AI cluster — nasazení jazykového modelu

**Zprovoznění inference modelu se 70 miliardami parametrů na sdíleném univerzitním GPU clusteru.**

[Architektura a průchod](docs/demo.md) · [Podklady a stav](docs/evidence.md) · [English](README.md) · [Všechny projekty](https://github.com/Dolik64)

## Co jsem nastavoval

Na existujícím výukovém clusteru FEL ČVUT jsem připravoval prostředí pro provoz LLM: přidělení prostředků přes **Slurm**, Python a úložiště modelu, nasazení **NousResearch/Hermes-4-70B** pomocí **vLLM** a přístup k jeho API z notebooku přes SSH tunel. Součástí práce byla příprava lokálního Open WebUI a pozdější experiment se dvěma výpočetními uzly.

Mým příspěvkem bylo nastavení softwaru na uživatelské úrovni, rezervace prostředků, vzdálený přístup a řešení provozních problémů. Hardware, síť a správu samotného clusteru zajišťuje univerzita.

## Technické řešení

| Oblast | Moje práce |
| --- | --- |
| Výpočetní prostředky | Požadavek ve Slurmu na jeden uzel, 96 CPU a 16 GPU zařízení NVIDIA A16. |
| Nasazení modelu | Stažení Hermes-4-70B, příprava dočasného úložiště a cache, konfigurace vLLM. |
| Více GPU | Zdokumentovaná konfigurace BF16, tensor parallelism 8 a pipeline parallelism 2 v jednom uzlu. |
| Vzdálený přístup | SSH tunel přes přihlašovací uzel a autentizovaný požadavek na seznam modelů. |
| Rozhraní | Instalace lokálního Open WebUI a příprava připojení. |
| Další experiment | Stažení stejné revize modelu na dva uzly pro experiment s Qwenem a diagnostika startu. |

Počet 16 označuje GPU zařízení viditelná pro běhové prostředí, nikoli 16 fyzických karet. Nastavení TP8 × PP2 se vztahuje k popsanému spuštění v jednom uzlu.

## Doložené výsledky

- **Hermes API odpovídalo:** uložená odpověď autentizovaného `/v1/models` uvádí model `hermes`.
- **Probíhala inference:** historické logy vLLM zaznamenávají generování. Nejde o řízený benchmark rychlosti.
- **Open WebUI bylo nainstalováno:** podklady obsahují úspěšnou instalaci; úplný průchod chatem v prohlížeči není doložen.
- **Příprava dvou uzlů se dokončila:** model byl stažen na oba uzly. Zachycený start následně skončil chybějící knihovnou `libcudart.so.13`; úspěšnou distribuovanou inferenci tyto záznamy nepotvrzují.

Jde o případovou studii provedeného nasazení. [Průchod](docs/demo.md) vysvětluje postup a [přehled podkladů](docs/evidence.md) rozlišuje skutečné výpisy od poznámek a návrhů. Veřejné trvale běžící demo zde není.

**Technologie:** Linux · Slurm · Python · CUDA · vLLM · Hugging Face Hub · SSH · Open WebUI · Docker

Tento repozitář obsahuje prezentační dokumentaci a schéma. Neobsahuje zdrojový kód aplikací, spustitelné nasazovací skripty, surové chaty, přístupové údaje ani interní adresy.
