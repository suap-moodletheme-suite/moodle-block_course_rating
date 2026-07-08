# Moodle Block Plugin - Course Rating (Avaliação de Curso)

Este é um plugin de bloco para o Moodle que permite aos estudantes avaliarem os cursos com notas de 1 a 5 estrelas e deixarem comentários textuais sobre a sua experiência.

## 🚀 Requisitos e Instalação

* **Moodle:** Compatível com Moodle 3.11 ou superior.
* **Instalação:** 
  1. Baixe ou clone este repositório.
  2. Extraia o conteúdo na pasta de blocos do seu Moodle: `<moodle_root>/blocks/course_rating`.
  3. Acesse a administração do Moodle para executar a atualização do banco de dados.

---

## 🗄️ Estrutura de Banco de Dados

O plugin cria e gerencia duas tabelas no banco de dados do Moodle. *Nota: Em execução, o Moodle adiciona o prefixo configurado (ex: `mdl_block_`).*

### Tabela de Classificações (`course_rating`)
Armazena a nota e o comentário atual de cada usuário para cada curso.

| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `id` | Int | Chave primária auto-incremento |
| `rating` | Int | Nota da classificação (1 a 5) |
| `message` | Text | Comentário/feedback textual do estudante |
| `userid` | Int | ID do usuário que realizou a avaliação |
| `courseid` | Int | ID do curso avaliado |
| `createdat` | Datetime | Data e hora de criação do registro |
| `updatedat` | Datetime | Data e hora da última edição da avaliação |

### Tabela de Histórico (`course_rating_history`)
Guarda o histórico de avaliações anteriores caso o usuário edite sua nota ou comentário.

| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `id` | Int | Chave primária auto-incremento |
| `rating` | Int | Nota antiga da classificação |
| `message` | Text | Comentário antigo |
| `originid` | Int | ID da classificação correspondente na tabela principal (`course_rating`) |
| `createdat` | Datetime | Data e hora em que a versão antiga foi arquivada |

---

## ⚙️ Configuração do Bloco

Ao adicionar o bloco à página do curso, você pode configurar o momento em que o formulário de avaliação ficará visível aos alunos:

1. **Após concluir o curso (Padrão):** O formulário de avaliação só é exibido se o estudante tiver preenchido os requisitos de conclusão do curso.
   
   ![](/pix/config-02.png)

2. **Enquanto estiver cursando:** Permite que o estudante avalie o curso a qualquer momento da sua jornada.
   
   ![](/pix/config-01.png)

---

## 🛠️ Desenvolvimento (Compilação de CSS e JS)

O código JavaScript e folhas de estilo estão localizados na pasta `amd/src` e utilizam o **Gulp** para otimização e minificação.

Para configurar o ambiente de build:

1. Entre no diretório de fontes AMD:
   ```bash
   cd amd/src
   ```
2. Instale as dependências de desenvolvimento:
   ```bash
   npm install
   ```
3. Execute o script de compilação/minificação:
   ```bash
   npm run minify
   ```

---

## 📂 Estrutura de Arquivos Principais

* **[version.php](file:///C:/Users/2080882/projetos/IFRN/suap-moodletheme-suite/block_course_rating/version.php):** Define a versão do plugin (necessário incrementar ao realizar atualizações).
* **[edit_form.php](file:///C:/Users/2080882/projetos/IFRN/suap-moodletheme-suite/block_course_rating/edit_form.php):** Formulário de edição de configuração da visibilidade do bloco.
* **[block_course_rating.php](file:///C:/Users/2080882/projetos/IFRN/suap-moodletheme-suite/block_course_rating/block_course_rating.php):** Lógica principal, processamento de formulário e renderização do bloco.
* **[endpoint.php](file:///C:/Users/2080882/projetos/IFRN/suap-moodletheme-suite/block_course_rating/endpoint.php):** Ponto de entrada AJAX para buscar e atualizar avaliações/comentários de forma assíncrona.
* **[templates/](file:///C:/Users/2080882/projetos/IFRN/suap-moodletheme-suite/block_course_rating/templates):** Contém os arquivos Mustache que definem o layout do bloco (`rating.mustache`, `rating_bars.mustache`, etc.).
