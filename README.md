# Zenith OS — App wrapper (Capacitor)

Esse app não roda o servidor sozinho — ele só abre uma janela apontando pro
Zenith OS que já roda no Termux (`127.0.0.1:7777`). Você continua rodando
`npm start` normalmente no Termux; o app é só a "casca" nativa com ícone,
permissões e tela cheia, no lugar de abrir pelo Chrome.

## Passo a passo

1. Crie um repositório novo no GitHub (ex: `zenith-os-app`) e suba **esta
   pasta inteira** (`wrapper/`) pra raiz dele.

2. (Opcional, mas recomendado) Coloque uma imagem quadrada em
   `resources/icon.png` (1024x1024px) — vai virar o ícone do app em todos os
   tamanhos automaticamente. Sem isso, o app usa o ícone padrão do Capacitor.

3. No GitHub, vá em **Actions** → escolha o workflow "Build APK" →
   **Run workflow** (botão manual, aba `workflow_dispatch`). Ou simplesmente
   dê um `git push` na branch `main` que ele builda sozinho.

4. Espere o job terminar (~3-5 min) e baixe o arquivo `zenith-os-debug-apk`
   em **Actions → (a run que rodou) → Artifacts**. É um `.zip` com o
   `app-debug.apk` dentro.

5. Transfira o APK pro celular e instale (vai pedir pra liberar "instalar de
   fontes desconhecidas" — normal, é um APK de debug não assinado pela
   Play Store).

## O que esse app já faz

- Ícone e nome próprios ("Zenith OS") na gaveta de apps
- Abre em tela cheia, sem barra de endereço, como app nativo
- Permissão de internet (fala com o servidor local) e de galeria (pra
  escolher a imagem de fundo, no `desktop.html`)

## O que NÃO faz (ainda)

- Não roda o Node.js sozinho — o servidor Termux continua precisando estar
  de pé. Se quiser eliminar esse passo (o app subir o servidor sozinho),
  isso é outro projeto — precisa embutir um runtime Node dentro do APK.
- Modo DeX/Bluetooth (mouse e teclado virtuais numa TV) — combinamos deixar
  pra depois, é um módulo nativo separado.

## Debug rápido

Se o app abrir e mostrar a tela de "não consegui falar com o servidor",
é porque o Termux não está com `npm start` rodando, ou está rodando numa
porta diferente de 7777 (nesse caso, ajuste em `capacitor.config.json`,
campo `server.url`).
