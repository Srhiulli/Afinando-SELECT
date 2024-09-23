---
theme: seriph
background: './imagebg.webp'
title: Fundamentos do SELECT no SQL 
info: |
  ## Slidev Starter Template
  Consultas Simples e Práticas em SQL 
class: text-center
drawings:
  persist: false
transition: slide-left
mdc: true
---
<style>
    .slidev {
    background-image: url('./background.jpg');
    background-size: cover;
    background-position: center;
  }
p {
  font-size: 1.2em;
  font-weight: 500;
  background-color: #FF6B6B;
  background-image: linear-gradient(45deg, #FFD93D 10%, #FF6B6B 40%, #FF9F43 90%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
  line-height: 1.5;
  text-align: justify;
  margin: 20px 0;
}
h3 {
  font-size: 1.5em;
  font-weight: 600;
  background-color: #4E4E50;
  background-image: linear-gradient(45deg, #8B9DA5 20%, #4E4E50 80%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
  line-height: 1.2;
  margin: 15px 0;
}
</style>

<div class="absolute top-0 right-0 m-[15px_50px]">
  <CurrentDateTime />
</div>

# <div class="bg-gray bg-opacity-8 rounded-lg absolute top-40 left-60">Afinando o SELECT</div>
##### Consultas Simples e Práticas em SQL
  

<div class="absolute bottom-0 right-0 m-6 flex items-center gap-2">
  <p class="text-sm ">Sarah Iulli</p>
  <a href="https://github.com/Srhiulli" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---
transition: slide-up
level: 2
---
# O que é um banco de dados SQL?
<br>
<p>Um banco de dados SQL é muito parecido com uma planilha do Excel. Ele guarda as informações em<span v-mark.underline.orange> forma tabelas</span>.</p>
<br>

### Exemplo de tabela contact:
````md magic-move {lines: true}
```ts {*|1||2-4|*}
| id | created_at  | updated_at  | owner_id_agency   | email              | phone      | name       |
|8e32| 20:29:45.42 | 20:29:45.42 | 0af8dc24-4c25-435 | sajsas@gmail.com   | 48928323732| Maria Dora |
|8e32| 20:29:45.42 | 20:29:45.42 | 0af8dc24-4c25-435 | cleitinho@gmail.com| 48928323732| Cleitinho  |
|8e32| 20:29:45.42 | 20:29:45.42 | 0af8dc24-4c25-435 | jessica@gmail.com  | 48928323732|Jessica Dora|
|8e32| 20:29:45.42 | 20:29:45.42 | 0af8dc24-4c25-435 | dora@gmail.com     | 48928323732| Maria Dora |
```
````
---
transition: slide-up
level: 2
layout: two-cols
layoutClass: gap-16
layout: image-left
image: https://cdn.jsdelivr.net/gh/slidevjs/slidev-covers@main/static/6terqWC_KCk.webp
---

### Exemplo de uma query (consulta):
Se quisermos buscar dados em uma tabela ou mais tabelas, usamos um <span v-mark.underline.orange>SELECT:</span>
<br><br>

```sql {all|1|2|3|4|5|all} twoslash
SELECT *
FROM contact
WHERE owner_id_agency = "0af8dc24-4c25-435"
ORDER BY created_at DESC 
LIMIT 5
```
---
transition: slide-up
level: 2
layout: two-cols
layoutClass: gap-16
layout: image-left
image: https://cdn.jsdelivr.net/gh/slidevjs/slidev-covers@main/static/NtcKHag5GA4.webp
---

### Exemplo de uma query (consulta):
Selecionando por colunas específicas na busca
<br><br>

```sql {all|1|all} twoslash
SELECT email, phone, name
FROM contact
WHERE owner_id_agency = "0af8dc24-4c25-435"
ORDER BY created_at DESC 
LIMIT 5
```
---
transition: slide-left
layout: image-left
image: https://cdn.jsdelivr.net/gh/slidevjs/slidev-covers@main/static/REjuIrs2YaM.webp
---
### Filtros LIKE e ILIKE no SQL

LIKE sensível as letras maiúsculas
```sql
SELECT * 
FROM user 
WHERE name LIKE 'Jo%'
```

ILIKE não diferencia maiúsculas e minúsculas

```sql
SELECT * 
FROM user 
WHERE name ILIKE 'Jo%'
```
---
transition: slide-left
layout: image-left
image: https://cdn.jsdelivr.net/gh/slidevjs/slidev-covers@main/static/4uH95YbrT0c.webp
---

### Operador > <> < no SQL
Maior que 
```sql
SELECT * 
FROM deal 
WHERE created_at > '%2024-08-10%'
```

Diferente de 
```sql
SELECT * 
FROM user 
WHERE email <> '%clint.digital%'
```

Menor que 
```sql
SELECT * 
FROM user 
WHERE updated_at < '%2024-08-10%'
```

---
transition: slide-up
layout: image-left
image: './imageindice.webp'
---

### O que é uma coluna indexada?
Uma coluna indexada em um banco de dados é como um índice de um livro. <br><br>
Ela facilita a busca rápida de informações.<br><br>Quando uma coluna é indexada, o banco de dados pode encontrar dados mais rapidamente, sem precisar ler todas as informações.

### Como saber se uma coluna é indexada?
```sql
SELECT tablename, indexname, indexdef
FROM pg_indexes
WHERE tablename = 'nome_da_tabela'
```
---
transition: slide-up
layout: image-left
image: './image.png'
---

### Otimização de Consultas com AND, WHERE no SQL 🚀

```sql {all|3|4|all} twoslash
SELECT *
FROM contact
WHERE owner_id_agency = "0af8dc24-4c25-435"
AND name = "Cleitinho" 
ORDER BY created_at DESC 
LIMIT 5
```

💡 Dica: Use WHERE e AND para buscar apenas o necessário e economize tempo e processamento!
<br><br>
Caso pesquise um WHERE ou AND em uma coluna que não é indexada, a busca não será otimizada, fazendo o SELECT ler todas as linhas do banco

---
transition: slide-left
layout: image-left
image: https://cdn.jsdelivr.net/gh/slidevjs/slidev-covers@main/static/mI-QcAP95Ok.webp
---
### LIMIT no SQL 🚀:
<br>
O limitador de linhas LIMIT ✂️

```sql {all|6|all} twoslash
SELECT *
FROM contact
WHERE owner_id_agency = "0af8dc24-4c25-435"
AND name = "Cleitinho"
ORDER BY created_at DESC 
LIMIT 5
```
<br><br>

💡 Dica: Menos é mais! Limite o número de registros para um retorno mais limpo. 

---
transition: slide-left
---
# Usando alias para dar um <span v-mark.underline.pink>apelido</span> para as tabelas 
<br>

Um alias para uma tabela pode ser usado para abreviar o nome da tabela e tornar a consulta mais legível, especialmente ao trabalhar com múltiplas tabelas.

<br>

```sql
SELECT c.name, c.email
FROM contact c
WHERE c.owner_id = 'dnwueh32xhe32dwend31p31p'
LIMIT 5
```
<br><br>

Um alias torna sua consulta mais limpa, curta e fácil de entender! E irá facilitar no JOIN -->
---
transition: slide-left
layout: image-left
image: https://cdn.jsdelivr.net/gh/slidevjs/slidev-covers@main/static/4uH95YbrT0c.webp
---

### JOIN no SQL 🚀

O JOIN no SQL é como juntar duas tabelas e combinar seus dados com base em uma relação comum.


Resumindo: O JOIN conecta os dados de duas tabelas com base em uma chave comum, permitindo que você traga informações relacionadas em uma única consulta! 🎉
<br><br>

<div v-click> <h4> Como selecionar os nomes dos contatos de uma conta que possuem a tag "Abacate"? </h4> </div>
<div v-click> <h4> Qual coluna temos em comum na tabela tags e contact? </h4> </div>


---
transition: slide-left
---

<joinAnimationDemo />

---
transition: slide-left
layout: two-cols
---

<div class="grid grid-cols-2 gap-2 flex items-center">
  <div>
<joinAnimationDemoOnlyContactId />
  </div>
  <div>

```sql {all|2|3|4-5|1|6-7|all} twoslash
SELECT c.name, t.name
FROM contact c
JOIN tags t ON t.contact_id = c.id
WHERE c.owner_id_agency = '478982xu2hi3wp382492'
AND t.name = 'Abacate'
ORDER BY t.created_at DESC
LIMIT 20
```
  </div>
</div>



---
transition: slide-left
layout: image-right
image: './background.jpg'
---
# IA para Formulação de Queries SELECT
<br>

**Prompt**
##### Quero selecionar todos as contas com mais de 10 dispositivos em um SQL.

**Resposta:**
```sql
SELECT owner_id_agency, COUNT(channel_id) AS device_count
FROM channel_id
GROUP BY owner_id_agency
HAVING COUNT(channel_id) > 10;
```

**Problema** 
##### Problema é que owner_id_agency não existe na tabela channel_id, e preciso buscar na tabela channel_account
---
transition: slide-left
layout: image-right
image: https://cdn.jsdelivr.net/gh/slidevjs/slidev-covers@main/static/REjuIrs2YaM.webp
---
**Solução**
##### Detalhe os campos e tabelas:

**Prompt**
#####  Quero listar `owner_id`e `channel_id` dos dispositivos na tabela `channel_account` com mais de 10 dispositivos.

**Resultado**
```sql
SELECT owner_id, channel_id
FROM channel_account
GROUP BY owner_id, channel_id
HAVING COUNT(*) > 10;
```
---
transition: slide-up
layout: image-left
image: https://cdn.jsdelivr.net/gh/slidevjs/slidev-covers@main/static/NgzaXnY9hF0.webp
---
# Dicas de Prompts para a IA
<br>

##### **"Me ajude a escrever um SELECT que busca todos os clientes que criaram uma conta há menos de 10 dias."** 
<br>

##### **"Como posso otimizar essa query que seleciona dados da tabela de tags?"**
 <br>

##### **"Quero criar uma query com JOIN entre as tabelas `deal` e `contact`, pode me ajudar?"**

---
transition: slide-up
layout: image
image: '/image copy 4.png'
---
```sql
SELECT  name, email, phone, deleted_at
FROM contact
WHERE owner_id_agency = '92a0c5f8-3d6e-4f6c-9111-82b0647d6e38'
AND deleted_at IS NOT NULL

```
```sql
SELECT d.*
FROM deal d
JOIN contact c ON d.contact_id = c.id
JOIN "user" u ON d.user_id = u.id
WHERE d.owner_id_agency = 'b11275e4-e290-4cac-a21b-8c1d765f502b'
AND d.origin_id = '3f9d4075-7eb5-464b-822d-f75308101c64'
AND d.created_at >= '2024-01-01'
```
```sql
SELECT c."name", c.phone, c.email, u.first_name, d.status, d.stage 
FROM contact c 
JOIN deal d on d.contact_id = c.id 
JOIN "user" u on d.user_id = u.id
WHERE d.owner_id_agency = 'b11275e4-e290-4cac-a21b-8c1d765f502b'
AND d.origin_id = '3f9d4075-7eb5-464b-822d-f75308101c64'
```
```sql
SELECT * FROM "public"."webhook" 
WHERE ("event" ILIKE '%webhook%') 
AND ("data"::TEXT ILIKE '%jhonathan@teste.com.br%') 
AND ("owner_id" = '22512a26-c5e2-44b1-b4a2-891e7503e128')
--and ("app_integration_id" = 'e970b7f2-c169-4224-a8e1-d30b1d01cdcf')
ORDER BY "created_at";
```
---
transition: slide-down
layout: image
image: '/image copy 4.png'
---
```sql
SELECT name c, email c, phone c, d.deleted_at 
FROM contact c 
JOIN deal d ON c.id = d.contact_id 
WHERE ("origin_id" = '2453ab29-c043-4402-9dd8-585299de12e6')
AND (d.deleted_at IS NOT NULL)
AND (d.owner_id_agency = '0c7e405e-ba8c-4897-b1a6-33079a60179c')
AND (d.deleted_at >= '2024-03-27');
```
