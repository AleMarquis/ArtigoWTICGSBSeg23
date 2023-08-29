# Artigo WTICG SBSeg23

Este repositório está vinculado ao artigo "Segurança em Internet das Coisas: Uma Análise de Comportamento de Rede sob Ataque", de Carrer, A. e Margi, C. O artigo foi publicado no Workshop de Trabalhos de Iniciação Científica e de Graduação do XXIII Simpósio Brasileiro em Segurança da Informação e de Sistemas Computacionais.

Resumo do Artigo: "Para viabilizar mecanismos de detecção e mitigação de ataques em Internet das coisas (IoT) é vital entender como diferentes ataques afetam o desempenho da rede. A literatura em geral contém análises de ataques da camada de rede. Neste trabalho implementamos ataques de camada de enlace (Blackhole e Greyhole) e de camada de transporte (Flooding) e analisamos o comportamento da rede observando a taxa de resposta do servidor e a indisponibilidade do protocolo de roteamento. As simulações foram realizadas com diferentes densidades de atacantes e diferentes distâncias do atacante ao servidor. Os resultados demonstram a capacidade de relacionar as métricas coletadas com o tipo de ataque e localização aproximada do nó atacante."

## Resumo

Neste repositório são abordadas as questões de instalação e modificação do sistema operacional Contiki-NG para a implementação dos ataques (arquivos .c) e a simulação dos resultados por meio dos arquivos de configuração do Cooja (arquivos .csc)

O README apresenta informações de (i) Como instalar o Sistema Operacional Contiki-NG e o Emulador Cooja; (ii) Como modificar o Sistema Operacional para aplicar os ataques implementados; (iii) Como simular os ataques com base nos arquivos de configuração do Cooja (.csc)

### Instalação do Contiki-NG

O tutorial de instalação do Contiki-NG pode ser encontrado na documentação do sistema operacional. É recomendada a instalação via Imagem do Docker para a replicação deste artigo.

O passo-a-passo da instalação pode ser encontrado neste link: [Instalação Via Docker](https://docs.contiki-ng.org/en/develop/doc/getting-started/Docker.html)

### Modificação do Sistema Operacional

Os ataques implementados no artigo são de duas categorias distintas, Blackhole e Greyhole, que são ataques implementados no Framer do sistema operacional, e Flooding, que é implementado na aplicação do dispositivo. Assim, em cada pasta dentro da raiz deste repositório contém os arquivos necessários para replicar os exeperimentos do artigo. Em todas as pastas com o nome dos ataques, temos os arquivos do Framer e a pasta entitulada Attack, que possui a aplicação e o código compilado dos nós, para sua implementação.

A instalação deve ser feita substituindo os códigos do framer do Contiki-NG e duplicando a pasta com os binários dos nós na pasta example do Sistema Operacional desta maneira:

Para cada implementação de ataque deve ser feito, a partir da pasta que leva o nome do ataque:

- Substituir framer-802154.c e framer-802154.h do Contiki no caminho: ```contiki-ng/os/net/mac/framer``` com os códigos disponibilizados na pasta ```framer``` deste repositório
- Inserir a pasta Attack na pasta de examples do Contiki no caminho: ```contiki-ng/examples```

### Simulação

Com o contiki instalado e os ataques implementados, basta abrir o Cooja escrevendo o comanado ```cooja``` no terminal

Se a instalação foi correta, a interface gráfica do Cooja, software usado para as simulações, será aberta.

Para preparar os ambientes de simulação basta ir em ```File > Open Simulation``` e selecionar o arquivo .csc dentro da pasta ```contiki-ng/examples/Attack```

Depois disso, basta iniciar a simulação clicando em ```Simulation > Start Simulation```. Informações importantes como a troca de mensagens entre nós e atributos essenciais podem ser encontradas na aba Mote Output do Cooja em: ```View > Mote Output```

Caso deseje alterar algumas configurações da simulação, como analisar também a energia dos nós pelo Módulo Energest, ou mudar o ID dos nós atacantes, isto pode ser feito modificando os códigos originais. Estas modificiações relevantes são acompanhadas de comentáiros explicativos.

Exemplos gerais:

- O módulo Energest pode ser inserido no Makefile dentro da pasta Attack
- Mensagens do framer podem ser desativadas no Mote Output seguindo o comentário da linha 50 do arquivo framer-802154.c do ataque.
- O ID dos atacantes podem ser modificados alterando a variável attackerNode no Framer **E** no udp-attack-client.c

Qualquer dúvida pode ser encaminhada ao autor principal do artigo.
