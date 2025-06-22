
# ✅ Projeto: Alarme Automotivo - Experiência 6  
**Placa:** AX301 - FPGA Cyclone IV EP4CE6F17C8

## 📌 1. Objetivo

Implementar um sistema de alarme automotivo com as seguintes condições:

- **Alarme Liga se:**
  1. Faróis ligados + Ignição desligada
  2. Porta aberta + Ignição ligada

**Importante:**  
As entradas da placa AX301 são **ativas em nível baixo** (lógica invertida).

## 📌 2. Entradas e Saídas

| Sinal | Função | Pino na FPGA | Localização Física |
|---|---|---|---|
| porta | Porta do motorista | M15 | KEY1 |
| ignicao | Ignição | M16 | KEY2 |
| farol | Faróis | E16 | KEY3 |
| alarmeSom | Saída do Alarme | C11 | Buzzer |

## 📌 3. Estrutura de Arquivos

```
/seu_projeto/
├── alarme.vhd
├── tb_alarme.vhd
├── alarme.qsf
└── README.md
```

## 📌 4. Passos no Quartus II

### 4.1 Criação do Projeto

1. File → New Project Wizard
2. Nome do projeto: alarme
3. Dispositivo: Cyclone IV E → EP4CE6F17C8

### 4.2 Inserção dos Arquivos

- Adicione o arquivo alarme.vhd
- Adicione o arquivo tb_alarme.vhd (opcional para simulação)

### 4.3 Pin Planner (.qsf)

Use o conteúdo do alarme.qsf para configurar os pinos.

### 4.4 Compilação

- Processing → Start Compilation

### 4.5 Gravação na FPGA

- Tools → Programmer
- Selecione o .sof
- Clique em Start

## 📌 5. Simulação no Linux

### ✅ ModelSim (Modo Terminal)

```bash
vcom alarme.vhd
vcom tb_alarme.vhd
vsim -c work.tb_alarme -do "run -all; quit;"
```

### ✅ GHDL + GTKWave (Open Source)

**Instalação:**

```bash
sudo apt install ghdl gtkwave
```

**Simulação:**

```bash
ghdl -a alarme.vhd
ghdl -a tb_alarme.vhd
ghdl -e tb_alarme
ghdl -r tb_alarme --vcd=onda.vcd
gtkwave onda.vcd
```

## ✅ 6. Observações

- Entradas da AX301: Ativas em nível baixo (lógica invertida)
- Saída (alarmeSom): Ligado em nível alto

## ✅ Fim!
