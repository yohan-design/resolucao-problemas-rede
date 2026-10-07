# 03 — Problema de DNS

## Situação
O computador possui conectividade por IP, mas não consegue resolver nomes de domínio.

## Possíveis causas
Servidor DNS incorreto, indisponível ou cache DNS desatualizado.

## Diagnóstico
```cmd
ping 8.8.8.8
nslookup www.google.com
ipconfig /all
```

## Solução
Limpar o cache DNS:

```cmd
ipconfig /flushdns
```

Em uma rede de laboratório, pode ser necessário corrigir o servidor DNS configurado. Após a alteração, repetir o `nslookup`.

## Verificação final
```cmd
nslookup www.google.com
ping www.google.com
```
