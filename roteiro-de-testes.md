# Roteiro de testes para os prints

Execute os comandos no Prompt de Comando (CMD) e substitua `SEU_GATEWAY` pelo endereço do gateway da sua rede, conforme mostrado no `ipconfig`.

## Teste 1 — Configuração
```cmd
ipconfig /all
```
Print sugerido: `../imagens/teste-01-ipconfig.png`

## Teste 2 — Gateway
```cmd
ping SEU_GATEWAY
```
Print sugerido: `../imagens/teste-02-ping-gateway.png`

## Teste 3 — Internet por IP
```cmd
ping 8.8.8.8
```
Print sugerido: `../imagens/teste-03-ping-externo.png`

## Teste 4 — DNS
```cmd
nslookup www.google.com
```
Print sugerido: `../imagens/teste-04-nslookup.png`

## Teste 5 — Rota
```cmd
tracert www.google.com
```
Print sugerido: `../imagens/teste-05-tracert.png`

## Checklist
- [ ] Executei os 5 testes.
- [ ] Tirei os prints.
- [ ] Coloquei os prints na pasta `imagens`.
- [ ] Conferi se os arquivos abrem corretamente.
- [ ] Enviei o conteúdo para o repositório GitHub.
