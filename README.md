# BlazeDemo JMeter Tests

Este projeto contém testes de carga e pico utilizando o Apache JMeter para o site BlazeDemo.



# Teste de Carga

Simula acessos constantes ao site BlazeDemo por um período prolongado.

# Teste de Pico

Simula aumento repentino de usuários em curto período.

# Executar Localmente (CLI)

bash

jmeter -n -t tests/blazedemo.jmx -l results/result.jtl -j results/jmeter.log


Gerar relatório HTML:

bash

jmeter -g results/result.jtl -o report


# Pipeline GitHub Actions

Os testes são executados automaticamente nos eventos:

* `push`
* `pull_request`

O relatório gerado fica disponível nos Artifacts.

# Autora
Naziane Alves Pinto