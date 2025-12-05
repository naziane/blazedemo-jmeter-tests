# BlazeDemo – Testes de Performance com Apache JMeter

Este projeto contém testes de performance utilizando Apache JMeter para avaliar o comportamento da aplicação BlazeDemo em diferentes cenários de carga, incluindo testes de pico (250 RPS) e testes de carga.

# *Cenário de Teste*

# *Endpoints Monitorados*
1. https://blazedemo.com/
2. https://blazedemo.com/reserve.php
3. https://blazedemo.com/purchase.php?flight=1
4. https://blazedemo.com/purchase.php

# *Componentes do Plano de Teste*
- **Concurrency Thread Group**  
  - Simula usuários concorrentes para atingir o throughput desejado.
- **Throughput Shaping Timer (TST)**  
  - Garante taxa exata de **250 requests/second**.


# Teste de Carga

O cenário (Carga) busca gerar 250 requisições por segundo constantes para cada endpoint.

# Valores para Concurrency Thread Group
- Threads estimadas: 150
- Ramp-up time: 60 segundos
- Ramp-up steps: 10
- Hold: 120 segundos

A carga de 150 usuários virtuais alcançara 150 threads em 60 segundos.
Então, a cada steps será iniciado 15 threads em 60 segundos.
Depois de todas a threads iniciadas o teste mantem executando por 120 segundos, simulando a carga constante no sistema.


# Teste de Pico – 250 RPS

O cenário (Pico) tem objetivo de iniciar 250 requisições por segundo.

# Valores para Concurrency Thread Group
- Threads estimadas: 250
- Ramp-up time: 5 segundos
- Ramp-up steps: 10
- Hold: 60 segundos

A carga de 250 usuários virtuais alcançara 250 threads em 5 segundos.
Então, a cada steps será iniciado 25 threads em 5 segundos.
Depois de todas a threads iniciadas o teste mantem executando por 60 segundos, simulando a carga constante no sistema.

Isso garante margem suficiente para atingir o throughput real sem perda de requisições.

# Valores utilizados no TST (Throughput Shaping Timer)

| Tempo (s) | RPS |
|----------|-----|
|  30       | 0 → 250 |
|  120      | 250 constante |
|  30       | 250 → 0 |

Um pico de 250 requisicoes em 30 segundos, onde se mantem por 120 segundos constante e baixa as requisicoes em 30 segundos.



# *Execução Automática – GitHub Actions*

O pipeline `jmeter.yml`:

 -Instala Java 17  
 - Baixa e configura JMeter  
 - Instala Plugins (TST, CST, Graphs, etc.)  
 - Executa o teste em modo CLI  
 - Gera relatório HTML  
 - Faz upload como artifact


# *Resultados*

Após cada execução, ficam disponíveis como artifacts:

jmeter-results	Arquivo JTL
jmeter-report	Relatório HTML completo

# *Acessar o relatório*

Vá até a aba “Actions”.

Na seção “Artifacts”, localize o arquivo chamado jmeter-report.

Fazer download do arquivo

Clique no arquivo jmeter-report para baixá-lo.

Descompactar o arquivo

# *Abrir o relatório*

Dentro da pasta extraída, localize o arquivo index.html.

Abra este arquivo em um navegador web (Chrome, Firefox ou Edge) para visualizar o relatório completo do JMeter.


# *Como rodar localmente*

Instale o JMeter 5.6.3

Instale o Plugins Manager

Baixe plugins:

jpgc-casutg
jpgc-tst

Execute:

jmeter -n -t tests/blazedemo.jmx -l results/results.jtl
jmeter -g results/results.jtl -o results/html


# *Autora*
 Naziane Alves Pinto