# 04 — Cabo de rede desconectado ou com defeito

## Situação
O computador não detecta corretamente a conexão Ethernet ou apresenta conexão instável.

## Possíveis causas
Cabo desconectado, conector danificado, cabo com defeito, porta do switch/roteador com problema ou placa de rede desativada.

## Diagnóstico
Verificar fisicamente as duas pontas e os LEDs da porta, quando disponíveis.

```cmd
netsh interface show interface
ipconfig /all
ping SEU_GATEWAY
```

## Solução
Reconectar o cabo, testar outro cabo, testar outra porta e confirmar se o adaptador está habilitado.

## Verificação final
Repetir `ipconfig /all` e `ping SEU_GATEWAY`.
