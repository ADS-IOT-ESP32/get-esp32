# ESP32-CAM com ESP-IDF — GPIO e Varredura Wi-Fi

Projeto desenvolvido na disciplina de **Internet das Coisas**, da **Universidade Federal do Ceará (UFC)**, com o objetivo de configurar o ambiente de desenvolvimento da ESP32-CAM utilizando o **ESP-IDF** e realizar testes básicos de programação e comunicação com a placa.

Neste repositório estão os dois experimentos preservados pelo grupo:

- **GPIO Blink:** controle de uma saída digital no GPIO 4;
- **Wi-Fi Scan:** varredura das redes Wi-Fi disponíveis no ambiente.

## 🎯 Objetivo

Compreender o fluxo básico de desenvolvimento para sistemas embarcados utilizando a ESP32-CAM, passando pelas etapas de configuração do ambiente, compilação, gravação e execução de programas na placa.

Os testes permitiram trabalhar com dois recursos fundamentais da ESP32:

1. controle de GPIO;
2. comunicação Wi-Fi.

## 👥 Integrantes

- Aurelice
- Anderson
- Pedro Willy
- Talyson
- Yngrid

## 🛠️ Ferramentas utilizadas

- **ESP32-CAM**
- **Cabo USB**
- **ESP-IDF v6.1**
- **ESP-IDF PowerShell**
- **Windows 11**

## 📁 Estrutura do repositório

```text
.
├── README.md
├── .gitignore
├── gpio_blink/
│   ├── CMakeLists.txt
│   └── main/
│       ├── CMakeLists.txt
│       └── blink_main.c
├── wifi_scan/
│   ├── CMakeLists.txt
│   ├── main/
│   │   ├── CMakeLists.txt
│   │   ├── Kconfig.projbuild
│   │   ├── idf_component.yml
│   │   └── scan.c
│   └── README.md
└── slides/
    └── apresentacao-esp32.pdf
```

> As pastas `build/` não devem ser adicionadas ao repositório, pois são geradas automaticamente pelo ESP-IDF durante a compilação.

## 🔌 Projeto 1 — GPIO Blink

O projeto `gpio_blink` configura o **GPIO 4** como saída digital e alterna seu estado a cada segundo.

Durante a execução, o terminal também apresenta as mensagens:

```text
LED ligado
LED desligado
```

O trecho principal do programa utiliza:

```c
#define LED_GPIO GPIO_NUM_4
```

e alterna o nível lógico do pino utilizando `gpio_set_level()`.

## 📡 Projeto 2 — Wi-Fi Scan

O projeto `wifi_scan` inicializa a ESP32 em modo **Station (STA)** e realiza uma varredura dos pontos de acesso Wi-Fi disponíveis.

Para cada rede encontrada, o programa pode apresentar informações como:

- SSID;
- intensidade do sinal (RSSI);
- modo de autenticação;
- tipo de criptografia;
- canal utilizado.

A quantidade máxima de redes armazenadas pode ser configurada pelo menu do projeto. Por padrão, o exemplo utiliza até **10 pontos de acesso**.

## ⚙️ Pré-requisitos

Antes de executar os projetos, é necessário possuir:

- uma ESP32-CAM;
- conexão USB com o computador;
- ESP-IDF instalado e configurado;
- terminal do ESP-IDF disponível.

A instalação oficial do ESP-IDF pode ser consultada na documentação da Espressif:

https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/index.html

## ▶️ Como executar

Os comandos devem ser executados no **ESP-IDF PowerShell** ou em outro terminal no qual o ambiente do ESP-IDF esteja configurado.

### 1. Escolha um dos projetos

Para o teste de GPIO:

```bash
cd gpio_blink
```

Para a varredura Wi-Fi:

```bash
cd wifi_scan
```

### 2. Defina o alvo

```bash
idf.py set-target esp32
```

Esse comando normalmente precisa ser executado apenas durante a configuração inicial do projeto ou quando o alvo for alterado.

### 3. Compile o projeto

```bash
idf.py build
```

Se a compilação for concluída corretamente, o ESP-IDF criará automaticamente a pasta `build/`.

### 4. Identifique a porta serial

No Windows, a porta utilizada pela placa pode ser identificada pelo **Gerenciador de Dispositivos**, na seção **Portas (COM e LPT)**.

Durante os testes apresentados pelo grupo foi utilizada a porta `COM3`, mas esse valor pode ser diferente em outro computador.

### 5. Grave o programa na ESP32

Substitua `COM3` pela porta correspondente à sua placa:

```bash
idf.py -p COM3 flash
```

### 6. Abra o monitor serial

```bash
idf.py -p COM3 monitor
```

Também é possível gravar o programa e abrir o monitor em um único comando:

```bash
idf.py -p COM3 flash monitor
```

Para sair do monitor serial do ESP-IDF, utilize:

```text
Ctrl + ]
```

## 📡 Configuração opcional do Wi-Fi Scan

O projeto de varredura possui opções adicionais que podem ser acessadas com:

```bash
idf.py menuconfig
```

No menu **Example Configuration**, é possível alterar, entre outras opções:

- quantidade máxima de redes armazenadas na lista;
- canais específicos que serão utilizados durante a varredura.

Caso nenhuma configuração especial seja necessária, o projeto pode ser compilado utilizando os valores padrão.

## 🧹 Arquivos gerados automaticamente

A pasta `build/` é criada pelo ESP-IDF durante:

```bash
idf.py build
```

Ela contém arquivos temporários e binários de compilação e, por isso, não deve ser versionada.

O arquivo `.gitignore` presente na raiz do repositório impede que essas pastas sejam adicionadas pelo Git:

```gitignore
**/build/
```

## 📊 Resultados

Os testes permitiram verificar o funcionamento básico da ESP32-CAM com o ESP-IDF.

No experimento de GPIO, foi possível configurar o GPIO 4 como saída e alternar seu estado periodicamente. Já no experimento de Wi-Fi, a ESP32 realizou a busca por redes disponíveis e exibiu informações sobre os pontos de acesso encontrados.

A atividade contribuiu para a compreensão do processo de desenvolvimento de aplicações embarcadas, desde a preparação do ambiente até a execução do código na placa, servindo como base para aplicações futuras de Internet das Coisas.

## 📄 Apresentação

Os slides utilizados durante a apresentação da atividade estão disponíveis na pasta `slides/`.

## 📚 Referências

- **Espressif Systems — ESP-IDF Programming Guide:**  
  https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/index.html
