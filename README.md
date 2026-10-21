# tcp-port-scanner

**Estudos de segurança da informação e redes com Python e Bash.**

O projeto reúne exercícios para compreender o funcionamento de ferramentas de segurança. A implementação principal é um **scanner TCP didático**: recebe um alvo pela linha de comando e tenta estabelecer uma conexão nas portas **80 e 22**, exibindo aquelas que aceitam a conexão.

## Port scanner: como funciona

O arquivo [`PortScan/haknox.sh`](PortScan/haknox.sh) usa Bash para executar código Python 3. O fluxo é:

1. Receber o alvo no argumento obrigatório `-t`.
2. Criar um socket IPv4 (`AF_INET`) do tipo TCP (`SOCK_STREAM`).
3. Tentar uma conexão com `socket.connect_ex`, com timeout de 3 segundos por porta.
4. Exibir `[+]80 aberta` ou `[+]22 aberta` quando a conexão for aceita.
5. Exibir uma mensagem quando ocorrer uma exceção de socket.

As portas são verificadas **sequencialmente**, na ordem 80 e 22. A técnica é **TCP connect**: o sistema operacional gerencia o estabelecimento da conexão TCP.

## Tecnologias

- **Python 3:** lógica do scanner.
- **Biblioteca padrão:** `socket` para conexões de rede e `argparse` para a interface de linha de comando.
- **Bash:** script de entrada e execução do Python.
- **Conceitos:** IPv4, TCP, portas, resolução de nomes e timeout.

O scanner utiliza apenas módulos da biblioteca padrão do Python; não exige instalação de pacotes com `pip`.

## Executar

### Requisitos

- Ambiente com Bash, como Linux ou WSL.
- Python 3 disponível pelo comando `python3`.
- Um alvo próprio ou um ambiente de laboratório autorizado.

Na pasta raiz do repositório:

```bash
# Consultar a ajuda da linha de comando
bash PortScan/haknox.sh -h

# Verificar as portas 80 e 22 da própria máquina
bash PortScan/haknox.sh -t 127.0.0.1
```

O argumento `-t` aceita um endereço IPv4 ou um nome que possa ser resolvido para IPv4.

### Interpretar a saída

Se houver um serviço acessível na porta 80, a saída incluirá:

```text
[+]80 aberta
```

Essa é uma saída ilustrativa. O resultado depende dos serviços ativos e das condições da rede. Quando `connect_ex` retorna um código diferente de zero, o código atual não imprime uma classificação para a porta. Portanto, a ausência de uma linha não distingue porta fechada, filtrada ou timeout.

## Estrutura

```text
tcp-port-scanner/
├── PortScan/
│   ├── haknox.sh        # Scanner TCP com Python executado por Bash
│   └── aprendizado.sh   # Rascunho de estudo, ainda sem lógica de varredura
├── .gitattributes
├── LICENSE
└── README.md
```

Para executar o scanner, utilize `haknox.sh`. O arquivo `aprendizado.sh` é um rascunho incompleto.

## Escopo da versão atual

- Alvo único por execução e suporte a IPv4.
- Portas fixas no código: 80 e 22.
- Tentativas sequenciais, sem uso de threads.
- Saída no terminal, sem exportação de resultados.
- Sem identificação de serviços, versões ou vulnerabilidades.

O objetivo desta versão é exercitar sockets TCP, argumentos de linha de comando, tratamento de exceções e leitura de resultados de conexão.

## Próximas melhorias

Itens planejados, ainda não implementados:

- [ ] Permitir a escolha de portas e do timeout pela linha de comando.
- [ ] Apresentar os códigos de retorno e mensagens de erro de forma mais clara.
- [ ] Exportar resultados estruturados em JSON ou CSV.
- [ ] Adicionar testes em ambiente local controlado.
- [ ] Documentar exemplos reproduzíveis e decisões de implementação.

## Uso em laboratório

Utilize a ferramenta em sistemas próprios ou com autorização do responsável pelo ambiente.

## Autor

**Gustavo Henrique Xavier de Brito**  
[GitHub](https://github.com/GustavoHenrique-png) · [LinkedIn](https://www.linkedin.com/in/gustavohenriquexdebrito/)

## Licença

Este projeto está disponível sob a [licença MIT](LICENSE).
