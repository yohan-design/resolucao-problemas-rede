# Comandos de diagnóstico de rede — Windows

## ipconfig
Mostra a configuração de rede do computador.

```cmd
ipconfig
ipconfig /all
```

## ipconfig /release e /renew
Usados para liberar e solicitar novamente uma configuração IPv4 obtida por DHCP.

```cmd
ipconfig /release
ipconfig /renew
```

## ipconfig /flushdns
Limpa o cache local de resolução DNS.

```cmd
ipconfig /flushdns
```

## ping
Verifica se existe comunicação entre o computador e um destino.

```cmd
ping 127.0.0.1
ping SEU_GATEWAY
ping 8.8.8.8
```

## nslookup
Consulta o DNS e mostra informações sobre a resolução de nomes.

```cmd
nslookup www.google.com
```

## tracert
Exibe os saltos utilizados para alcançar um destino.

```cmd
tracert www.google.com
```

## arp -a
Exibe a tabela ARP armazenada localmente.

```cmd
arp -a
```

## netsh interface show interface
Mostra o estado das interfaces de rede.

```cmd
netsh interface show interface
```
