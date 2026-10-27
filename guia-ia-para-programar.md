# Guia prático: programar e gerar renda com IA

Para quem tem anos de estrada em programação, nunca virou “craque” e quer usar as IAs como alavanca, não como ameaça.

## 0. As 12 regras de ouro (se você ler só isto)

1. **Você é o dono do produto; a IA é um desenvolvedor júnior ultrarrápido** que nunca cansa, sabe um pouco de tudo e erra com total confiança.
2. **Especifique antes de pedir.** 80% da qualidade do resultado vem da clareza do pedido (use o formulário que acompanha este guia).
3. **Fatias pequenas.** Peça uma funcionalidade por vez, rode, teste, só então avance.
4. **Rode tudo.** Código que você não executou é hipótese, não resultado.
5. **Use Git desde o minuto zero.** Commit a cada passo que funciona. É o seu botão “desfazer”.
6. **Cole o erro completo**, nunca “deu erro, arruma”.
7. **Peça o plano e as suposições** antes do código.
8. **Entenda o que foi gerado.** Quem terceiriza o entendimento fica refém da IA e não evolui.
9. **Nunca implemente por conta própria: login, pagamentos, criptografia.** Use serviços e bibliotecas consagradas.
10. **Nunca cole senhas, chaves de API ou dados pessoais de clientes** no chat.
11. **Conversa longa degrada.** Quando a IA começar a se embolar, resuma e comece uma conversa nova.
12. **Código virou commodity; o diferencial é problema certo + nicho + distribuição + confiança.**

---

## 1. O que você precisa entender sobre como as IAs funcionam

- **Elas geram texto plausível**, não “consultam a verdade”. Por isso podem inventar funções, bibliotecas, flags de comando e até pacotes que não existem (as chamadas *alucinações*). Quanto mais obscuro o tema, maior o risco.
- **Têm data de corte de conhecimento.** Bibliotecas, APIs e frameworks mudam. Se algo parece desatualizado, cole a documentação atual no pedido ou use uma ferramenta com acesso à web.
- **Não têm memória entre conversas** (a menos que o produto ofereça recurso de memória). Cada conversa nova começa quase do zero: você precisa reapresentar o projeto.
- **Janela de contexto é finita.** Em conversas muito longas, a IA “esquece” ou mistura decisões antigas. Isso causa a maioria dos “ela começou a fazer besteira do nada”.
- **Seguem o que você pede, inclusive o que você pediu mal.** Pedido vago gera resposta genérica; pedido contraditório gera código contraditório.
- **Sem ferramentas, não executam nada.** Um chat comum só escreve código; quem roda, testa e vê o erro é você. Ferramentas agênticas (que leem seus arquivos e executam comandos) mudam isso, mas também exigem mais cuidado com permissões.
- **Tendem a concordar com você.** Peça explicitamente críticas, riscos e alternativas, senão elas validam até ideias ruins.

## 2. Seu novo papel

| A IA é muito boa em | A IA é fraca em |
|---|---|
| Boilerplate, CRUDs, telas, scripts, conversões | Decidir **o que** vale a pena construir |
| Explicar código e conceitos | Saber o seu contexto de negócio e seus clientes |
| Testes, documentação, refatoração | Arquitetura de sistemas grandes sem direção |
| Traduzir entre linguagens/frameworks | Depurar problemas de ambiente que ela não enxerga |
| Primeiras versões em minutos | Detalhes recentes, nichos obscuros, versões novas |
| Alternativas e prós/contras | Segurança “por padrão” (ela erra se você não cobrar) |

Seu trabalho passa a ser: **definir o problema, especificar, revisar, testar e decidir**. Isso é *engenharia de produto*, e é aprendível.

## 3. Tipos de ferramenta (e quando usar cada uma)

Produtos mudam todo mês; pense em categorias:

1. **Chat (ex.: Claude no navegador/app):** ideal para planejar, aprender, discutir arquitetura, gerar protótipos e arquivos pequenos.
2. **Assistentes dentro do editor/IDE:** autocompletar e pequenas edições enquanto você programa.
3. **Agentes de linha de comando/projeto (ex.: Claude Code):** leem o repositório, editam vários arquivos, rodam testes e comandos. Os mais poderosos para projetos reais, exigem Git e revisão de diffs.
4. **Construtores “vibe coding” / no-code com IA:** ótimos para protótipos e validação; costumam limitar a manutenção e a portabilidade.
5. **APIs:** para embutir IA dentro do seu próprio produto.

**Escolha do modelo:** modelos maiores/mais caros para arquitetura, bugs difíceis e revisão; modelos menores/rápidos para tarefas simples e repetitivas. Confira sempre quais estão disponíveis, porque a lista muda rápido.

## 4. Anatomia de um bom pedido

Todo pedido de programa precisa responder:

1. **Objetivo:** o que é e qual problema resolve.
2. **Público e contexto de uso.**
3. **Escopo:** obrigatório, desejável e **o que NÃO fazer**.
4. **Stack e ambiente:** linguagem, frameworks, sistema operacional, versões.
5. **Restrições:** prazo, custo, dependências, offline, privacidade.
6. **Qualidade:** testes, segurança, desempenho, estilo de código.
7. **Formato da entrega:** arquivo único, projeto, passo a passo.
8. **Critérios de aceite:** como saber que está pronto.
9. **Seu nível:** para a IA calibrar a explicação.
10. **Exemplos:** entradas e saídas esperadas.

**Antes**

> Faz um app de controle de gastos.

**Depois**

> Quero um app web (apenas navegador, sem backend) para registrar gastos pessoais. Público: eu e minha esposa, uso no celular. Obrigatório: cadastrar gasto (valor, categoria, data), listar por mês, total por categoria em gráfico simples, exportar CSV. Fora do escopo: login, nuvem. Dados salvos no navegador. HTML/CSS/JS puro, arquivo único. Interface em português, tema escuro. Antes de codar, liste suas suposições e proponha o plano.

O **formulário** deste pacote monta esse tipo de pedido para você, sem esquecer nada.

## 5. Fluxo de trabalho eficiente

1. **Especifique** (formulário ou texto equivalente).
2. **Peça o plano e as suposições.** Corrija o plano antes de gerar qualquer código. Corrigir plano custa segundos; corrigir código custa horas.
3. **Construa em fatias verticais:** a menor versão que funciona de ponta a ponta (ex.: cadastrar e listar um gasto) e depois acrescente.
4. **Rode e teste cada fatia.** Se der erro, cole a mensagem completa.
5. **Commit.** Mensagem curta, uma por fatia que funciona.
6. **Revise o diff** (o que mudou) antes de aceitar. Pergunte “por que você mudou isso?” quando não entender.
7. **Refatore e documente** no fim, não no começo.

**Regra anti-ciclo:** se a IA errou 3 vezes seguidas o mesmo problema, **pare**. Opções: (a) peça um diagnóstico em vez de uma correção (“liste 5 hipóteses para a causa, da mais à menos provável”); (b) abra uma conversa nova com resumo do estado atual; (c) simplifique o problema; (d) mude de abordagem ou de modelo.

## 6. Gerenciando contexto como profissional

- Mantenha um **arquivo de contexto do projeto** (ex.: `PROJETO.md`): objetivo, stack, decisões tomadas, estrutura de pastas, convenções, o que já foi feito, o que falta. Cole no início de cada conversa nova. Em agentes de código, esse arquivo costuma ser lido automaticamente.
- **Resumo de passagem:** ao final de uma sessão longa, peça: “Resuma o estado atual do projeto, decisões e próximos passos em um texto que eu possa colar numa conversa nova.”
- **Anexe só o relevante.** Enfiar o projeto inteiro dilui a atenção da IA.
- **Uma conversa por assunto.** Misturar tarefas confunde.

## 7. Depuração com IA

Modelo de relato de bug:

```
Esperado: …
Aconteceu: …
Mensagem de erro completa: (cole tudo, não resuma)
Ambiente: SO, versões de linguagem/bibliotecas
Código relevante: (só os trechos envolvidos)
Já tentei: …
Antes de corrigir, liste as hipóteses mais prováveis.
```

Dicas: peça para **adicionar logs** em vez de adivinhar; reproduza o bug no menor exemplo possível; desconfie de correções que “consertam” silenciando o erro (`try/except` vazio).

## 8. Aprender enquanto produz (a parte que muda sua carreira)

Você disse que nunca passou do nível “mediano”. A IA pode ser o melhor tutor particular que já existiu, **se você usar para aprender e não só para terceirizar**.

- Peça: “Explique este código linha por linha para alguém no meu nível.”
- Peça: “Por que você escolheu essa abordagem e não outra?”
- Peça: “Me faça 5 perguntas para testar se entendi este trecho.”
- De vez em quando, **escreva você o trecho** e peça revisão.
- Leia os diffs. Pergunte “o que pode dar errado aqui?”.
- Estude por camadas: **Git, HTTP/web, bancos de dados, segurança básica, leitura de erros, testes, arquitetura simples**. Esses fundamentos são o que permite supervisionar a IA.

**Armadilha:** aceitar código que você não entende. Quando quebrar (e vai quebrar), você estará perdido e o cliente também.

## 9. Segurança, legalidade e qualidade

- **Segredos:** chaves de API e senhas nunca vão no código nem no chat. Use variáveis de ambiente e `.gitignore`.
- **Pacotes inventados:** a IA pode sugerir bibliotecas que não existem, e atacantes registram esses nomes com malware. Confira sempre no repositório oficial (PyPI, npm etc.): existe? tem uso? é mantido?
- **Entradas do usuário:** valide e sanitize tudo. Cobre da IA: “revise este código procurando falhas de segurança (injeção, XSS, autenticação, exposição de dados)”.
- **Login e pagamentos:** use serviços prontos (provedores de autenticação, gateways de pagamento). Não crie o seu.
- **Licenças:** verifique a licença das bibliotecas usadas em produto comercial.
- **Privacidade/LGPD:** se coletar dados pessoais, defina o que coleta, por quê, onde guarda e como apaga.
- **Revisão humana obrigatória** para tudo que mexe com dinheiro, dados de terceiros ou permissões.
- **Agentes com acesso ao seu computador:** dê o mínimo de permissão, trabalhe em pasta de projeto, leia os comandos antes de aprovar.

## 10. Gerar renda de verdade

**Realidade:** se qualquer pessoa agora constrói apps rápido, o *código* deixa de ser o diferencial. O que vale é:

1. **Escolher um problema real e pago** (alguém já gasta tempo ou dinheiro com isso).
2. **Conhecer o nicho** melhor que um desenvolvedor genérico.
3. **Distribuição:** como o cliente descobre você.
4. **Confiança, suporte e manutenção contínua.**

**Caminhos práticos (do mais rápido ao mais lento para dar retorno):**

1. **Serviço antes de produto:** automações, planilhas, scripts, sites e pequenos sistemas sob medida para comércios e profissionais locais. Gera caixa e ensina o que o mercado quer.
2. **Ferramentas de nicho (micro-SaaS):** resolvem uma dor específica (agendamento, orçamento, controle de estoque, relatórios, integração com WhatsApp/Pix/ERPs).
3. **Extensões, plugins, applets e utilitários desktop** publicados em lojas e repositórios, com versão paga ou doações.
4. **Templates, kits e conteúdo educacional** sobre o que você aprendeu fazendo.
5. **Apps para o grande público:** o mais disputado e o mais caro de divulgar; deixe para depois.

**Método:**

1. Liste 10 dores que você observa (trabalho atual, família, comércios do bairro).
2. Converse com 5 pessoas que têm a dor. Pergunte quanto tempo/dinheiro gastam hoje.
3. Construa a **menor** versão que resolve a dor central (use a IA para isso: dias, não meses).
4. **Venda antes de polir:** pré-venda, piloto pago, mensalidade simbólica.
5. Cobre desde cedo; produto gratuito não valida nada.
6. Meça: quem usa, quem volta, quem paga.

**Custos ocultos para planejar:** manutenção, suporte, hospedagem, custo de APIs de IA, impostos e formalização (MEI/CNPJ, se for faturar). Consulte um contador, isto aqui não é aconselhamento financeiro ou jurídico.

**Honestidade:** a maioria dos apps não gera renda relevante. O melhor caminho para quem está começando é um nicho conhecido, um cliente pagante e iteração rápida.

## 11. Erros comuns

- Pedir o sistema inteiro de uma vez.
- Não usar Git e perder a versão que funcionava.
- Aceitar código sem rodar, sem testar e sem entender.
- Misturar vários assuntos na mesma conversa longa.
- Não dizer a versão/SO/ambiente e receber comandos que não funcionam.
- Insistir 10 vezes no mesmo erro com a mesma conversa.
- Pedir só elogios e nunca crítica.
- Construir meses sem mostrar a ninguém.
- Colocar chave de API no repositório público.

## 12. Checklist antes de publicar ou vender

- [ ] Roda do zero em máquina limpa (siga o seu próprio README).
- [ ] Testei os fluxos principais **e** os erros (campo vazio, sem internet, dado absurdo).
- [ ] Sem segredos no código ou no histórico do Git.
- [ ] Dependências conferidas (existem, licença ok, atualizadas).
- [ ] Revisão de segurança feita (pedida à IA e conferida por mim).
- [ ] Backup/forma de recuperar dados do usuário.
- [ ] Política de privacidade e termos, se coletar dados.
- [ ] Forma de o cliente pedir suporte.
- [ ] Versão e changelog.

## 13. Biblioteca de prompts úteis

**Planejar**
> Antes de codar: resuma o que entendeu, liste suas suposições, proponha a arquitetura e um plano em etapas pequenas e testáveis. Aguarde minha aprovação.

**Pedir crítica**
> Aponte falhas, riscos e alternativas para esta ideia/arquitetura. Não concorde só para me agradar.

**Revisar código**
> Revise este código como um sênior: bugs, casos de borda, segurança, desempenho e legibilidade. Priorize por gravidade e explique cada ponto.

**Depurar**
> Não corrija ainda. Liste as 5 causas mais prováveis, como confirmar cada uma e só então proponha a correção.

**Explicar**
> Explique este código como se eu fosse intermediário em [área], com um exemplo pequeno e os conceitos que preciso estudar.

**Testes**
> Escreva testes para os casos normais, de borda e de erro. Diga o que cada teste protege.

**Segurança**
> Faça uma revisão de segurança deste projeto (injeção, XSS, autenticação, segredos, dependências, permissões) e liste correções em ordem de prioridade.

**Resumo de passagem**
> Resuma o estado atual do projeto (objetivo, stack, decisões, estrutura, pendências) para eu colar numa conversa nova.

**Refatorar com segurança**
> Refatore sem mudar o comportamento. Mostre o plano, aplique em passos pequenos e diga como verificar que nada quebrou.

## 14. Mentalidade final

- Você não está competindo com a IA; está competindo com quem **não sabe** usá-la bem.
- Sua vantagem de anos de experiência é **julgamento**: saber o que está errado, o que é perigoso, o que é viável. A IA multiplica isso.
- Faça pequeno, publique cedo, aprenda com o uso real.
- Volte a este guia a cada projeto novo e use o formulário para começar cada um do jeito certo.

*Observação: ferramentas, modelos e preços de IA mudam rápido. Os princípios deste guia envelhecem devagar; os detalhes de produto, confira sempre nas fontes atuais.*
