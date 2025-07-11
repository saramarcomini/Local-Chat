- Chat Local na Rede

Um projeto de chat em tempo real que funciona inteiramente em uma rede local, sem a necessidade de conexão com a internet. A aplicação utiliza um servidor Python com WebSockets para a comunicação e uma interface web básica em HTML e JavaScript.


- Funcionalidades

* **Chat em Tempo Real:** As mensagens são enviadas e recebidas instantaneamente por todos os clientes conectados.
* **Identificação de Usuário:** Ao entrar no chat, o usuário é solicitado a fornecer um nome.
* **Histórico de Mensagens:** Novos usuários recebem as últimas 20 mensagens do chat ao se conectarem.
* **Operação Local:** Roda em qualquer rede local (Wi-Fi, Ethernet), ideal para escritórios, casas ou eventos.
* **Leve e Simples:** Não requer frameworks complexos ou bancos de dados.


 - Vídeo de Demonstração

Assista a um vídeo rápido mostrando o chat em ação:

[**>> LINK PARA O VÍDEO AQUI <<**](https://youtu.be/JhxM4uyj2cE)


- Como Funciona

A aplicação é dividida em duas partes principais: o **Backend** (servidor em Python) e o **Frontend** (interface web).

### Backend (Servidor Python)

O script Python é o coração do projeto e executa duas tarefas simultaneamente:

1.  **Servidor HTTP (Porta 8080):** Utilizando os módulos `http.server` e `threading`, ele serve os arquivos estáticos (`index.html`, `script.js`, `styles.css`) para qualquer um que acesse seu endereço IP na rede local. Isso permite que os usuários carreguem a interface do chat em seus navegadores.

2.  **Servidor WebSocket (Porta 8000):** Este é o responsável pela comunicação em tempo real.
    * Quando um novo usuário se conecta, o servidor primeiro recebe o nome dele.
    * Em seguida, envia o histórico de mensagens recentes para esse novo usuário.
    * Quando um usuário envia uma mensagem, o servidor a recebe, formata com o nome do remetente (`Nome: Mensagem`) e a **transmite para todos os outros usuários conectados**.
    * Ele também gerencia a conexão e desconexão dos clientes.

### Frontend (HTML, CSS e JavaScript)

O frontend é a interface com a qual o usuário interage no navegador.

* **`index.html`:** Define a estrutura da página: um título, uma área para exibir as mensagens (um `textarea` somente leitura) e um campo para digitar uma nova mensagem.
* **`script.js`:** Contém toda a lógica do lado do cliente:
    * Ao carregar a página, pede o nome do usuário.
    * Estabelece uma conexão WebSocket com o servidor usando o endereço de host da página (`location.hostname`), tornando a conexão automática na rede local.
    * Quando uma mensagem é recebida do servidor, ela é adicionada à área de chat.
    * A função `enviar()` pega o texto digitado pelo usuário e o envia para o servidor através da conexão WebSocket.


- Como Executar

### Pré-requisitos

* **Python 3** instalado.
* A biblioteca `websockets` do Python.

### Passos

1.  **Salve os arquivos:** Certifique-se de que os três arquivos (`servidor.py`, `index.html`, `script.js`) estão na mesma pasta. Você pode nomear o arquivo Python como `servidor.py`.

2.  **Instale a dependência:** Se você ainda não tiver a biblioteca `websockets`, abra seu terminal ou prompt de comando e execute:
    ```bash
    pip install websockets
    ```

3.  **Inicie o servidor:** Navegue até a pasta onde salvou os arquivos e execute o script Python:
    ```bash
    python server.py
    ```
    Você verá mensagens no console indicando que os servidores HTTP e WebSocket estão rodando.

4.  **Encontre o seu IP Local:** Você precisará do endereço IP da máquina que está rodando o servidor na sua rede local.
    * **No Windows:** Abra o `cmd` e digite `ipconfig`. Procure pelo "Endereço IPv4".
    * **No macOS ou Linux:** Abra o terminal e digite `ifconfig` ou `ip addr`.

5.  **Acesse o Chat:** Em qualquer outro dispositivo (ou no mesmo) conectado à mesma rede, abra um navegador web (Chrome, Firefox, etc.) e acesse o seguinte endereço:
    ```
    http://<SEU_IP_LOCAL>:8080
    ```
    Substitua `<SEU_IP_LOCAL>` pelo endereço que você encontrou no passo anterior. Por exemplo: `http://192.168.1.10:8080`.

Pronto! A página do chat irá carregar, pedirá seu nome e você poderá começar a conversar com outras pessoas na mesma rede.
