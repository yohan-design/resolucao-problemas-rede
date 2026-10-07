# 05 — Conflito de endereço IP

## Situação
Dois dispositivos da mesma rede utilizam o mesmo endereço IPv4.

## Possíveis causas
Dois IPs manuais iguais, reserva DHCP incorreta ou falta de organização do plano de endereçamento.

## Diagnóstico
```cmd
ipconfig
arp -a
```

O `arp -a` mostra associações IP/MAC conhecidas pelo computador e pode ajudar na investigação. A confirmação deve ser feita comparando os dispositivos e o plano de endereçamento.

## Solução
Garantir um endereço IPv4 exclusivo para cada dispositivo. Em redes DHCP, revisar reservas e faixa de distribuição. Em redes com IP manual, escolher endereços livres e documentados.

## Verificação final
```cmd
ipconfig /renew
ping SEU_GATEWAY
```
