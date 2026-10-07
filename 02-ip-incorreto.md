# 02 — Endereço IP incorreto

## Situação
O computador possui um endereço IP que não corresponde à rede utilizada.

## Possíveis causas
Configuração manual errada, DHCP indisponível ou máscara/gateway incompatíveis.

## Diagnóstico
```cmd
ipconfig
ipconfig /all
```

Observe IPv4, máscara, gateway, DHCP e DNS. Um endereço na faixa `169.254.x.x` pode indicar que o computador não recebeu uma configuração IPv4 válida por DHCP.

## Solução
Para redes com DHCP:

```cmd
ipconfig /release
ipconfig /renew
```

Para IP manual, corrigir o IPv4, a máscara e o gateway conforme o plano de endereçamento da rede.

## Verificação final
```cmd
ping SEU_GATEWAY
```
