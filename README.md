# Resolução de Problemas de Rede

**Disciplina:** Redes de Computadores  
**Professor:** Álvaro Machado Junior  
**Turma:** 3º Ano Técnico em Informática  
**Entrega:** 07/10/2026

## 1. Sobre o projeto

Este projeto apresenta situações comuns de problemas em redes de computadores e descreve uma metodologia para identificar suas causas e aplicar soluções. O objetivo é desenvolver a capacidade de observar sintomas, realizar testes, interpretar resultados e corrigir falhas de conectividade.

Foram estudados cinco problemas:

1. Computador sem acesso à internet;
2. Endereço IP incorreto;
3. Problema de DNS;
4. Cabo de rede desconectado ou com defeito;
5. Conflito de endereço IP.

Para cada situação são apresentados: o que está acontecendo, possíveis causas, procedimentos e comandos de diagnóstico e formas de solucionar o problema.

## 2. Ferramentas e comandos utilizados

| Comando/Ferramenta | Finalidade |
|---|---|
| `ipconfig` | Exibe as configurações de IPv4, máscara, gateway e DNS no Windows. |
| `ipconfig /all` | Mostra informações detalhadas dos adaptadores de rede, incluindo DHCP, DNS e endereço físico. |
| `ipconfig /release` | Libera a configuração IPv4 obtida por DHCP. |
| `ipconfig /renew` | Solicita uma nova configuração IPv4 ao servidor DHCP. |
| `ipconfig /flushdns` | Limpa o cache local de resolução de nomes DNS. |
| `ping` | Testa a comunicação com outro dispositivo ou endereço e ajuda a verificar conectividade. |
| `nslookup` | Consulta o DNS para verificar a resolução de nomes para endereços IP. |
| `tracert` | Mostra os saltos percorridos pelos pacotes até um destino. |
| `arp -a` | Exibe a tabela ARP conhecida pelo computador, relacionando IPs e endereços MAC. |
| `netsh interface show interface` | Mostra o estado das interfaces de rede no Windows. |

> **Observação:** Os resultados dos comandos dependem da rede utilizada durante os testes. Por isso, os prints devem ser feitos no computador do aluno e colocados na pasta `imagens/`.

## 3. Metodologia geral de diagnóstico

Uma forma organizada de resolver problemas de rede é começar pelos elementos mais próximos do computador e avançar até a internet. Primeiro, verifica-se o cabo ou o Wi-Fi e o estado do adaptador. Em seguida, observa-se a configuração de IP, máscara, gateway e DNS. Depois, são feitos testes de conectividade com `ping` e de resolução de nomes com `nslookup`. Por fim, `tracert` pode ajudar a identificar em qual trecho do caminho existe uma falha.

## 4. Problemas analisados

### 4.1 Computador sem acesso à internet

**O que está acontecendo**  
O computador está conectado à rede, mas não consegue acessar sites ou outros serviços da internet.

**Possíveis causas**  
A falha pode estar relacionada à conexão física, configuração de IP, gateway, DNS, adaptador de rede ou ao próprio acesso à internet.

**Como identificar**

```cmd
ipconfig /all
ping 127.0.0.1
ping SEU_GATEWAY
ping 8.8.8.8
nslookup www.google.com
```

O primeiro teste verifica as informações da interface. O `ping 127.0.0.1` verifica a pilha de rede local. O teste ao gateway verifica a comunicação com o roteador. O `ping 8.8.8.8` verifica se existe comunicação com um endereço externo. O `nslookup` verifica se nomes de domínio estão sendo resolvidos pelo DNS.

**Como interpretar**  
Se o computador não consegue alcançar o gateway, o problema tende a estar na rede local ou na configuração do equipamento. Se o gateway responde e `8.8.8.8` não responde, pode existir uma falha no acesso externo. Se `8.8.8.8` responde, mas `www.google.com` não é resolvido, a suspeita principal é DNS.

**Como resolver**  
Verificar o cabo ou Wi-Fi, confirmar IP, máscara, gateway e DNS, renovar a configuração DHCP, limpar o cache DNS e testar novamente. Quando necessário, reiniciar o adaptador ou o roteador.

---

### 4.2 Endereço IP incorreto

**O que está acontecendo**  
O computador recebeu uma configuração de IP que não pertence à rede correta ou que não permite a comunicação com os demais dispositivos.

**Possíveis causas**  
Configuração manual incorreta, DHCP indisponível, máscara errada, gateway incorreto ou parâmetros de rede incompatíveis.

**Como identificar**

```cmd
ipconfig
ipconfig /all
```

Compare o IPv4, a máscara e o gateway com a configuração esperada da rede.

**Exemplo**  
Supondo uma rede `192.168.10.0/24`, um computador configurado como `192.168.20.15` está em uma rede diferente e pode não conseguir se comunicar corretamente com os dispositivos da rede `192.168.10.0/24`.

Também pode ser observado um endereço automático na faixa `169.254.x.x`, o que geralmente indica que o Windows não conseguiu obter uma configuração IPv4 válida por DHCP.

**Como resolver**

Se a rede utiliza DHCP:

```cmd
ipconfig /release
ipconfig /renew
```

Se a rede utiliza IP manual, corrigir IPv4, máscara e gateway de acordo com o plano de endereçamento adotado.

Depois, testar:

```cmd
ping SEU_GATEWAY
```

---

### 4.3 Problema de DNS

**O que está acontecendo**  
O computador consegue alcançar a rede ou até a internet por endereço IP, mas não consegue abrir sites usando nomes como `www.google.com`.

**Possíveis causas**  
Servidor DNS indisponível, endereço DNS configurado incorretamente ou cache DNS desatualizado.

**Como identificar**

```cmd
ping 8.8.8.8
nslookup www.google.com
ipconfig /all
```

Uma comparação útil é verificar se o `ping 8.8.8.8` funciona enquanto a resolução de `www.google.com` falha. Nesse cenário, a conectividade IP pode estar funcionando enquanto a resolução de nomes apresenta problema.

**Como resolver**

Primeiro, limpar o cache local:

```cmd
ipconfig /flushdns
```

Depois, verificar a configuração de DNS. Em uma rede de laboratório, podem ser utilizados servidores DNS conhecidos, como `8.8.8.8` ou `1.1.1.1`, desde que isso esteja de acordo com a política da rede utilizada.

Depois do ajuste, repetir:

```cmd
nslookup www.google.com
ping www.google.com
```

---

### 4.4 Cabo de rede desconectado ou com defeito

**O que está acontecendo**  
O computador não detecta corretamente a conexão Ethernet ou apresenta conexão instável.

**Possíveis causas**  
Cabo desconectado, conector mal encaixado, cabo danificado, porta do switch/roteador com problema ou placa de rede desativada.

**Como identificar**

Verifique fisicamente se o cabo está conectado nas duas pontas e observe os LEDs da porta de rede, quando disponíveis.

No Windows, também é possível verificar as interfaces:

```cmd
netsh interface show interface
ipconfig /all
```

Depois, testar a conectividade:

```cmd
ping SEU_GATEWAY
```

**Como resolver**  
Reconectar o cabo, testar outro cabo de rede, testar outra porta do switch/roteador e confirmar se o adaptador Ethernet está habilitado. Após a correção, executar novamente `ipconfig` e `ping`.

---

### 4.5 Conflito de endereço IP

**O que está acontecendo**  
Dois dispositivos tentam utilizar o mesmo endereço IPv4 na mesma rede. Isso pode provocar perda de comunicação, instabilidade e mensagens de conflito de IP.

**Possíveis causas**  
Configuração manual repetida, reserva DHCP mal planejada ou uso simultâneo de IP estático e DHCP sem organização.

**Como identificar**

Primeiro, descobrir o próprio IP:

```cmd
ipconfig
```

Depois, consultar a tabela ARP:

```cmd
arp -a
```

Também podem ser realizados testes para comparar o comportamento da rede e identificar quando o problema aparece. Em ambientes controlados, é possível desligar temporariamente um dispositivo suspeito e verificar se a comunicação volta ao normal.

**Como resolver**  
Garantir que cada dispositivo possua um endereço IPv4 exclusivo. Em redes com DHCP, corrigir reservas ou escopos quando necessário. Em endereçamento manual, escolher um IP disponível dentro da faixa correta e evitar reutilização de endereços.

Após a correção:

```cmd
ipconfig /renew
ping SEU_GATEWAY
```

## 5. Fluxo de diagnóstico

```text
Início
  ↓
Verificar cabo/Wi-Fi e adaptador
  ↓
Executar ipconfig /all
  ↓
O IP, máscara, gateway e DNS estão corretos?
  ├── Não → Corrigir configuração / renovar DHCP
  └── Sim
       ↓
   ping 127.0.0.1
       ↓
   ping SEU_GATEWAY
       ↓
   ping 8.8.8.8
       ↓
   nslookup www.google.com
       ↓
   Problema identificado
       ↓
   Aplicar correção
       ↓
   Repetir os testes
       ↓
     Fim
```

## 6. Testes realizados

Os testes devem ser executados no computador do aluno, preferencialmente no Prompt de Comando (CMD). Os resultados devem ser capturados em print e adicionados à pasta `imagens/`.

### Teste 1 — Configuração de rede

```cmd
ipconfig /all
```

**Objetivo:** verificar IPv4, máscara, gateway, DHCP, DNS e adaptador.

**Print:** `imagens/teste-01-ipconfig.png`

### Teste 2 — Conectividade local

```cmd
ping SEU_GATEWAY
```

**Objetivo:** verificar se o computador alcança o roteador/gateway da rede.

**Print:** `imagens/teste-02-ping-gateway.png`

### Teste 3 — Conectividade externa por IP

```cmd
ping 8.8.8.8
```

**Objetivo:** verificar conectividade com um endereço IP externo.

**Print:** `imagens/teste-03-ping-externo.png`

### Teste 4 — Resolução DNS

```cmd
nslookup www.google.com
```

**Objetivo:** verificar se o DNS consegue transformar o nome do domínio em endereço IP.

**Print:** `imagens/teste-04-nslookup.png`

### Teste 5 — Caminho até o destino

```cmd
tracert www.google.com
```

**Objetivo:** observar os saltos entre o computador e o destino e auxiliar na localização de falhas no caminho.

**Print:** `imagens/teste-05-tracert.png`

## 7. Documentação das soluções

A solução de um problema de rede deve ser aplicada somente depois de identificar a causa provável. Reiniciar equipamentos pode resolver algumas falhas temporárias, mas não substitui o diagnóstico. O ideal é registrar o sintoma, realizar os testes, aplicar uma correção específica e repetir os testes para confirmar o resultado.

| Problema | Testes principais | Solução mais comum |
|---|---|---|
| Sem internet | `ipconfig`, `ping`, `nslookup` | Corrigir conectividade, gateway ou DNS |
| IP incorreto | `ipconfig /all` | Corrigir IP ou renovar DHCP |
| DNS | `nslookup`, `ipconfig /flushdns` | Corrigir DNS e limpar cache |
| Cabo | inspeção física, `netsh`, `ping` | Reconectar/substituir cabo ou trocar porta |
| Conflito de IP | `ipconfig`, `arp -a` | Definir IP exclusivo e revisar DHCP |

## 8. Conclusão

A resolução de problemas de rede exige uma sequência lógica de verificação. Comandos como `ipconfig`, `ping`, `nslookup`, `tracert` e `arp` permitem observar diferentes partes do funcionamento da rede e ajudam a reduzir tentativas aleatórias de correção. Ao relacionar os sintomas aos resultados dos testes, é possível identificar a causa provável, aplicar uma solução e confirmar se o serviço voltou a funcionar.

Este projeto demonstra, portanto, uma abordagem prática para o diagnóstico de problemas comuns em redes de computadores.

## 9. Estrutura do repositório

```text
Projeto_Resolucao_Problemas_Rede/
├── README.md
├── docs/
│   ├── 01-sem-acesso-internet.md
│   ├── 02-ip-incorreto.md
│   ├── 03-problema-dns.md
│   ├── 04-cabo-rede.md
│   ├── 05-conflito-ip.md
│   └── comandos-diagnostico.md
├── testes/
│   └── roteiro-de-testes.md
└── imagens/
    └── README.md
```

## 10. Responsável

**Yohan Teixeira Rodrigues**  
**3º Ano Técnico em Informática**
