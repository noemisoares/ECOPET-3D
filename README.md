# ECOPET-3D

Projeto desenvolvido no curso de Ciência da Computação da Universidade Católica de Pernambuco (UNICAP), na disciplina de Gerenciamento de Projetos (Prof. Danilo Paiva Lúcio), voltado à transformação de garrafas PET em filamento para impressão 3D por meio de preparação/corte da tira, aquecimento, conformação e tração[cite: 7].

> **Nota de escopo:** Este `README.md` reúne a documentação técnica do MVP e o estado atual do repositório. Alguns itens descritos no relatório técnico (como modelos 3D, esquema elétrico e medições experimentais) ainda não estão versionados nos arquivos atuais[cite: 6, 7].

## Visão geral e arquitetura

O fluxo do processo é dividido em cinco etapas: preparação da garrafa PET, corte em tira contínua, aquecimento do material, tração e conformação no hotend e recolhimento em carretel[cite: 7].

- **Subsistema mecânico e estrutural:** base em MDF, peças impressas em 3D (suportes, mancais, engrenagens de redução e mecanismo de tração) e hotend adaptado (bloco de alumínio e bico de referência nominal de 1,75 mm)[cite: 7].
- **Hardware e eletrônica:** Arduino Nano (ATmega328P), motor de passo NEMA 17, driver/ponte H L298N, cartucho aquecedor, termistor NTC 100 kΩ (divisor resistivo em entrada analógica) e alimentação principal de 12 V DC (com regulação para 5 V)[cite: 7].
- **Software e controle:** firmware em C/C++ para Arduino Nano (`115200` baud) e interface web via Web Serial API para envio de comandos JSON e acompanhamento de telemetria em tempo real[cite: 5, 7].

## Estrutura do repositório

```text
ECOPET-3D/
├── README.md
├── firmware/
│   └── fabricaembarcado.ino
├── web/
│   └── pet_filament_extruder_web_serial_controller_arduino_firmware.html
└── tests/
    └── simulador_serial.html
```

### Descrição das pastas e arquivos atuais

- `firmware/fabricaembarcado.ino`: código embarcado do Arduino Nano para leitura térmica, acionamento do aquecimento e controle do motor de passo via L298N[cite: 6, 7].
- `web/pet_filament_extruder_web_serial_controller_arduino_firmware.html`: painel web com conexão Web Serial (`115200` baud), gráfico de temperatura em tempo real, ajuste de temperatura-alvo e controle de velocidade/sentido do motor[cite: 5, 6].
- `tests/simulador_serial.html`: simulador de bancada para testar leitura/simulação de dados JSON, gráfico e estados sem depender do hardware conectado[cite: 6].
- `hardware/` *(planejada)*: modelos 3D, arquivos de fatiamento/fabricação, esquema elétrico e lista de componentes[cite: 6, 7].

## Tecnologias e ferramentas

### Software e comunicação
- Arduino IDE e C/C++ para Arduino[cite: 7]
- Biblioteca `Stepper.h`[cite: 7]
- HTML, CSS e JavaScript com Web Serial API[cite: 5, 7]
- Comunicação serial a `115200` baud[cite: 5, 7]

### Fabricação digital e hardware
- Impressoras 3D Bambu Lab P2S e Anet A6; fatiadores Bambu Studio e Ultimaker Cura (STL e G-code)[cite: 7]
- Arduino Nano (ATmega328P), termistor NTC 100 kΩ, hotend, relé/acionamento térmico, motor de passo NEMA 17, driver L298N, fonte 12 V DC, base em MDF e peças impressas em 3D[cite: 5, 7]

## Como executar

### 1. Firmware (Arduino Nano)
1. Abra `firmware/fabricaembarcado.ino` na Arduino IDE[cite: 6, 7].
2. Conecte o Arduino Nano via USB e selecione a placa e a porta serial corretas[cite: 7].
3. Confirme a instalação da biblioteca `Stepper`[cite: 7].
4. Compile e envie o código para a placa[cite: 7].

### 2. Interface web (Web Serial)
1. Abra `web/pet_filament_extruder_web_serial_controller_arduino_firmware.html` no Google Chrome ou Microsoft Edge[cite: 5, 6, 7].
2. Clique em **Conectar Serial** e escolha a porta do Arduino[cite: 5, 7].
3. Ajuste a temperatura-alvo, ative o aquecimento e acione o motor quando o conjunto estiver pronto[cite: 5, 7].

### 3. Simulador de teste (sem hardware)
1. Abra `tests/simulador_serial.html` no navegador[cite: 6].
2. Use os botões de simulação, auto-teste ou envio de JSON para validar a visualização antes de conectar ao equipamento físico[cite: 6].

## Resultados, limitações e próximos passos

O projeto documenta a reconstrução do MVP físico e o controle serial/web para validar o fluxo de transformação de garrafas PET em filamento[cite: 7]. Medições quantitativas (diâmetro médio, massa processada, tempo de produção e regularidade) ainda não foram registradas em testes controlados[cite: 7].

**Pontos de melhoria e segurança:**
- Calibração do termistor, estabilidade térmica e avaliação de controle por histerese ou PID[cite: 7].
- Limite máximo de temperatura e desligamento automático em caso de falha/desconexão do sensor[cite: 7].
- Validação de comandos seriais e testes do filamento em impressoras 3D[cite: 7].
- Cuidados de segurança: não tocar no hotend quente, manter partes móveis protegidas, verificar conexões e dissipação do L298N, usar ambiente ventilado, manter chave/meio físico de desligamento e operar apenas com garrafas PET limpas e secas[cite: 7].

## Equipe

- Noemi Soares
- Willian Rodrigues
- Ricardo Nery
- Maria Luiza
- Gabriel Araújo[cite: 7]

## Licença

A licença de uso, modificação e distribuição do projeto ainda será definida[cite: 7].
