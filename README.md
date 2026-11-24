# ECOPET 3D

## Sobre o projeto

O **ECOPET 3D** é um projeto de inovação social que transforma garrafas PET descartadas em filamento com potencial de utilização em impressão 3D.

A solução une sustentabilidade, fabricação digital, eletrônica e desenvolvimento de software. O processo envolve a preparação e o corte da garrafa, o aquecimento e a conformação do PET, a tração do material e o recolhimento do filamento produzido.

## Objetivo do repositório

Este repositório centraliza os materiais relacionados ao desenvolvimento do ECOPET 3D, incluindo:

- arquivos de fabricação das peças;
- imagens do equipamento;
- firmware do Arduino;
- interface web de controle;
- procedimentos e resultados de testes.

A organização busca facilitar a compreensão, a manutenção, a reprodução e a evolução do projeto.

## Estado atual

O projeto possui um **MVP físico e computacional construído e funcional**.

A estrutura mecânica e os componentes eletrônicos foram integrados ao firmware embarcado e à interface web. O sistema permite aquecer e conformar a tira de PET, controlar o motor de tração e acompanhar o funcionamento do equipamento pelo navegador.

Embora o MVP esteja funcional, o projeto ainda pode receber melhorias relacionadas à segurança, calibração do sensor, estabilidade térmica, controle da velocidade e regularidade do filamento produzido.

## Arquitetura do sistema

O ECOPET 3D está organizado em quatro partes principais.

### 1. Estrutura mecânica

Sustenta os componentes e conduz o PET durante o processo. Inclui base estrutural, suportes, peças impressas em 3D, mecanismo de tração e sistema de recolhimento.

### 2. Sistema eletrônico e térmico

Os principais componentes são:

- Arduino Nano;
- hotend e elemento de aquecimento;
- termistor NTC 100k;
- relé;
- motor de passo;
- driver L298N;
- fonte de alimentação de 12 V.

### 3. Firmware embarcado

O arquivo `fabricaembarcado.ino` contém o código executado no Arduino Nano. O firmware é responsável por:

- ler e suavizar a temperatura do termistor;
- acionar o aquecedor pelo relé;
- controlar velocidade e sentido do motor de passo;
- receber comandos pela porta serial;
- enviar telemetria para a interface web.

O código utiliza a biblioteca `Stepper.h`, com motor configurado para 200 passos por volta e comunicação serial a **115200 baud**.

### 4. Interface web

O arquivo `pet_filament_extruder_web_serial_controller_arduino_firmware.html` funciona como painel de controle e monitoramento.

Por meio da Web Serial API, a interface permite:

- conectar o navegador ao Arduino;
- acompanhar a temperatura atual e definir a temperatura-alvo;
- ligar e desligar o aquecedor e o motor;
- ajustar velocidade e sentido de rotação;
- acompanhar a temperatura em um gráfico em tempo real.

## Funcionamento do MVP

1. A garrafa PET é higienizada, seca e cortada em uma tira contínua.
2. A tira é posicionada no equipamento.
3. A interface web é conectada ao Arduino pela porta serial.
4. A temperatura-alvo é definida e o aquecedor é acionado.
5. O Arduino monitora a temperatura pelo termistor.
6. O motor puxa a tira de PET pelo conjunto aquecido.
7. O material é conformado e recolhido no carretel.
8. A interface apresenta a temperatura e os estados do sistema.

A temperatura e a velocidade de tração influenciam diretamente o formato e a regularidade do filamento.

## Controle e comunicação

O firmware calcula a média de 10 leituras do termistor para reduzir ruídos. A temperatura é verificada aproximadamente a cada **300 ms** e a telemetria é enviada a cada **500 ms**.

O aquecedor utiliza controle liga/desliga: abaixo da temperatura-alvo, o relé é ligado; ao alcançar ou ultrapassar o valor definido, o relé é desligado.

A comunicação utiliza mensagens em formato semelhante a JSON.

### Exemplos de comandos

```json
{"target":240}
{"heater":1}
{"motor":1}
{"speed":15}
{"dir":1}
```

### Exemplo de telemetria

```json
{
  "temp": 238.5,
  "target": 240,
  "relay": 1,
  "speed": 15,
  "motor": 1
}
```

## Estrutura do repositório

```text
ECOPET-3D/
├── README.md
├── hardware/
│   ├── imagens/
│   ├── modelos-3d/
│   ├── arquivos-fabricacao/
│   ├── esquema-eletrico/
│   └── lista-de-componentes.md
├── firmware/
│   └── fabricaembarcado.ino
├── web/
│   └── pet_filament_extruder_web_serial_controller_arduino_firmware.html
└── tests/
    ├── procedimentos/
    └── resultados/
```

### Descrição das pastas

- `hardware/`: imagens, modelos 3D, arquivos de fabricação, esquema elétrico e lista de componentes.
- `firmware/`: código embarcado executado no Arduino Nano.
- `web/`: interface web de controle e monitoramento.
- `tests/`: procedimentos, medições e resultados dos testes.

> Pastas sem conteúdo podem ser adicionadas conforme os respectivos arquivos forem produzidos.

## Tecnologias e ferramentas

### Software

- Arduino IDE;
- C/C++ para Arduino;
- biblioteca `Stepper.h`;
- HTML, CSS e JavaScript;
- Web Serial API;
- comunicação serial a 115200 baud.

### Fabricação digital

- Bambu Lab P2S;
- Anet A6;
- Bambu Studio;
- Ultimaker Cura;
- arquivos STL e G-code.

### Hardware

- Arduino Nano;
- termistor NTC 100k;
- hotend;
- relé;
- motor de passo;
- driver L298N;
- fonte de 12 V;
- base em MDF;
- peças produzidas por impressão 3D.

## Como executar

### 1. Carregar o firmware

1. Abra `fabricaembarcado.ino` na Arduino IDE.
2. Conecte o Arduino Nano ao computador.
3. Selecione a placa e a porta serial corretas.
4. Verifique se a biblioteca `Stepper` está disponível.
5. Compile e envie o firmware.

### 2. Abrir a interface web

1. Abra o arquivo HTML no Microsoft Edge ou Google Chrome.
2. Clique em **Conectar Serial**.
3. Selecione a porta do Arduino.
4. Defina a temperatura-alvo.
5. Ative o aquecimento e acompanhe a temperatura.
6. Acione o motor quando o equipamento estiver preparado.

> A interface depende de um navegador compatível com a Web Serial API.

## Resultados

O projeto resultou em um MVP físico e computacional capaz de aquecer e conformar a tira de PET, controlar o motor de tração, medir e exibir a temperatura, receber comandos pela interface web e enviar telemetria em tempo real.

Medições como diâmetro médio, massa processada, tempo de produção e regularidade do filamento ainda devem ser documentadas por testes controlados.

## Limitações e melhorias

Os principais pontos de melhoria são:

- calibração do termistor;
- estabilidade da temperatura;
- controle mais preciso da velocidade;
- regularidade do diâmetro do filamento;
- tratamento de erros da comunicação serial;
- validação dos comandos recebidos;
- testes do filamento em impressoras 3D;
- desligamento automático em caso de falha do sensor;
- limite máximo de temperatura;
- implementação de histerese ou controle PID.

## Segurança

O equipamento possui componentes aquecidos, elétricos e móveis. Durante a utilização:

- não toque no hotend;
- mantenha as conexões elétricas protegidas;
- desligue a alimentação antes de realizar ajustes;
- mantenha mãos e objetos afastados das partes móveis;
- utilize o equipamento em ambiente ventilado;
- não deixe o sistema funcionando sem supervisão;
- confirme a leitura do termistor antes de ativar o aquecedor;
- mantenha um meio físico de desligar a alimentação.

> A versão atual do firmware identifica valores extremos do termistor, mas ainda deve ser ajustada para desligar automaticamente o aquecedor em caso de falha ou desconexão do sensor.

## Contexto acadêmico

Projeto desenvolvido no curso de Ciência da Computação da Universidade Católica de Pernambuco, na disciplina de Tecnologias Digitais para Inovação Social.

## Equipe

- Noemi Soares
- Willian Rodrigues
- Ricardo Nery
- Maria Luiza
- Gabriel Araújo

## Licença

A licença de uso, modificação e distribuição do projeto ainda deverá ser definida.
