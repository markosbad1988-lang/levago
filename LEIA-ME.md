# 📦 LevaGO — Guia de Lançamento (MVP real)

App de entregas em tempo real: qualquer pessoa entrega, com ou sem veículo.
Stack: **Firebase (Auth + Firestore) + Vercel** — o mesmo caminho do ValiFast.

---

## 1️⃣ Criar o projeto no Firebase (10 min)

1. Acesse https://console.firebase.google.com → **Adicionar projeto** → nome: `levago` (região: southamerica-east1 quando perguntar).
2. **Authentication** → Começar → método **E-mail/senha** → Ativar.
3. **Firestore Database** → Criar banco → modo **produção** → região `southamerica-east1`.
4. Na aba **Regras** do Firestore, apague tudo e cole o conteúdo do arquivo `firestore.rules`.
   ⚠️ Na função `isAdmin()`, troque `seuemail@exemplo.com` pelo SEU e-mail → **Publicar**.
5. **Configurações do projeto (⚙️) → Seus apps → ícone Web (</>)** → registre o app `levago-web` → copie o objeto `firebaseConfig`.

## 2️⃣ Configurar o app (2 min)

Abra o `index.html` e, logo no início do `<script type="module">`:

- Cole os valores do seu `firebaseConfig` em `FIREBASE_CONFIG` (apiKey, authDomain, projectId, etc.).
- Em `ADMIN_EMAIL`, coloque o **mesmo e-mail** que você usou nas regras. É ele que libera a aba **💼 Admin** no app.
- `CENTER` já está em Valença-RJ. Mude se quiser lançar em outra cidade.

## 3️⃣ Publicar na Vercel (5 min)

Seu fluxo de sempre:

1. Crie um repositório no GitHub (ex.: `levago`) e suba os arquivos desta pasta.
2. Na Vercel → **Add New Project** → importe o repositório → Deploy (é site estático, sem build).
3. Pronto: `levago.vercel.app` (ou o domínio que preferir).

> Edições futuras: edita o `index.html` → push no GitHub → a Vercel publica sozinha, igual ao ValiFast.

## 4️⃣ Criar as primeiras contas (teste real)

1. No celular, abra o site → **Criar conta** (conta única: todo mundo pode pedir E entregar).
2. Em outro celular (ou aba anônima) → **Criar conta** com outro e-mail (será o entregador do teste — ninguém pode aceitar o próprio pedido).
3. Com você logado no seu e-mail de dono, a aba **💼 Admin** aparece automaticamente.

### Teste do fluxo completo
1. **Loja**: aba *Nova* → marque coleta e entrega no mapa → descreva o item → *Publicar*.
2. **Entregador**: a entrega aparece na hora no mapa → toque no pin → *Aceitar*.
3. **Loja**: aba *Pedidos* → aparece o **código de coleta** (mostre ao entregador) e o **PIN** (botão de WhatsApp envia ao cliente).
4. **Entregador**: chegou na loja → digita o código → status vira "em rota" → a loja acompanha o GPS dele ao vivo no mapa.
5. No destino → digita o **PIN** → saldo creditado (60%) → avaliações dos dois lados.
6. **Entregador**: aba *Perfil* → informa a chave PIX → *Solicitar saque*.
7. **Você (Admin)**: vê o saque pendente, paga o PIX manualmente e clica em *Marcar pago*.

## 5️⃣ Como funciona o dinheiro nesta fase (modelo "concierge")

O app **controla** os valores, mas o dinheiro ainda circula por fora (PIX manual):

| Quem | O quê |
|---|---|
| Loja | Paga a você por fatura (semanal, via PIX) a soma dos totais das entregas concluídas — o Admin mostra o acumulado. |
| Entregador | Acumula saldo no app (60% de cada entrega) e solicita saque; você paga o PIX em até 24h e marca como pago. |
| Você | Fica com a comissão (40% Básico / 25% Parceiro) + mensalidades dos Parceiros. |

⚠️ **Antes de pagar um saque**, confira no painel Admin/console se as entregas do entregador realmente constam como concluídas — nesta fase o controle final é seu.

Quando tiver volume (~30+ entregas/semana), o próximo passo é automatizar com **split de pagamento** (Asaas ou Pagar.me): a loja paga no app, o sistema divide automaticamente e o saque vira automático. Isso exigirá **CNPJ**.

## 6️⃣ Pendências para operação séria (checklist)

- [ ] **CNPJ** (MEI não permite intermediação de pagamento — avalie ME) e conta PJ.
- [ ] **Termos de uso + Política de Privacidade (LGPD)**: você coleta localização e dados financeiros. Posso redigir os dois quando quiser.
- [ ] Deixar claro nos termos que o entregador é **autônomo** (sem vínculo empregatício).
- [ ] Verificação de identidade dos entregadores (nesta fase: aprove manualmente, peça documento por WhatsApp antes de liberar entregas de maior valor).
- [ ] Seguro/fundo de extravio (sugestão: reservar R$ 0,50 por entrega da sua comissão).

## 🔒 Limitações conhecidas do MVP (honestidade acima de tudo)

- Os códigos de coleta/PIN ficam no documento da entrega; um usuário tecnicamente avançado logado poderia lê-los. Para o volume inicial de Valença, o risco é baixo; a correção definitiva (Cloud Functions validando os códigos no servidor) entra na fase 2.
- O saldo do entregador é atualizado pelo próprio app dele; por isso o pagamento de saques passa pela sua conferência manual no Admin.
- Sem recuperação de senha na tela ainda (o Firebase Console permite redefinir manualmente em Authentication → usuário → ⋮ → Redefinir senha).

Nada disso impede o lançamento em cidade pequena com pagamento manual — impede apenas escalar sem a fase 2.

---

## 📱 Divulgação sugerida (semana 1)

1. Instale o app em 5 lojas pessoalmente (padaria, farmácia, pizzaria...) e cadastre com elas.
2. Recrute 5–10 entregadores num grupo de WhatsApp da cidade ("ganhe por entrega, receba via PIX, trabalhe a pé ou de bike").
3. Primeira semana: comissão zero pras lojas (promoção de lançamento) — você só valida o fluxo.

Boa sorte com o lançamento! 🚀
