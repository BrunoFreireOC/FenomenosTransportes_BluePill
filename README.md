# FenomenosTransportes_BluePill
Este repositório contém o código do microcontrolador STM32F103C8T6 (BluePill), em que o software computa o fluxo do sensor de fluxo YS- a partir da contagem do número de pulsos.

O software configura uma interrupção no pino da BluePill, e armazena quantos pulsos está sendo contado. Também é configurado um Timer que tem uma rotina de interrupção a cada um segundo, em que na rotina de interrupção (ISR) é armazenado o valor do contador, e é feito a conversão de Número de Pulsos(N, adimensional) em Fluxo (F, L/min). É necessário saber o fator de correção do sensor, que pode variar entre sensores semelhantes, a fórmula prevista em que o Número de Pulsos é **atualizado a cada um segundo**.

$F = \frac{N}{\mathrm{FACTOR}}$

Para visualização do Fluxo, foi utilizado um LCD 16x2 com módulo I2C.

| Tipo de periférico | Periférico      | Descrição                                |
|--------------------|-----------------|------------------------------------------|
| Timer              | TIM2            | Atualização do contador                  |
| I2C                | I2C1            | Comunicação com LCD                      |
| USART              | USART1          | Comunicação UART. baud = 115200          |
| USB                | FS (DFU)        | Enviar código via USB                    |
| System Core        | SYS (Debug SWD) | Habilitar SWD para depuração com ST-Link |
| GPIO               | PA1 (EXTI1)     | Entrada de pulsos com interrupção        |
| GPIO               | PA2 (EXTI2)     | Interrupção para começar a calibração    |
| GPIO               | PA3 (EXTI3)     | Interrupção para terminar a calibração   |

<img src="https://github.com/user-attachments/assets/657fb3ea-dc91-4a50-a7a4-9bb63cf27bbb" alt="BluePill Pinout" style="height: 340px; width: 640px;"/>
