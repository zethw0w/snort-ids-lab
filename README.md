# Snort IDS — Análise de snort.log

Desafio DFIR do módulo **Snort** (Defense Operations / FIAP): o IDS Snort gerou um `snort.log` (formato pcap/tcpdump) que precisa ser analisado para responder a duas perguntas, no formato `FIAP{id_referer}`.

## Análise

`snort.log` é uma captura pcap de 43 pacotes (tráfego HTTP para `www.ethereal.com` + anúncios do Google). Analisado com `tshark`.

| Pergunta | Resposta | Como |
|---|---|---|
| ID do 10º pacote | **`0xc0a1`** | `tshark -Y "frame.number==10" -V` → campo `Identification` do IP |
| Referer do 4º pacote | **`http://www.ethereal.com/development.html`** | `tshark -Y "frame.number==4"` → cabeçalho HTTP Referer |

**Resposta final:** `FIAP{0xc0a1_http://www.ethereal.com/development.html}`

## Sobre o Snort
O repositório também documenta a configuração do Snort como IPS/IDS (regras em `/etc/snort/rules`, modo sniffer/verbose, criação de regras `alert icmp`/`alert tcp`), conforme o roteiro do curso.

## Estrutura
`prints/` — tipo do arquivo, lista de pacotes, ID do 10º pacote, Referer do 4º, resposta.
