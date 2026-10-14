# Configurações centralizadas

Repositório lido pelo **Config Server** da ATV4 de Sistemas Distribuídos.

Não é uma aplicação: aqui só moram arquivos de configuração. O Config Server
clona este repositório na inicialização e passa a servir estes valores aos
clientes, pela porta 8888.

## Arquivos

A convenção de nome é `{aplicação}-{perfil}.properties`, e é ela que faz o
roteamento: o cliente cujo `spring.application.name` é `cliente-vendas`, rodando
com o perfil `dev`, recebe o conteúdo de `cliente-vendas-dev.properties`.

| Arquivo | Serve |
| --- | --- |
| `cliente-vendas-dev.properties` | `cliente-vendas`, perfil `dev` |
| `cliente-estoque-dev.properties` | `cliente-estoque`, perfil `dev` |
| `cliente-relatorios-dev.properties` | `cliente-relatorios`, perfil `dev` |

Cada um define duas propriedades:

- `mensagem.boasvindas` — o texto que o cliente devolve em `GET /mensagem`
- `server.port` — a porta em que o cliente sobe

A porta vir daqui é proposital: é a prova de que a configuração foi mesmo
carregada do servidor. Sem ele no ar, os três clientes subiriam na 8080.

## Consultar

Com o Config Server rodando:

```
http://localhost:8888/cliente-vendas/dev
http://localhost:8888/cliente-estoque/dev
http://localhost:8888/cliente-relatorios/dev
```

## Alterar

Editar um arquivo aqui e commitar já muda o que o servidor entrega — ele lê o
repositório a cada requisição. Os clientes, porém, leem a configuração só na
inicialização, então é preciso reiniciá-los para ver a mudança.

---

Aplicação que consome estas configurações:
[atv4-config-server-temporario](https://github.com/Paulo-Henrique-RDL/atv4-config-server-temporario)
