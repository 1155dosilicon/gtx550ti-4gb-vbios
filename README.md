# VBIOS — GeForce GTX 550 Ti 4 GB (versão chinesa modificada)

Dump da VBIOS de uma **GTX 550 Ti de 4 GB** genérica vendida na China. A NVIDIA nunca lançou uma 550 Ti de 4 GB: são placas GF106 recondicionadas/modificadas. Se a sua é dessas e a BIOS corrompeu (ou você quer comparar), esta ROM pode ajudar.

*English summary below.*

## Identificação da placa

| Campo | Valor |
|---|---|
| GPU | GF106 (Fermi) — GeForce GTX 550 Ti |
| PCI ID | `10DE:1244`, subsystem `10DE:0939` (ID de referência NVIDIA, sem fabricante) |
| VRAM informada | 4096 MiB (nvidia-smi) |
| Versão da VBIOS | `70.26.41.00.00` |
| Produto / projeto | `GF106B Board - 14280010` / `1428-0010` |
| Board ID | `0xD119` |
| Chip SKU | 200 |
| Build Date | 02/16/16 |
| Modification Date | 02/03/26 |
| UEFI | Sim — GOP versão `0x10017`, assinado por "Microsoft Corporation UEFI CA 2011" |
| EEPROM | Macronix MX25L4005A (512 KB), ID `C2,2013` |

## Arquivo

`GTX550Ti-4GB-70.26.41.00.00.rom` — 122 368 bytes

- SHA-256: `659c0d61d578b3c43e3fb9a6ff47610cd81db967c1872f63782b95cec1efbc0d`
- MD5: `b0d6adb36c6752b20e17341d3d986f48`

Conteúdo (duas imagens PCI, checksums conferidos):

| Offset | Tamanho | Tipo |
|---|---|---|
| `0x0000` | 61 440 B | BIOS legada x86 (VGA) |
| `0xF000` | 60 928 B | Driver UEFI GOP x64 (última imagem) |

A 550 Ti original não tinha UEFI; esta tem GOP, então funciona com CSM desligado / boot UEFI puro.

Dump feito com `nvflash64 5.590.0` (versão patched por Vipeax) usando `nvflash64 --save`. A saída completa do `--version` está em [`nvflash-version.txt`](nvflash-version.txt).

## Como gravar (por sua conta e risco)

1. **Faça backup da sua BIOS antes:** `nvflash64 --save minha_bios.rom`
2. Confira se o PCI ID / subsystem da sua placa bate (`nvflash64 --version`).
3. Grave: `nvflash64 -6 GTX550Ti-4GB-70.26.41.00.00.rom` (`-6` ignora a diferença de subsystem ID, se houver).
4. Reinicie.

⚠️ Placas "4 GB" chinesas variam muito de memória (fabricante, quantidade de chips, straps). Gravar a BIOS de outra placa pode deixá-la sem vídeo. Se isso acontecer, dá para recuperar com uma segunda placa de vídeo / vídeo integrado ou um gravador SPI (CH341A) direto no chip MX25L4005A.

Testado funcionando com o driver NVIDIA 391.35 (último com suporte a Fermi) no Windows 11.

---

## English

VBIOS dump from a Chinese-market **GeForce GTX 550 Ti 4 GB** (GF106, PCI `10DE:1244`, subsystem `10DE:0939`, version `70.26.41.00.00`). NVIDIA never made a 4 GB 550 Ti, so these are modified boards. The ROM contains a legacy x86 image plus a UEFI GOP image, so the card works with pure UEFI boot (CSM off).

Dumped with `nvflash64 --save` (nvflash 5.590.0, patched). Always back up your own BIOS first and check that your card's IDs match. Flash with `nvflash64 -6 <file>.rom` at your own risk.
