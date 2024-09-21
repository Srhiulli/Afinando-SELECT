---
theme: seriph
background: './background.jpg'
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
image: https://cover.sli.dev
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
image: https://cover.sli.dev
---

### Exemplo de uma query (consulta):
Buscando por colunas específicas
<br><br>

```sql {all|1|all} twoslash
SELECT email, phone, name
FROM contact
WHERE owner_id_agency = "0af8dc24-4c25-435"
ORDER BY created_at DESC 
LIMIT 5
```

---
transition: slide-right
layout: image-left
image: https://cover.sli.dev
---

### Otimização de Consultas com AND, WHERE e LIMIT no SQL 🚀:
<br>

O Filtro Mágico do WHERE e AND 🧙‍♂️

```sql {all|3|4|all} twoslash
SELECT *
FROM contact
WHERE owner_id_agency = "0af8dc24-4c25-435"
AND name = "Cleitinho"
ORDER BY created_at DESC 
LIMIT 5
```
<br><br>

💡 Dica: Use WHERE e AND para buscar apenas o necessário, e economize tempo e processamento!

---
transition: slide-left
layout: image-left
image: https://cover.sli.dev
---
### Otimização de Consultas com AND, WHERE e LIMIT no SQL 🚀:
<br>
O Cortador de Fila LIMIT ✂️

```sql {all|6|all} twoslash
SELECT *
FROM contact
WHERE owner_id_agency = "0af8dc24-4c25-435"
AND name = "Cleitinho"
ORDER BY created_at DESC 
LIMIT 5
```
<br><br>

💡 Dica: Menos é mais! Limite o número de registros para consultas mais rápidas.

---
transition: slide-up
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
---

### JOIN no SQL 🚀

O JOIN no SQL é como juntar duas tabelas e combinar seus dados com base em uma relação comum.

```sql
SELECT c.name, t.name
FROM c.contact c
JOIN t.tags t ON t.contact_id = c.id
WHERE c.id = "478982xu2hi3wp382492"
ORDER BY t.name DESC
LIMIT 4;
```

Resumindo: O JOIN conecta os dados de duas tabelas com base em uma chave comum, permitindo que você traga informações relacionadas em uma única consulta! 🎉

---
transition: slide-up
---

<joinAnimationDemo />