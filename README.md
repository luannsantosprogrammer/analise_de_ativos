# 🕵️‍♂️ RPA com Python Selenium para vistoria de materiais ativos em cliente

Este repositório contém um script Python que automatiza o processo de verificação de equipamentos ativos em nome de clientes e aguardam serem tirados de ativos enquanto fisicamente está na logística reversa, utilizando o Selenium e planilhas do Google Sheets. Ele foi pensado para rodar em ambientes como o Google Colab, facilitando a integração com APIs do Google.

---
🚀 Instalação de Bibliotecas
As bibliotecas necessárias são instaladas via pip no Colab:

python
Copiar
Editar
!pip install -q selenium
!pip install -q webdriver-manager
!pip install -q pandas
!pip install -q plyer
!pip install -q lxml html5lib
!pip install -q beautifulsoup4
📚 Bibliotecas Utilizadas
selenium, webdriver_manager – Automação do navegador

pandas – Manipulação de dados

bs4 (BeautifulSoup) – Leitura e parsing de HTML

gspread, google.auth – Conexão com Google Sheets

requests – Envio de notificações web

IPython.display – Exibir notificações dentro do Colab

🔐 Autenticação com Google
Antes de mexer com o Google Sheets, o código autentica o usuário via Colab:

python
Copiar
Editar
auth.authenticate_user()
creds, _ = default()
gc = gspread.authorize(creds)
📋 Fluxo Geral do Programa
1. Buscar Dados da Planilha de Produção
python
Copiar
Editar
def buscar_dados():
    ...
    return dados
Puxa os números de série (Nª SÉRIE) de uma aba chamada TESTE na planilha Produção.

2. Gerar Registro de Equipamentos Ativos
python
Copiar
Editar
def gerar_dados(n_serie):
    ...
Se um equipamento está ativo, adiciona ele na planilha Equipamentos_duplicados e envia uma notificação.

3. Verifica Onde Parou
python
Copiar
Editar
def onde_parei(dados):
    ...
    return novos_dados, aba_vistos, dados_vistos
Controla o ponto onde o script parou na última execução para evitar reprocessamento.

4. Checa se Já Foi Alterado
python
Copiar
Editar
def verificar_se_foi_alterado(n_serie):
    ...
Verifica se o número de série já foi processado anteriormente na planilha Equipamentos_alterados.

5. Verifica se o Equipamento Está Ativo
python
Copiar
Editar
def verificando_ativo(driver):
    ...
Interage com a interface web via Selenium.

Aplica filtros com o número de série.

Se estiver ativo e ainda não registrado, adiciona em uma nova aba e notifica.

🧠 Automação de Login
O bot faz login automaticamente caso não esteja logado:

python
Copiar
Editar
documento = driver.find_element(...)
senha = driver.find_element(...)
codigo = driver.find_element(...)
Preenche os campos de CPF, senha e códigos.

Após login bem-sucedido, inicia a verificação automática.

🛠️ Configuração do Navegador (Headless)
python
Copiar
Editar
options = webdriver.ChromeOptions()
options.add_argument("--headless")
...
driver = webdriver.Chrome(options=options)
Executa o navegador sem abrir uma janela gráfica (modo invisível).

🔁 Loop Principal
python
Copiar
Editar
while True:
    ...
    verificando_ativo(driver)
Fica rodando o processo de verificação até que algo pare ou o script seja interrompido.

Em caso de falha, envia uma notificação para a URL cadastrada via requests.post.

🔔 Notificações no Colab
python
Copiar
Editar
def notify_colab(title, message):
    ...
Exibe alertas visuais direto no Colab pra avisar que algo foi identificado.

📎 Observações
Esse código foi feito pra rodar no Google Colab.

Necessita permissões de acesso ao Google Sheets.

A URL para envio de notificações deve ser configurada na variável url.

✅ Exemplo de Uso
Basta executar o notebook no Colab e seguir as instruções para login (CPF, senha e códigos). O robô cuida do resto.

