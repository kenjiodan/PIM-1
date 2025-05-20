# PIM-1

**Grupo do PIM**<br><br>
 
Daniel Kenji Peris Silva - F3640G6<br> 
Edmundo Silva dos Santos Junior - H717HA2<br>
Gustavo Feitosa da Costa Sabino - R827858<br>
Renan Vitor de Brito Florencio - H5814J8<br>
Stephany Cleise Souza Melgueiro - R8492G4<br>
Yasmin Dantas de Souza - F360172<br>

## Documentação do Sistema de Análise de Dados de Usuários  

 

**2. Visão Geral do Sistema**

O sistema opera através de uma interface de linha de comando (CLI), guiando o usuário por um menu de opções para interagir com as funcionalidades. As principais capacidades incluem:

* Adição de novos registros de usuários.
* Carregamento de dados de usuários previamente armazenados em um arquivo Excel.
* Cálculo e exibição de estatísticas descritivas (média, moda, mediana) para atributos numéricos dos usuários.
* Persistência dos dados em formato Excel para consultas e análises futuras.

**3. Arquitetura do Sistema**

O sistema é estruturado em módulos funcionais implementados como funções em Python. A interação com o usuário ocorre diretamente no terminal. A persistência dos dados é gerenciada através da biblioteca `openpyxl` para leitura e escrita em arquivos Excel. Cálculos estatísticos são realizados utilizando a biblioteca padrão `statistics` do Python. A manipulação de diretórios é feita com o módulo `os`.

**4. Componentes e Funcionalidades**

**4.1. `limpar_tela()`**

* **Descrição:** Função responsável por limpar a tela do terminal, proporcionando uma interface mais organizada para o usuário a cada nova interação com o menu ou funcionalidade.
* **Tecnologias:** Módulo `os` do Python (`os.system('cls')` para Windows, `os.system('clear')` para outros sistemas).

**4.2. `adicionar_usuario(dados)`**

* **Descrição:** Permite a inclusão de um novo usuário no sistema. Solicita ao usuário o nome e a idade. O número de acessos é automaticamente definido como 1, e o tempo de uso como 0. Os dados do novo usuário são adicionados à estrutura de dados na memória.
* **Parâmetros:**
    * `dados`: Uma lista Python de dicionários, onde cada dicionário representa um usuário.
* **Interação:** Através de prompts no terminal (`input()`).
* **Atualização de Dados:** Modifica a lista `dados` adicionando um novo dicionário de usuário.

**4.3. `carregar_dados_excel()`**

* **Descrição:** Lê os dados dos usuários armazenados no arquivo Excel (`dados_usuarios.xlsx`). A função lida com a ausência do arquivo e com possíveis inconsistências no cabeçalho.
* **Localização do Arquivo:** Definida pela variável global `NOME_ARQUIVO_EXCEL` (dentro da pasta `dados_excel`).
* **Tecnologias:** Biblioteca `openpyxl`.
* **Retorno:** Uma lista de dicionários contendo os dados dos usuários carregados do Excel. Retorna uma lista vazia em caso de erro ou arquivo não encontrado.

**4.4. `salvar_dados_excel(dados)`**

* **Descrição:** Persiste os dados dos usuários (contidos na lista `dados`) em um arquivo Excel (`dados_usuarios.xlsx`). Cria o arquivo e a pasta se não existirem, ou sobrescreve o arquivo existente.
* **Localização do Arquivo:** Definida pela variável global `NOME_ARQUIVO_EXCEL`.
* **Tecnologias:** Biblioteca `openpyxl`.
* **Parâmetros:**
    * `dados`: A lista de dicionários de usuários a serem salvos.

**4.5. `calcular_estatisticas(dados)`**

* **Descrição:** Realiza cálculos estatísticos (média, mediana e moda) para os atributos numéricos (idade, acessos, tempo de uso) presentes na lista de dados de usuários. Os resultados são exibidos no terminal com uma breve explicação de cada cálculo.
* **Tecnologias:** Biblioteca `statistics` do Python (`mean()`, `median()`, `mode()`).
* **Parâmetros:**
    * `dados`: A lista de dicionários de usuários para análise.
* **Saída:** Impressão dos resultados estatísticos no terminal.

**4.6. `exibir_menu()`**

* **Descrição:** Apresenta o menu principal do sistema ao usuário no terminal, listando as opções disponíveis. Garante que apenas opções válidas sejam aceitas através de tratamento de erros.
* **Interação:** Através de `print()` para exibir o menu e `input()` para receber a escolha do usuário.
* **Retorno:** Uma string representando a opção selecionada pelo usuário.

**4.7. `main()`**

* **Descrição:** Função principal que inicia e controla o fluxo de execução do sistema. Mantém a lista de dados dos usuários na memória, exibe o menu, recebe a entrada do usuário e chama as funções apropriadas com base na escolha. O loop principal continua até que o usuário opte por sair.
* **Gerenciamento de Dados:** Inicializa e atualiza a lista `dados_usuarios`.
* **Controle de Fluxo:** Utiliza um loop `while` para manter o sistema em execução até que o usuário escolha sair.

**5. Persistência de Dados**

Os dados são armazenados em um arquivo Excel (`dados_usuarios.xlsx`) localizado dentro da pasta `dados_excel`. A biblioteca `openpyxl` é utilizada para:

* **Escrita:** Criar o arquivo (e a pasta, se necessário) e escrever os dados dos usuários em linhas, com a primeira linha contendo os cabeçalhos ("nome", "idade", "acessos", "tempo\_uso").
* **Leitura:** Abrir o arquivo e ler os dados linha por linha, convertendo cada linha em um dicionário Python representando um usuário.

**6. Interação com o Usuário**

A interação com o sistema é feita exclusivamente através da linha de comando. O usuário navega pelo sistema através de um menu textual, digitando o número correspondente à opção desejada. O sistema fornece prompts claros para entrada de dados (nome e idade ao adicionar um usuário) e exibe mensagens informativas sobre o sucesso ou falha das operações, bem como os resultados das análises estatísticas.

**7. Considerações sobre a Implementação**

* **Automatização:** O número de acessos é inicializado em 1 e o tempo de uso em 0 para novos usuários, simulando uma coleta automática básica no momento do registro. Em um sistema real, esses dados seriam rastreados dinamicamente.
* **Análise Estatística:** A análise se limita a média, moda e mediana. Análises mais complexas não estão implementadas.
* **Tratamento de Erros:** O sistema inclui tratamento básico de erros para entradas de usuário e operações de arquivo, mas pode ser expandido para lidar com cenários mais complexos.
* **Interface:** A interface é puramente textual, focada na funcionalidade essencial para atender aos requisitos do projeto.

**8. Como Executar o Sistema**

1.  Certifique-se de ter o Python instalado em seu sistema.
2.  Instale a biblioteca `openpyxl` executando `pip install openpyxl` no terminal.
3.  Salve o código Python em um arquivo (por exemplo, `analise_dados.py`).
4.  Execute o arquivo Python no terminal usando o comando `python analise_dados.py`.
5.  Siga as instruções do menu para interagir com o sistema.

Esta documentação fornece uma visão detalhada da estrutura, funcionalidades e operação do Sistema de Análise de Dados de Usuários em Python.
