# TryHackMe — Pre-Security: Hardware e Processo de Boot

## Os componentes do PC comparados ao corpo humano

**Placa-mãe** — o "esqueleto e sistema nervoso" do
computador. Segura os componentes no lugar e conecta
tudo: CPU socket, slots de RAM, slots de expansão e
várias portas. Todo o resto se conecta através dela.

**CPU (processador)** — comparável à parte do cérebro
que executa instruções: somar números, processar
comandos, etc. A CPU faz isso pelo computador inteiro.

**RAM** — comparável à memória de curto prazo. Armazena
dados que a CPU precisa acessar rapidamente. É volátil
— quando a energia desliga, a memória se perde. RAM
moderna usa tecnologias como DDR5/DDR6 pra mais
velocidade e performance.

**SSDs e HDDs** — dispositivos de armazenamento,
comparáveis à memória de longo prazo. HDDs usam peças
móveis, o que limita a performance. SSDs não têm
partes móveis e usam chips de memória, sendo bem mais
rápidos — mas HDDs continuam populares pela grande
capacidade a baixo custo. Conectam via SATA ou slots
PCI Express.

**Adaptador de rede** — semelhante à corda vocal:
usado pra comunicação com outros sistemas. Existe em
versões com e sem fio, geralmente integrado à placa-mãe
mas também pode ser adicionado como placa de expansão,
conectando via slots PCI Express.

**Fonte de alimentação (PSU)** — como o coração que
bombeia energia pra todos os componentes. Se os
componentes precisam de mais força do que o PSU
fornece, o sistema falha. Recebe energia da tomada e
distribui via conectores como o principal da
placa-mãe e conectores Molex.

**Placa de vídeo** — comparável ao córtex visual do
cérebro. Recebe informações do sistema operacional e
programas, processa e envia dados visuais pro monitor.
Conecta via PCI Express.

**Dispositivos de entrada e saída** — equivalem aos
sentidos. Entrada: teclado, microfone, mouse, scanner.
Saída: monitor, impressora, alto-falante. Conectores
comuns: USB, HDMI, DisplayPort.

---

## Processo de inicialização do PC

**1. Botão liga**
Sinal enviado pro PSU (fonte de alimentação) — a
energia começa a fluir pros componentes.

**2. Firmware inicia (UEFI)**
UEFI = *Unified Extensible Firmware Interface*.
Gerencia a inicialização de todos os componentes.
O BIOS fazia a mesma função antes, mas foi substituído
pelo UEFI.

**3. POST (Power-On Self Test)**
Teste automático de todos os componentes — verifica
se estão presentes, configurados e funcionando. Se
algo falha, emite sinais de alarme.

**4. Seleção do dispositivo de boot**
O UEFI tem uma lista ordenada de dispositivos e busca
onde está a rotina de boot do sistema operacional.

**5. Bootloader inicia**
Transfere o SO do dispositivo de boot pra RAM. Depois
da transferência, o UEFI passa o controle dos
componentes pro sistema operacional.

```
PSU → UEFI → POST → Boot Device → Bootloader → SO na RAM
```
