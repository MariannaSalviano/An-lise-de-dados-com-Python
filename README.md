# Análise de dados com Python
Projetos de análise de dados com Python e bibliotecas como Pandas e Matplotlib.

# 🧠 Análise Inteligente de Vendas com Python + Pandas + Matplotlib
Um projeto completo de análise de dados desenvolvido no **Google Colab** utilizando **Python**, **Pandas** e **Matplotlib**.  
O objetivo é demonstrar habilidades sólidas em manipulação de dados, integração de múltiplas bases, criação de métricas avançadas e visualizações de insights.

---

## 🚀 Sobre o Projeto

Este projeto simula uma operação real de vendas, unificando informações de **clientes**, **produtos** e **transações**, permitindo análises profundas como:

- Faturamento por produto e categoria  
- Margem de lucro  
- Ranking de clientes mais lucrativos  
- Sazonalidade mensal de vendas  
- Estruturação de base unificada  
- Visualizações profissionais de dados  
- Métricas de negócio usadas no mercado  

É um projeto ideal para demonstrar capacidade analítica em processos seletivos e compor um portfólio sólido de Data Analysis.

---

## 📁 Estrutura do Repositório


```Python
import pandas as pd
```

```Python
vendas = pd.read_csv('/content/Vendas.txt')
clientes = pd.read_csv('/content/Clientes.txt')
produtos = pd.read_csv('/content/Produtos.txt')
```

```Python
vendas['faturamento'] = vendas['quantidade'] * vendas['preco_unitario']
faturamento_por_produto = vendas.groupby('id_produto')['faturamento'].sum().reset_index()
faturamento_por_produto
```

```Python
merge_tabelas = vendas.merge(clientes, on='id_cliente').merge(produtos, on='id_produto')
merge_tabelas.head()
```

```Python
merge_tabelas['lucro_unitario'] = merge_tabelas['preco_unitario'] - merge_tabelas['custo']
merge_tabelas['lucro_total'] = merge_tabelas['lucro_unitario'] * merge_tabelas['quantidade']
```

```Python
merge_tabelas.groupby(['id_cliente', 'nome'])['lucro_total'].sum().sort_values(ascending=False).head(5)
```

```Python
import matplotlib.pyplot as plt
```

```Python
merge_tabelas.groupby('categoria')['faturamento'].sum().plot(kind='bar', figsize=(8,4), color='gray')
plt.title('Faturamento por Categoria')
plt.xlabel('Categoria')
plt.ylabel('Receita Total')
plt.show()
```

```Python
top = merge_tabelas.groupby('nome')['lucro_total'].sum().sort_values(ascending=False).head(5)
top.plot(kind='barh', figsize=(8,4), color='gray')
plt.title('Top 5 Clientes Mais Lucrativos')
plt.xlabel('Lucro Total')
plt.show()
```

```Python
ticket_medio = merge_tabelas.groupby('nome')['faturamento'].mean().sort_values(ascending=False)
ticket_medio
```

```Python
ticket_categoria = merge_tabelas.groupby('categoria')['faturamento'].mean()
ticket_categoria
```

```Python
freq_clientes = merge_tabelas['nome'].value_counts()
freq_clientes
```

```Python
LTV = merge_tabelas.groupby('nome')['faturamento'].sum().sort_values(ascending=False)
LTV
```

```Python
produtos_mais_vendidos = merge_tabelas.groupby('nome_produto')['quantidade'].sum().sort_values(ascending=False)
produtos_mais_vendidos
```

```Python
mais_vendas_dia = merge_tabelas.groupby('data_venda')['quantidade'].sum().sort_values(ascending=False)
mais_vendas_dia
```

```Python
bins = [18, 25, 35, 50]
labels = ['18-25', '26-35', '36-50']
merge_tabelas['faixa_etaria'] = pd.cut(merge_tabelas['idade'], bins=bins, labels=labels)
```

```Python
vendas_por_faixa = merge_tabelas.groupby('faixa_etaria')['faturamento'].sum()
vendas_por_faixa
```

```Python
top3 = merge_tabelas.groupby('categoria')['lucro_total'].sum().nlargest(3)
top3
```

```Python
participacao = merge_tabelas.groupby('categoria')['faturamento'].sum()
participacao / participacao.sum() * 100
```

```Python
merge_tabelas[['quantidade', 'lucro_total']].corr()
```

