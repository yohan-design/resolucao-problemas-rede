# 01 — Computador sem acesso à internet

## Situação
O computador está conectado à rede, mas não consegue acessar páginas ou outros serviços da internet.

## Possíveis causas
- Problema no cabo ou Wi-Fi;
- Adaptador de rede desativado;
- IP, máscara ou gateway incorretos;
- Falha no roteador;
- Problema de DNS;
- Falha no acesso externo.

## Diagnóstico
```cmd
ipconfig /all
ping 127.0.0.1
ping SEU_GATEWAY
ping 8.8.8.8
nslookup www.google.com
```

## Interpretação
O diagnóstico deve ser feito por etapas. Primeiro, verificar a configuração local. Depois, testar a pilha TCP/IP, o gateway, a conectividade externa e, por último, a resolução DNS.

## Solução
Corrigir a configuração encontrada, renovar o endereço por DHCP quando necessário, ajustar DNS e verificar o equipamento de rede. Depois, repetir os testes.

## Evidência
Adicionar um print do `ipconfig /all`, um do `ping` e, quando necessário, um do `nslookup`.
