# Evolução do Setor – site no GitHub Pages + Firebase

Site estático (GitHub Pages) que guarda os dados no **Firestore** e exige **login** (e-mail e senha).
Arquivos: `index.html`, `firebase-config.js`, `firestore.rules`.

## 1. Firebase (uma vez)
1. https://console.firebase.google.com > **Adicionar projeto**.
2. **Authentication > Começar > E-mail/senha > Ativar**. Em **Usuários**, crie os usuários (e-mail e senha).
   Em **Configurações > Ações do usuário**, desative "Ativar criação (cadastro)" para ninguém se cadastrar sozinho.
3. **Firestore Database > Criar banco de dados** > modo produção > região `southamerica-east1` (São Paulo).
4. Aba **Regras**: cole o conteúdo de `firestore.rules`, troque os e-mails pelos usuários criados e **Publicar**.
5. **Configurações do projeto > Seus apps > </> (Web)**: registre o app e copie o objeto de configuração
   para o arquivo `firebase-config.js`.

## 2. GitHub
1. Crie o repositório (por exemplo na organização `digital-kpis`, nome `evolucao-setor`).
2. Envie os 3 arquivos para a raiz da branch `main` (Add file > Upload files).
3. **Settings > Pages > Deploy from a branch > main / (root) > Save**.
4. O endereço fica `https://ORGANIZACAO.github.io/evolucao-setor/` (leva 1 a 2 minutos).
5. No Firebase: **Authentication > Configurações > Domínios autorizados** > adicione `ORGANIZACAO.github.io`.

## 3. Primeiro uso
Abra o site, entre com o login e use **Importar planilhas** para enviar as planilhas mensais (.xlsx).
Cada dia vira um documento em `dias/AAAA-MM-DD`; reenviar um mês substitui os dias dele.
Metas e valores lançados à mão ficam em `config/metas`. Tudo aparece para todos os usuários autorizados, em tempo real.

## Observações
- O banco guarda só dados **agregados por dia** (totais, SLAs, motivos de cancelamento, pedidos por separador).
  Não guarda nome nem endereço de cliente. Os nomes dos separadores (colaboradores) ficam no banco.
- Custo: o volume (cerca de 5 KB por dia) cabe com folga na cota gratuita do Firebase (plano Spark).
- A chave (`apiKey`) do Firebase é pública por natureza. Quem protege os dados são o login e as regras:
  não use regras abertas (`allow read, write: if true`).
- Para apagar: botão **Remover mês** (por mês) ou **Remover todos os dados** (esvazia a coleção `dias`).
