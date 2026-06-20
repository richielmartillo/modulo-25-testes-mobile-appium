# Anotações sobre Appium, ADB e testes mobile

Este arquivo reúne anotações sobre ferramentas usadas no módulo 25 para testes mobile com Android, Appium e emuladores.

---

## ADB — Android Debug Bridge

O **ADB** é uma ferramenta de linha de comando que permite a comunicação entre o computador e um dispositivo Android, seja ele físico ou emulado.

De forma simples, o ADB funciona como uma ponte entre o PC e o Android. Com ele é possível instalar aplicativos, remover aplicativos, executar comandos, acessar logs e depurar o ambiente de testes.

### Comandos principais

```bash
adb devices
```

Mostra quais dispositivos Android estão conectados ao computador.

Exemplo de resultado:

```bash
List of devices attached
emulator-5554 device
```

Esse resultado indica que o emulador está conectado e pronto para receber comandos.

```bash
adb install app.apk
```

Instala um aplicativo APK no dispositivo ou emulador.

```bash
adb uninstall com.nome.do.app
```

Desinstala um aplicativo usando o nome do pacote.

```bash
adb logcat
```

Exibe os logs do Android.

```bash
adb shell
```

Abre um terminal dentro do Android.

---

## Appium Doctor

O **Appium Doctor** é uma ferramenta que verifica se o ambiente está configurado corretamente para rodar testes mobile com Appium.

Ele funciona como um diagnóstico do ambiente, apontando dependências instaladas, configurações ausentes e possíveis problemas.

### Comando

```bash
appium-doctor
```

### O que ele verifica

| Item | Para que serve |
|---|---|
| Node.js | Necessário para rodar o Appium |
| Java JDK | Necessário para automação Android |
| Android SDK | Conjunto de ferramentas do Android |
| ADB | Comunicação entre computador e Android |
| UiAutomator2 | Driver usado para automação Android |
| Emulador ou dispositivo físico | Local onde os testes serão executados |

### Exemplo de ambiente correto

```bash
✔ Node.js is installed
✔ ANDROID_HOME is set
✔ adb exists
✔ Java is installed
```

### Exemplo de problema

```bash
✖ ANDROID_HOME is not set
```

Nesse caso, o Appium Doctor está indicando que a variável de ambiente `ANDROID_HOME` não foi configurada.

---

## Appium Inspector

O **Appium Inspector** é uma ferramenta gráfica usada para inspecionar elementos da interface de aplicativos móveis.

Ele permite iniciar uma sessão com o Appium, visualizar a tela do aplicativo e identificar elementos que podem ser usados nos testes automatizados.

Com ele é possível obter informações como:

- `id`
- `text`
- `class`
- `xpath`
- atributos dos elementos da tela

Essas informações ajudam na criação dos scripts de automação.

---

## Capabilities

As **capabilities** são configurações enviadas para o Appium para definir como a sessão de teste deve ser iniciada.

Elas informam qual plataforma será usada, qual dispositivo será conectado, qual driver de automação será utilizado e qual aplicativo deve ser aberto.

Em outras palavras, elas dizem para o Appium:

> Inicie uma sessão de teste neste dispositivo, usando este app e estas configurações.

### Exemplo de capabilities

```json
{
  "platformName": "Android",
  "appium:deviceName": "emulator-5554",
  "appium:automationName": "UiAutomator2",
  "appium:app": "./apps/app.apk"
}
```

### Explicação dos campos

| Capability | Significado |
|---|---|
| `platformName` | Define a plataforma usada no teste, neste caso Android |
| `appium:deviceName` | Nome do dispositivo ou emulador conectado |
| `appium:automationName` | Driver de automação usado pelo Appium |
| `appium:app` | Caminho do arquivo APK que será instalado ou aberto |

---

## Device Farm

Uma **Device Farm** é uma infraestrutura que disponibiliza vários dispositivos físicos ou virtuais para execução de testes mobile.

Ela permite testar o aplicativo em diferentes modelos, versões de Android, tamanhos de tela e configurações, aumentando a cobertura dos testes.

Esse recurso é útil principalmente quando o projeto precisa validar o comportamento do app em muitos dispositivos diferentes.

---

## Emulador

O **emulador** é um software que simula um dispositivo Android dentro do computador.

Ele permite instalar, executar e testar aplicativos sem precisar de um celular físico.

No contexto dos testes mobile, o emulador é muito usado para estudar, praticar automação e validar funcionalidades básicas do aplicativo.

---

## Google USB Driver

O **Google USB Driver** é um driver usado no Windows para permitir que o computador reconheça dispositivos Android conectados via USB.

Ele é importante quando os testes são executados em um celular físico, pois permite que ferramentas como o ADB e o Appium se comuniquem com o aparelho.

---

## SDK Command Line Tools

As **SDK Command Line Tools** são ferramentas de linha de comando do Android SDK.

Elas permitem instalar pacotes, configurar componentes do Android, criar emuladores e executar operações essenciais para desenvolvimento e testes mobile.

Essas ferramentas fazem parte da base necessária para trabalhar com Android, ADB, emuladores e Appium.

---

## UIAutomator2

O **UIAutomator2** é o driver usado pelo Appium para automatizar aplicativos Android.

Ele permite que o Appium interaja com elementos da interface do aplicativo, como botões, campos de texto, menus e telas.

No Appium, ele aparece normalmente dentro das capabilities:

```json
"appium:automationName": "UiAutomator2"
```

---

## Virtual Device Manager

O **Virtual Device Manager** é uma ferramenta do Android Studio usada para criar, configurar e gerenciar emuladores Android.

Com ele é possível escolher o modelo do dispositivo, versão do Android, tamanho da tela e outras configurações do emulador.

---

## Comparação rápida das ferramentas

| Ferramenta | Função principal |
|---|---|
| ADB | Faz a comunicação entre o computador e o Android |
| Appium | Automatiza testes em aplicativos mobile |
| Appium Doctor | Verifica se o ambiente do Appium está configurado corretamente |
| Appium Inspector | Ajuda a inspecionar elementos da tela do app |
| Android Studio | Fornece ferramentas para desenvolvimento e emulação Android |
| Emulador | Simula um dispositivo Android no computador |
| UIAutomator2 | Driver usado pelo Appium para automatizar apps Android |
| Google USB Driver | Permite que o Windows reconheça dispositivos Android via USB |

---

## Lógica do módulo 25

A lógica principal do ambiente de testes mobile pode ser entendida assim:

```txt
ADB = ponte entre o computador e o Android
Appium = ferramenta que automatiza o aplicativo
Appium Doctor = ferramenta que verifica se o ambiente está correto
Appium Inspector = ferramenta que ajuda a localizar elementos da tela
Emulador = Android virtual usado para executar os testes
UIAutomator2 = driver usado pelo Appium para controlar o app Android
```

Resumo:

O computador usa o **ADB** para se comunicar com o Android.  
O **Appium** usa essa comunicação para automatizar o aplicativo.  
O **Appium Inspector** ajuda a encontrar os elementos da tela.  
O **Appium Doctor** verifica se tudo está configurado corretamente.  
O **emulador** simula o celular onde os testes serão executados.