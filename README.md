# MODELO DE BESS GENÉRICO NO ANATEM
<br>Modelo Dinâmico de Sistema de Armazenamento de Energia em Baterias (BESS) implementado em ambiente ANATEM com base no modelo de BESS desenvolvido pelo EPRI/WECC [1]
## DESCRIÇÃO
<br>O modelo foi implementado como uma topologia de CDU (código DTDU no ANATEM), sendo desenvolvida uma topologia distinta para cada módulo do modelo do EPRI: REGC_A (Renewable Energy Generator/Converter Model, versão A), REEC_C (Renewable Energy Electrical Controller, versão C), e REPC_A (Renewable Energy Plant Controller, versão A). As topologias são associadas aos controladores por meio do código ACDU. As toplogias e suas respectivas associações são definidas no arquivo BESS_DADOS.dat, na pasta MODELOS.
<br>A implementação do estudo de caso foi realizada seguindo as orientações do ONS para teste de controladores de modelos dinâmicos. Para teste do modelo, utilizou-se uma rede padrão de 4 barras: BESS - Rede Eq. de MT - Trafo de Conexão - Rede Eq. de AT - Barra Infinita, conforme ilustrado na figura abaixo.
<br><br> 
![Imagem1](https://github.com/LSF-IEE/SAEB_ANATEM/assets/79756059/68982fe0-d99a-4e28-9ff6-8de3cd974165)
<br><br>
Para uma base de potência de Sb = 6 MVA, as impedâncias da rede implementadas são:
<br>Z12 = 1 + j10 %
<br>Z23 = 0.01 + j6 %, tap = 1.0
<br>Z34 = 0.006 + j0.06 %
<br>Tensões base de 138 kV na alta do transformador e 34.5 kV na baixa.
<br><br> Foram considerados 5 casos convergidos de fluxo de potência no ANAREDE:
<br> CASO 1: BESS standby (P = 0, Q = 0)
<br> CASO 2: BESS injetando ativa (P > 0, Q = 0)
<br> CASO 3: BESS absorvendo ativa (P < 0, Q = 0)
<br> CASO 4: BESS injetando ativa e reativa (P = >, Q > 0)
<br> CASO 5: BESS injetando ativa e absorvendo reativa (P > 0, Q < 0)
<br> Para alterar o caso a ser simulado, deve-se mudar o seguinte comando no código de execução DARQ (arquivo CASO_BASE.stb):  SAV   N .\REDE\PADRAO_ONS.sav, onde N={1,2,3,4,5}. 
## PARAMETRIZAÇÃO
<br> Os principais parâmetros de controle (ganhos de controladores PI, constantes de tempo, limitadores, etc) foram reproduzidos a partir dos valores padrão indicados em [2]. Esses parâmetros podem ser alterados diretamente no arquivo BESS_DADOS.dat, na seção de definição das toplogias (DTDU).
<br> Os parâmetros referentes as flags de ativação dos modos de controle, aos locais remotos, e a potência nominal do BESS devem ser alterados na seção de associação das topologias (ACDU), no arquivo BESS_DADOS.dat.
## ARQUIVOS
<br>CASO_BASE.stb: arquivo principal para execução no ANATEM. Faz a chamada dos outros arquivos, define e executa a simulação.
<br>MODELOS\BESS_DADOS.dat: contém a implementação das topologias de controladores (DTDU)
<br>Arquivo .cdu de Sistema de Armazenamento de Energia em Baterias (SAEB) implementado em ambiente ANATEM com base no modelo de BESS desenvolvido pelo EPRI/WECC
<br>
Ref: [1] WECC. “WECC Battery Storage Dynamic Modeling Guideline”, Relatório Técnico, Western Electricity Coordinating Council, 2016. 
<br>
Endereço de acesso:  https://www.wecc.org/Reliability/WECC%20Battery%20Storage%20Guideline%20updates_%20Bo%204-5-17%20SLT%204-7-17%20XX%20SC.docx 
<br>
Acesso em 21/09/2022.
