
# Alarme Automotivo em VHDL para Placa AX301 (Cyclone IV EP4CE6E22C8N)

## Descrição do Projeto

Este projeto implementa um **alarme automotivo** em VHDL, para ser sintetizado na placa AX301 com FPGA Cyclone IV (EP4CE6E22C8N).  
O sistema utiliza **3 chaves** para simular sensores do carro:
- **SW0**: Porta do motorista aberta (`porta_motorista`)
- **SW1**: Ignição ligada (`ignicao`)
- **SW2**: Faróis acesos (`farois`)

A saída do alarme aciona um **buzzer** (pino físico C11 da FPGA).

### Lógica do Alarme
O alarme (buzzer) dispara (ativa) se:
- Os faróis estão acesos **e** a ignição está desligada;  
**OU**
- A porta do motorista está aberta **e** a ignição está ligada.

Em todos os outros casos, o buzzer permanece desligado.

---

## Tabela Verdade

| SW0 (`porta_motorista`) | SW1 (`ignicao`) | SW2 (`farois`) | `buzzer` (saída) |
|:----------------------:|:---------------:|:--------------:|:----------------:|
| 0                      | 0               | 0              | 0                |
| 0                      | 0               | 1              | 1                |
| 0                      | 1               | 0              | 0                |
| 0                      | 1               | 1              | 0                |
| 1                      | 0               | 0              | 0                |
| 1                      | 0               | 1              | 1                |
| 1                      | 1               | 0              | 1                |
| 1                      | 1               | 1              | 1                |

---

## Passo a Passo: Implementação no Quartus Prime

### 1. Criar um Novo Projeto

1. Abra o Quartus Prime.
2. Vá em **File > New Project Wizard**.
3. Escolha uma pasta e nomeie o projeto (ex: `alarme_carro`). Clique em **Next**.
4. Mantenha *Empty project* e clique em **Next**.
5. Selecione a família **Cyclone IV E** e o dispositivo **EP4CE6E22C8N** (confirme o pacote e a velocidade conforme sua placa). Clique em **Next** e depois **Finish**.

---

### 2. Adicionar o Arquivo VHDL

- Crie um novo arquivo em **File > New > VHDL File**.
- Cole o código VHDL do seu alarme (entidade com `porta_motorista`, `ignicao`, `farois`, `buzzer`).
- Salve como `alarme.vhd`.
- Adicione o arquivo ao projeto em **Project > Add/Remove Files in Project**.
- Verifique se sua entidade VHDL está como Top-Level Entity (se necessário, clique com o direito e selecione "Set as Top-Level Entity").

---

### 3. Compilar o Projeto

- Vá em **Processing > Start Compilation**.
- Aguarde a conclusão. Corrija eventuais erros ou avisos.

---

### 4. Configurar os Pinos no Pin Planner

1. Vá em **Assignments > Pin Planner**.
2. Na janela que abrir, localize cada sinal (Node Name) do seu código.
3. Atribua as localizações dos pinos conforme abaixo:

   | Sinal              | Função         | Pino / Chave na Placa  |
   |--------------------|---------------|------------------------|
   | porta_motorista    | Entrada       | SW0                    |
   | ignicao            | Entrada       | SW1                    |
   | farois             | Entrada       | SW2                    |
   | buzzer             | Saída         | C11                    |

   **Obs:**  
   - Os sinais `porta_motorista`, `ignicao` e `farois` devem ser ligados às chaves SW0, SW1 e SW2 da placa, respectivamente.
   - O sinal `buzzer` deve ser ligado ao pino físico **C11** do FPGA (conectado ao buzzer onboard).

4. Após configurar, salve e feche o Pin Planner.

---

### 5. Gerar o Arquivo .sof e Gravar na Placa

1. Após a compilação, encontre o arquivo `.sof` na pasta do projeto.
2. Vá em **Tools > Programmer**.
3. Selecione **USB-Blaster** em Hardware Setup.
4. Clique em **Auto Detect** para reconhecer o FPGA.
5. Adicione o arquivo `.sof` clicando em **Add File**.
6. Marque a opção **Program/Configure** para o arquivo.
7. Clique em **Start** para gravar o FPGA.

---

## Pronto!

Agora, ao acionar as chaves conforme a tabela verdade, o buzzer deve disparar apenas nas condições programadas.

---

**Dicas:**
- Confirme os pinos das chaves e do buzzer com o manual da AX301, caso seu kit tenha uma configuração diferente.
- Sempre salve o projeto e confira as mensagens do Quartus ao compilar.

---
