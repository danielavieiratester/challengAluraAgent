# challengAluraAgent
Entrega obrigatória para conclusão da imersão IA e obtenção do certificado.

# 🐾 AUPP - Assistente Virtual para Adoção de Animais

Projeto de um assistente virtual para apoio ao processo de adoção de animais da **Associação Unidos Pelas Patas (AUPP)**.

A solução utiliza Inteligência Artificial integrada ao **Telegram**, permitindo que uma pessoa interessada em adoção informe suas preferências, consulte animais resgatados cadastrados, manifeste interesse em um animal e receba o Termo de Adoção.

O workflow foi desenvolvido utilizando **n8n**, modelo de IA generativa e banco de dados **PostgreSQL**.

---

## 🎯 Objetivo

Facilitar o primeiro contato entre pessoas interessadas em adoção e a ONG.

O assistente conduz o usuário por um questionário para identificar suas preferências e consulta a base de animais resgatados.

O objetivo não é substituir a avaliação realizada pelos protetores da ONG, mas automatizar as etapas iniciais do processo.

---

## 🤖 Funcionamento

O atendimento é iniciado pelo Telegram.

O bot conduz a conversa fazendo **uma pergunta por vez**.

São coletadas as seguintes preferências:

1. Espécie
   - Cachorro
   - Gato

2. Pelagem
   - Curta
   - Longa

3. Porte
   - Pequeno
   - Médio
   - Grande

4. Faixa etária
   - Filhote
   - Adulto
   - Idoso

5. Temperamento

6. Aceitação de animal especial

Depois de obter as informações, o agente consulta os animais cadastrados no banco de dados.

---

## 🔎 Seleção do animal

O assistente procura o animal com maior compatibilidade com as preferências informadas.

São considerados critérios como:

- espécie;
- pelagem;
- porte;
- idade;
- temperamento;
- condição de animal especial.

Não é necessária correspondência exata entre todas as características.

Caso nenhum animal corresponda completamente às preferências, o sistema apresenta outro animal disponível na base, possibilitando que o usuário conheça um resgatado com perfil diferente.

**Se houver pelo menos um animal cadastrado e disponível na consulta, o assistente deve apresentar um animal real ao usuário.**

O sistema nunca deve inventar animais ou características.

---

## 🐶 Apresentação do resgatado

Quando um animal é selecionado, podem ser apresentadas informações como:

- nome;
- espécie;
- raça;
- idade;
- porte;
- pelagem;
- cor;
- temperamento;
- castração;
- vacinação;
- chipagem;
- convivência com outros animais;
- condição especial;
- história do resgate;
- foto.

A foto do animal é disponibilizada por meio de URL armazenada na base de dados.

O assistente também informa quais características correspondem às preferências do usuário e quais são diferentes.

---

## 👤 Manifestação de interesse

Após apresentar o animal, o bot pergunta se o usuário deseja fornecer seus dados para manifestação de interesse.

Caso aceite, são solicitados individualmente:

1. Nome completo
2. E-mail
3. Autorização para contato de uma protetora da AUPP

A autorização de contato pode ser:

- `true` — autoriza contato;
- `false` — não autoriza contato.

A negativa de autorização **não impede o registro da manifestação de interesse**.

---

## 💾 Registro do interessado

Após receber todas as informações necessárias, o AI Agent utiliza uma Tool do PostgreSQL para registrar o interessado.

Os principais dados armazenados são:

```text
nome_usuario
email_usuario
nome_resgatado
dt_envio_termo
autoriza_contato
